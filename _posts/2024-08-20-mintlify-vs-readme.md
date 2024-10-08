---
layout: single
title: 'Comparing docs platforms: Readme vs Mintlify'
date: '2024-08-21T00:00:00.000Z'
author: frances
modified_time: '2024-08-21T00:00:00.000Z'
---

Recently I investigated migrating from the Readme docs platform to Mintlify for one of my clients, [Sensible](https://sensible.so/). I'll briefly record my impressions here:

### Mintlify pros:

- As of this writing, Mintlify is cheaper than Readme for a comparable set of features.

- In my testing, Mintlify's LLM-powered search results are much more accurate and usefully formatted than Readme's. For example, when I search for "OCR" in the docs I wrote for Sensible, Mintlify's LLM bot gives a far superior answer. Mintlify correctly reassures the reader that Sensible automatically performs OCR before extracting document data, and discusses OCR configuration options for edge cases. Sensible goes off in the wrong direction by discussing how to extract document data using an API call.

  | Mintlify                                     | Readme                                       |
  | -------------------------------------------- | -------------------------------------------- |
  | ![Mintlify LLM](/assets/images/llm_mint.png) | ![Readme LLM](/assets/images/llm_readme.png) |
  
- Mintlify in theory enables publishing your docs as a subpath instead of a subdomain on your main site. I was excited to publish our docs at `sensible.so/docs` instead of `docs.sensible.so`; it would have been a huge SEO boost. Unfortunately, it turned out that with Sensible's Webflow-powered website, I could only have enabled the subpath approach using a hacky and insecure approach; no thanks.

- Mintlify's API reference display is much nicer than Readme's. Readme hides lots of documentation under easily-missed accordions, to the point that many customers ask for API documentation that they don't realize already exists. Mintlify lays it all right out there.

### Mintlify cons:

The platform, while showing a lot of potential, still feels pretty immature when compared to Readme.

In particular, lack of test infrastructure on deployment was a big issue for me. During the migration, I wrote many GitHub actions to test and validate my docs, but I felt the tests should have been baked into the platform already. For example, the following seem like basic misses to me:

  - Invalid MDX would silently fail, so that certain pages weren't rendering at all, with no way for me to discover the problem except manually clicking through topics in the published site.

  - To configure your docs, you edit a `mint.json` config file. That file is the source of truth for your docs, but it's seriously lacking in validation. For example, if I enter an invalid navigation link while building my table of contents in `mint.json`, there's no deployment error. Nor does Mintlify's link-checking CLI tool catch this invalid entry. Likewise, when I mistakenly created two `redirect` parameters, the second set of redirects failed, without warning me that I'd created an extraneous parameter.

I've watched Mintlify deploy features rapidly over the last year or so, so it wouldn't surprise me if these rough edges get smoothed out with time.

In the end, I decided to stick with Readme because the migration process grew too painful. Going from a lax syntax like MD (which Readme supports) to a strict syntax like MDX (which Mintlify supports) was always going to be rough, especially when MDX infamously lacks informative error messages. As it turned out, there were enough formatting errors in the migrated MDX files that Mintlify returned to me that I knew I'd be looking at a manual, line-by-line effort to fix the errors, which I wasn't on board with. I know they're improving their migration process, so maybe the story will be different in future. In the meantime, I'd certainly consider Mintlify for non-migration scenarios, for example when I'm writing docs from scratch in my role as a founding docs writer for startups.
