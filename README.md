# docker_images
Automated build pipeline for Docker images

[![CircleCI](https://circleci.com/gh/ataber/docker_images.svg?style=svg)](https://circleci.com/gh/ataber/docker_images)

## How it works

Whenever this repo is pushed to, CircleCI runs a workflow which builds the changed images (as chronicled in `git diff`) and their dependent images, and then pushes those built images to [Dockerhub](https://hub.docker.com/u/ataber) with useful tags.

## What the scripts do
- `build-and-deploy-images` is used by CircleCI jobs to build and deploy.
- `check-if-changed` is used by CircleCI to compile the changed images and their dependent images.
- `generate_circle_config` should be run manually to modify the CircleCI config file if there are new images added or the dependency graph changes. Note that this script may not produce an accurate config file and manual post-run checks should be done before committting the result.
