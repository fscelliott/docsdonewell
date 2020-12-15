---
layout: single
title: Docs-first tip: test prerelease Github packages
date: '2020-12-15T09:55:00.001-08:00'
author: frances
modified_time: '2020-12-15T13:13:14.240-08:00'


---

I'm all about a docs-first approach -- for example, in the latest SDK domain-model overhaul I participated in, I was able to contribute to the API's call signature consistency  by commenting early on the technical design docs.

I'm also about testing my code samples as early as possible! And today I found a way to do it in Python; hope it helps other! I'm sure it's quite familiar to QA teams, but it was my first time figuring it out (guess I've never been so ahead of a release curve as now).

### Question: I wanted to test a prerelease branch of an SDK hosted as a python package on Github. Normally I install this package through pip, like `pip some-sdk`. How to install it straight from GitHub?

### Answer:

It's pretty simple! I used pipenv. For example, say I wanted to install the new-feature-branch branch of https://github.com/some-sdk. In an empty project dir, I can run:


`pipenv install -e git+https://github.com/some-sdk.git@new-feature-branch#egg=some-sdk`

Then I just run my sample code using pipenv:

`pipenv run python sample_code.py`

I'm sure there are similarly easy approaches for other nice package managers, like npm for javascript, etc.

### Resources that helped me:

- https://stackoverflow.com/questions/47617552/how-to-specify-in-the-pipfile-package-from-custom-git-branch-using-pipfile

- https://stackoverflow.com/questions/21638929/how-to-determine-the-name-of-an-egg-for-a-python-package-on-github

### Troubleshooting

If you're not getting the results you expect:
- are you pulling the branch as you expect? do you see the methods/attributes that you expect from your branch? you can examine your module in your code, for example: 
  `import somesdk ` then `print(dir(somesdk)) #see methods and attributes`
- try `pipenv clean` to uninstall anything not specified in Pipfile.lock
- examine your Pipefile.lock. Does the `req` for your package listed there match the latest commit hash for the branch you want?
- 
