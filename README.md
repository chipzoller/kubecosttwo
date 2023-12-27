# Kubecost 2.0 Helm chart

This is a concept for the Kubecost 2.0 Helm chart.

## Version Support

Kubecost strives to support as many versions of Kubernetes as possible. Below is the version support matrix which has been tested. Versions outside of the stated range may still work but are untested.

| Chart Version                | Kubernetes Min | Kubernetes Max |
|--------------------------------|----------------|----------------|
| 1.107                          | 1.20           | 1.28           |
| 1.108                          | 1.20           | 1.28           |

## Installation

To install via Helm, run the following command.

```sh
helm upgrade --install kubecost -n kubecost --create-namespace \
  --repo https://kubecost.github.io/cost-analyzer/ cost-analyzer \
  --set kubecostToken="aGVsbUBrdWJlY29zdC5jb20=xm343yadf98"
```

Alternatively, add the Helm repository first and scan for updates.

```sh
helm repo add kubecost https://kubecost.github.io/cost-analyzer/
helm repo update
```

Next, install the chart.

```sh
helm install kubecost kubecost/cost-analyzer -n kubecost --create-namespace \
  --set kubecostToken="aGVsbUBrdWJlY29zdC5jb20=xm343yadf98"
```

While Helm is the [recommended install path](http://kubecost.com/install) for Kubecost, especially in production, Kubecost can alternatively be deployed with a single-file manifest using the following command. Keep in mind when choosing this method, Kubecost will be installed from a development branch and may include unreleased changes. We recommend using the manifest from a release branch, such as v1.108.

```sh
kubectl apply -f https://raw.githubusercontent.com/kubecost/cost-analyzer-helm-chart/develop/kubecost.yaml
```

## Adjusting Log Output

The log output can be customized during deployment by using the `LOG_LEVEL` and/or `LOG_FORMAT` environment variables.

### Adjusting Log Level

Adjusting the log level increases or decreases the level of verbosity written to the logs. To set the log level to `trace`, the following flag can be added to the `helm` command.

```sh
--set 'kubecostModel.extraEnv[0].name=LOG_LEVEL,kubecostModel.extraEnv[0].value=trace'
```

### Adjusting Log Format

Adjusting the log format changes the format in which the logs are output making it easier for log aggregators to parse and display logged messages. The `LOG_FORMAT` environment variable accepts the values `JSON`, for a structured output, and `pretty` for a nice, human-readable output.

| Value  | Output                                                                                                                     |
|--------|----------------------------------------------------------------------------------------------------------------------------|
| `JSON`   | `{"level":"info","time":"2006-01-02T15:04:05.999999999Z07:00","message":"Starting cost-model (git commit \"1.91.0-rc.0\")"}` |
| `pretty` | `2006-01-02T15:04:05.999999999Z07:00 INF Starting cost-model (git commit "1.91.0-rc.0")`                                     |
