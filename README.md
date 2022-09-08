# Docker Sync Action
GitHub Action that syncs your docker images across registries 🤹‍♀️

Schedule an automatic daily or weekly workflow, which will ensure that docker images from different registries (or repositories) are in sync.

## Usage

Create a new workflow file `.github/workflows/sync-docker-images.yml` with the following configuration:

```
name: Sync Docker Images

on:
  schedule:
    - cron: "0 0 * * *"

jobs:
  sync-docker-images:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Sync docker iamges
        uses: titenkov/docker-sync-action@v1
        with:
          source: alpine:latest
          destination: titenkov/alpine:latest
          destination-credentials: titenkov:${{ secrets.DOCKER_IO_TOKEN }}
```

