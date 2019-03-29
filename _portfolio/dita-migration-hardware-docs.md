---
title: "Migrating hardware calibration procedures to DITA"
excerpt: "Streamlining procedural variations for better single sourcing"
author: frances
#not including layout since it's in the defaults
---

<!-- toc -->
- [TLDR](#tldr)
- [Goals and results](#goals-and-results)
- [Before](#before)
- [After](#after)
<!-- tocstop -->


## TLDR
To skip straight to my writing sample, see 
<a href="https://drive.google.com/file/d/18uNb2zUvpzIL6pAgSWgZONeIRnX6vWtn/preview" target="_blank">PXIe-XXXX Calibration Template</a>



## Goals and results

My goals were to develop a reusable, minimal structure and introduce consistency to a heterogenous doc set that had evolved greatly over time.
Another writer has since inherited this doc set, and resued about 90% of my content for her release.


In mentoring my successor, I've learned several DITA reuse lessons:

- Attempting to implement a "semicontrolled" vocabulary through conrefs (for example, conreffing table titles, math variables, and figure titles) is probably overdoing it in most cases
- Successful sharing strategies need to be flexible, and can allow for mixed approaches. For example, we're using a combination of standard conrefs and push topics for test conditions and cautions, and that seems to work:

![conditions library](/assets/images/portfolio/dita_reuse_test_conditions_library.png)

- Conreffing generic instructions (while using keydefs for numbers, equations, and figures) seems to work reasonably well, though our library topic for steps is getting a little out of hand and I worry future writers will have difficulty finding the steps they need. I've tried to break the library topic  up by subject area to help with this issue, and if I had to do it again, I probably wouldn't author such granular keydefs.



### Before 

  A previous writer's introduction to the Adjustment section represented a compromise between our legacy step-by-step coding instructions and a newer, shorter format -- but was still quite lengthy:

  ![Before](/assets/images/portfolio/dita_reuse_adjust_before.png)

### After 

I split up the Adjustment introduction into reusable chunks, cut a lot of content, and included coding instructions only for select portions: 



  ![Before](/assets/images/portfolio/dita_reuse_adjust_after.png)
  
 
Here's the full DITA template I authored:

<iframe src="https://drive.google.com/file/d/18uNb2zUvpzIL6pAgSWgZONeIRnX6vWtn/preview" width="100%" height="800em"></iframe>

When you look at the source behind a typical topic I structured, you can see it's entirely reused:



![Conreffed dita topic](/assets/images/portfolio/dita_reuse_verifying_current_output.png)








