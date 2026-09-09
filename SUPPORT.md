# Support policy for the Podman Container Tools Projects

## Supported Versions

Unless otherwise noted all our projects only support the latest released version on GitHub.
If you use an older version from distribution repositories, we likely do not support it and
expect you to retest with the latest upstream version.

### Long Term Support (LTS) Versions

Sometimes exceptions are made to support a certain release branch for longer when the
majority of maintainers agrees that it makes sense. These releases will only receive
critical bug fixes and security fixes. The currently supported versions are noted in
the following table. There is however no guarantee that all issues will be fixed, for
example, if a backport is deemed too complex.

| Project | Version | Support End |
| ------- | ------- | ----------- |
| Podman  | 5.8     | 2027-06-07  |
| Buildah | 1.43    | 2027-06-07  |
| Skopeo  | 1.22    | 2027-06-07  |

Maintainers who are in favor of declaring a branch LTS are responsible for supporting
that one. Other maintainers are free to ignore backport work/review requests for LTS
branches if they do not wish to participate in that work.

## Expectations on support

The Podman Container Tools maintainers provide a "best effort" support of our Projects.
We are an upstream community, and not a vendor; as such, we do not provide support contracts.
We also do not offer Service Level Agreements (SLAs). If your business requires SLA guarantees,
please consult a provider offering dedicated enterprise support.

If you are using a package from a Linux distribution, please use the Linux distribution's mechanism
as support unless you are willing to reproduce problems on the main branch of our upstream code.
There is no guarantee a maintainer will look at your issue; we certainly try to do so
but sometimes things might still be missed.

Please read our [contributing guidelines](CONTRIBUTING.md#reporting-issues) on how to properly
report issues.
