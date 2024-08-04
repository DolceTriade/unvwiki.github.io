---
title: Contributing Code
permalink: /Contributing/Code/
---

As we use GitHub for hosting, you may very easily
[fork](https://help.github.com/articles/fork-a-repo) our
[project](https://github.com/Unvanquished/Unvanquished) (or any
sub-project, such as the [Dæmon](https://github.com/DaemonEngine) engine
or [Urcheon](https://github.com/DaemonEngine/Urcheon)). From there, you
may [open a pull
request](https://help.github.com/articles/using-pull-requests).

## Before you start coding

If your intended change may be controversial, or you're not sure how to
implement it, it would be wise to discuss your intentions with other
developers via [chat](chat "wikilink"), the , or a GitHub issue. In the
case of a gameplay change, it should be discussed on the [gameplay
tracker](https://github.com/Unvanquished/gameplay).

## Correct and readable code

- Follow established [coding conventions](Coding_convention "wikilink").
- Test your commit before opening a pull request or pushing.
- Verify that your code passes the [automated
  builds](Continuous_integration "wikilink"). After you open a pull
  request in GitHub, you will see messages about "checks passing" or
  "checks failing", which indicate their status. To catch more warnings
  before you push, consider enabling the USE_WERROR CMake option.

## Proper Git usage

- Write [good commit
  messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).
- Each individual commit should successfully compile and ideally be
  otherwise free of regressions. Correspondingly, when revising a pull
  request under review, rebase and modify earlier buggy commits rather
  than adding "fix" commits at the end.
- Avoid submitting a large number of commits in one pull request.

## GitHub etiquette

- People with commit access should always merge their own pull requests.
  Don't merge another contributor's code as they may have good reasons
  to hold back that aren't obvious.
- Get the approval of another team member before merging.
- Do not merge pull requests that have been open for less than 24 hours.
  Mistakes are likely if people don't get a chance to review.

[Category:Contributing](Category:Contributing "wikilink")