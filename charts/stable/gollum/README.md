# gollum

![Version: 3.0.0](https://img.shields.io/badge/Version-3.0.0-informational?style=flat-square) ![AppVersion: latest](https://img.shields.io/badge/AppVersion-latest-informational?style=flat-square)

Gollum is a simple wiki system built on top of Git

**This chart is not maintained by the upstream project and any issues with the chart should be raised [here](https://github.com/k8s-at-home/charts/issues/new/choose)**

## Source Code

* <https://github.com/gollum/gollum>
* <https://github.com/gollum/docker>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://library-charts.k8s-at-home.com | common | 4.0.0 |

## TL;DR

```console
helm repo add k8s-at-home https://k8s-at-home.com/charts/
helm repo update
helm install gollum k8s-at-home/gollum
```

## Installing the Chart

To install the chart with the release name `gollum`

```console
helm install gollum k8s-at-home/gollum
```

## Uninstalling the Chart

To uninstall the `gollum` deployment

```console
helm uninstall gollum
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install gollum \
  --set env.TZ="America/New York" \
    k8s-at-home/gollum
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install gollum k8s-at-home/gollum -f values.yaml
```

## Custom configuration

N/A

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| gollum.additionalArgs | list | `["--h1-title"]` | Additional arguments for starting gollum |
| gollum.config | string | `"# Push and pull on commit\nGollum::Hook.register(:post_commit, :hook_id) do |committer, sha1|\n     committer.wiki.repo.git.pull('origin', committer.wiki.ref)\n     committer.wiki.repo.git.push('origin', committer.wiki.ref)\nend\n"` | Gollum config.rb customizations [[ref]](https://github.com/gollum/gollum#config-file) |
| gollum.gitBranch | string | `"master"` | Branch to pull |
| gollum.gitUrl | string | `"https://github.com/k8s-at-home/charts.git"` | Repository URL to pull (accepts access tokens) Example: https://user:access-token@git.example.com/user/repo.git |
| gollum.syncCommand | string | `"git pull && git push"` | Command run during the sync cron |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"gollumorg/gollum"` | image repository |
| image.tag | string | `"latest"` | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| service | object | See values.yaml | Configures service settings for the chart. |

## Changelog

All notable changes to this application Helm chart will be documented in this file but does not include changes from our common library. To read those click [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common#changelog).

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

### [3.0.0]

#### Changed

- Upgraded the common library dependency to version 4.0.0. This introduced (potentially) breaking changes to `initContainers` and `additionalContainers`. Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-4.0.0/charts/stable/common/) for the up-to-date values.

### [2.1.1]

- Fixed init script order to clear before cloning not after
- Switched cron script to be sh not bash, fixing failing crons

### [2.0.0]

#### Changed

- **BREAKING**: Upgraded the common library dependency to version 3.2.0. This introduces several breaking changes (`service`, `ingress` and `persistence` keys have been refactored).
  Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-3.2.0/charts/stable/common/) for the up-to-date values.
- Removed default controller type

### [1.0.0]

#### Added

- Initial version

[3.0.0]: #300
[2.0.0]: #200
[1.0.0]: #100

## Support

- See the [Docs](https://docs.k8s-at-home.com/our-helm-charts/getting-started/)
- Open an [issue](https://github.com/k8s-at-home/charts/issues/new/choose)
- Ask a [question](https://github.com/k8s-at-home/organization/discussions)
- Join our [Discord](https://discord.gg/sTMX7Vh) community

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.5.0](https://github.com/norwoodj/helm-docs/releases/v1.5.0)
