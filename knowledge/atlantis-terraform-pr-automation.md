# Atlantis — Terraform Pull Request Automation

**Quelle:** https://www.runatlantis.io/
**Gespeichert:** 2026-03-28

Self-hosted Tool für Terraform-Workflows über Git Pull Requests. Kein SaaS, kein Vendor-Lock-in.

Kernprinzip: PR öffnen → `terraform plan` läuft automatisch als Kommentar → nach Approve `terraform apply`. Entwickler brauchen keine direkten Cloud-Credentials — Atlantis hält die Secrets.

- GitHub, GitLab, Bitbucket, Azure DevOps unterstützt
- Läuft auf VM, Kubernetes, Fargate
- Audit-Log für alle Änderungen und Genehmigungen
- Laut Projektseite im Einsatz bei 600+ Repos und 300 Entwicklern

#terraform #gitops #infrastructure #devops #self-hosted
