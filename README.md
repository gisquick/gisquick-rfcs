# Gisquick RFCs

## What is an RFC?

The "RFC" (request for comments) process is intended to provide a
consistent and controlled path for new features or changes.

Many changes, including bug fixes and documentation improvements can be
implemented and reviewed via the normal GitHub pull request workflow.

Some changes though are "substantial", and we ask that these be put
through a bit of a design process and produce a consensus among the
Gisquick core team and the community.

## The RFC life-cycle

An RFC goes through the following stages:

- **Pending:** when the RFC is submitted as a PR.
- **Active:** when an RFC PR is merged and undergoing implementation.
- **Landed:** when an RFC's proposed changes are merged to master.
- **Rejected:** when an RFC PR is closed without being merged.

[Pending RFC List](https://github.com/gislab-npo/gisquick-rfcs/pulls)

## When to follow this process

You need to follow this process if you intend to make "substantial"
changes to any part of Gisquick platform listed below:

[gisquick](https://github.com/gislab-npo/gisquick)
[gisquick-settings](https://github.com/gislab-npo/gisquick-settings)
[qgis-plugin](https://github.com/gislab-npo/gisquick-qgis-plugin)

If you submit a pull request to implement a new feature without going
through the RFC process, it may be closed with a polite request to
submit an RFC first.

Other use case for RFC is to present "substantial" feature request,
which should be implemented by Gisquick's core team. In this case,
feature should be evaluated, and approximate cost of implemention should
be estimated. If there will be enough will to accept this feature,
and funding for development will be arranged, the RFC should become
active and impleentation of feature should start.

## Why do we need to do this

Every new feature adds more complexity to the project. Sometimes it takes
significant time to implement particular functionality, and also there
may be demand for several similar features. It's better to have a consistent
workflow for documenting of what is planned, new ideas and proposals,
or for public discussion.

## Gathering feedback before submitting

It's often helpful to get feedback on your concept before diving into the
level of details required for an RFC. **You may open an issue on this repo
to start a high-level discussion**, with the goal of eventually formulating
an RFC pull request with the specific proposal/implementation.

## What the process is

In short, to get a major feature added to Gisquick, one must first get the
RFC merged into the RFC repo as a markdown file. At that point the RFC
is 'active' and may be implemented with the goal of eventual inclusion
into Gisquick.

* Fork the RFC repo https://github.com/gislab-npo/gisquick-rfcs

* Copy `0000-template.md` to `active-rfcs/0000-my-feature.md` (where
'my-feature' is descriptive. don't assign an RFC number yet).

* Fill in the RFC. Put care into the details.

* Submit a pull request. As a pull request the RFC will receive design
feedback from the larger community, and the author should be prepared
to revise it in response.

* Build consensus and integrate feedback. RFCs that have broad support
are much more likely to make progress than those that don't receive any
comments.

* Eventually, the [core team] will decide whether the RFC is a candidate
for inclusion.

* An RFC can be modified based upon feedback from the [core team] and community.
Significant modifications may trigger a new final comment period.

* An RFC may be rejected after public discussion has settled
and comments have been made summarizing the rationale for rejection.
A member of the [core team] should then close the RFC's associated pull request.

* An RFC may be accepted at the close of its final comment period. A [core team]
member will merge the RFC's associated pull request, at which point the RFC will
become 'active'.

## Details on Active RFCs

Once an RFC becomes active then authors may implement it and submit the
feature as a pull request to the Gisquick repo. Becoming 'active' is not a rubber
stamp, and in particular still does not mean the feature will ultimately
be merged; it does mean that the core team has agreed to it in principle
and are amenable to merging it.

Furthermore, the fact that a given RFC has been accepted and is
'active' implies nothing about what priority is assigned to its
implementation, nor whether anybody is currently working on it.

Modifications to active RFC's can be done in followup PR's. We strive
to write each RFC in a manner that it will reflect the final design of
the feature.

## Implementing an RFC

The author of an RFC is not obligated to implement it. Of course, the
RFC author (like any other developer) is welcome to post an
implementation for review after the RFC has been accepted.

An active RFC should have the link to the implementation PR listed if there is one.
Feedback to the actual implementation should be conducted in the implementation PR
instead of the original RFC PR.

If you are interested in working on the implementation for an 'active'
RFC, but cannot determine if someone else is already working on it,
feel free to ask (e.g. by leaving a comment on the associated issue).

## Reviewing RFC's

Members of the [core team] will attempt to review some set of open RFC
pull requests on a regular basis. If a core team member believes an RFC PR
is ready to be accepted into active status, they can approve the PR using
GitHub's review feature to signal their approval of the RFC.

**Gisquick's RFC process owes its inspiration to the [Vue RFC process] and [React RFC process]**

[Vue RFC process]: https://github.com/vuejs/rfcs
[React RFC process]: https://github.com/reactjs/rfcs
