# helm-github-arc

A Crossplane Configuration package that installs the GitHub Actions Runner Controller (ARC) Helm chart with a minimal, stable interface.

## Overview

`helm-github-arc` renders a single Helm release for the GitHub Actions Runner Controller (gha-runner-scale-set-controller). It exposes only the inputs needed for chart values, namespace, and release name, keeping the interface stable while allowing full Helm overrides.

## Features

- **Minimal Helm interface**: values and overrideAllValues with stable defaults
- **Predictable naming**: defaults to `<metadata.name>` in the `arc-systems` namespace
- **GitOps friendly**: ships a `.gitops/` deploy chart

## Prerequisites

- Crossplane installed in the cluster
- Crossplane providers:
  - `provider-helm` (>=v1.0.2)
- Crossplane function:
  - `function-auto-ready` (>=v0.6.0)

## Quick Start

```yaml
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: helm-github-arc
spec:
  package: ghcr.io/hops-ops/helm-github-arc:latest
```

```yaml
apiVersion: helm.hops.ops.com.ai/v1alpha1
kind: GitHubARC
metadata:
  name: github-arc
  namespace: example-env
spec:
  clusterName: example-cluster
  values:
    replicaCount: 2
```

## Development

```bash
make render
make validate
make test
```
