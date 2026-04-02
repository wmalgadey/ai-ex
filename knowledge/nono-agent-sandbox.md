# nono — OS-level Sandbox für KI-Agenten

**Quelle:** https://nono.sh
**Gespeichert:** 2026-04-02

Open-Source-Sicherheitstool für KI-Agenten vom Sigstore-Gründer. Kernel-Enforcement statt Anwendungs-Guardrails — was nicht explizit erlaubt ist, ist auf OS-Ebene blockiert.

**Isolation:** Landlock (Linux), Seatbelt (macOS), WSL2 — prinzipiell nicht von innen aushebelbar

**Features:**
- Zulassungslisten auf Kernel-Ebene (Dateisystem, Netzwerk, Prozesse)
- Undo/Rollback — inhaltsadressierte Snapshots vor jeder Sitzung
- Audit Trail — kryptographisch gesichert via Merkle-Tree
- Supply-Chain-Herkunft — Sigstore-Signierung für vertrauenswürdige Quellen
- Runtime Supervisor — dynamische Freigaben zur Laufzeit

SDKs: Python, TypeScript, Rust. Kostenlos, plattformübergreifend.

#security #sandbox #agents #supply-chain #kernel #open-source
