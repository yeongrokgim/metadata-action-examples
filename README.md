# metadata actions examples

This repository aims to provide hands-on experience of https://github.com/docker/metadata-action

## Default

- Default behavior on `tags:` ([source](https://github.com/docker/metadata-action/blob/master/README.md?plain=1#L399))

```yaml
tags: |
  type=schedule
  type=ref,event=branch
  type=ref,event=tag
  type=ref,event=pr
```

| `github.event_name` | `github.ref`        | version |
| ------------------- | ------------------- | ------- |
| `pull_request`      | `refs/pull/1/merge` | `pr-1`  |
| `push`              | `refs/heads/main`   | `main`  |
