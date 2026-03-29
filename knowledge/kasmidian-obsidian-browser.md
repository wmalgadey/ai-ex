# Kasmidian — Obsidian im Browser für KI-Agenten

**Quelle:** https://github.com/Cityjohn/Kasmidian
**Gespeichert:** 2026-03-30

Minimales Docker-Projekt das Obsidian als browserbasierte Desktop-Anwendung bereitstellt — primär damit KI-Agenten dauerhaft auf einen Vault zugreifen können.

Basis ist das offizielle Kasm-Obsidian-Image (VNC auf Port 6901). Das Problem: kein Window Manager, minimierte Fenster verschwinden permanent. Kasmidian ergänzt eine XFCE-Taskleiste. Vault wird per Volume gemountet.

Kontext des Autors: "Aristos"-Personal-Coaching-Framework mit KI-Agenten-Zugriff auf Obsidian.

Alternativer Ansatz zu direktem Vault-Mount — nützlich wenn kein Dateisystem-Zugriff möglich ist.

#obsidian #docker #kasm #agents #vault #browser
