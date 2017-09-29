Introduction
=============

Please begin by reading and understanding the following article (don't hesitate
to ask questions if you need to); it is one of the most articulate and
well-formed explanations of a useful git workflow that I have found to date:
`Git Workflow <http://nvie.com/posts/a-successful-git-branching-model/>`_

Key Branching Differences
---------------------------

The article above outlines the essence of what we will be following, but with
some minor differences:

*   We will not be merging anything into the master branch until we fully
    release into production mode

*   We will not be using any hotfix branches until we fully release into
    production mode

*   We may decide not to use release branches and opt to have releases be
    merges from develop instead (but they must be tagged!); once more
    automation tools are added to the project, it may be useful to have release
    or staging branches which can be automatically deployed to a QA environment
    before being released

This means that currently, the important aspects of the flow are the develop,
and feature branches, along with utilizing Pull Requests to merge features into
develop.

Pull Requests
================

There may be certain exceptions, however, as a general rule, please always use
a Pull Request to get review or approval before merging anything into any
branch; when creating the PR, make sure to check that the branch you are
merging into is set correctly and that you tag or mention anyone who might need
to provide input on the PR! If we want to do squash merges for feature branches
or non-default merges, then we will have to opt not to use the "Merge" button
provided in Bitbucket and handle our merges manually once a PR has been
approved.

Feature Branch Naming Conventions
------------------------------------

For the context of our projects, feature branches are meant to semantically
encompass any task, feature, improvement, etc. that we are working on in
development. These feature branches should only be merged to develop, never
anything else.

Unless there is a specific reason not to, there should almost always be a JIRA
task for what is being worked on; as long as there is a JIRA task, you should
always prefix your branch name with the task identifier. To use the task for
creating this documentation as an example, I would create a branch off of
develop called "DSNP-44-document-git-workflow". This allows JIRA to
automatically associate that branch with the task when you push commits in the
branch to the origin.

Commit Messages
==================

Start by reading
`this article <http://chris.beams.io/posts/git-commit/>`_
which explains a concrete stance on the matter that will be discussed below.

Consistent formatting is important for commit messages. We will not necessarily
be enforcing everything exactly as written in the above article, but please
follow the "seven rules of a great commit message" that it outlines with the
exception of character wrapping, and one additional rule specific to our team.
As shown below, our commit message rules modify the character limits. For
example, if your subject line is 55 or 60 characters... we are not going to be
strict about enforcing a 50 character limit. However, if your subject line is
70 or 100 characters... please find a way to reduce it, and add a body to the
commit message if there is additional information.

Commit Message Guidelines:

*   Separate subject from body with a blank line
*   Limit the subject line to ~60 characters
*   Capitalize the subject line
*   Do not end the subject line with punctuation
*   Use the imperative mood in the subject line
*   Wrap the body at ~80 characters
*   Use the body to explain what and why, not how
*   Prefix your subject line with the JIRA task ID
    (e.g. "DSNP-44 Add git workflow documentation")

Smart Commits:

<coming soon (not currently enabled for our project)!>
