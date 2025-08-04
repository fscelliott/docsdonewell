---
layout: single
title: Mixed results with AI-assisted changelogs
author: frances
---

Recently I experimented with prompting Claude to generate new-feature release announcements based on docs and past changelog examples.

I found a pattern consistent with my other experiments: AI-generated changelogs are fine for higher-level, less technical announcements, and fairly unsatisfactory for more technical or detailed announcements.

Here are a few examples.

## Describing new features

I wanted to announce a new feature for my client [Sensible](https://sensible.so/). End users can now use "named anchors" to define, then reference a text match, for more concise syntax.

Here's Claude's attempt, and my beef with it:

### Claude output

> New feature: Named anchors for reusable anchor definitions
>
> You can now define named anchors and reuse them across multiple fields using the new `anchorDefinition` type. This eliminates redundant anchor configuration and enables cleaner syntax when multiple fields share the same anchor logic.
> Define a named anchor with `"type": "anchorDefinition"` and a `name` parameter, then reference it in other fields using `"anchor": {"ref": "anchor_name"}`. Named anchors work within Conditional methods, allowing you to define language-specific or context-dependent anchors that can be referenced by subsequent fields.
>
> For more information, see [Reuse anchor variables](https://docs.sensible.so/docs/anchor#reuse-anchor-variables).

Commentary: This assumes the reader knows an anchor's purpose, which isn't a given. It's also overly verbose given that most technical readers are familiar with variable declaration and reference as fundamental to coding languages. A code example would be much simpler. It also misses out on an advanced use case. 

### My version

Here's my stab at it. For the sake of the experiment, I wrote this before prompting Claude so I wouldn't bias my own writing:



> You can now name and reuse [anchors](doc:anchor) as variables for concise syntax. Anchors are labels that locate data for layout-based methods.
>
> Example syntax:
>
> ```
> "fields": [
>     {
>       /* declare a complex named anchor variable for later reuse */
>       "type": "anchorDefinition",
>       "name": "liability_workers_comp",
>       "anchor": {
>         "start":{"text":"Certificate of liability insurance","type":"equals"},
>         "match":{"text":"workers compensation","type":"equals"},
>         "end":{"type":"equals","text":"the acord name and logo are registered marks of acord"}
>       }
>     },
>     {
>       /* extract text from a box 1.15" to the right of the named anchor  */
>       "id": "subrogation_waived",
>       "method": {
>         "id": "box",
>         "offsetX": 1.15,
>         "position": "right"
>       },
>       "anchor": {
>         "ref": "liability_workers_comp"
>       }
>     },
> ```
>
> You can [conditionally](doc:conditional) assign values to anchor variables depending on previously extracted document data. For example, assign a `"customer_id"` anchor the value of either `"customer number"` or `"identificación del cliente"` depending on the form's language. For more information, see [Anchor variables](doc:anchor-nuances).

## Deprecating old features

I was also unsatisfied with Claude's attempt to write a deprecation announcement. I wanted to communicate a change to my client's code editor.


### Claude output

Here's Claude's attempt:


> ### Deprecation: Sensible Instruct visual authoring interface removed
>
> The Sensible Instruct visual authoring interface has been removed. Configuration authoring is now exclusively done in JSON using SenseML syntax.
>
> The updated interface provides a streamlined experience with compact visual output representation and JSON output in the right pane. You can toggle between these views while working entirely in the JSON-based SenseML editor.
>
> Previously supported Sensible Instruct methods (Query, List, and Table) remain available as SenseML methods with JSON configuration.

Commentary: Again, lots of telling without showing. Too much passive voice. Without some tailor-made prompting, Claude also can't glean from the docs that we're removing this feature in order to pave the way for a better feature.

### My version

Here's my version, again written without glancing at Claude:



> ## Deprecation: Sensible Instruct visual authoring tool
>
> We've removed [Sensible Instruct](doc:https://docs.sensible.so/changelog/april-2023#visual-authoring-with-gpt-4-sensible-instruct), a visual tool for authoring LLM-based SenseML methods that augmented JSON-based authoring. Stay tuned for new ways to author LLM-based methods in future.
>
> By default, you now author all SenseML methods in JSON and view extracted document data in a compact visual format. You can also switch between viewing output visually or as JSON.
>
> Compact visual view of output:
> \[screenshot]
>
> JSON view of output:
> \[screenshot]
