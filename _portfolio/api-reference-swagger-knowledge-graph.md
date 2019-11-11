---
title: "1.0 Swagger API reference"
excerpt: "Swagger reference for IBM Watson cognitive API"
author: frances
#not including layout since it's in the defaults
---


At IBM Watson, I was the first technical writer to document the Knowledge Graph API.

## Results

Because I'd educated myself in ML (for example, by [studying machine learning](https://www.franceselliott.com/2016/05/04/studying-machine-learning-through.html), I was able to write the following Swagger API reference almost entirely by myself, with minimal developer input. Please note the following PDF represents only the tip of the iceberg; I also wrote extensive documentation on the json payload parameters, not shown here for the sake of brevity:

<iframe src="https://drive.google.com/file/d/11-A0oHiriONG14xwMepQ6u9DCdCAbLIZ/preview" width="100%" height="800em"></iframe>


## UX contributions

The API usability was pretty raw when I documented the 1.0 version. To be frank, the API really needed a good overhaul by a developer to get to a useable version. I moved on before I could contribute to such an overhaul, so instead, I prioritized providing sample use cases and example calls.  I would say that the most challenging endpoint to document was GET /relationshipsByTemplate, an in-development endpoint that required me to leverage my knowledge of the semantic web and to experiment heavily with the endpoint myself in order to come up with relevant examples. 



The API has since been substantially changed. For the current docs, see the Knowledge Graph endpoints in the Watson Discovery service (link changes frequently).

