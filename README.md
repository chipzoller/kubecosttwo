# Kubecost 2.0 Preview Helm Chart

Welcome to the preview of the 2.0 Kubecost Helm Chart. This repository contains an early and experimental version of what Kubecost 2.0 could be.

Follow the instructions below to add this to your Helm repositories and then install the Chart.

## Instructions

```sh
helm repo add kubecosttwo https://chipzoller.github.io/kubecosttwo/
helm install kubecost -n kubecost kubecosttwo/kubecost --create-namespace
```
