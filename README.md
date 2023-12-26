# Kubecost 2.0 Preview Helm Chart

Welcome to the preview of the 2.0 Kubecost Helm Chart. This repository contains an early and experimental version of what Kubecost 2.0 could be.

Follow the instructions below to add this to your Helm repositories and then install the Chart.

## Instructions

```sh
helm repo add kubecosttwo https://chipzoller.github.io/kubecosttwo/
helm install kubecost -n kubecost kubecosttwo/kubecost --create-namespace
```

## Benefits

The restructuring modifications made in this repository and reflected by this preview chart have several benefits.

1. The "code" and the Helm repository are all in the same GitHub repository separated by branches, making it simpler and aligning with industry standards.
2. The major version split between application and chart make it such that the chart can be modified and released independently of the application (another standard practice). This is beneficial to users in that they do not need to wait for the next app version to receive chart-only fixes.
3. The state of the chart on the `main` branch has the `appVersion` set to `"development"` which, along with a slight template modification, allows for any deployments made from that chart version to always run the nightly latest images. This ensures CI tests are always in-sync and, further, that users clearly are able to see and understand this does not represent a released state.

## Releasing

The release process is very simple. A chart releasing action has been added making this process simpler still. The following steps should be followed.

1. If this is a new major or minor version, create a release branch from `main`. The current naming schema is `release-<M>.<m>` where `M` is the major version and `m` is the minor version.
2. After the release branch has been created, modify the `Chart.yaml` file to change the `appVersion` field to the version of the application being released (in Semver 2.0 format). Ex., `"2.1.0"`. Modify the `version` field to reflect the version of the chart keeping in mind the major version separation. For example, if the `appVersion` field was changed to be `"2.1.0"` then the `version` field would become `"3.1.0"`. Push changes to the release branch.
3. Create a Helm chart release using the release branch as the target branch. The release version should always be the Helm chart version. The release notes should specify which app version this deploys. Tags and release titles always start with a `v` (lower-case letter V).
