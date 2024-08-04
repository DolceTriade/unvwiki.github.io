---
title: Contributing Patches
permalink: /Contributing/Patches/
---

The standard way to contribute changes is to fork the repository, commit
the change, push it to a git branch and then open a pull request on our
forge. Our current forge being hosted by GitHub, a GitHub account is
therefore needed. If one day we host our forge elsewhere (for example on
GitLab), an account on that other place would be required instead.

If for some reasons you cannot have an account on GitHub, you may rely
on patches, but it is required to strictly follow those rules:

- You have to find someone willing to merge your commit in a branch for
  you, push that branch, and do the pull request for you. It is
  important that prior to you sending your patches, you have to find
  someone “willing” to do the pull-request task for you. It is not
  permitted to “expect” someone to do it.
- The patches should be based on a current development branch at the
  time of the publication, the target branch being either our a future
  branch named like . If the commit is older at the time you publish the
  patch, the rebase task up to you.
- The commit should be distributed with the explicit reference it is
  expected to be merged on, this reference being part of an upstream
  development branch as said earlier. If the patch format doesn't carry
  this information, this information should be given in any way of
  attachment to the patch. For example if you send patches by mail to
  someone willing to do the pull-request work for you, if the patch
  format doesn't carry the parent commit reference, you should write
  this reference down in the mail body.
- As with native git commits, patch should come with meaningful enough
  titles.

When behaving with the team and with people willing to do pull-request
tasks for you, or not, it is important to remember that :

- Publishing a patch never creates an expectation that should be
  fulfilled.
- The one willing to do the pull-request task for you has full rights to
  stop willing to at any time.
- It is not allowed to put any pressure on someone willing to do for you
  something that is up to you.
- It's better to avoid any pressure on anyone in all cases.

If you cannot push to GitHub but you can push your changes to another
public Git repository somewhere else, it is better to push and publish
our changes on such public Git repository than sending raw patches,
rebased on current target development branch as usual. This strongly
reduces the amount of work to do for the one willing to do the pull
request task for you and then increases your chance to find someone
willing to and reduce the chance of the one willing to do being
discouraged by the effort.

[Category:Contributing](Category:Contributing "wikilink")