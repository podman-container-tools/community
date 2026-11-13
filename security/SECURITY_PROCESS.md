# Security Process for Maintainers

> **Note:** This document is meant for maintainers or contributors to document how we work on Security Issues.
> Information on how to report a vulnerability is described here: [SECURITY.md](../SECURITY.md).

## Podman Container Tools Security Team

The Security team is responsible for triaging, fixing, allocating and publishing CVE's for and coordinating
new releases with said fixes for all Podman Container Tools projects.

The Team consist all of all Core Maintainers (mandatory membership defined in the Governance) and per
repository Maintainers (voluntary membership, but encouraged).

Reviewers and other Contributors should not be part of the security team.

The Security team members will have access to the security@lists.podman.io mailing list and all GitHub security advisories.

## Confidentially

The security team members, the reporters and possibly additional contributors must keep all information about
security issues private until they are officially made public by the security team, i.e. by publishing a CVE.
No details must be shared with anyone outside this group unless it is required to get the issue fixed, e.g.
coordinating with another project. A person working on a fix is allowed to *privately* mention that they are
working on a security issue for planning purposes, however no details about the problem must be shared in this
case.

## Security channel

In order to securely communicate and coordinate between members we use a private matrix channel where all
security team members should be part off.

## Process

### Triage

First, we define one or two triagers who rotate on a weekly basis. If a member is unavailable during that
time they should switch their slot with another person in advance.
(TODO figure out how can manage such a schedule? Does the CNCF calendar system)

Their task is to read and check the reports if they are valid or not. Obviously incorrect reports should be
closed right away. The main repos (podman, buildah, skopeo, container-libs) should have a security thread
model published which should be used as basis for the triage.
If the triager is unsure if the report is valid they should consult with a second person, ideally the SME
of the right code area in question.

If the report is not a valid security issue then the security advisory should be closed and one of the
following steps taken:
- If the problem is real but not security relevant a public issue should be created.
- If the the usage of the Tool is "incorrect" according to the thread model consider creating an issue
  about this to request an update the documentation about that case to warn other users, or directly
  open a PR add this case. (For example exposing the Podman socket over TCP is simply insecure but this
  is not a Podman security issue if a users does it regardless, the documentation should however warn
  about the risks.)
- Otherwise if nothing valuable can be taken from it just closing it is enough.

If the report is found to be a duplicate of an existing report close the new one, linking to the previous report.

When the report is valid the triager should click "Accept and open as draft" on the report and assign one
security team member responsible for handling the issue ideally based on the expertise of the code area.
Please ask for a volunteer first before assigning someone if nobody took it.

If needed a security team member is allowed to pull in another *known* contributor
to the advisory who can assist them in writing a fix or review the fix, in this case simply add the person as
collaborator on the GitHub security advisory. However before doing so please ask them if they are willing to
help first and that they agree to keep any shared details [confidential](#Confidentially). Note that the
security team member is still the one responsible to ensure the issue is getting fixed in a timely manner.

We primarily expect security reports to come in as GitHub security advisories, if we get reports per email
the triager should either instruct the reporter to create a GitHub security advisory or create one themselves.
If the email is spam it should just be discarded on the mailing list of course without responding.
In any case the triager should link the created advisory in the email thread so others can see it was done
and is tracked properly in GitHub.
When communicating on the email lists always keep the security list in CC.

### Severity

Once the issue is assigned the person is responsible for it should assign a CVSS 3.1 score (TODO link to guidance here).
Depending on that there are two ways how we will fix issues:

#### Low or Medium Severity fixes

If the problem is found to be Low or Medium Severity and is unlikely/impossible to exploit in practice or
when an exploit requires already sufficient privileges on the host already then the fix should happen in
public as regular PR without explicitly mentioning the security impact in the commit or PR description.

However if the design or approach to fix the problem is not clear or very large it is recommended to first
discus with other maintainers in private about the right approach to avoid PRs which are open for weeks/months.

Public PRs can be reviewed by the entire team, they run through the normal process, including all CI checks,
and provide an actual linkable public PR history and as such preserves the discussion on them.
This is done to balance the workload of the security team better as private fixes cause increased workload
for everyone, and carry more risk due the missing CI run.

If despite a Low/Medium CVSS score you think there is significant risk to users you may instead use the private
fork PR like High or Critical ones, see below.

#### High or Critical Severity fixes

Because these could have a greater impact to users we keep them private and use the private GitHub security
advisory fork feature to develop the fix on a private PRs. No CI will run for these fixes so its the
responsibility of the PR author to run required testing themselves. From basic things like validation to the
actual functionality tests which are being added in the PR.
This is required to ensure CI is not failing after merge.

Do not merge these private PRs right away! See [Publish](#Publish) below.

Note in order to merge these private fork PRs the merge/branch protection on the repository must be disabled.
To do so, go to the repository settings, under Ruleset pick the right rule and add a bypass for your account name
then Save the ruleset (Button is at the bottom) then go back to the advisory, reload the page, click merge and
then do not forget to update the Ruleset again to remove your bypass.

There also seem to be GitHub bug where the merge might trigger a 500 server error response. In that case open the
main repository and manually confirm that all the targeted branches got the right fix merged. The PRs on the private
fork are likely still marked as open, in that case you must close them manually. Only once the PRs are closed GitHub
will allow you to publish an advisory.

### CVE assignment

- ~~Option 1) Use github "request CVE" feature. This is no longer workable, we are waiting 12+ weeks for CVE there.~~
- Option 2) Contact RH Prodsec and send them all details (TODO create template with all details they ask normally).
  Problem, we need to coordinate an unembargo date with them if they agree to embargo the issue at all so we have
  less control over when things are published. The response time with them is not super predictable either, a CVE
  assignment might only need a day or a few weeks in the worst case.
- Option 3) Use the new Akrites CNA which is run by the Linux Foundation? (Very new, we never used it, unclear if
  there is any advantage over RH Prodsec)
- Option 3) Become a CNA ourselves (best long term solution?). This would give us "instant" CVE assignment without
  having to coordinate or wait for another CNA. We have full control over what we publish and nobody else can publish
  a CVE for our Projects without going through is one way or another.
  ref: https://github.com/ossf/wg-vulnerability-disclosures/blob/main/docs/guides/becoming-a-cna-as-an-open-source-org-or-project.md

In order for a proper CVE the assignee should provide a meaningful advisory description while keeping it concise.
In most cases the reporter description is likely not optimal so replace it with your own and fill out all the metadata:
- Affected version ranges
- Fixed versions, see [Publish](#Publish) below
- Link to the commit(s) which fix the issue
- Describe meaningful workarounds if possible
- Give credits to the reporter if they want to be credited.

Examples:
 - https://github.com/podman-container-tools/podman/security/advisories/GHSA-2cvf-wqm6-wr9g
 - https://github.com/podman-container-tools/podman/security/advisories/GHSA-4hq8-gpf5-8p68

Once a CVE is received add it it to the advisory metadata.

### Publish

Once the fixes are ready (either merged in case of the public PR fixes or ready to be merged for the
private security PR forks) and a CVE was assigned the assignee should coordinate a new release with
the main release person(s) for the affected repository. The private security fork PRs should be merged
right before the release process will be started to reduce the time of the commits being public and
the fix not being released in a version.

If there are multiple pending advisories it makes sense to group several fixes into one release to keep
the release overhead low and not require that many updates on the end user side.
The main release persons should all be part of the Security Team so they can coordinate such things in
private if needed.

Once you know which version contains the fixes update the advisory metadata to include the right fixed
version numbers. Then right after the release is published (tag is pushed), publish the GitHub security
advisory.

### Timeline

Ideally all reports should be fixed and released withing 30 days from the initial report day. This is
not a hard rule of course, just an aspirational goal, which also largely depends on how long reserving
a new CVE number takes.
Exceptions are possible, in case when cross project coordination is required or when the patches are
much larger/complicated to write and review withing that timeline. Holiday season may also be a valid
reason for delays, we cannot expect everybody to be around during such time.

## Security Repository

In order to not loose track of security advisories across all repos we will use use a private GitHub
repository and a private GitHub project board.

The purpose of this repo/board is to serve as coordination point for the security team.
A GitHub workflow automation on the repo should automatically import all github security advisories
from all our repos and create an issue for them on the repo. The issue is then added to the project
board automatically. (There is no way to add security advisories directly to a board)

The board will reflect the following states: Triage, Assigned, In Progress, Waiting for Release, Done.
Once the security advisory is published or closed the automation will close the issue automatically and
move it to Done.
The states are defined as issue field "Vulnerability State".

Most parts should be taken care of by the automation which runs on a cron schedule.

The only manual steps on the repo would be:
- Assign the member responsible for fixing to the issue once it was triaged if nobody else self assigned the issue already.
- Update the Vulnerability State to "In Progress" when working on the fix (the automation moves it automatically if it sees
  a private fork, however as noted above we do not use them for all fixes so for public ones move manually).
- Move to "Waiting for Release" once the fix has been reviewed (or merge din case of a public PR) and a CVE was assigned.

Never manually close the or open an issue on the repo with the "Vulnerability" Issue Type. The automation handles
the creation and closing of the issues based on the advisory states. It will close the issue once the advisory was either
closed or published.

With this anyone on the team gets an overview of all issues on all repos in one page with its current status in the process.

In general the issues are meant to only hold metadata, all comments should happen on the advisory because that is the only
place where we can talk to the reporter and can add additional people outside the main team on a case by case basis.
