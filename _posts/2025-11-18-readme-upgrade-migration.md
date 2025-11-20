---
"title": Guide to  recent breaking API Readme changes
---

Recently I learned that Readme would automatically migrate one of my documentation projects to their newest version. I knew this would break my existing third-party GitHub [integration](https://github.com/flowcommerce/readme-sync), which relies on an older version of the Readme API and which I chose at a time when Readme's own GitHub integration was much less powerful than it now is. Side note: I will move heaven and earth to achieve static site generation rather than submit to the inefficiencies inherent in authoring docs in a webapp. Even if it meant choosing a third-party open source tool that's now archived, it was still worth it!

After skimming Readme's documentation on the upgrade, I had several pressing concerns that I've since cleared up through sandbox tests in advance of the migration. I'll note these advanced Q&As here in case they help documentarians:

- **Question**:  I'm worried about obscure and difficult-to-troubleshoot syntax errors when I move from a lax markup (MD) to a strict markup (MDX). In my experience MDX has lousy error messages. Will this be a terrible PITA requiring line-by-line editing?
  - **Answer**: Not a big problem, as it turns out. Maybe 9 topics out of hundreds threw syntax errors. I found that LLMs were really helpful for resolving inadequate syntax error messages. My most successful strategy was to provide Claude with a complete MD topic as context and prompt, `Which lines in this topic contain MDX syntax errors? Provide reasoning, evidence, and line numbers`.  Asking for "reasoning" and "evidence" seemed to greatly improve the results. Of course it wasn't perfect -- as a sanity test, I asked the LLM if an MD topic contained any curly braces that weren't properly contained in code fences. The LLM replied no -- even though I was staring at the offending curly brace in question! 

- **Question**: Will the transition from MD to MDX respect all my markup tags? In trial migrations to other platforms, I've noticed that the conversion stripped my `<br/>` tags, for example -- hugely important for some of my reference topic formatting!
  - **Answer**: I've noticed all my formatting tags are respected, whew! 
- **Question:** Can I sync my openapi YAML spec, or is this a one-time import? Maintaining an API reference in MDX would be a deabreaking inefficiency! 
  - **Answer**, yes I can sync it with Readme's bidrectional sync feature, contrary to my initial impression! If I import my spec file in the webapp, I get a chance to disable webapp modifications. After that, Readme persists a copy of my spec in the source GitHub file directory; I just point my URL in the webapp to that new instance, and the spec is synced.<sup>2</sup>
- **Question:** I see Readme's latest CLI demands a different file structure than I currently use. Must I manually restructure static file directories and reauthor their metatdata frontmatter? That would be a PITA!<sup>1</sup> 
  - **Answer**: If I use bidirectional sync and avoid the CLI, then no, I don't have to restructure my files. Readme automatically upgrades me and populates the webapp with my new MDX topics; I point the webapp admin site at a target empty GitHub repo, and it syncs the files to that repo in the desired file format and directory structure. Yay! I can effectively abandon my old MD files; I don't have to convert them by hand to MDX.

- **Question**: What's the deal with GitHub branching and bidirectional syncing? Do I have to rename my `main` branch in GitHub to a semantic version?
  - **Answer**: I believe that Readme expects you to ignore the GitHub `main` branch, and instead treat a versioned branch as your permanently open, published branch, e.g. `v1.0`. That seems to be working for me at present, but what that means is that I'm constantly ignoring prompts from GitHub to create pull requests from my versioned branch into main. (My main branch is simply empty at this point).

- **Question:** Is GitHub actually syncing? Can I force a sync? Why isn't my change showing up?
  - **Answer** Bidirectional syncing is a lot slower that my previous integration, on the order of minutes. I haven't yet found a way to manually kick off a sync, but I notice the flow is much faster from webapp -> GH than GH --> webapp. I also notice that a webapp page edit won't sync to GitHub until I both save AND navigate away from the page (at least if I'm syncing to my published branch). I wish I could see status through a GitHub action, but alas, that's not the case.




**Footnotes**

1. You can't use bidirectional sync and the CLI together; they're separate tools requiring different static file directory structures. The structure required by the bidirectional sync appears more elegant and maintainable to me.

2. It _does_ appear that through the web app, someone can make minor edits to the MDX, and Readme combines those MDX edits plus your spec file to publish the API reference. I'll probably discourage my contributors from making such edits just to keep things centralized.

