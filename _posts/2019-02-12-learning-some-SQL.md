---
layout: single
title: Learning some SQL
date: '2019-02-12T09:55:00.001-08:00'
author: frances
tags:
- technical learning
modified_time: '2020-06-22T10:55:00.001-08:00'


---



My technical project management work currently involves transforming clinical data into a normalized format and loading it into a database for machine learning researchers to use.
The project has me wishing I knew more  about SQL -- I run a couple of reporting queries that developers wrote for me through mySQL workbench on a weekly basis, but  wish I could formulate queries of my own.

Recently, a request came in to broaden a existing muti-database query to span more databases.  Before I passed it on to our database developer, I decided to take the opportunity to study the current query, learn more about SQL, and see if I could then size the work involved in broadening the query. (or even do it myself).

I ultimately concluded that broadening the query would probably involve creating new tables in the databases in question -- so it wouldn't be quite the quick query rewrite that I hoped it would be. My suspicion was strengthened when I took the request to the dev manager and he assigned it lower priority on backlog. 

I'm attaching here my notes on the SQL query (with dB names changed) so that I can remember my learning process starting from zero; all comments are mine:

```

#why is there no 'use db' statement? I guess it's because we are dealing w multiple dBs we mention below? 

#so let's grab a bunch of columns from a bunch of different tables that we INNER JOIN on later
#we start by grabbing 'provider name' column, then provider name, etc
SELECT DISTINCT providerTable.provider_name AS 'Provider'
        #and project names
        ,projectTable.project_name AS 'Project'
	    #ok some conditional logic to get the 'batch' column.        
        #from the 'batch report', there are a lot of 'provider_id's w value 1 (and some w/ 2, 3, 4, 5 etc
        #oooook, contextual knowledge: this is just to deal w/ some batch naming historical idiosyncricities. for provider 1, we only use batch_id; for all others, we use batch id + sub batch id
       ,CASE WHEN reportTable.provider_id =1 THEN reportTable.batch_id
       WHEN reportTable.provider_id<>1 THEN CONCAT(reportTable.batch_id, reportTable.sub_batch_id)
       END AS 'Batch ID'
	
	    #batch_details is in: complete.batch, complete.missing_images, complete.missing_reports, complete.study_frequency
        #so batch_delails must becoming from complete.batch b/c other tables aren't mentionend in this query
        #but WHY isn't batch_details prefixed? is it because its UNIQUE in this query whereas other fields might be shared across other tables mentioned here?
        #for example, 'group_flag" shows up in complete and controller, which are both mentioned.
        #experiment, I did prefix w/ batchTable.batch_detail...and query still executes so...yeah, think I'm right. 
        #and I just saw something about 'ambiguous column name error' so yeah.
       ,batch_detail AS 'Batch Description'
       #same comment -- guess it comes from batchTable.sub_condition
       ,sub_condition AS 'Sub Condition'
       ,splitTable.group_flag AS 'Group Flag'
       ,splitTable.split_id AS 'Split'
        ,splitTable.team_id AS'Team ID'
	    #looks like we are formatting date_delivered a little more nicely
       ,date_format( splitTable.date_delivered ,'%m/%d/%Y') AS 'Date Delivered'
        ,splitTable.number_of_patients AS 'Number Of Patients'

FROM

#OK, controller isn't some SQL notion (as I originally thought), it's just a DB name like complete or report, and split_details is a table in there.
#I guess we start w/ controller as our 'from' table b/c it's the main table we want, we just want to gussy it up w/ names columns instead of numeric ID columns
#and note that I turned some short var names (like st) into long ones (like splitTable) to make this easier to read for myself
controller.split_details splitTable

#So we combine w/ the reportTable  FIRST in order to take care of that weird batch # stuff? Don't really understand this bit, come back to it?
INNER JOIN status.batch_report reportTable
ON

#batch id, subbatchid, provider id, and project id all have to match
splitTable.batch_id = reportTable.batch_id and splitTable.sub_batch_id = reportTable.sub_batch_id and splitTable.provider_id = reportTable.provider_id  and splitTable.project_id = reportTable.project_id

#now we have another inner join.
#here's a nice illustration of how this works: https://academy.vertabelo.com/blog/illustrated-guide-multiple-join/ 
#here we pick up the provider name column
INNER JOIN controller.provider providerTable
ON reportTable.provider_id = providerTable.provider_id

#here we pick up the project name column
INNER JOIN controller.project projectTable
ON reportTable.project_id = projectTable.project_id

#here we pick up batch_detail and sub_condition
#not sure why we have to match on so many conditions vs providerTable and projectTable
#I guess provider and project tables are just super simple (id+name) so we don't need to match on much
INNER JOIN complete.batch batchTable
ON reportTable.batch_id = batchTable.batch_id and reportTable.sub_batch_id = batchTable.sub_batch_id and reportTable.provider_id = batchTable.provider_id  and reportTable.project_id = batchTable.project_id;


```

