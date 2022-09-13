# 🐳 Docker Sync Action

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-v3-undefined.svg?logo=github&logoColor=white&style=flat)](https://github.com/marketplace/actions/docker-sync-action)

This github action syncs your docker images across registries 🤹‍♀️

Schedule an automatic workflow, which will ensure that docker images from different registries (or repositories) are in sync. This github action is using [Skopeo](https://github.com/containers/skopeo) command line utility under the hood.

```yaml
- uses: titenkov/docker-sync-action@v1
  with:
    source: titenkov/notifir
    destination: ghcr.io/notifir
    destination-credentials: titenkov:${{ secrets.GH_TOKEN }}
```

## Usage

Here is an example of what to put in your `.github/workflows/sync-docker-images.yml` file to trigger the action.

```yaml
name: Sync Docker Images

on:
  schedule:
    - cron: "0 * * * *" # Run every hour

jobs:
  sync:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Sync docker images
        uses: titenkov/docker-sync-action@v1
        with:
          source: titenkov/notifir
          destination: ghcr.io/notifir
          destination-credentials: titenkov:${{ secrets.GH_TOKEN }}
```

In the example, the action will take all the images from `titenkov/notifir` repository and sync them to `ghcr.io/notifir`.

## Action inputs

Supported transport types: `containers-storage`, `dir`, `docker`, `docker-archive`, `docker-daemon`, `oci`, `oci-archive`, `ostree`, `tarball`.

| Name                      | Description                                                                                                       | Required | Default  |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------- | -------- |
| `source`                  | Your source image repository                                                                                      | true     | -        |
| `source-transport`        | Your source transport type                                                                                        | false    | 'docker' |
| `source-credentials`      | Your source credentials (`user:password`)                                                                         | false    | 'null'   |
| `source-tls`              | Require HTTPS and verify certificates when talking to container registry or daemon                                | false    | 'false'  |
| `destination`             | Your destination image repository                                                                                 | true     | -        |
| `destination-transport`   | Your destination transport type                                                                                   | false    | 'docker' |
| `destination-credentials` | Your destination credentials (`user:password`)                                                                    | false    | 'null'   |
| `destination-tls`         | Require HTTPS and verify certificates when talking to container registry or daemon                                | false    | 'false'  |
| `format `                 | MANIFEST TYPE (oci, v2s1, or v2s2) to use in the destination (default is manifest type of source, with fallbacks) | false    | 'v2s2'   |

## Contact

I would love to hear your feedback! Tell me what you loved and what you want to improve about this action at ✉️ feedback@titenkov.com, or feel free to open a Github Issue.<br />
