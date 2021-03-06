# Anchor Code Repository

Repo for developing shared Anchor code.

## What is Anchor?

Anchor is a (secure) booting tool that will pull an image from an object store
and use it to boot a diskless node. It mostly consists of a dracut module that
is configured to use different pluggable methods to bootstrap authentication
and download a image for a node. The main scope for Anchor is to provide an
extensible framework for handling different diskless boot methods, with a
primary focus on pulling data from an object store and mounting a squashfs
image overlayed with a local ramdisk.

## What else do I need to boot?

Honestly, a lot. Two main repositories that the clusters team rely on are our
Anchor Operations repository to handle automation steps to build and deploy
images, and our Chart repository to handle needed services that communicate
with Anchor. Copies of the public version of these two repositories are stored
under the `contrib` folder.  Management of these services and operations can be
done in a thousand different ways, and is left to each individual organization
to solve however they see best.

## Repository Structure

| Path       | Feature                                                         |
| --- | --- |
| `src`      | Dracut module source directory                                  |
| `doc`      | Documentation pages                                             |
| `contrib`  | Auxiliary directory containing contributions that are not part of anchor proper. This includes common CI configurations, build script examples, etc. |
| `build.sh` | Script to build RPM.                                            |

## Current modules

| Auth | Provided By | Description |
| --- | --- | --- |
| `ACME` | `lib/lib_acme.sh` | Automatically issue certificates from a trusted CA to a node per RFC 8555. |
| `SSH` | `lib/lib_dropbear.sh` | Start a dropbear server with a trusted root login key, wait until files put in place. Optionally send client network data to a URL. |
| `NFS` | `lib/lib_nfs.sh` | Mount an NFS share to retrieve the files needed for authentication. |
| `None` | | Do not authenticate. Skip to the next stage. |

| Image | Provided By | Description |
| --- | --- | --- |
| `squashfs` | `lib/lib_squashfs.sh` | Download squashfs image from an rsync server or mutual TLS HTTP server. |
| `buildah` | `lib/lib_buildah.sh` | Download an uncompressed image from a docker registry. Build a squashfs live on boot. |

## Change log

* 0.1.5 - Add NFS authentication module, add URL polling to dropbear
* 0.1.4 - Add `rngd` binaries and bash library to populate `/dev/random` prior
  to ACME and curl operations
* 0.1.3 - Remove `BOOTIF` requirement for setting `root=ok`
* 0.1.2 - Add `url-lib` dracut module dependency to install curl with needed
  HTTPS libraries
* 0.1.1 - First fully-featured release following the migration to a shared code
  repository
