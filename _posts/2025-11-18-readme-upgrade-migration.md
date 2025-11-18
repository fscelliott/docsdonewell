---
"title": Guide to  recent breaking API Readme changes
---

About a week ago, I got an email that my Readme-based documentation project for a client would be automatically migrated to the newest version. I knew this would break my existing third-party GitHub [integration](https://github.com/flowcommerce/readme-sync), which relies on an older version of the Readme API and which I chose at a time when Readme's own GitHub integration was much less powerful than it now is. Side note: I never want to submit to the inefficiencies inherent in authoring docs in a webapp, and will move heaven and earth to achieve static site generation! Even if it meant choosing a third-party open source tool that's now archived, it was still worth it!

After skimming Readme's documentation on the upgrade, I had several pressing concerns that I've since cleared up through sandbox tests in advance of the migration. I'll note them here in case they help other:

- **Question**:  I'm worried about obscure and difficult to troubleshoot syntax errors when I move from a lax markup (MD) to a strict markup (MDX), given that in my experience MDX has lousy error messages (often lacking line numbers for example). Will this be a terrible PITA requiring line-by-line hand editing?
  - **Answer**: Not a big problem, as it turns out. I had maybe 9 topics out of hundreds throw errors. I found that LLMs were really helpful for troubleshooting the syntax errors and sped up the process incredibly. My best prompt responses were when I gave Claude a whole MD topic as context and asked, `Which lines in this topic contain MDX errors? Provide reasoning, evidence, and line numbers`.  Asking for "reasoning" and "evidence" seemed to greatly improve the results. Of course it wasn't perfect -- once as a sanity test, I asked the LLM if an MD topic contained any curly braces that weren't properly contained in code fences. The LLM replied no -- even though I was staring at the offending curly brace in question! 

- **Question**: Will the transition from MD to MDX respect all my markup tags? In trial migrations to other platforms, I've noticed that the conversion stripped my `<br/>` tags, for example -- hugely important for some of my reference topic formatting!
  - **Answer**: Pretty smooth! I've noticed all my formatting tags are respected. 
- **Question:** Can I sync my openapi YAML spec, or is this a one-time import? It would be a dealbreaker in inefficiency if I had to maintain an API reference in MDX going forward! 
  - **Answer**, yes I can sync it! At first, I was under the impression that with Readme's bi-directional sync, I'd be forced into a one-time import of my spec.  But happily I was wrong. If you import your spec file, you get a chance to disable webapp modifications. After that, they'll persist a copy of your spec in their static file directory; just point your URL in the webapp to that new instance, and you'll have bi-directional syncing of the spec file. <sup>2</sup>
- **Question:** I have an existing static file directory. Will I have to commit to manually restructuring static file directories and reauthoring their metatdata frontmatter? That would be a PITA, but I can see their latest CLI demands a different structure than I currently use.<sup>1</sup> 
  - **Answer**: If I use bidirectional sync, then no, I don't have to restructure my files at all. They upgrade me and populate the webapp with my MDX topics; I point the webapp admin site at a target empty GitHub repo, and it syncs the files to that repo in the desired file format and directory structure. Yay! I can effectively abandon my old MD files; I don't have to convert them by hand to MDX.

- **Question**: What's the deal with GitHub branching and bi-directional syncing? Do I have to rename my `main` branch in GitHub to a semantic version?
  - **Answer**: I think that Readme maybe expects you to ignore the GitHub `main` branch, and instead treat a versioned branch as your permanently open, published branch, e.g. `v1.0`? Let me know if I'm wrong! That seems to be working for me at present, but what that means is that I'm constantly ignoring prompts from GH to create pull requests from my versioned branch into main. (My main branch is just empty at this point)

- **Question** GitHub actually syncing? Can I force a sync? Why isn't my change showing up?
  - **Answer** Bi-directional syncing is a lot slower that what I'm used to with my existing integration, but if I wait a few minutes I see changes show up. I haven't yet found a way to manually kick off a sync, but I notice the flow is much faster from webapp -> GH than GH --> webapp. I also notice that a webapp page edit won't sync to GitHub until I both save AND navigate away from the page (at least if I'm syncing to my published branch). Wish I could see status through a GitHub action, but alas, that's not the case.




**Footnotes**

1. You can't use bi-directional sync and the CLI together; they're separate tools requiring separate static file directory structures. The structure required by the bi-directional sync looks more elegant and maintainable to me.
2. It does appear that through the web app, someone can make minor edits to the MDX, and Readme combines those MDX edits plus your spec file to publish the API reference. I'll probably discourage my contributors from making such edits just to keep things centralized.

