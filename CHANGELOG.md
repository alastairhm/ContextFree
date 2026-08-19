# Changelog

All notable changes to this repository are documented here.

## Unreleased

- Converted `docker_image/Dockerfile` to a multi-stage build: the `cfdg` binary is compiled in a build stage and only it plus its runtime shared libs are copied into the final image. Reduces the built image size from ~700MB to ~140MB; no change to the CLI's behavior.
- Expanded `README.md` with a repo layout overview, rendering instructions, and an examples gallery.
- Added `CLAUDE.md` with guidance for Claude Code when working in this repo.
