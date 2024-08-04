---
title: Contributing Merge
permalink: /Contributing/Merge/
---

## Common merge rules

As a start, some things copy pasted from
[Contributing/Code](Contributing_Code "wikilink"):

- People with commit access should always merge their own pull requests.
  Don't merge another contributor's code as they may have good reasons
  to hold back that aren't obvious.
- Get the approval of another team member before merging.
- Do not merge pull requests that have been open for less than 24 hours.
  Mistakes are likely if people don't get a chance to review.

## Merge role hierarchy

I suggest to formally define three roles (this may not translate into
GitHub user interface):

### Super merger

The purpose of super merger role is to be able to take some decisions to
unstuck situations.

The super merger can, as an exception, merge someone else's pull
request, if needed for example if the pull request looks ready but is
sleeping for too long and the submitter is not answering, or to merge
some things that looks ready for a release and delaying a release is not
wanted.

In all cases, those are exceptions and when going the exception way it's
recommended to first write a motivated comment and to wait a delay of
one day between the motivated comment and the merge.

### Merger

Everyone with commit access is a merger, so basically the team members.

A merger can also merge a pull request from a contributor who doesn't
have commit permission, or for any reason explaining why the author will
not do it, the merger is then considered the reviewer and the approver.

Merging someone else's code and being the approver requires the merged
code to have been written against Unvanquished source, porting a code
from another software (for example porting from ioquake3 engine to Dæmon
engine) requires the porting effort to be reviewed by someone else than
the merger.

Any merger is an approver to someone else.

### Contributors

External contributors without commit permission, but submitting pull
requests.

## Closing an unmerged pull request from someone else

### Superseded

If you believe an original pull request that is not yours is superseded
by another one that you believe does the same and that was merged, and
if you believe there is nothing more to merge in the original one, don't
close it immediately but:

> - Ask the original author (mention him in your GitHub comment) if he
>   believes there is nothing left to merge in the original pull
>   request,
> - Express your intention to close the pull request.
>
> If the original author agrees with the closing, you can close the pull
> request without waiting more.
> If there is no answer after one month has passed, you can close the
> pull request.
> Add a comment saying you're closing the PR at the moment you can close
> the pull request.

### Stalled

A pull request is considered stalled if it had no activity in one year.

We don't have dozens of thousands pull request so we have no urge to
clean-up them. Our team is small and the work is sometime done in very
slow pace, so we better not close all stalled PR just for purity.

If you believe a stalled a change from a stalled pull request is wanted
but the pull request can't be merged without being reworked, don't close
it. It will be closed the day a reworked pull request will be merged
instead and after we have followed the “Superseded” pull request closing
rule.

If a pull request that is not yours is stalled and you believe it has no
hope to get merged, you can follow similar rules in order to close it:

> - Ask the original author (mention him in your GitHub comment) if he
>   plans to resume on it,
> - Express your intention to close the pull request.
>
> If the original author agrees with the closing, you can close the pull
> request without waiting more.
> If there is no answer after one month has passed, you can close the
> pull request.
> Add a comment saying you're closing the PR at the moment you can close
> the pull request.
>
> If the original author has deleted his GitHub account, express your
> intention to close the pull request and also wait for a month, to
> leave time to other people of the team to react.

It means a stalled pull request may be closed after one year of stalling
plus one month of lack of response from the original author. It doesn't
mean a stalled pull request should be closed, whatever the time spent in
stalling.

[Category:Contributing](Category:Contributing "wikilink")