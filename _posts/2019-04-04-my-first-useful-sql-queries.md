---
layout: single
title: My first business-useful SQL queries
date: '2019-04-04T09:55:00.001-08:00'
author: frances
tags:
- techcomm
- dita
modified_time: '2019-04-04T13:13:14.240-08:00'


---


Whoo-hoo! In the last few weeks, I went from zero knowledge of SQL, to authoring two SQL queries that were actually useful for my project management tasks! That SQL coursera [course](https://www.coursera.org/learn/analytics-mysql?specialization=excel-mysql)  I took (part of the Excel to MySQL: Analytic Techniques for Business Specialization) turned out to be really useful!

A disclaimer -- before publishing, I thought about whether sharing my SQL snippets would reveal any workplace-confidential information. 

I don't think so because:

- It's no secret we're collecting clinical images for machine-learning training

- I've redacted the names of all databases involved

- I'm not sharing any of the query results 



 OK! So, onward to my SQL queries:

  ## SQL query #1:

I got a request from my boss asking for an inventory of the clinical data we've received that is intended for machine-learning training.

For each of our data providers and for each of our projects, she wanted the data bucketed by:

 

- Total number of patients 
- Total number of studies by modality 
- Total number of images by modality



Since she CC'd me, not just the dB engineers, I thought I'd take a crack at it to lessen the engineers' load.

Before I started writing the query, I: 

- explored all table schemas
- figured out only 1 table had modalities; examined those possible modality values.
- knew I needed to link this modalities table to other tables; figured out which fields were MUL keys.
- Determined I'd use accession_number to figure out # of unique images based on dB source.
- Knew I could leverage other queries I'd seen to get the rest of the info.

The meat of the query I came up with is as follows: (NOTE: database names REDACTED)

```

SELECT provider_id,  project_id, batch_id, modality, COUNT(DISTINCT src_patient_id) AS 'TOTAL PATIENTS', COUNT(DISTINCT accession_number) AS 'TOTAL STUDIES', COUNT(DISTINCT location) AS 'TOTAL IMAGES'
FROM redactedDB.image_linker
GROUP BY provider_id, project_id, batch_id, modality;

```


…and then  I make it a little fancier with some inner joins to show provider/project names:

```

SELECT DISTINCT providerTable.provider_name AS 'Provider'
        #following is to get names instead of IDs (ie provider name, not provider id); copied from batch_summary_report query - felliott
        ,projectTable.project_name AS 'Project'
        
       ,CASE WHEN reportTable.provider_id =1 THEN reportTable.batch_id
       WHEN reportTable.provider_id<>1 THEN CONCAT(reportTable.batch_id, reportTable.sub_batch_id)
       END AS 'Batch_ID'
              

       ,batch_detail AS 'Batch_Description'
       
       #here's the info we are really interested in; this is the part I modified -Felliott
        ,COUNT(DISTINCT linkerTable.src_patient_id) AS 'Total Patients'
       ,linkerTable.modality AS 'Modality'
       ,COUNT(DISTINCT linkerTable.accession_number) AS 'Total_Studies'
       ,COUNT(DISTINCT linkerTable.location) AS 'Total Images'
       


FROM redactedDB.image_linker linkerTable


INNER JOIN redactedDB.batch_report reportTable
ON

linkerTable.batch_id = reportTable.batch_id and linkerTable.sub_batch_id = reportTable.sub_batch_id and linkerTable.provider_id = reportTable.provider_id  and linkerTable.project_id = reportTable.project_id


INNER JOIN redactedDB.provider providerTable
ON reportTable.provider_id = providerTable.provider_id

INNER JOIN redactedDB.project projectTable
ON reportTable.project_id = projectTable.project_id

INNER JOIN redactedDB.batch batchTable
ON reportTable.batch_id = batchTable.batch_id and reportTable.sub_batch_id = batchTable.sub_batch_id and reportTable.provider_id = batchTable.provider_id  and reportTable.project_id = batchTable.project_id
GROUP BY Provider, Project, Batch_ID, Batch_Description, modality;

```

#### Troubleshooting:

In writing the query, I uncovered some duplicate listings of images in one of our dBs. Our lead dB engineer confirmed it needed to be cleaned up, so I opened a github card.

Frustratingly, when I compared my results to other, prexisting SQL queries, I realized that I was in some cases overcounting the # of patients and images per project and provider. 
I asked a DB engineer to correct my query; what he sent me was constructed a little differently BUT he had the same discrepancies.

We concluded together that this was because a patient could have MULTIPLE modalities -- duh, of course.
At this point, I was wondering what our data needs were, and I suggested perhaps bucketing patients by the modality of their primary study, and ignoring other modalities (but, I thought this might be tough since checking for a primary study involves checking CTP codes.)
However, my boss seemed to be satisfied instead with a query that showed all total patients (not double counted) combined with a report of modality frequency (i.e., how many patients have more than 1 modality, and what modality combos they have).

#### SQL features I learned about from writing this query:



I learned about a couple of SQL functions that were not covered in the coursera course by examining the code of the DB engineer who helped me out by writing an alternate query to mine: 

- UNION ALL -- useful when dealing with almost-duplicate dBs where you have run the same query (with some modifications) across both then combine the results
- GROUP_CONCAT -- really nice for getting the list of image modalities as a comma-separated list on a per-provider/per-project basis! yeah!

## SQL Query #2

When I first started project managing this team, I relied on an SQL query, let's call it 'data summary', that let me know when clinical data had been ingested into our database by provider and project, and gave me a rough sense of the quality of that data (IE, rough estimates of whether patients had, at a bare minimum, associated images and reports).

Recently, our dB engineers introduced another quality check: counting the number of patients who had at least one complete study that was of primary interest to our algorithms team (ie, the study had the right CTP or other medical codes or descriptions).  This quality check information isn't stored in any tables at present, but I did find the SQL queries they were using to run it.

I decided I wanted  to integrate the new quality checks into the existing data summary query.
So, I took the new query, which ran on a per-project/per-provider basis, and turned it into a subquery so I could get some totals. 

Then, I ran into big challenges trying to combine it with the existing data summary query, and after a day of trying stuff out on my own, bailed and asked a dB engineer for advice. When I talked to a dB engineer, his first response was to show me how to create a temporary table for the new quality checks, then combine those with the existing data summary. However, the dB admin was reluctant to grant me CREATE TEMP TABLE privileges (I learned there can be all sorts of problems with temporary table names colliding, etc) and recommended that we create a private dB in my name if I wanted create table privileges. I didn't feel like I did enough dB work to warrant my own dB (especially since none of the engineers appear to have their own), so I worked with a dB engineer to rewrite the query without creating tables.

I'm kinda not surprised that I needed some help on this one -- in the end, the engineer came up with a query that features a subquery inside a subquery inside an inner join(!!!!) that sounds very complicated to me, especially compared with create/drop table solution, but what do I know of standard SQL practices? In any case, it runs quickly. Here it is, with comments indicating the stuff I wrote:

```

SELECT 
         
        DISTINCT p.provider_name AS 'Provider'
        ,pr.project_name AS 'Project'
        ,CASE WHEN r.provider_id =1 THEN r.batch_id
            WHEN r.provider_id<>1 THEN CONCAT(r.batch_id, r.sub_batch_id)
        END AS 'Batch'
        ,batch_detail AS 'Batch Info'
        ,sub_condition AS 'Sub Condition'
        ,total_patients AS 'Total Patients'
        

######################## Frances stuff START 
  
        #frances: backticks identify column names as opposed to literal strings
        ,ps.`Patients with at least 1 complete primary study` 
        ,ps.`Patients with no complete primary study`
        ,ps.`Total primary images missing`
        ,ps.`Total primary reports missing`
################################### Frances stuff END
        
        
        
        
        ,total_studies AS 'Total Studies'
        ,total_reports AS 'Total Reports Received'
        ,total_images AS 'Total Images Received'
        ,patient_no_images AS 'Unique Patient with no images'
        ,missing_reports AS 'Number of studies with no reports'
        ,missing_images AS 'Number of studies with no images'
        ,missing_reports_images AS 'Number of studies with no reports and no images'
        ,b.record_insert_date AS 'Batch Load Date'



FROM dbREDACTED.batch_report r

INNER JOIN dbREDACTED.provider p
    ON r.provider_id = p.provider_id
INNER JOIN dbREDACTED.project pr
    ON r.project_id = pr.project_id
 INNER JOIN
        (
        SELECT

################## Frances stuff start

             Provider_ID
            ,Project_ID
            ,Batch
            ,sub_batch_id
            ,COUNT(case when CompletePrimaryStudies > '0' then 1 else null end) as 'Patients with at least 1 complete primary study'
            ,COUNT(case when CompletePrimaryStudies = '0' then 1 else null end) as 'Patients with no complete primary study'
            ,SUM(ImagesMissing_PrimaryStudies) as 'Total primary images missing'
            ,SUM(ReportsMissing_PrimaryStudies) as 'Total primary reports missing'
##########################################Frances stuff END
            FROM
					(SELECT
                                
								l.src_patient_id     
################## Frances stuff START
                                ,l.provider_id as 'Provider_ID'
                                ,l.project_id as 'Project_ID'
                                ,CASE 
                                    WHEN l.provider_id =1 THEN l.batch_id
                                    WHEN l.provider_id<>1 THEN CONCAT(l.batch_id, l.sub_batch_id)
                                END AS 'Batch'
                                ,l.sub_batch_id
##########################################Frances stuff END
                                ,SUM(IF(is_primary_procedure=1 AND image_exists = 1 AND report_exists = 1, 1, 0 )) AS 'CompletePrimaryStudies' 
                                
                                ,SUM(IF(is_primary_procedure=1 AND image_exists = 0, 1, 0 )) AS 'ImagesMissing_PrimaryStudies' 
                                ,SUM(IF(is_primary_procedure=1 AND report_exists = 0, 1, 0 )) AS 'ReportsMissing_PrimaryStudies'
                                ,SUM(IF(is_primary_procedure=0, 1, 0 )) AS 'OtherStudies' 
                                ,SUM(IF(is_primary_procedure=0 AND image_exists = 0, 1, 0 )) AS 'ImagesMissing_OtherStudies' 
                                ,SUM(IF(is_primary_procedure=0 AND report_exists = 0,1, 0 )) AS 'ReportsMissing_OtherStudies'
                                ,COUNT(*) AS 'TotalStudies'
                                ,SUM(IF(image_exists = 1 AND report_exists = 1, 1, 0)) AS 'TotalCompleteStudies'

		FROM dbREDACTED.linker AS l
###########################Frances stuff START
                    GROUP BY l.src_patient_id) as subquery_table_alias
                    
        GROUP BY Provider_ID, Project_ID, Batch, sub_batch_id) AS ps
        
    ON r.provider_id = ps.provider_id and r.project_id =ps.project_id and r.batch_id =ps.Batch and r.sub_batch_id =ps.sub_batch_id
################################# Frances stuff END
INNER JOIN dbREDACTED.batch b
    ON r.batch_id = b.batch_id and r.sub_batch_id = b.sub_batch_id and r.provider_id = b.provider_id  and r.project_id = b.project_id;


```



