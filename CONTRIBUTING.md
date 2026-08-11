# Contributing to the Podman Container Tools Projects

We'd love to have you join the community!
Below summarizes the processes that we follow.

Note the Podman Container Tools organization is a large GitHub organization with many different people working on different tools and libraries.
Please also read the contributing docs in each repository, if they exist, as they may contain more repository-specific information.

This document is not specific to any language; language-specific guidelines are contained in other files.
Rules specific to the Go language can be found [here](CONTRIBUTING_GO.md).
We recommend you read the guidelines of the language your repository is written in after finishing with this file.

This document is primarily aimed at the above-listed repositories within the Podman Container Tools GitHub organization.
However, most of the things here listed are very generic and apply when contributing to most public projects

## Topics

* [LLM ("AI") Policy](#llm-ai-policy)
* [Communications](#communications)
* [Reporting Issues](#reporting-issues)
* [Working On Issues](#working-on-issues)
* [Submitting Pull Requests](#submitting-pull-requests)
  * [Describe your Changes in Commit Messages](#describe-your-changes-in-commit-messages)
  * [DCO Sign-off](#DCO-Sign-off)
  * [Code review](#code-review)
  * [Rebasing](#rebasing)
* [Find bad changes with git bisect](#find-bad-changes-with-git-bisect)
* [Becoming a Maintainer](#becoming-a-maintainer)

## LLM ("AI") Policy

If your contribution is aided by LLMs or other AI tools, please read the [LLM Policy](LLM_POLICY.md).
This project follows this LLM policy, which includes comments, issues, PRs, and any other interactions with the team.

## Communications

For general user support questions please use these channels:

- **Matrix**: [Podman Matrix Room](https://matrix.to/#/#podman:matrix.org)
- **Discord**: [Join our Discord server](https://discord.gg/x5GzFF6QH4)
- **IRC**: `#podman` on [libera.chat](https://libera.chat/)
- **GitHub Discussions**: Ask questions and share ideas in our project repositories under the Discussions Tab.

While some maintainers are active in these channels most help is given by other experienced users.
Please be patient when you ask questions, there is also no guarantee that someone will give you an answer.
If you think you found a bug it should be reported on GitHub, but see [Reporting Issues](#reporting-issues) first below.

To reach maintainers, use our development Matrix channel on [#podman-dev:matrix.org](https://matrix.to/#/#podman-dev:matrix.org).
This channel is only used to coordinate the development of the Podman Container Tools Projects.
Use it to discuss project changes, highlight critical issues, or to ask for reviews of specific PRs.
Please do not spam this channel with unrelated information.

We follow the CNCF [Code of Conduct](https://github.com/cncf/foundation/blob/main/code-of-conduct.md) across all channels and repositories.

## Reporting Issues

Before reporting an issue, check our backlog of Open GitHub Issues to see if someone else has already reported it.
If so, feel free to add your scenario, or additional information, to the discussion.
Or simply "subscribe" to it to be notified when it is updated.
Please do not add comments like "+1" or "I have this issue as well" without adding any new information.
Instead, please add a thumbs-up emoji to the original report.

Note: Older closed issues/PRs are automatically locked.
If you have a similar problem please open a new issue instead of commenting.

If you find a new issue with the project we'd love to hear about it!
The most important aspect of a bug report is that it includes enough information for us to reproduce it.
Please include as much detail as possible, including all requested fields in the template.
Not having all requested information makes it much harder to find and fix issues.
A reproducer is the best thing you can include.
Reproducers make finding and fixing issues much easier for maintainers.
The easier it is for us to reproduce a bug, the faster it'll be fixed!
It is your responsibility to narrow down the problem to a reasonable extent. We may not be willing to
run complex third party applications. Ideally the reproducer uses only our command line applications
or other common applications that can be assumed to be available on most Linux distributions.
For example, using curl for API queries is perfectly fine, while some large (unknown) Python script
with many external dependencies would not be a minimal reproducer.
If you do not provide the requested information, we may close the issue if we cannot reproduce it.

In general, we only support the latest upstream release. Therefore, we expect you to test that the problem
still exists in the latest version before reporting a bug. Each release fixes many bugs, so it is possible
that the problem you report has already been fixed. If you are able to compile from the main branch and
test there; that would be even better, though we do not normally require that.

Also the issue tracker is for actual problems/features or other things that maintainers
may need to work on. It is not a tool to get generic end user support, you can use GitHub Discussions for that.

Please don't include any private/sensitive information in your issue!
Security issues should NOT be reported via GitHub and should instead be reported via the process described [here](SECURITY.md).

## Working On Issues

Once you have decided to contribute to Podman by working on an issue, check the unassigned backlog of open issues in the
repository you want to work. If you want to work on a specific issue that is already assigned but does not appear
to be actively being worked on, please ping the assignee in the issue and ask if you can take over.
If they do not respond after several days, you can notify a maintainer to have the issue reassigned.
When working on an issue, please always assign it to yourself.
In some repositories you can use the `/assign` bot command in a comment on an issue to assign it to yourself. If that does not work simply state in the comment that you are working on it.

Never open a PR for an issue when another PR is already open and linked to that issue. If the existing PR was not
reviewed yet; try contacting a maintainer to ask about the status if you'd like to see the fix merged.
If the PR was reviewed but the author abandoned it, i.e., did not respond to review comments, you can ask a maintainer
if you can take it over instead.

## Submitting Pull Requests

No Pull Request (PR) is too small!
Typos, additional comments in the code, new test cases, bug fixes, new features, more documentation, ... it's all welcome!

If you are a new contributor to the project, please do not create more than two open Pull Requests. If the existing PRs
have not been reviewed yet, please wait before opening more PRs; this may be enforced via a GitHub setting depending
on the repository activity. Do not spam-ping maintainers for reviews. If the PR has not been reviewed after several
weeks, you can try to ping a maintainer and ask nicely or use our [communication channels](#communications).

Our projects follow the normal GitHub PR workflow for contributions.
If you never worked with GitHub and git before you likely first need to understand some basic about them.
The general work you have to do when you contribute the first time is something like this:
 - Fork the project on GitHub.
 - Clone that fork locally.
 - Create a new branch.
 - Make your change and commit it.
 - Push the branch to your fork.
 - Open a PR against the upstream repo.

You can find some easy tutorial online such as [this one](https://opensource.com/article/19/7/create-pull-request-github)
and check out the official [GitHub docs](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests)
that contain much more detail.

All development happens on the `main` branch so all PRs should be submitted against that branch.
Maintainers will take care of backporting if needed.

While bug fixes can first be identified via an "issue" in GitHub, that is not required.
It's ok to just open up a PR with the fix, but make sure you include the same information you would have included in an issue - like how to reproduce it.

PRs for new features should include some background on what use cases the new code is trying to address.
When possible and when it makes sense, try to break-up larger PRs into smaller ones - it's easier to review smaller code changes.
But only if those smaller ones make sense as stand-alone PRs.

Regardless of the type of PR, all PRs should include:
* Well-documented code changes, both through comments in the code itself and high-quality commit messages.
  A commit message should answer *why* a change was made.
* Additional tests. Ideally, they should fail without your code change applied. A test can be a unit test
  (see language-specific documentation for details on these) or in a more complex suite often found in the
  `test/` or `tests/` directory in each respective repo. Sometimes it may not be possible to add a useful
  test (e.g. a race condition that is very hard to trigger), in that case a maintainer can decide to merge
  without tests.
* Documentation updates to reflect the changes made in the pull request often found in the `docs/` directory.

Squash your commits into logical pieces of work that might want to be reviewed separate from the rest of the PRs.
Code changes, test and documentation updates should be part of the same commit as long as they are for the same
feature/bug fix. Dependency updates are best kept in an individual commit. Totally unrelated changes, i.e.
fixing typos in a different code part or adding a completely different feature should go into their own PR.
Often squashing down to just one commit is acceptable since in the end the entire PR will be reviewed anyway.
When in doubt, ask a maintainer how they prefer it.

When your PR fixes an issue, please note that by including `Fixes: #00000` in the commit description.
For a simple PR with one commit the PR description should normally be just the same message you wrote
in the commit message.
More details on this are below, in the "Describe your changes in Commit Messages" section.

Most of our repositories follow a two-ack policy for merges.
PRs will be approved and reviewed by maintainers or reviewers listed in the `MAINTAINERS.md` file from the
respective repository or the core maintainers which are listed here [`MAINTAINERS.md`](MAINTAINERS.md).
They will then be merged by one of these maintainers. Two reviews are normally required for a pull request to be merged.
Small PRs, like a simple typo fix or a small dependency update, are OK to be merged with just one review.

### Describe your Changes in Commit Messages

Describe your problem.
Whether your patch is a one-line bug fix or 5000 lines of a new feature, there must be an underlying problem that motivated you to do this work.
Convince the reviewer that there is a problem worth fixing and that it makes sense for them to read past the first paragraph.

Describe user-visible impact.
Straight up crashes and lockups are pretty convincing, but not all bugs are that blatant.
Even if the problem was spotted during code review, describe the impact you think it can have on users.
Keep in mind that the majority of users run packages provided by distributions, so include anything that could help route your change downstream.

Quantify optimizations and trade-offs.
If you claim improvements in performance, memory consumption, stack footprint, or binary size, include
numbers that back them up.
But also describe non-obvious costs.
Optimizations usually aren’t free but trade-offs between CPU, memory, and readability; or, when it comes to heuristics, between different workloads.
Describe the expected downsides of your optimization so that the reviewer can weigh costs against
benefits.

Once the problem is established, describe what you are actually doing about it in technical detail.
It’s important to describe the change in plain English for the reviewer to verify that the code is behaving as you intend it to.

Solve only one problem per patch.
If your description starts to get long, that’s a sign that you probably need to split up your patch.
For a feature or bug, we expect code, docs, and tests to be part of the same commit. Do not split them into
separate commits unless they are actually about different things.

If the patch fixes a logged bug entry, refer to that bug entry by number or URL at the end of the commit message
but before the [DCO Sign-off](#DCO-Sign-off) line.
If the patch follows from a mailing list discussion, give a URL to the mailing list archive.
Please format these lines as `Fixes:` followed by the URL or, for GitHub bugs, the bug number preceded by a #.
For example:

```
Fixes: #00000
Fixes: https://github.com/podman-container-tools/<repository>/issues/00000
```

However, try to make your explanation understandable without external resources. The shared URL should also not
be a private site to ensure all contributors and maintainers can access it.
In addition to giving a URL to a mailing list archive or bug, summarize the relevant points of the discussion that led to the patch as submitted.

If you want to refer to a specific commit, don’t just refer to the SHA-1 ID of the commit.
Please also include the oneline summary of the commit, to make it easier for reviewers to know what it is about. If the commit was merged in GitHub, referring to a GitHub PR number is also a good option, as that will retain all discussion from development, and makes including a summary less critical.
Examples:

```
Commit f641c2d9384e ("fix bug in rm -fa parallel deletes") [...]
PR #00000
```

When referring to a commit by SHA, you should also be sure to use at least the first twelve characters of the SHA-1 ID.
The Podman repository holds a lot of objects, making collisions with shorter IDs a real possibility.
Bear in mind that, even if there is no collision with your six-character ID now, that condition may change five years from now.

The following git config settings can be used to add a pretty format for outputting the above style in the git log or git show commands:

```
[core]
        abbrev = 12
[pretty]
        fixes = Fixes: %h (\"%s\")
```

### DCO Sign-off

The DCO sign-off is a line at the end of the commit message for the given patch.
Your signature certifies that you wrote the patch or otherwise have the right to pass it on as an open-source patch.
The rules are simple: if you can certify the below (from [developercertificate.org](http://developercertificate.org/)):

```
Developer Certificate of Origin
Version 1.1

Copyright (C) 2004, 2006 The Linux Foundation and its contributors.
660 York Street, Suite 102,
San Francisco, CA 94110 USA

Everyone is permitted to copy and distribute verbatim copies of this
license document, but changing it is not allowed.

Developer's Certificate of Origin 1.1

By making a contribution to this project, I certify that:

(a) The contribution was created in whole or in part by me and I
    have the right to submit it under the open source license
    indicated in the file; or

(b) The contribution is based upon previous work that, to the best
    of my knowledge, is covered under an appropriate open source
    license and I have the right under that license to submit that
    work with modifications, whether created in whole or in part
    by me, under the same open source license (unless I am
    permitted to submit under a different license), as indicated
    in the file; or

(c) The contribution was provided directly to me by some other
    person who certified (a), (b) or (c) and I have not modified
    it.

(d) I understand and agree that this project and the contribution
    are public and that a record of the contribution (including all
    personal information I submit with it, including my sign-off) is
    maintained indefinitely and may be redistributed consistent with
    this project or the open source license(s) involved.
```

Then you just add a line to the end of every git commit message:

    Signed-off-by: Joe Smith <joe.smith@email.com>

Use a real name (sorry, no anonymous contributions).
A real name does not require a legal name, nor a birth name, nor any name that appears on an official ID (e.g. a passport).
Your real name is the name you convey to people in the community for them to use to identify you as you.
The key concern is that your identification is sufficient enough to contact you if an issue were to arise in the future about your contribution.

Please set your `user.name` and `user.email` git configs correctly, then you can sign-off your commits automatically with `git commit -s`
so there should never be a need to add this line manually. The git Author field must match the the Signed-off-by line.

Note while the term "sign" is used this has nothing to do with real digital signing, like an gpg signature. So there is no requirement to
sign commits with gpg or similar.

Commits without a correct DCO Signed-off-by line cannot be merged or even considered.

### Code review

Once the PR is submitted a reviewer will take a look at it.
Should nobody respond to the PR after several weeks, please ping a maintainer on GitHub or
use our [Communications](#communications) channel and ask there.
Sometimes PRs are overlooked or forgotten.

Keep an eye out for the CI results on the PR. If you are a new contributor, a maintainer must first approve the GitHub workflows.
If all is well then all tasks should succeed.
On some repos the CI tests can take several hours to finish.
If something failed, try to take a look at the logs to see if that seems related to your change or not.
Then try to fix your code or the test depending on what you think is right.
If you are unsure or think it is unrelated, ask a maintainer.
Some tests are flaky and will pass on a re-run. If you lack permissions to rerun the tests,
just wait for a maintainer to rerun them for you. Do not unnecessarily force push
the branch in that case.

The Primary CI system we use is GitHub Actions. Jobs triggered by Packit are not merge blockers
and should be considered of secondary importance. Contributors and maintainers should feel free
to ignore failure status on such jobs.

After the reviewers and maintainers take a look, they will either write a comment stating `LGTM` (looks good to me) and approve the PR, in which case you do not need to do any further changes, or they write a comment with review feedback that you should address.
Note that most changes require two reviews so only the second reviewer will actually merge the PR.

If changes were requested, make them locally in your branch and the amend them into the commit from the PR.
You can use `git commit -a --amend` for that.
This will add the current changes to the previous commit.
Please do not push extra commits that say things like "apply code review" or "fix x" where x is a bug introduced in a commit from your PR.
In that case, always squash the change into the right commit to keep the git history clean.
Our projects merge the commits as is and will not squash them on merge to preserve the full original context.

### Rebasing

When you create a branch to work on a fix or feature, it no longer will be updated with the latest changes from the upstream `main` branch.
In order to keep your branch up to date you should rebase. Please never use a merge to do this as this will clutter the history with unnecessary commits.

In order to do so add the upstream repo as remote in git, i.e. for podman-container-tools/podman use:
```
$ git remote add upstream git@github.com:podman-container-tools/podman.git
```

Then fetch the latest changes there with
```
$ git fetch upstream
```

And assuming you are still in your fix/feature branch:
```
$ git rebase upstream/main
```

If the PR is open longer you may have to rebase.
You must rebase when there is a merge conflict.
This means the lines that you changed were also changed after you created your branch.
In this case, Git does not know which change is right.
You will need to manually resolve it.
Check [here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line) for more information on how to do this.

It is strongly recommended to always rebase on a new push to ensure it is testing against the latest code.

## Find bad changes with git bisect

git bisect is very powerful command in order to quickly find commits that caused a regression.

For example, assume you updated Podman and now something that used to work fine is no longer working.
This is called a regression.
If the change was not intentional, it may be hard to identify the cause.
A `git bisect` can help with that.

First, identify a version that you know worked (the "good version"), and a version that you know does not work (the "bad version").
Second, ensure you have a simple test for the bug or broken behavior, so you can easily check if a version of the code is broken.
Then, you can run:
```
$ git bisect start <bad version> <good version>
```

Now git will go through the commits between them via binary search to find the first bad commit.
On each commit, you need to compile the binary.
Then, perform your test to see if the commit is broken or not.
Then, use the
```
$ git bisect good
```
command if it is working.
If it is not working, use this command instead:
```
$ git bisect bad
```

Compile and test again, repeating these steps until git has only one commit left.
This should be the first bad commit.
If you file an issue, this bisect information is very useful to project reviewers and maintainers as it can quickly lead to the root cause.

Given this can be a long manual process you can automate the bisect run if you have a good reproducer.
For example, assume there is a regression with `podman run $IMAGE someCommand` where it fails to run and throws an error.
You can automate this after the `git bisect start` command to find the first commit with the problem automatically by using:
```
$ git bisect run sh -c "make podman && bin/podman run $IMAGE someCommand || exit 1"
```
This will automatically run the given test command (the `sh -c "..."`) on each commit visited by the binary search.
If the command returns 0, git will automatically mark the commit as good; any other exit code will mark the commit as bad.
The `make podman` command here is required to recompile podman each time we are at a new commit.
This is important as it would otherwise not test the correct binary for the given commit, leading to incorrect results.
Then, after this, run your test of choice.
You can also pass complex scripts or commands.
As long as the exit code is 0 for the good case and > 0 for the bad case, it will work.

Sometimes `git bisect` is not perfect.
It can fail to find a bad commit.
There can be many reasons for this, but a common one is that the problem is not in the tool you are testing, but rather some external dependency.
Dynamically linked external libraries, external programs called by the tool, or even the kernel could be causing the bug.
In these cases, identifying the cause will be more difficult.

There is much more useful information in the [git documentation](https://git-scm.com/docs/git-bisect) about this.

## Becoming a Maintainer

Regular contributors may like to become a maintainer over time.
The process to do so is spelled out in our [Governance](GOVERNANCE.md#Contributor-Ladder).
