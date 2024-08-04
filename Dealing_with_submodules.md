---
title: Dealing with submodules
permalink: /Dealing_with_submodules/
---

## Heavy usage of submodules

The Unvanquished repository makes heavy usage of submodules, and
submodules having submodules.

Most of the time, developers don't have to commit the submodules
themselves. A submodule change that doesn't break compatibility does not
strictly require to be committed.

For example if a pull request is split between and . The submodule is
committed after pull-requests for both repositories are merged.

For a method of working that prevents to mistakenly commits submodule
changes, follow the following instructions.

## Dealing with submodules

### Configuring Git to ignore submodules when diffing and committing

If you're contributing to the , the parent repository is . If you only
contribute to the the and the Dæmon repository is not a submodule, the
parent repository is .

In parent repository type this command:

    git config diff.ignoreSubmodules all

This will remove all submodule changes from and never commit any
submodule change when doing .

### Purposedly diffing and committing submodule changes

To explicitly list submodule changes and commit them you can then do:

    git -c diff.ignoreSubmodules=none diff
    git -c diff.ignoreSubmodules=none commit -am ”message”

### Doing a splitted pull-request

You need to do a splitted pull-request if you have changes in multiples
repositories and requiring each others.

You will have to be a developer with repository write access, and you
will have to push your branches using the exact same branch name, with
suffix. For example the branch would be named like .

The [CI](Continuous_integration "wikilink") automatically fetches
submodule branch when building parent branch.

For example if you modify both and and the changes in requires changes
from to build, you need to do a splitted pull request. You would push
both your Unvanquished and Dæmon changes to upstream with a branch name
like . And the CI will automatically fetch the branches of both and .

### Bisecting a tree with submodules

When bisecting the history, you may have to run on every step.

While a submodule change that doesn't break compatibility does not
strictly requires to be committed, frequent submodule commits makes
easier to bisect the tree in the following time.

That's why from time to time we commit the submodules so we can bisect
the commits committing the submodules. Such commits, only meant for
making bisecting easier, are never done within a pull-requests.

### Checking out across submodule creation/deletion

When you do a checkout that crosses a submodule creation/deletion
boundary, the default behavior of `git checkout` no longer works
reliably:

- If you go from before a submodule deletion (e.g. Unvanquished
  e7f250b0) to after it, its contents will be left in the working tree
  as untracked files.
- If you go from before to after a conversion of a submodule to a
  regular directory (e.g., Git will refuse to check it out at all.
- Going past the Daemon submodule introduction (Unvanquished d7dabfb6a;
  Feb 2017) tends to put the repo in a seriously broken state. None of
  the following advice can deal with that case.

`git submodule update --init --recursive` is no use in these cases, but
they can be fixed by adding flags to `git checkout`:

- `--recurse-submodules` will get it to clean up the deleted submodule
  properly, and also does the job of `git submodule update`
- `--force` convinces Git to go through with replacing the submodule
  with a regular directory. However, you run the risk of erasing unsaved
  work.

As a general method of safely and completely checking out a historical
commit since the Daemon submodule introduction, try

    [ -z "$(git status --porcelain || echo x)" ] && git checkout e7f250b0 --force --recurse-submodules

The checkout only proceeds if the status doesn't error and its output is
empty, which indicates there are no modified or untracked files.

When using `git bisect`, the default is to automatically check out
commits using Git's broken default behavior. You can take responsibility
for checkouts yourself by using `git bisect start --no-checkout`, then
`git checkout --recurse-submodules --force BISECT_HEAD` at each step.