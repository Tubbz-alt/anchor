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
with Anchor. Management of these services and operations can be done in a
thousand different ways.

## Repository Structure

| Path       | Feature                                                         |
| ---------- | --------------------------------------------------------------- |
| `src`      | Dracut module source directory                                  |
| `doc`      | Documentation pages                                             |
| `contrib`  | Auxiliary directory containing contributions that are not part  |
|            | of anchor proper. This includes common CI configurations, build |
|            | script examples, etc.                                           |
| `build.sh` | Script to build RPM.                                            |
