---
layout: single
title: AI-assisted docs reference writing for a niche scripting language
date: '2025-05-08T09:55:00.001-08:00'
author: frances
tags:
- techcomm
- dita
modified_time: '2025-05-08T09:55:00.001-08:00'


---

Recently, I experimented with asking an AI to write reference docs for a custom extension to a rather niche, obscure scripting language (JsonLogic).

TLDR: The AI performed poorly. It hallucinated heavily about the niche language, to the extent that its code examples were worse than useless. This is in contrast to the success I've had with basic code examples in well-known languages like Python.

My methodology was as follows:

1. I authored the reference docs myself, looking at the pull request, especially its unit tests and comments.

2. I asked Claude to author the reference docs. As a baseline, I gave it the code delcaring the oeprator's functionality. Beyond that I provided varying levels of context:
   1. I prompted with zero additional context
   2. I prompted with the context of Claude's project knowledge of my documentation
   3. I prompted with the context of Claude's project knowledge + specific examples of my reference documentation for other JsonLogic custom operations.
   
Prompt #3 was the most successful, but none of these prompts returned satisfactory results. For comparison, here's my docs, versus the most successful prompt

## The handcrafted docs


> ## Let  
>  
> Use this operator to declare named variables scoped to the Let operator. This operator addresses JsonLogic's lack of built-in support for named variable declaration.  
>  
> ```json  
> {  
>   "let": [  
>     { /* 1st arg: initialize named variables using key/value pair syntax */ },  
>     { /* 2nd arg: operate on the named variables. Sensible evaluates variables in order */ }  
>   ]  
> }  
> ```  
>  
> ### Example  
>  
> ```json  
> {  
>   "fields": [],  
>   "postprocessor": {  
>     "type": "jsonLogic",  
>     "rule": {  
>       "let": [  
>         {  
>           /* declare values with key:value pair syntax */  
>           "a": 5,  
>           "b": 3,  
>           /* c is sum of a + b (8) */  
>           "c": {  
>             "+": [  
>               { "var": "a" },  
>               { "var": "b" }  
>             ]  
>           }  
>         },  
>         /* operate on named values (5 * 8) */  
>         {  
>           "*": [  
>             { "var": "a" },  
>             { "var": "c" }  
>           ]  
>         }  
>       ]  
>     }  
>   }  
> }  
> ```  
>  
> This returns:  
>  
> ```json  
> /* postprocessor output */  
> 40  
> ```  




## The AI-generated docs

### Prompt

Here's the prompt:

```
write a reference documentation page for this custom JsonLogic operation,
in the same style as the documentation pages in your project knowledge base:

function op_let(
  // content redacted; private code base
logicEngine.addMethod(
  "let",
  { traverse: false, method: op_let },
  { useContext: true }
);
```

The results:

- Were far too verbose
- Failed to explain the 'why' for this custom operation, which is simply that JsonLogic lacks native support for variable declaration.
- Failed to explain the scope for the varaible declaration, a key point.
- Were very prone to code sample hallucination. The first few prompts, for example, resulted in a code sample that made heavy use of a `do` operation that's not supported in JsonLogic.
- Failed to provide a concise, useful description of the method's args

Here are the results:

> ## Let operation  
> Use the let operation to define temporary variables within the scope of a JsonLogic expression. This provides a way to create named intermediate values that can be referenced in subsequent expressions, making complex transformations more readable and maintainable.  
>  
> ### Parameters  
> **Parameter** | **Description**  
> --- | ---  
> 1 | An object with variable names as keys and JsonLogic expressions as values  
> 2 | The JsonLogic expression to evaluate using the defined variables  
>  
> ```json  
> {  
>   "let": [  
>     {  
>       "variable1": JsonLogic expression for value1,  
>       "variable2": JsonLogic expression for value2,  
>       ...  
>     },  
>     JsonLogic expression using defined variables  
>   ]  
> }  
> ```  
>  
> ### Examples  
> **Config**  
>  
> ```json  
> {  
>   "id": "calculated_invoice",  
>   "method": {  
>     "id": "customComputation",  
>     "jsonLogic": {  
>       "let": [  
>         {  
>           "subtotal": { "var": "invoice_subtotal.value" },  
>           "tax_rate": { "var": "tax_rate.value" },  
>           "tax_amount": { "*": [  
>             { "var": "subtotal" },  
>             { "/": [ { "var": "tax_rate" }, 100 ] }  
>           ] }  
>         },  
>         {  
>           "eachKey": {  
>             "invoice_summary": {  
>               "eachKey": {  
>                 "subtotal": { "var": "subtotal" },  
>                 "calculated_tax": { "var": "tax_amount" },  
>                 "total": { "+": [ { "var": "subtotal" }, { "var": "tax_amount" } ] },  
>                 "tax_rate_percentage": { "cat": [ { "var": "tax_rate" }, "%" ] }  
>               }  
>             }  
>           }  
>         }  
>       ]  
>     }  
>   }  
> }  
> ```  
>  
> **Example document**  
> The following image shows the example document used with this example config:  
> _Show Image_  
>  
> **Output**  
> ```json  
> {  
>   "calculated_invoice": {  
>     "invoice_summary": {  
>       "subtotal": 850.00,  
>       "calculated_tax": 68.00,  
>       "total": 918.00,  
>       "tax_rate_percentage": "8%"  
>     },  
>     "type": "object"  
>   }  
> }  
> ```  
>  
> ### Notes  
> - Variables defined in the let operation are accessible only within the scope of the second parameter.  
> - Variable definitions can reference previously defined variables within the same let operation. For example, if you define variables x and y, the definition of y can reference x.  
> - Variables are evaluated in the order they appear in the definition object.  
> - The operation maintains access to the document context, so you can still use the var operator to access document data.  
> - Variable names in the let operation can be any valid JSON property name.  
> - If a variable name conflicts with a field in the document context, the variable definition takes precedence within the scope of the let operation.  
>  
> ### Use cases  
> This operation is particularly useful for:  
> - Breaking down complex calculations into named steps for better readability  
> - Avoiding repeating the same calculation multiple times  
> - Creating intermediate values that can be referenced multiple times in a complex transformation  
> - Building complex objects with multiple derived fields  
> - Organizing multi-step data transformations in a clear, logical manner  
>  
> For other JsonLogic operations in Sensible, see JsonLogic extensions.  










