# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Top rule

Never commit directly to `master`. Always make changes on a branch and open a PR to merge. When a change warrants it, update `README.md` and `CHANGELOG.md` (create `CHANGELOG.md` if it doesn't exist yet) as part of the same PR.

## What this repo is

A personal collection of [Context Free Art](https://www.contextfreeart.org/index.html) (`.cfdg`) scripts, plus a Docker image that wraps the `cfdg` command-line renderer (built from https://github.com/MtnViewJohn/context-free) so scripts can be rendered to PNG without installing the renderer locally. There is no application source code in this repo — the only "build" is the Docker image build.

## Layout

- `scripts/*.cfdg` — Context Free Art source scripts (the actual grammar/DSL, not shell scripts).
- `Examples/*.png` — rendered output images, one per script in `scripts/`, matched by filename.
- `docker_image/` — the Dockerfile and Taskfile for building/pushing the `alastairhm/contextfree` image, which bakes the `cfdg` binary and uses it as the container `ENTRYPOINT`.
- `draw.sh` — convenience wrapper to render a script from the repo root using the Docker image.

## Common commands

Render a script from the repo root (writes `Examples/<name>.png`):

```bash
./draw.sh <size> <name>   # e.g. ./draw.sh 1024 fractal_tree
```

This runs `docker run --rm -v ${PWD}:/mnt alastairhm/contextfree -s<size> -c "scripts/<name>.cfdg" "Examples/<name>.png"` — the container mounts the repo root at `/mnt`, so paths are relative to the repo root, and `-c` centers the drawing.

Build/push/test the Docker image (run from `docker_image/`, requires [Task](https://taskfile.dev)):

```bash
task build   # docker buildx build -t alastairhm/contextfree:latest .
task push    # docker push alastairhm/contextfree:latest
task test    # renders docker_image/input_file.cfdg -> docker_image/output.png
```

Without Task, run the underlying `docker buildx build` / `docker run` commands directly from `docker_image/Taskfile.yml`.

There is no local `cfdg` binary expected on the host — all rendering happens inside the Docker container built from `docker_image/Dockerfile`, which compiles `cfdg` from source (`make` with `bison`, `flex`, `libpng`, `libicu` deps) and installs it to `/usr/local/bin/cfdg`.

## Working with `.cfdg` files

When adding or editing a script in `scripts/`, the corresponding rendered output belongs in `Examples/` under the same base filename (e.g. `scripts/foo.cfdg` → `Examples/foo.png`). Render with `./draw.sh` to regenerate the PNG after changing a script.
