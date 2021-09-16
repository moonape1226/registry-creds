# registry-creds <!-- omit in toc -->

- [Chart Details](#chart-details)
- [Installation](#Installation)
    - [Adding Helm repository](#adding-helm-repository)
    - [Installing the Chart](#installing-the-chart)
    - [Uninstalling the Chart](#uninstalling-the-chart)
- [Configuration](#configuration)

## Chart Details

This chart deploys [registry-creds](https://github.com/alexellis/registry-creds) related resources on a Kubernetes
cluster. The resources are derived from it's [menifest.yaml](https://github.com/alexellis/registry-creds/blob/master/manifest.yaml).

**Note.**

This helm chart will create `registry-creds-secret` secret resource from docker authentication information provided in `values.yaml`. 

Secret `registry-creds-secret` will be copied to all K8S namespaces with name `docker-registry-registrycreds`. This application will also update the `ImagePullSecrets` config in default serviceaccount for all namespace to use `docker-registry-registrycreds`.

Deleting helm release will delete `registry-creds-secret` as well as all `docker-registry-registrycreds` secrets, but it won't affect pulling image if you are not using private images.

## Installation

### Adding Helm repository

In order to be able to install the chart you will have to add the repository where the chart is hosted:

```console
helm repo add registry-creds https://moonape1226.github.io/registry-creds/charts
```

### Installing the Chart

```console
helm install registry-creds registry-creds/registry-creds
```

### Uninstalling the Chart

````console
helm uninstall registry-creds
````

## Configuration

The following table lists the configurable parameters of this chart and their default values.

Parameter | Description | Default
--- | --- | ---
`replicaCount` | number of replicas | `1`
`image.repository` | container image repository | `"ghcr.io/alexellis/registry-creds"`
`image.tag`  | container image tag | `""` (follow appVersion if not present)
`image.pullPolicy` | container image pull policy | `"IfNotPresent"`
`container.args` | container arguments | `["--enable-leader-election"]`
`container command` | container command | `["/controller"]`
`imagePullSecrets` | container image pull secret | `[]`
`nameOverride` | override name of app |`""`
`fullnameOverride` | override full name of app | `""`
`podAnnotations` | annotations to be added to pods | `{}`
`podSecurityContext` | privilege and access control settings for a Pod | `{}`
`securityContext` | privilege and access control settings for a Container | `{}`
`resources.limits.cpu` | cpu resource limit | `"100m"`
`resources.limits.memory` | memory resource limit | `"64Mi"`
`resources.requests.cpu` | cpu resource request | `"100m"`
`resources.requests.memory` | memory resource request | `"50Mi"`
`tolerations` | list of node taints to tolerate  | `[]`
`nodeSelector` | Node labels for pod assignment | `{}`
`affinity` | node affinity | `{}`
`terminationGracePeriodSeconds` | graceful period before a Pod is killed | `10`
`registrySecret.username` | docker registry username | `"username"`
`registrySecret.password` | docker registry password | `"password"`
`registrySecret.registryURL` | docker registry URL | `"https://index.docker.io/v1/"`
`registrySecret.annotations` | annotatations to be added to created registry secret | `{}`
`registrySecret.labels` | Labels to be added to created registry secret | `{}`
