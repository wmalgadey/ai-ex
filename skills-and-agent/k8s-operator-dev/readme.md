# K8s Operator Development

**Quelle:** https://github.com/Sagart-cactus/claude-k8s-plugin
**Gespeichert:** 2026-03-01

Claude Code Plugin für Kubernetes CRD Operator Development mit Kubebuilder und Tilt. Interessant wegen des integrierten Safety-Guards — blockiert `kubectl`/`helm` automatisch auf Non-Kind-Clustern.

## Features

- Guided workflow für K8s Operators (Kubebuilder)
- Tilt-basierter Fast Dev Loop mit Live-Updates
- Safety Guards gegen versehentliche Produktions-Deployments
- Commands: `/k8s:create-operator`, `/k8s:dev`, `/k8s:verify`, `/k8s:checklist`
- Skills: CRD Design, Webhook Patterns, RBAC, Templates

## Prerequisites

Go, Kubebuilder, kind, kubectl, Kustomize, Tilt — Installation via `/k8s:prereqs`.

#claude-code #kubernetes #k8s #operators #kubebuilder #tilt #plugin
