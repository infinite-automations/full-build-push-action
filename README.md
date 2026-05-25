# full-build-push-action

Simple github action that uses various docker actions to build and publish multiarch container images with meaningful tags.

`full-build-push-action` just act like a wrapper to include one action instead of 4 or 5.
There's no special code included with some additional content.

Included actions:

- [docker/setup-qemu-action](https://github.com/marketplace/actions/docker-setup-qemu)
- [docker/setup-buildx-action](https://github.com/marketplace/actions/docker-setup-buildx)
- [docker/login-action](https://github.com/marketplace/actions/docker-login)
- [docker/metadata-action](https://github.com/marketplace/actions/docker-metadata-action)
- [docker/build-push-action](https://github.com/marketplace/actions/build-and-push-docker-images)

<!-- action-docs-all source="action.yml" project="infinite-automations/full-build-push-action" version="0.0.0" -->
## Description

Simple github action that uses various docker actions to build and publish multiarch container images with meaningful tags.

## Inputs

| name | description | required | default |
| --- | --- | --- | --- |
| `context` | <p>build's context is the set of files located in the specified path</p> | `false` | `.` |
| `file` | <p>path to the Dockerfile (default ./Dockerfile)</p> | `false` | `./Dockerfile` |
| `checkout-deploy-key` | <p>checkout deploy key</p> | `false` | `""` |
| `registry` | <p>container registry</p> | `true` | `ghcr.io` |
| `user` | <p>container registry user</p> | `true` | `${{ github.actor }}` |
| `token` | <p>container registry token</p> | `true` | `""` |
| `push` | <p>push the image to the registry</p> | `false` | `true` |
| `provenance` | <p>generate provenance attestation for the build</p> | `false` | `false` |
| `platforms` | <p>container target platforms</p> | `false` | `linux/amd64,linux/arm/v7,linux/arm64` |


## Runs

This action is a `composite` action.

## Usage

```yaml
- uses: infinite-automations/full-build-push-action@0.0.0
  with:
    context:
    # build's context is the set of files located in the specified path
    #
    # Required: false
    # Default: .

    file:
    # path to the Dockerfile (default ./Dockerfile)
    #
    # Required: false
    # Default: ./Dockerfile

    checkout-deploy-key:
    # checkout deploy key
    #
    # Required: false
    # Default: ""

    registry:
    # container registry
    #
    # Required: true
    # Default: ghcr.io

    user:
    # container registry user
    #
    # Required: true
    # Default: ${{ github.actor }}

    token:
    # container registry token
    #
    # Required: true
    # Default: ""

    push:
    # push the image to the registry
    #
    # Required: false
    # Default: true

    provenance:
    # generate provenance attestation for the build
    #
    # Required: false
    # Default: false

    platforms:
    # container target platforms
    #
    # Required: false
    # Default: linux/amd64,linux/arm/v7,linux/arm64
```
<!-- action-docs-all source="action.yml" project="infinite-automations/full-build-push-action" version="0.0.0" -->