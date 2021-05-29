---
title: Installing on Synology NAS devices
summary: Describes how to install Stash on Synology NAS devices using docker.
authors:
    - jeremymeyers
    - bnkai
    - AnTiMatteIR
date: 2021-05-23
---

# Installing on Synology NAS devices

- Make sure [the Docker app is installed][synology-docker-howto] and running correctly.
- [Search the registry for stash][stash-dockerhub] and install.
- Create a Stash image with the following set up in 'advanced options'

## *Volume* Tab

|  File/Folder | Mount path | Description  |
|---|---|---|
| `docker/Stash/generated`  | `/generated`  | Thumbnails, clips, etc  |
| `docker/Stash/metadata`  | `/metadata`  | Database  |
| `docker/Stash/config`  | `/root/.stash`  | Configuration files  |
| `docker/Stash/cache`  | `/cache`  | Cache files  |
| (where your porn lives)  | `/data`  | Location of your porn  |

## *Environment* Tab
(These will need to be the same as the volumes you created in the *Volume* tab.

| Variable  | Value  |
|---|---|
| `PATH`  | (keep as is)  |
| `STASH_CACHE`  | `/cache`  |
| `STASH_METADATA`  | `/metadata`  |
| `STASH_GENERATED`  | `/generated`  |
| `STASH_STASH`  | `/data`  |
|   |   |   |

## *Port* Tab
You will need to set a default port in the *Port* tab, otherwise Docker will assign a different port every time Stash is launched.  Leave the container port as-is.

## *Network* Tab
Make sure that "Use The Same Network As Docker Host" is checked.

(thanks to backer `HereIam80` for these instructions)


{% include 'links.md' %}