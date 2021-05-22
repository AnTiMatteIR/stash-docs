---
title: Getting Started
summary: Describes the basics of Stash (see also README.md)
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
date: 2021-05-22
---
# Getting started
## Stash - An organizer for your porn, written in Go

<https://stashapp.cc>

Stash is a locally hosted web-based app written in Go which organizes and serves your porn.

- It can gather information about videos in your collection from the internet, and is extensible through the use of community-built plugins for a large number of content producers.
- It supports a wide variety of both video and image formats.
- You can tag videos and find them later.
- It provides statistics about performers, tags, studios and other things.

You can watch a [SFW demo video][sfwdemovid] to see it in action.


### Installing stash

#### via Docker

Follow [this README.md][dockerreadme] in the docker directory.


#### via pre-compiled binaries

The Stash server runs on macOS, Windows, and Linux. Download the [latest release here][latestrelease].

Run the executable (double click the exe on windows or run `./stash-osx`, or `./stash-linux` respectively, from the terminal on macOS / Linux) and navigate to either <https://localhost:9999> or <http://localhost:9999> to get started.

!!! info "Note for Windows users"
    Running the app might present a security prompt since the binary isn't yet signed. Bypass this by clicking "more info" and then the "run anyway" button.


##### FFMPEG

If stash is unable to find or download FFMPEG then download it yourself from the link for your platform:

- [macOS ffmpeg][macosffmpeg], [macOS ffprobe][macosffprobe]
- [Windows][windowsffmpeg]
- [Linux][linuxffmpeg]

The `ffmpeg(.exe)` and `ffprobe(.exe)` files should be placed in `~/.stash` on macOS / Linux or `C:\Users\YourUsername\.stash` on Windows.


### Usage

#### Quickstart Guide

1. Download and install Stash and its dependencies
2. Run Stash. It will prompt you for some configuration options and a directory to index (you can also do this step aferwards)
3. After configuration, launch your web browser and navigate to the URL shown within the Stash app.

!!! info
    Not that Stash does not currently retrieve and organize information about your entire library automatically.

    You will need to help it along through the use of [scrapers][scrapers]. The Stash community has developed scrapers for many popular data sources which can be downloaded and installed from [this repository][scrapersrepo].


#### CLI

Stash runs as a command-line app and local web server. There are some command-line options available, which you can see by running `stash --help`.

For example, to run stash locally on port 80 run it like this (OSX / Linux): `stash --host 127.0.0.1 --port 80`


#### SSL (HTTPS)

Stash can run over HTTPS with some additional work. First you need to generate a SSL certificate and key combo. Here is an example using openssl:

```
openssl req -x509 -newkey rsa:4096 -sha256 -days 7300 -nodes -keyout stash.key -out stash.crt -extensions san -config <(echo "[req]"; echo distinguished_name=req; echo "[san]"; echo subjectAltName=DNS:stash.server,IP:127.0.0.1) -subj /CN=stash.server
```

This command would need customizing for your environment. [This link][opensslhelp] might be useful.

Once you have a certificate and key file name them `stash.crt` and `stash.key` and place them in the `~/.stash` directory. Stash detects these and starts up using HTTPS rather than HTTP.


### Customization

#### Themes and CSS customization

There is a [directory of community-created themes][cssthemes] on our Wiki, along with instructions on how to install them.

You can also make Stash's interface fit your desired style with [custom CSS snippets][csssnippets] and [CSS Tweaks][csstweaks]


### Support (FAQ)

Answers to other Frequently Asked Questions can be found on our [Wiki][wiki]

For issues not addressed there, there are a few options:

- Read this documentation ;)
- Check the in-app documentation (using the `?` Icon in the top right corner)
- Join the [Discord server][discord], where the community can offer further support.

{% include 'links.md' %}