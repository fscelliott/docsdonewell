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

Recently, I experimented with asking an AI to write reference docs for a custom extension to a rather niche, obscure scripting language.

TLDR: The AI did poorly. It hallucinated heavily about the niche language, to the extent that its code examples were worse than useless. This is in contrast to the success I've had with basic code examples in well-known languages like Python.

My methodology was as follows:

1. I authored the reference docs myself, looking at the pull request, especially its unit tests and comments.

2. I asked Claude to author the reference docs. As a baseline, I gave it the code delcaring the oeprator's functionality. Beyond that I provided varying levels of context:
   - 1 prompt with zero additional context
   - 1 prompt with Claude's 'project knowledge' of my documentation
   - 1 prompt with the project knowledge + specific examples of my reference documentation for other JsonLogic custom operations.
   

    given varying levels of context:
   - zero context beyond the code declaring the operator's functionality 


In general, I'm finding that when I ask an AI to write docs in the same style and template as docs I've already written, they do OK.

Of course, they can't write docs when I have to document flows that are still in development, or where an opinion on flow is needed.




I've been documenting some custom JsonLogic operations recently, so I was able to ask Claude the following:


## Prompt with no context/general knowledge

> Write a reference documentation page for this custom JsonLogic operation, including a simple code example for how to use it:

```
function op_let(
// redacted, in private repo
// defines the Let operation
  )
```

and I got back:


### response # 1

# JsonLogic "let" Operator

## Overview

The `let` operator enables the definition of local variables within a JsonLogic expression. This powerful feature allows you to store intermediate calculation results and reference them later in the same expression, improving readability and reducing redundancy.

## Syntax

```
{
  "let": [
    {
      "variable1": <expression1>,
      "variable2": <expression2>,
      ...
    },
    <resultExpression>
  ]
}
```

## Parameters

- **First argument**: An object where each key is a variable name and each value is a JsonLogic expression that will be evaluated to determine the variable's value.
- **Second argument**: A JsonLogic expression that will be evaluated using the variables defined in the first argument.

## Behavior

1. The operator evaluates each variable definition in the order they appear in the object.
2. Each variable's expression can reference previously defined variables.
3. The variables are scoped only to the `resultExpression`.
4. The operator returns the result of evaluating the `resultExpression`.

## Context and Scope

- Variables defined with `let` take precedence over any data in the context.
- The original context is still accessible within the `let` operation.
- Nested `let` operations create nested scopes.

## Error Handling

The operator will throw an error if:
- The input is not an array of exactly 2 elements.
- The first element is not an object.

## Example

```javascript
const jsonLogic = {
  "let": [
    {
      "x": 10,
      "y": 5,
      "sum": { "+": [{ "var": "x" }, { "var": "y" }] },
      "product": { "*": [{ "var": "x" }, { "var": "y" }] }
    },
    {
      "if": [
        { ">": [{ "var": "sum" }, 20] },
        { "var": "product" },
        { "var": "sum" }
      ]
    }
  ]
};

// Usage with the engine
const result = logicEngine.run(jsonLogic, { otherData: 42 });
// result will be 15 (the sum of x and y, since sum = 15 is not > 20)
```

## Implementation

```javascript
function op_let(
  input: unknown,
  context: unknown,
  above: unknown[],
  engine: LogicEngine
) {
  throwOnConfigError(
    Array.isArray(input) && input.length == 2,
    "Invalid args for let"
  );
  
  const [vars, fn] = input;
  throwOnConfigError(
    typeof vars == "object" && vars && !Array.isArray(vars),
    "Invalid args for let"
  );
  
  const extendedAbove = [context, ...above];
  
  let state: Record<string, unknown> = {};
  
  for (const [varName, varFn] of Object.entries(vars)) {
    state = {
      ...state,
      [varName]: engine.run(varFn, state, { above: extendedAbove }),
    };
  }
  
  return engine.run(fn, state, { above: extendedAbove });
}

// Registration
logicEngine.addMethod(
  "let",
  { traverse: false, method: op_let },
  { useContext: true }
);
```

## Common Use Cases

- Avoiding repeated complex calculations
- Breaking down complex logic into readable parts
- Creating intermediate results for better readability
- Building complex conditional expressions with named components

## Performance Considerations

- Variables are evaluated sequentially and only once
- Using `let` can improve performance by preventing redundant calculations
- Each variable is immutable once defined

## Related Operators

- `var`: Access values from the data context
- `map`: Apply transformations to arrays
- `reduce`: Accumulate values from arrays

## Prompt with general knowledge

> Write a reference documentation page for this custom JsonLogic operation, in the same style as the documentation pages in your project knowledge base:

```
function op_let(
// redacted, in private repo
// defines the Let operation
  )
```


and I got back:


### response # 2

Let operation
Use the let operation to define and bind variables for use in subsequent JsonLogic expressions. This operation creates a local scope where variables can be defined and then used in a function body, making complex transformations more readable and maintainable.
Parameters
PositionDescription1An object mapping variable names to expressions that compute their values2The expression to evaluate using the defined variables
Example
Config
json{
  "let": [
    {
      "total": { "var": "invoice_total.value" },
      "tax": { "var": "tax_amount.value" },
      "subtotal": { "*": [{ "var": "total" }, { "/": [100, { "+": [100, { "var": "tax_rate.value" }] }] }] }
    },
    {
      "eachKey": {
        "invoice_summary": {
          "eachKey": {
            "total_with_tax": { "var": "total" },
            "tax_amount": { "var": "tax" },
            "subtotal_without_tax": { "var": "subtotal" },
            "calculated_tax": { "-": [{ "var": "total" }, { "var": "subtotal" }] }
          }
        }
      }
    }
  ]
}
Example document
The following image shows the example document used with this example config:
Show Image
Output
json{
  "invoice_summary": {
    "total_with_tax": 1150.75,
    "tax_amount": 95.89,
    "subtotal_without_tax": 1054.86,
    "calculated_tax": 95.89
  }
}
Notes

Variable definitions can reference previously defined variables within the same let operation
Variables defined in the let operation are only accessible within its scope (the second parameter)
The operation evaluates each variable definition in the order they appear in the object
Each variable's value is computed using the JsonLogic engine, so you can use any valid JsonLogic expression
The context (document data) is still accessible via the var operator inside the let scope
This operation is especially useful for complex transformations that reuse intermediate calculations

Use cases

Creating reusable intermediate values in complex calculations
Making transformations more readable by giving meaningful names to values
Avoiding redundant computations by calculating values once and reusing them
Structuring complex document data transformations in a more maintainable way


For more information about JsonLogic operations in Sensible, see the JsonLogic reference.

Then I got more specific:

#### Prompt:


And got back:

#### Response 3:
Let operation
Use the let operation to define temporary variables within the scope of a JsonLogic expression. This provides a way to create named intermediate values that can be referenced in subsequent expressions, making complex transformations more readable and maintainable.

Parameters
Parameter	Description
1	An object with variable names as keys and JsonLogic expressions as values
2	The JsonLogic expression to evaluate using the defined variables
json
{
  "let": [
    {
      "variable1": JsonLogic expression for value1,
      "variable2": JsonLogic expression for value2,
      ...
    },
    JsonLogic expression using defined variables
  ]
}
Examples
Config

json
{
  "id": "calculated_invoice",
  "method": {
    "id": "customComputation",
    "jsonLogic": {
      "let": [
        {
          "subtotal": { "var": "invoice_subtotal.value" },
          "tax_rate": { "var": "tax_rate.value" },
          "tax_amount": { "*": [{ "var": "subtotal" }, { "/": [{ "var": "tax_rate" }, 100] }] }
        },
        {
          "eachKey": {
            "invoice_summary": {
              "eachKey": {
                "subtotal": { "var": "subtotal" },
                "calculated_tax": { "var": "tax_amount" },
                "total": { "+": [{ "var": "subtotal" }, { "var": "tax_amount" }] },
                "tax_rate_percentage": { "cat": [{ "var": "tax_rate" }, "%"] }
              }
            }
          }
        }
      ]
    }
  }
}
Example document
The following image shows the example document used with this example config:

Show Image

Output

json
{
  "calculated_invoice": {
    "invoice_summary": {
      "subtotal": 850.00,
      "calculated_tax": 68.00,
      "total": 918.00,
      "tax_rate_percentage": "8%"
    },
    "type": "object"
  }
}
Notes
Variables defined in the let operation are accessible only within the scope of the second parameter.
Variable definitions can reference previously defined variables within the same let operation. For example, if you define variables x and y, the definition of y can reference x.
Variables are evaluated in the order they appear in the definition object.
The operation maintains access to the document context, so you can still use the var operator to access document data.
Variable names in the let operation can be any valid JSON property name.
If a variable name conflicts with a field in the document context, the variable definition takes precedence within the scope of the let operation.
Use cases
This operation is particularly useful for:

Breaking down complex calculations into named steps for better readability
Avoiding repeating the same calculation multiple times
Creating intermediate values that can be referenced multiple times in a complex transformation
Building complex objects with multiple derived fields
Organizing multi-step data transformations in a clear, logical manner
For other JsonLogic operations in Sensible, see JsonLogic extensions.








