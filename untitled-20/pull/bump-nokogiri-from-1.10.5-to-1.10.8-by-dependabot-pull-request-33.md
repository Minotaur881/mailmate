# Bump nokogiri from 1.10.5 to 1.10.8 by dependabot · Pull Request \#33

Bumps [nokogiri](https://github.com/sparklemotion/nokogiri) from 1.10.5 to 1.10.8.Release notes

_Sourced from_ [_nokogiri's releases_](https://github.com/sparklemotion/nokogiri/releases)_._

> ## 1.10.8 / 2020-02-10
>
> ### Security
>
> \[MRI\] Pulled in upstream patch from libxml that addresses [CVE-2020-7595](https://github.com/advisories/GHSA-7553-jr98-vx47). Full details are available in [\#1992](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1992). Note that this patch is not yet \(as of 2020-02-10\) in an upstream release of libxml.
>
> ## 1.10.7 / 2019-12-03
>
> ### Bug
>
> * \[MRI\] Ensure the patch applied in v1.10.6 works with GNU `patch`. [\#1954](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1954)
>
> ## 1.10.6 / 2019-12-03
>
> ### Bug
>
> * \[MRI\] Fix FreeBSD installation of vendored libxml2. \[\#1941, [\#1953](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1953)\] \(Thanks, [@​nurse](https://github.com/nurse)!\)

Changelog

_Sourced from_ [_nokogiri's changelog_](https://github.com/sparklemotion/nokogiri/blob/master/CHANGELOG.md)_._

> ## 1.10.8 / 2020-02-10
>
> ### Security
>
> \[MRI\] Pulled in upstream patch from libxml that addresses [CVE-2020-7595](https://github.com/advisories/GHSA-7553-jr98-vx47). Full details are available in [\#1992](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1992). Note that this patch is not yet \(as of 2020-02-10\) in an upstream release of libxml.
>
> ## 1.10.7 / 2019-12-03
>
> ### Fixed
>
> * \[MRI\] Ensure the patch applied in v1.10.6 works with GNU `patch`. \[[\#1954](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1954)\]
>
> ## 1.10.6 / 2019-12-03
>
> ### Fixed
>
> * \[MRI\] Fix FreeBSD installation of vendored libxml2. \[[\#1941](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1941), [\#1953](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1953)\] \(Thanks, [@​nurse](https://github.com/nurse)!\)

Commits

* [`6ce10d1`](https://github.com/sparklemotion/nokogiri/commit/6ce10d15d7af6ad65813a495eaf168f73eba211c) version bump to v1.10.8
* [`2320f5b`](https://github.com/sparklemotion/nokogiri/commit/2320f5bd6319dca9c68d85bbf41629bbf8052a49) update CHANGELOG for v1.10.8
* [`4a77fdb`](https://github.com/sparklemotion/nokogiri/commit/4a77fdb789aefed7ca65c7c7f57ad4dca0d3b209) remove patches from the hoe Manifest
* [`570b6cb`](https://github.com/sparklemotion/nokogiri/commit/570b6cbc5fbc5ee7ef969332c587b951ae35bcd0) update to use rake-compiler ~1.1.0
* [`2cdb68e`](https://github.com/sparklemotion/nokogiri/commit/2cdb68e95aa075ac36a08d4d82d9b410a950a051) backport libxml2 patch for [CVE-2020-7595](https://github.com/advisories/GHSA-7553-jr98-vx47)
* [`e6b3229`](https://github.com/sparklemotion/nokogiri/commit/e6b3229ec53ddf70f1d198bba0d3fc13fde842a8) version bump to v1.10.7
* [`4f9d443`](https://github.com/sparklemotion/nokogiri/commit/4f9d443c2fddc40eefec3366000861433aff6179) update CHANGELOG
* [`80e67ef`](https://github.com/sparklemotion/nokogiri/commit/80e67ef636ce0ddd55a4a7578d7bbdb186002560) Fix the patch from [\#1953](https://github-redirect.dependabot.com/sparklemotion/nokogiri/issues/1953) to work with both `git` and `patch`
* [`7cf1b85`](https://github.com/sparklemotion/nokogiri/commit/7cf1b85a5f8033252e55844ab2765e8f612d4d89) Fix typo in generated metadata
* [`d76180d`](https://github.com/sparklemotion/nokogiri/commit/d76180d0d26a7afb76d84e0de2550ac3bb6abb15) add gem metadata
* Additional commits viewable in [compare view](https://github.com/sparklemotion/nokogiri/compare/v1.10.5...v1.10.8)

[![Dependabot compatibility score](https://camo.githubusercontent.com/d7abbdc4a4995b613812cf220876b06c42f6cdd329686b708cdffacd3b1a2bf1/68747470733a2f2f646570656e6461626f742d6261646765732e6769746875626170702e636f6d2f6261646765732f636f6d7061746962696c6974795f73636f72653f646570656e64656e63792d6e616d653d6e6f6b6f67697269267061636b6167652d6d616e616765723d62756e646c65722670726576696f75732d76657273696f6e3d312e31302e35266e65772d76657273696f6e3d312e31302e38)](https://help.github.com/articles/configuring-automated-security-fixes)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

Dependabot commands and options

You can trigger Dependabot actions by commenting on this PR:

* `@dependabot rebase` will rebase this PR
* `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
* `@dependabot merge` will merge this PR after your CI passes on it
* `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
* `@dependabot cancel merge` will cancel a previously requested merge and block automerging
* `@dependabot reopen` will reopen this PR if it is closed
* `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
* `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version \(unless you reopen the PR or upgrade to it yourself\)
* `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version \(unless you reopen the PR or upgrade to it yourself\)
* `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency \(unless you reopen the PR or upgrade to it yourself\)
* `@dependabot use these labels` will set the current labels as the default for future PRs for this repo and language
* `@dependabot use these reviewers` will set the current reviewers as the default for future PRs for this repo and language
* `@dependabot use these assignees` will set the current assignees as the default for future PRs for this repo and language
* `@dependabot use this milestone` will set the current milestone as the default for future PRs for this repo and language

You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/jyruzicka/omniboard/network/alerts).

