---
layout: single
title: AI tools for writing developer documentation
date: '2022-01-18T00:00:00.000Z'
author: frances
modified_time: '2023-03-09T00:00:00.000Z'

---

Recently I investigated a few AI-powered tools for writing developer documentation. My investigation was prompted by two things:

- I had a front-row seat in GPT's populatity rise; I documented a GPT3 powered tool from my client Sensible back in December 2022, just before GPT's explosive entry into the public imagination, and I was immediately stunned by its potential compared to other AI tools I've documented in the past. So I was pretty excited to see what LLMs could do for documentation writing.

- Existential ~~dread~~ curiosity -- will AI replace documentarians?   My initial answer is no; we still need humans to write high-quality developer docs, but tools like GPT will absolutely change how we write. And I think that's a good thing! I'm encouraged by early research on AI's transformative role, such as those that found that ["separate studies of both writers and programmers find 50% increases in productivity with AI, and higher performance and satisfaction"](https://twitter.com/emollick/status/1631397931604488194).

Anyway, two tools that I recently investigated are:

- **Copilot labs** (powered by Codex, a version of GPT-3). I've see encouraging chatter about Copilot's ability to generate code from prompts among engineers on Slack, so I thought I'd try out it's "Explain code" capabilities. After all, a large part of my job is reading and explaining code! Could Copilot help me or do it better than me?
- **Theneo** -- a new developer portal tool that says it uses AI to generate Stripe-like docs.

Let's dive in!



Copilot review 
===

Getting access
---

There were a couple of things here: 

- I didn't realize that the "explain" feature is part of Copilot *Labs*.  I signed up for Copilot, then installed *both* Copilot and Copilot Labs in VS Code from the Visual Studio marketplace, and made sure that I'd authorized Github in VS Code  by previously installing the [GitHub Pull Requests and Issues](https://code.visualstudio.com/docs/sourcecontrol/github) extension.

- I also didn't want to expose any code from private codebases. So in the interest of security, in Github I (somewhat regretfully) removed any of the sharing/suggestion features for Copilot: 

  ![copilot settings](/assets/images/copilot_1.png)

Experience
---

To test out Copilot, I decided to test its explanation of a code block against my own. I decided to write my own first, then compare it to Copilot's.

**My explanation**

For my test, I chose a code I was reading in order to document a new feature, [which uses GPT3 to extract tables from PDFs](https://docs.sensible.so/docs/nlp-table), for my client Sensible. I read the code, got a rough understanding, chatted with the code author, and wrote up the following explanation in the docs (Sensible has a core value of transparency, so I promise this explanation wasn't documentation overkill):

> For an overview of how the NLP Table method works, see the following steps:
>
> - Sensible extracts the table title, if present. In detail:
>  - Sensible extracts lines contained in a rectangular region immediately above each table, since that region is likely to contain the table title.
>   - The height of that region equals the line height of the first non-empty cell of the table + 0.1 inches, and the region extends down to the top boundary of the table.
>  - For information about how Sensible determines if lines are "contained" in a region, see Region.
> 
> - Sensible scores each table by how well it matches the descriptions you provide of the data you want to extract. To create the score:
>   - Sensible concatenates all your column descriptions with your overall table description.
>   - Sensible concatenates the first two rows of the table with the table title.
>  - Sensible compares the two concatenations using the OpenAPI Embeddings API.
> 
>
> 

**Versus Copilot's explanation**

My first tests helped me realize that you can't give Copilot big chunks of code to explain. You've got to keep it small.   

Here's what Copilot came up with compared to my preceeding explanation:

> /* Here is the explanation for the code above: 
>
> 1. The descriptions are the descriptions of the columns concatenated with the description of the dataset. 
> 2. The descriptions of the columns are concatenated with a space in between. 
> 3. The headers are the headers of the tables.
> 4. The headers of the tables are the first two rows of the tables concatenated with a space in between
> 5. The descriptionEmbedding is the embedding of the descriptions
> 6. The headerEmbeddings are the embeddings of the headers. */

Not super helpful. Here's the code in question for my explanation versus Copilot's explanation: 

```typescript
// Calculate an embedding for the concatenated column descriptions and the headers of all multi-row tables
    const descriptions = `${description}${
      description.length ? " " : ""
    }${columns.map((c) => c.description).join(" ")}`;
    const headers = multiRowTables.map((t) =>
      t.cells
        .filter((c) => c.row < 2) // Take first two rows of the table, to avoid false headers, and to let row contents influence the embedding
        .map((c) => c.line.text)
        .join(" ")
    );

    // Prepend each table's embedding string with its label/immediately preceding context, if present
    multiRowTables.map((t, i) => {
      const tableXRange = xRange(t.boundingPolygon);
      const tableYRange = yRange(t.boundingPolygon);

      // Use line height in table to inform lookback
      const lineHeight = t.cells[0]
        ? yExtent(t.cells[0].line.boundingPolygon)
        : 0;

      const boundingPolygon = [
        { x: tableXRange[0] - 0.1, y: tableYRange[0] - lineHeight - 0.1 },
        { x: tableXRange[1] + 0.1, y: tableYRange[0] - lineHeight - 0.1 },
        { x: tableXRange[1] + 0.1, y: tableYRange[0] },
        { x: tableXRange[0] - 0.1, y: tableYRange[0] },
      ];

      const lines = text.pages[t.page]!.lines.filter((l) =>
        isContained(l.boundingPolygon, boundingPolygon)
      );

      if (lines.length) {
        headers[i] = `${lines.map((l) => l.text).join(" ")} ${headers[i]}`;
      }
    });

    // Find the most promising table via its first two rows embedding
    // Split these calls for cache efficiency
    const descriptionEmbedding = array([
      (await embeddingWithCache([descriptions])).data[0].embedding,
    ]);
    const headerEmbeddings = array(
      (await embeddingWithCache(headers)).data.map((d) => d.embedding)
    );
```

However, I did find that for small snippets, Copilot was fine at explaining the mechanics of what was going on. For example, for this code snippet:

```typescript
      // Use line height in table to inform lookback
      const lineHeight = t.cells[0]
        ? yExtent(t.cells[0].line.boundingPolygon)
        : 0;
```

It returns:

```
/* Here is the explanation for the code above:
1. t.cells[0] is the first cell of the table, so we check if it is defined
2. If it is defined, we get the yExtent of the bounding polygon of the cell
3. If it is not defined, we set the lineHeight to 0 */
```



**Bottom line**

Copilot is great for helping me understand the mechanics or purpose of smaller snippets of code. However, it can't explain the *purpose* or *intent* behind large blocks of code very well -- which is my job as a documentarian.

Theneo review
===

Theneo promises to use AI to help you generate your API docs. 

Getting access
---

Getting access was easy; there was a self-serve signup link at https://www.theneo.io/. 

Experience
---

I was mostly intrigued by the promise of generating docs.  However, it turns out that Theneo is a pretty early-stage startup and lacks documentation, so I ended up with a lot of unanswered questions.

To test its generative capacity, I imported an openapi file I'd worked on, but with most of my description strings removed. 

I liked that there were a variety of formats supported for import:

![copilot settings](/assets/images/theneo_1.png)

Once I was in the API docs editor, my very first exposure to their auto-generated docs wasn't super impressive. It looked like I got to choose between different suggestions for each parameter:

![copilot settings](/assets/images/theneo_4.png)

"The URL of the webhook to be triggered" isn't great docs though -- what's the purpose of the webhook? Compare it to my docs for this particular webhook (again, for Sensible):  

> The webhook specifies to return document extraction results to the defined webhook as soon as they're complete, so you don't have to poll for results status. Sensible also calls this webhook on error. 



So I didn't get to a 'wow' moment in the first few minutes, and that was enough to make me to abandon my evaluation. Maybe there was some AI generative writing capacity that's really gold value in there, but if so, I missed it. 

**Bottom line**

My quick impressions of Theneo:

1. When they said 'stripe like docs' I thought they were promising the "three panel" format stripe offers with full code samples (like this: https://stripe.com/docs/checkout/quickstart) but I was disappointed that doesn't seem the case.
2. Ok so historically, documentation writers have been burned by vendor-lockin with crappy "techcomm tools". Personally that makes me very wary of anything that won't let me control/sync my content directly in GitHub as well as whatever interface the tool offers. (ie tool must play well with 'docs as code'). I can't tell how much Theneo supports this -- they have no docs, and CI deployment tab isn't enabled when I went the free/self-serve signup route so I can't go play with it.
3. I'm not super impressed with the auto-generated descriptions for API parameters at first glance. I'd still need a thinking human writing the docs.
4.  I can't tell how smart the AI generation is -- would it auto-generate reuse strategies for all params with the same description, for example? Would it do so according to the reuse rules of the underlying file format, i.e., for an openapi file, would it use `$ref` syntax? Or would it do something homegrown that I couldn't easily export?

Overall, it does get me thinking that there are plenty of AI-automatable tasks potentially to be done here with human review, but I'm not sure that Theneo has identified -- or at least showcased -- those most valuable areas yet.





