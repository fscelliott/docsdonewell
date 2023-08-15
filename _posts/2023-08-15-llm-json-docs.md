---
layout: single
title: Proofread documented JSON blobs using LLMs
date: '2023-08-15T00:00:00.000Z'
author: frances
modified_time: '2023-08-15T00:00:00.000Z'
---

I'm [documenting advanced prompt configuration for LLMs quite a bit these days](https://docs.sensible.so/docs/prompt), and so I thought I'd share a small tip for using LLMs to actually write the docs.

One of my more annoyingly manual tasks when writing API docs is to compare an actual returned JSON payload made with a test Postman call to the JSON structure I've documented. I haven't really found a semantic JSON comparison tool online that I'm thrilled with, and I haven't bothered to dig through VS Code extensions to see if there's a tool that can compare it for me. I'm sure it exists, I just haven't done the research. However, I found ChatGPT-3 gave me quite a nice answer to this prompt:

```
Compare the following JSON blobs. Sort the blobs alphabetically by their keys, then for the sorted blobs,
tell me if the blobs are structurally identical in terms of key names.
Ignore different values for the keys, ignore repeated array items, and ignore  empty arrays in the comparison.

BLOB 1:



{
  "cutoff_date": null,
  "extractions": [
    {
      "completed": "2022-10-31T16:27:53.741Z",
      "configuration": "config_for_x_company",
      "created": "2022-10-31T16:27:53.433Z",
      "document_name": "example.pdf",
      "environment": "string",
      "errors": [],
      "id": "246a6f60-0e5b-11eb-b720-295a6fba723e",
      "page_count": 100,
      "status": "COMPLETE",
      "type": "auto_insurance_quotes_all_carriers",
      "validations": [
        {
          "description": "Policy number must be 11 digits",
          "severity": "error"
        },
        {
          "description": "Company email must be in format string@string",
          "message": "Missing prerequisites - company_email",
          "severity": "skipped"
        }
      ],
      "validation_summary": {
        "errors": 0,
        "fields": 6,
        "fields_present": 4,
        "skipped": 1,
        "warnings": 1
      }
    }
  ]
},

BLOB 2:

{
  "cutoff_date": null,
  "extractions": [
    {
      "completed": "2023-08-14T17:17:04.582Z",
      "configuration": "anyco",
      "created": "2023-08-14T17:17:04.044Z",
      "environment": "production",
      "errors": [],
      "id": "28a9dafb-f314-4449-bbeb-4ae76e47d07a",
      "page_count": 1,
      "status": "COMPLETE",
      "type": "auto_insurance_quote",
      "validation_summary": {
        "errors": 0,
        "fields": 1,
        "fields_present": 1,
        "skipped": 0,
        "warnings": 0
      },
      "validations": []
    }
  ]
}

ChatGPT
After sorting the JSON blobs alphabetically by their keys, here's a comparison of the str
```


ChatGPT gave me back this quite-useful answer:

```
After sorting the JSON blobs alphabetically by their keys, here's a comparison of the structural identity of the two blobs in terms of key names:

Both BLOB 1 and BLOB 2 have the same structural layout in terms of key names. The keys within the "extractions" array and their nested structures are consistent between the two blobs. The keys are as follows:

- "cutoff_date"
- "extractions"
  - "completed"
  - "configuration"
  - "created"
  - "document_name"
  - "environment"
  - "errors"
  - "id"
  - "page_count"
  - "status"
  - "type"
  - "validations"
    - "description"
    - "message"
    - "severity"
  - "validation_summary"
    - "errors"
    - "fields"
    - "fields_present"
    - "skipped"
    - "warnings"


Please note that the comparison ignores differences in values, repeated array items, and empty arrays, focusing solely on the presence of keys and their nested structures.

```

I ask for the alphabetical sort, so I can eyeball the sorted blobs myself and sanity check the answer.

