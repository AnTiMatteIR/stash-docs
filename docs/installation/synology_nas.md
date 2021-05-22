# Installing on Synology NAS devices

- Make sure [the Docker app is installed](https://blog.pavelsklenar.com/how-to-install-and-use-docker-on-synology/) and running correctly.
- [Search the registry for stash](https://hub.docker.com/r/stashapp/stash) and install.
- Create a stash image with the following set up in 'advanced options'

## "Volume" Tab

|  File/Folder | Mount Path | Description  |
|---|---|---|
| docker/Stash/generated  | /generated  | Thumbnails, clips, etc  |
| docker/Stash/metadata  | /metadata  | Database  |
| docker/Stash/config  | /root/.stash  | Configuration Files  |
| docker/Stash/cache  | /cache  | Cache Files  |
| (where your porn lives)  | /data  | Location of your porn  |

## "Environment" Tab
(These will need to be the same as the Volumes you created in the "Volume" tab.

| variable  | Value  |
|---|---|
| PATH  | (keep as is)  |
| STASH_CACHE  | /cache  |
| STASH_METADATA  | /metadata  |
| STASH_GENERATED  | /generated  |
| STASH_STASH  | /data  |
|   |   |   |

## "Port" Tab
You will need to set a default port in the "Port" tab, otherwise Docker will assign a different port every time Stash is launched.  Leave the container port as-is.

## "Network" Tab
Make sure that "Use The Same Network As Docker Host" is checked.

(thanks to backer Herelam80 for these instructions)