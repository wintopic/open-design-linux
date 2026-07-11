# Open Design Linux

Unofficial, automated Linux AppImage builds of
[`nexu-io/open-design`](https://github.com/nexu-io/open-design).

This repository does not fork Open Design product code. GitHub Actions checks
the upstream project for a new stable release, checks out the exact upstream
tag, applies the small packaging-only patch under `patches/`, and runs the
upstream `tools-pack` Linux packaging command.

## Download

Download the newest `.AppImage` and matching `.sha256` file from this
repository's [Releases](../../releases/latest) page.

```bash
chmod +x open-design-*-linux-x86_64.AppImage
./open-design-*-linux-x86_64.AppImage --appimage-extract-and-run
```

`--appimage-extract-and-run` avoids depending on FUSE and is also the launch
mode used by Open Design's own Linux installer integration.

## Automated builds

The `Build Linux AppImage` workflow runs:

- every day at 03:17 UTC;
- manually with an upstream tag, branch, or commit;
- automatically only when the upstream stable tag has not already been
  published here, unless `force_rebuild` is selected.

The build uses the upstream containerized packaging lane to target an older
glibc baseline. The patch passes the already bootstrapped pnpm binary into
nested workspace builds, maps unpublished internal packages to the tarballs
built from the checked-out source, and enables non-interactive CI behavior; it
does not change the application. GitHub Actions dependencies are pinned to
commit hashes. Each Release contains the AppImage, a SHA-256 checksum, and
provenance metadata recording the upstream tag and commit.

## Trust and support

These are community builds and are not published or supported by the Open
Design maintainers. Review the workflow before using an artifact. Product
issues belong in the [upstream repository](https://github.com/nexu-io/open-design/issues);
Linux packaging issues specific to these artifacts belong here.

Open Design is licensed under Apache-2.0. See `LICENSE` and the upstream
repository for copyright notices.
