# metadata actions examples

This repository aims to provide hands-on experience of [metadata-action](https://github.com/docker/metadata-action)

> **NOTE**: Table columns
>
> - event: `github.event_name`. refer [^1], [^2]
> - ref: `github.ref`
> - version: `meta.outputs.version`
> - tags: `meta.outputs.json.tags`, without prefix `ghcr.io/yeongrokgim/metadata-action-examples:`

## Default

> **NOTE**: Default behavior on `tags:` ([source](https://github.com/docker/metadata-action/blob/master/README.md?plain=1#L399))

```yaml
tags: |
  type=schedule
  type=ref,event=branch
  type=ref,event=tag
  type=ref,event=pr
```

| event          | ref                             | version              | tags                 |
| -------------- | ------------------------------- | -------------------- | -------------------- |
| `pull_request` | `refs/pull/1/merge`             | `pr-1`               |                      |
| `push`         | `refs/heads/dummy-pull-request` | `dummy-pull-request` | `dummy-pull-request` |
| `push`         | `refs/heads/main`               | `main`               | `main`               |
| `push`         | `refs/tags/v0.0.1`              | `v0.0.1`             | `v0.0.1`, `latest`   |
| `create`       | `refs/tags/v0.0.1`              | `v0.0.1`             | `v0.0.1`, `latest`   |

## types

```yaml
tags: |
  type=schedule
  type=semver,pattern={{version}}
  type=semver,pattern={{major}}.{{minor}}
  type=semver,pattern={{major}}
  type=ref,event=branch
  type=ref,event=pr
  type=sha
```

| event    | ref                | version  | tags                                       |
| -------- | ------------------ | -------- | ------------------------------------------ |
| `push`   | `refs/heads/main`  | `main`   | `main`, `ha-908482c`                       |
| `create` | `refs/tags/v0.0.2` | `v0.0.2` | `0`,`0.0`,`0.0.2`, `sha-908482c`, `latest` |

## References

[^1]: Contexts - [github.event_name](https://docs.github.com/en/actions/learn-github-actions/contexts#context-availability:~:text=webhook%20payload.-,github.event_name,-string)
[^2]: Events that trigger workflows - [Events](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
