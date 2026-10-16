# Security and Disclosure Information Policy for the Podman Container Tools Projects

 * [Reporting a Vulnerability](#Reporting-a-Vulnerability)
 * [Security Announcements](#Security-Announcements)
 * [Security Vulnerability Response](#Security-Vulnerability-Response)

## Reporting a Vulnerability

If you think you've identified a security issue in a Podman Container Tools project,
please DO NOT report the issue publicly via the Github issue tracker,
mailing list, or any our public [communication channels](CONTRIBUTING.md#communications).

Instead, please report the issues as GitHub security advisory to us on the correct repository where you suspect the
issue is. If you picked the incorrect repository a maintainer may move it to another repository or ask you to report
it again on the other repository.
For example use https://github.com/podman-container-tools/podman/security/advisories/new for the Podman
repository.

Please provide a detailed report while also keeping it concise, DO NOT send long copy pasted LLM reports,
see our [LLM_POLICY.md](LLM_POLICY.md).
Ideally provide a reproducer of the problem or if you analyzed the source code then cite the right lines
by providing small snippets of the code or if you just mention line numbers please always include a git commit
SHA in case the code has already changed on the main branch.

Do not bother to assign a Severity rating (i.e. CVSS score), the maintainer will handle such assignments according to our judgement.

Alternatively, in case you do not want to create a GitHub advisory or have not received a response on the advisory you
created after a week, please use our private security mailing list [security@lists.podman.io](mailto:security@lists.podman.io?subject=Security%20Vunerablity%20Report)
and send the report there. This is a private mailing list for the maintainers.

If you have questions about already published CVEs/Advisories or about patches for vulnerabilities in
third party dependencies please use our regular public channels instead to ask about them.
The private reports should only be used for issues that require the confidentiality.

Also DO NOT send us any legal questionnaires there for any compliance questions or similar.
We are an upstream community, and not a vendor, see [SUPPORT.md](#SUPPORT.md)

## Security Announcements

Security fixes are announced through GitHub Security Advisories on our repositories and we make sure to assign
CVE numbers for these issues so they will also be communicated through the normal CVE system.

In addition, on repositories where we have dedicated release notes, security fixes are noted in the release notes.

The advisories should contain information about what versions were affected and in what version(s) the problem
was fixed. Note that the versions are only accurate for our upstream releases on our GitHub organization.
Builds from third party vendors may provide patches for different versions, if you use them please always contact
your vendor about any fixes and not us (the upstream project).

## Security Vulnerability Response

Each report is acknowledged and analyzed by the maintainers within 3 working days.

Any vulnerability information shared with maintainers stays within a Podman Container Tools project
and will not be disseminated to other projects unless it is necessary to get the issue fixed.

As the security issue moves from triage, to an identified fix, to release planning, the
maintainers will keep the reporter updated.
