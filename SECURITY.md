# Security Policy

Railpack turns application source and build configuration into deployable images. Builds can execute package managers, framework/build tools, and provider-defined build steps, so treat build input and build output as security-sensitive.

## Safe use

- Do not put production secrets in source files, Docker build arguments, or build-time variables that can be embedded in image layers. Use the target platform's runtime secret mechanism.
- Review `railpack.json`, Procfiles, lockfiles, install scripts, and provider selection when accepting a project from an untrusted source.
- Restrict build workers and their filesystem/network permissions; do not build untrusted repositories with host credentials or access to privileged sockets.
- Keep generated images, build logs, and local environment files out of Git. Redact tokens and private repository URLs from diagnostics.

## Reporting

Report security issues privately to the repository owner or through the repository host's private vulnerability-reporting feature when available. Include a minimal reproduction, affected commit/version, impact, and mitigation. Do not post credentials, exploitable details, or private build logs in public issues.

## Release verification

Use `RELEASE.md` and the upstream contribution guidance. Verify changes against the Go toolchain version declared in `go.mod`, run the repository's tests and relevant build/provider integration checks, inspect `git diff --check`, and review the exact staged diff. Upstream changes should be merged only after compatibility and test gates have been verified; a local toolchain mismatch is a release blocker, not a reason to skip tests.
