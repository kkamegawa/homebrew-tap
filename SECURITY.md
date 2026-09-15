# Security Policy

## Supported Versions

Only the formula on the default branch is supported. It always points at the latest stable
Relaypublisher release; older formula revisions do not receive fixes.

## Reporting a Vulnerability

Please do not report security vulnerabilities through public GitHub issues.

Instead, report them privately using GitHub Security Advisories ("Report a vulnerability" on the
repository's Security tab). If that is not available, contact the repository owner at
`<security-contact>`.

Vulnerabilities in the `relaypublisher` CLI itself belong to the Relaypublisher repository; report
them there the same way.

Please include:

- A description of the vulnerability and its impact
- Steps to reproduce
- Affected component (formula, tap CI workflow, or the downloaded release archive)

You can expect an initial response within 7 days.

## Scope Notes

This tap only points Homebrew at a release archive and its checksum. The following are of particular
interest:

- A formula whose `url` or `sha256` does not match the release's `SHA256SUMS.txt`
- Changes that could make the tap install a binary from anywhere other than the Relaypublisher release
- Weaknesses in the automation that updates the formula (the release workflow's GitHub App token and
  the pull request flow)
