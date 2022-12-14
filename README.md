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

## configuration / inputs

|key|description|default|required|
|-|-|-|-|
|checkout-deploy-key|""|""|no|
|registry|container registry| ghcr.io  |yes|
|user|container registry user|${{ github.actor }}|yes|
|token|container registry token|none|yes|
|platforms|container target platforms|linux/amd64,linux/arm/v7,linux/arm64|no|

## examples

### without semantic release

```yaml
name: container build
on:
  push:
    tags:
      - '**'
    branches:
      - '**'
  schedule:
    - cron: '0 0 * * *'
jobs:
  container-build:
    runs-on: ubuntu-latest
    permissions:
      packages: write
    steps:
      - name: checkout
        uses: actions/checkout@v2
      - name: container-build
        uses: kaiehrhardt/full-build-push-action@main
        with:
          token: "${{ secrets.GITHUB_TOKEN }}"
```

### with semantic release

container-build.yml

```yaml
name: container build
on:
  push:
    tags:
      - '**'
    branches:
      - '**'
      - '!master'
  schedule:
    - cron: '0 0 * * *'
jobs:
  container-build:
    runs-on: ubuntu-latest
    permissions:
      packages: write
    steps:
      - name: checkout
        uses: actions/checkout@v2
      - name: container-build
        uses: kaiehrhardt/full-build-push-action@main
        with:
          token: "${{ secrets.GITHUB_TOKEN }}"
          checkout-deploy-key: "${{ secrets.COMMIT_KEY }}"
```

release.yml

```yaml
name: release
on:
  push:
    branches:
      - master
      - main
jobs:
  release:
    runs-on: ubuntu-latest
    container: smartive/semantic-release-image:latest
    steps:
      - name: checkout
        uses: actions/checkout@v2
        with:
          ssh-key: "${{ secrets.COMMIT_KEY }}"
      - name: install semantic-release/github
        run: npm install semantic-release @semantic-release/github
      - name: semantic-release
        run: semantic-release
```
