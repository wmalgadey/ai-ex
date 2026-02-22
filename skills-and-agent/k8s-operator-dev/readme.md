# K8s Operator Development

Claude Code Plugin für Kubernetes CRD Operator Development mit Kubebuilder und Tilt.

## Links

- https://github.com/Sagart-cactus/claude-k8s-plugin

## Features

- Guided workflow für komplette K8s Operators (Kubebuilder)
- Tilt-basierter Fast Dev Loop mit Live-Updates
- Safety Guards: Blockiert kubectl/helm auf Non-Kind-Clustern
- Commands: `/k8s:create-operator`, `/k8s:dev`, `/k8s:verify`, `/k8s:checklist`
- Skills: CRD Design, Webhook Patterns, RBAC, Templates

## Prerequisites

- Go, Kubebuilder, kind, kubectl, Kustomize, Tilt
- Installation via `/k8s:prereqs`

## Use Cases

- Platform Engineering: Custom Operators für K8s/OpenShift
- Fast prototyping mit Tilt Dev Loop
- Safe local development mit Kind-Clustern
