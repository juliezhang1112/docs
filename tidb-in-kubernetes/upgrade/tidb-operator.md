---
title: Upgrade TiDB Operator and Kubernetes
summary: Learn how to upgrade TiDB Operator and Kubernetes.
category: how-to
---

# Upgrade TiDB Operator and Kubernetes

This document describes how to upgrade TiDB Operator and Kubernetes.

## Upgrade TiDB Operator

To upgrade TiDB Operator, modify the image version in the `values.yaml` file and then run `helm upgrade`:

{{< copyable "shell-regular" >}}

```shell
helm upgrade tidb-operator pingcap/tidb-operator --version=<chart-version> -f /home/tidb/tidb-operator/values-tidb-operator.yaml
```

When a new version of `tidb-operator` is released, you only need to update `operatorImage` in `values.yaml` and run the above command. But to guarantee safety, you must get the new `values.yaml` file from the new `tidb-operator` chart and merge the old `values.yaml` file with the new one. And then upgrade as above.

TiDB Operator is used for maintaining TiDB cluster. This means that when TiDB cluster is up and running, you can even stop TiDB Operator without affecting TiDB cluster that works well until you need to maintain the cluster for scaling, upgrading, etc.

## Upgrade Kubernetes

When there is a major version upgrade of Kubernetes, you need to make sure that `kubeSchedulerImageTag` matches the version. By default, this value is generated by Helm during the installation or upgrade process. To reset this value, execute `helm upgrade`.
