---
"title": Guide to  recent breaking Readme changes
---

About a week ago, I got an email that my Readme-based documentation project for a client would be automatically migrated to the newest version. I knew this would break my existing sync GitHub [integration](https://github.com/flowcommerce/readme-sync), which relies on an older version of the Readme API and which I chose at a time when Readme's own GitHub integration was much less full featured than it now is. Side note: I never want to submit to the inefficiencies inherent in authoring docs in a webapp, and will move heaven and earth to achieve a static site generation flow! Even if it meant choosing a third-party open source tool that's now archived, it was still worth it!



From Readme's documentation on the upgrade, I had several pressing concerns that I've since cleared up through sandbox tests in advance of the migration. I'll note them here in case they help other:



- **Question**:  I'm worried about obscure and difficult to troubleshoot syntax errors when I move from a lax markup (MD) to a strict markup (MDX), given that in my experience MDX has lousy error messages (often lacking line numbers for example). Will this be a terrible PITA requiring line-by-line hand editing?
  - **Answer**: Not a big problem, as it turns out. I had maybe 9 topics out of hundreds throw errors. I found that LLMs were really helpful for troubleshooting the syntax errors and sped up the process incredibly. My best prompt responses were when I gave it a whole MD topic as context and asked, `Which lines in this topic contain MDX errors? Provide reasoning, evidence, and line numbers`.  Asking for "reasoning" and "evidence" seemed to greatly improve the results. Of course it wasn't perfect -- once as a sanity test, I asked it if an MD topic contained any curly braces that weren't properly contained in code fences. The LLM replied no -- even though I was staring at the offending curly brace in question! 

- **Question**: Will the transition from MD to MDX respect all my markup tags? In trial migrations to other platforms, I've noticed that the conversion stripped my `<br/>` tags, for example -- hugely important for some of my reference topic formatting!
  - **Answer**: Pretty smooth! I've noticed all my formatting tags are respected. 
- Can I sync my openapi YAML spec, or is this a one-time import? It would be a dealbreaker in inefficiency if I had to maintain an API reference in MDX going forward! 
  - Whew, yes I can sync it! At first, I was under the impression that with Readme's bi-directional sync, I'd be forced into a one-time import of my spec. I thought I'd have to use their latest CLI instead, which would have been a terrible transition involving restructuring static file directories and reauthoring their metatdata frontmatter.<sup>1</sup>  But happily I was wrong. If you import your spec file, you get a chance to disable webapp modifications. After that, they'll persist a copy of your spec in their static file directory; just point your URL in the webapp to that new instance, and you'll have bi-directional syncing of the spec file. <sup>2</sup>
- **Question**: What's the deal with GitHub branching and bi-directional syncing? Do I have to rename my `main` branch in GitHub to a semantic version?
  - **Answer**: I think that Readme maybe expects you to ignore the GitHub `main` branch treat a versioned branch as your permanently open, published branch, e.g. `v1.0`? Let me know if I'm wrong! That seems to be working for me at present, but what that means is that I'm constantly ignoring prompts from GH to create pull requests from my versioned branch into main. (My main branch is just empty at this point)

- Is GitHub actually syncing? Can I force a sync? Why isn't my change showing up?
  - The bi-directional syncing is a lot slower that what I'm used to with my existing integration, but wait a few minutes and you'll see your changes show up. I haven't yet found a way to manually kick off a sync, but it is much faster from webapp -> GH than GH --> webapp.




**Footnotes**

1. You can't use bi-directional sync and the CLI together; they're separate tools requiring separate static file directory structures as far as I can tell.
2. It does appear that through the web app, someone can make minor edits to the MDX, and Readme combines those MDX edits plus your spec file to publish the API reference. I'll probably discourage my contributors from making such edits just to keep things centralized.

