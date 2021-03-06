---
title: Development
summary: Describes how to develop and build Stash from source.
authors:
    - StashAppDev
    - Leopere
    - friendlycrab
    - echo6ix
    - WithoutPants
    - InfiniteTF
    - f1delio
    - jeremymeyers
    - UncleRoger33
    - peolic
    - bnkai
    - AnTiMatteIR
date: 2021-05-23
---

# Development

## Compiling From Source Code

### Pre-requisites

* [Go][go-lang-download]
* [Revive][go-revive-github] - Configurable linter
    * Go Install: `go get github.com/mgechev/revive`
* [Packr2][go-packr2-github] - Static asset bundler
    * Go Install: `go get github.com/gobuffalo/packr/v2/packr2`
    * [Binary Download][go-packr2-releases]
* [Yarn][yarn-install] - Yarn package manager
    * Run `yarn install --frozen-lockfile` in the `stash/ui/v2.5` folder (before running make generate for first time).

!!! info
    You may need to run the `go get` commands outside the project directory to avoid modifying the projects module file.

### Environment

#### macOS

TODO

#### Windows

1. Download and install [Go for Windows][go-lang-download]
2. Download and install [MinGW][mingw-download]
3. Search for "advanced system settings" and open the system properties dialog.
    1. Click the `Environment Variables` button
    2. Add `GO111MODULE=on`
    3. Under system variables find the `Path`.  Edit and add `C:\Program Files\mingw-w64\*\mingw64\bin` (replace * with the correct path).

!!! info
    The `make` command in Windows will be `mingw32-make` with MinGW.

### Commands

* `make generate` - Generate Go and UI GraphQL files
* `make build` - Builds the binary (make sure to build the UI as well... see below)
* `make pre-ui` - Installs the UI dependencies. Only needs to be run once before building the UI for the first time, or if the dependencies are updated
* `make fmt-ui` - Formats the UI source code.
* `make ui` - Builds the frontend and the packr2 files
* `make packr` - Generate packr2 files (sub-target of `ui`. Use to regenerate packr2 files without rebuilding UI)
* `make vet` - Run `go vet`
* `make lint` - Run the linter
* `make fmt` - Run `go fmt`
* `make fmt-check` - Ensure changed files are formatted correctly
* `make it` - Run the unit and integration tests
* `make validate` - Run all of the tests and checks required to submit a PR

### Building a release

1. Run `make generate` to create generated files 
2. Run `make ui` to compile the frontend
3. Run `make build` to build the executable for your current platform

### Cross compiling

This project uses a modification of the [CI-GoReleaser][ci-goreleaser] docker container to create an environment
where the app can be cross-compiled.  This process is kicked off by CI via the `scripts/cross-compile.sh` script.  Run the following
command to open a bash shell to the container to poke around:

`docker run --rm --mount type=bind,source="$(pwd)",target=/stash -w /stash -i -t stashappdev/compiler:latest /bin/bash`

### Profiling

Stash can be profiled using the `--cpuprofile <output profile filename>` command line flag.

The resulting file can then be used with pprof as follows: 

`go tool pprof <path to binary> <path to profile filename>`

With `graphviz` installed and in the path, a call graph can be generated with:

`go tool pprof -svg <path to binary> <path to profile filename> > <output svg file>`


{% include 'links.md' %}