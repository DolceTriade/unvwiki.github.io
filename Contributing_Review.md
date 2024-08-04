---
title: Contributing Review
permalink: /Contributing/Review/
---

__TOC__

## Requesting a review

When submitting a pull-request, it is useful to explain not only what
the code is meant to do and why, but also express the state of the work
you submit and the kind of review you are looking for, in hope this
helps to reduce the pull request being trapped in situations that were
not intended that would slow down the review process.

Here are some questions you are invited to answer when submitting your
work:

**Those changes are implementing:**

- [ ] A fix.
- [ ] A new feature.
- [ ] A rewrite of something that already exists.
- [ ] A clean-up to drop legacy or unused stuff.

**Those changes are:**

- [ ] Made by me.
- [ ] Made by someon else:

**What the changes are for and what are they trying to accomplish:**

**The existing issues related to those changes:**

**My own personnal perceived status of the changes being submitted:**

- [ ] I believe it is ready to merge as is unless proven wrong.
- [ ] I believe it is ready to use but I'm requesting for comments so it
  can be refined.
- [ ] That's a work-in-progress, being made public to get early comments
  and make sure other peoples working on other branches know this is
  being worked on.

**I'm looking for this kind of review:**

- [ ] Generic proof-reading for mistakes.
- [ ] Comments about the the design itself, looking for better ways to
  do things.
- [ ] Opinion on what is expected to be brought or removed, is this
  wanted to begin with? if yes are there better ideas?
- [ ] Opinion on the way it's done or what it plans to achieves.
- [ ] Testing to be sure it works as expected or not regress.

**What I already tested and assume is already verified:**

**I request testing:**

- [ ] On a specific operating system, hardware brand or model, driver
  version:
- [ ] Of specific game options, configurations, in-game actions:

**My changes are expected to integrate this way in the target branch:**

- [ ] As a preparation for future changes that would be submitted in
  another pull request.
- [ ] As a single commit despite this being submitted as separate
  commits.
- [ ] As separate commits because I believe it's better for this change
  to do things step by step and I don't want to lose the ability to
  bisect those steps.

## Reviewing a contribution

When clicking the “Approve” button, please add a comment, a (*Looks Good
To Me*) mention is enough.

A message without any other comment is considered as an approval, better
click Approve anyway. A message with a comment for a better
implementation (not a bug fix) is considered as an approval, better
click Approve anyway.

### If the code looks to have no bug from you point of view

please write LGTM in all cases.

#### If you agree with the purpose of the change

Please write LGTM and Approve.

#### If you disagree with the purpose of the change

Please write LGTM but add a comment explaining why you don't approve.

This way, if the code has no bug, we can solve the politics separately
and if we decide to agree with the purpose of the change, we can merge
it without having to look back at the code, and to not block the merge
because we don't know if code is reviewed yet.

#### If you have a suggestion for a better implementation

Please write LGTM and approve and add a comment with your suggestion,
saying it is a suggestion.

This way, the submitter can decide to follow you or not.

If the submitter merged without following your recommendation, you are
free to implement your recommendation.

### If the code has a bug from your point of view

#### If you know the fix and this is obvious to do

Please state what you believe is a bug and suggest what you believe
would fix the bug.

You can write “LGTM if you do <suggestion>” and then write your
suggestion.

You can consider obvious a fix you believe there is no need to verify
the implementation of your recommendation.

Once the submitter implements your suggested fix the change will be
considered fully approved without needing any new comment.

#### If you don't know the fix or this is not obvious to do

Please explain why you believe is a bug, and if you an idea to fix it,
please share it.

### If you have any remark but it is not blocking

Please write LGTM, approve, and write your remark.

## Suggesting a change

Prefer to point out something that could be better, or suggest a change,
than give a direct order, because nobody is paid for that work and then
everything already done is already a gift that we not deserve.

For example instead of something like:

> Remove leading spaces.

Prefer something like:

> That leading space will be included in the translation string.

Basically, instead of saying what should be done, say why something can
be done.

## Approving the change

When you believe the submitted contribution of someone else is ready to
merge, you can approve it.

By approving someone else contribution, you help a lot this project!
Every merger is an approver.

[Category:Contributing](Category:Contributing "wikilink")