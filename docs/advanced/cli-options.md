---
title: Command line options
summary: List of advanced configuration and command line options
authors:
    - bnkai
    - AnTiMatteIR
date: 2021-05-29
---

# Command line options

Some configuration options can not be edited through the UI and should only be used if needed.

Depending on the option they can be configured either by editing the `config.yml` configuration file or by using an enviroment variable or in a few cases by using flags when running stash.

As an example the `port` option can be changed from the default `9999` to `1234`  by one of the below methods

* adding `port: 1234` to the config.yml file
* setting the ENV variable `STASH_PORT` to `1234` e.g.: `STASH_PORT=1234 ./stash`
* using the flag `--port` when running Stash `./stash --port 1234`


Configuration Option | YML | ENV | FLAG | Description | Comments
---------------------|:---:|:---:|:----:|-------------|:-------------:
host | host | STASH_HOST | --host | The ip address for the host that Stash is listening to | default: 0.0.0.0
port | port | STASH_PORT | --port | The port that Stash serves to | default: 9999 
external host | external_host | STASH_EXTERNAL_HOST | - | Needed in some cases when you use a reverse proxy | [Reverse proxy](reverse-proxy.md)
plugins path | plugins_path | - | - | The path to the Stash plugins folder | Only use if you need to override the default
scrapers path | scrapers_path | - | - | The path to the scrapers folder | Only use if you need to override the default
custom served folders | custom_served_folders | - | - | Allows configuration of mapped URLs to file system folders | [PR][stash-github-pr-620]
maximum upload size | max_upload_size | - | - | Change the maximum size (in MB) for partial imports | default: 1024 (1GB)

{% include 'links.md' %}