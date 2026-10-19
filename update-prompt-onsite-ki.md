# Monatliches Update – Onsite-KI-Modelle-Aufstellung (HTML)

> **Verwendung:** Wiederkehrende Aufgabe für den **Hermes-Agenten**. Hermes führt dieses Update monatlich selbstständig aus: Datei aus dem GitHub-Repo holen, inhaltlich aktualisieren, direkt auf `main` zurück-pushen. Menschliche Freigabe nur bei Unsicherheiten (siehe „Fehler- & Sonderfälle").

## Ziel-Repository & Dateien

- **Repo:** `frank-arendt-references` (Owner: Frank Arendt)
- **Zu aktualisierende Datei (liegt im selben Repo):** `onsite-ki-modelle.html`
- **Diese Anweisung (Referenz, nicht verändern):** `update-prompt-onsite-ki.md`
- **Deploy-Weg:** direkt auf `main` committen und pushen.

## Auslösung & Catch-up (Nachholen beim Start)

Diese Aufgabe wird per **Cronjob am Monatsanfang** ausgelöst. Zusätzlich gilt eine **Nachhol-Regel**, damit kein Monat ausfällt, wenn Hermes am Monatsanfang offline war:

- **Bei jedem Hermes-Start** (und einmal täglich) prüfen, ob das Update für den **laufenden Kalendermonat** bereits gelaufen ist.
- **Prüfmethode:** letzten Update-Zeitpunkt ermitteln – primär über die Commit-Historie der Datei (`git log -1 --format=%cI -- onsite-ki-modelle.html`) bzw. den Datumsstempel im Header/der Fußzeile von `onsite-ki-modelle.html`. Fällt dieser Zeitpunkt **in einen früheren Monat als den aktuellen**, wurde das Monatsupdate noch nicht gemacht.
- **Wenn noch nicht gelaufen → jetzt nachholen:** die komplette Prozedur (Schritte 0–7) unmittelbar ausführen.
- **Wenn im aktuellen Monat bereits gelaufen → nichts tun** (kein zweiter Lauf, kein Leer-Commit). Nur kurz „für [MONAT JJJJ] bereits aktualisiert" vermerken.
- **Doppelausführung vermeiden:** Falls Cron und Start-Catch-up zusammenfallen, schützt die Monatsprüfung vor einem zweiten Lauf. Optional eine Sperrdatei/Marker (z. B. `.last-update-YYYY-MM`) nutzen, um parallele Läufe zu verhindern.

---

**Aktualisierungsdatum:** `[MONAT JJJJ eintragen, z. B. August 2026]`

Du aktualisierst eine bestehende HTML-Aufstellung zu lokal betriebenen KI-Modellen für Amateure und KMU. Die Datei liegt im Repo `frank-arendt-references` als `onsite-ki-modelle.html` (siehe Schritt 0). Behalte Struktur, Design, Farbschema, Inhaltsverzeichnis und alle Abschnitte exakt bei – ändere nur inhaltliche Werte, die veraltet sind.

## Vorgehen (in dieser Reihenfolge)

0. **Zu überarbeitende Datei direkt von GitHub herunterladen.** Hole die aktuell im Repo liegende Fassung von `onsite-ki-modelle.html` als Ausgangsbasis – entweder über die Raw-URL oder per Repo-Klon:
   - **Direkt per URL (Raw):** `https://raw.githubusercontent.com/FrankArendt/frank-arendt-references/main/onsite-ki-modelle.html` (z. B. mit `curl -O` oder `wget`). Nutze immer die Datei aus `main`, nicht eine lokale Alt-Version.
   - **Alternativ per Klon/Pull** (nötig für den späteren Push): `git clone https://github.com/FrankArendt/frank-arendt-references.git` bzw. in vorhandenem Klon `git pull origin main`.
   - Prüfe, dass die heruntergeladene Datei vollständig und valides HTML ist, bevor du weitermachst. Arbeite auf dieser echten Datei – lege keine Kopie/Neu-Datei an. *(Hinweis: Für Schritt 6 – Push auf `main` – wird ohnehin ein Klon mit Schreibzugriff benötigt; wer nur die Raw-URL zieht, muss vor dem Commit noch klonen.)*

1. **Lies die Datei vollständig ein**, um Struktur und aktuelle Werte zu erfassen. Ändere niemals das Layout/CSS, nur Daten.

2. **Recherchiere per Websuche die folgenden Punkte neu** (jeweils mit Quelle und Datum, deutscher Markt / Geizhals bevorzugt):
   - Aktuelle populäre Open-Weight-Modelle je Größenklasse (0 / klein / mittel / groß). Prüfe, ob neue Versionen erschienen sind (z. B. neue Llama-, Qwen-, Gemma-, Phi-, Mistral-, DeepSeek-Generationen) und ersetze veraltete. **Verifiziere, dass genannte Modelle real existieren – erfinde keine Versionen.**
   - GPU-Neupreise: RTX 5060 Ti 16GB, RTX 5090 32GB, RTX 4090, jeweils günstigster Neuware-Anbieter (Geizhals DE).
   - **Neuere Grafikkarten-Generationen aktiv prüfen und einbauen, sobald real verfügbar:** Recherchiere, ob seit dem letzten Stand neue Consumer-/Prosumer-GPUs erschienen sind (z. B. NVIDIA RTX 50-Refresh / RTX 60-Serie / neue „Super"-Varianten, AMD Radeon mit hohem VRAM, Intel Arc High-VRAM, NVIDIA-Blackwell/Nachfolger-Workstationkarten wie RTX PRO). Kriterien: (a) **tatsächlich am deutschen Markt als Neuware lieferbar** (nicht nur angekündigt), (b) relevant für lokale KI (VRAM-Größe, Preis-Leistung, Effizienz). Wenn eine neue Karte eine bestehende Empfehlung schlägt (mehr VRAM zum gleichen Preis, besseres €/GB oder deutlich sparsamer), **ersetze die alte Empfehlung** und passe VRAM-Zuordnung, Preis, Stromkosten und Gesamtkosten an. Nur angekündigte, aber nicht kaufbare Karten höchstens als kurzen „am Horizont"-Hinweis, nicht als Empfehlung.
   - Mac Studio / Mac-Alternativen: aktuelles M-Max-Modell mit 128GB (oder mehr) Unified Memory prüfen; **falls eine neue M-Generation erschienen ist, diese übernehmen.** Neupreis.
   - Raspberry Pi 5 (8/16GB) Preis & Verfügbarkeit; **prüfen, ob ein Nachfolger (z. B. Pi 6) oder relevantes KI-Zubehör (AI HAT+ Nachfolger) verfügbar ist** und ggf. ergänzen.
   - SSD-Preise (hochwertige NVMe 2TB + Enterprise mit Power-Loss-Protection).
   - Aktueller deutscher Strompreis (Ct/kWh, Bestandskunden).
   - **Fertigrechner / Komplettsysteme aktiv aktualisieren:** aktuelle Dell-Precision- und Lenovo-ThinkStation-Baureihen prüfen; **sobald neue Modellgenerationen mit den neueren GPUs/CPUs ab Werk konfigurierbar sind, diese eintragen** und veraltete Baureihen ersetzen. Ebenso prüfen, ob weitere relevante Fertig-Anbieter/„AI-Workstation"-Systeme dazugekommen sind.
   - **CPU-Typen aktiv aktualisieren:** prüfen, ob neue relevante CPU-Generationen erschienen sind (z. B. neue AMD Ryzen / Ryzen AI Max / Threadripper (PRO), Intel Core / Core Ultra, Apple M-SoCs). Wenn eine neue Generation die bisherige Empfehlung je Cluster ablöst (bessere Mehrkern-Leistung, mehr PCIe-Lanes, bessere Effizienz), **die CPU-Empfehlung im Abschnitt „CPU & Fertigrechner" entsprechend ersetzen.**
   - Mobile Clients (Reins, Enchanted, Chatbox, Open WebUI) – noch aktuell/verfügbar? Neue empfehlenswerte Apps dazugekommen?
   - VPN (Tailscale/WireGuard), Runtimes (Ollama/vLLM), n8n/Hermes/OpenCode – relevante Neuerungen?
   - **Architektur-/Software-Komponenten aktiv auf bessere Alternativen prüfen und ggf. ergänzen/ersetzen** (Abschnitt „Praxisbetrieb"). Wenn seit dem letzten Stand ein Baustein erschienen ist, der eine bestehende Empfehlung klar schlägt (Leistung, Einfachheit, Sicherheit, Verbreitung, Wartung), aufnehmen bzw. austauschen. Betrifft alle vier Schichten:
     - **Modell-Runtime / Serving:** Alternativen zu Ollama/vLLM (z. B. LM Studio, llama.cpp, TGI, SGLang, LocalAI, MLX-Serving) – neue oder überlegene Optionen prüfen.
     - **Gateway / Routing:** Alternativen/Ergänzungen zu LiteLLM (z. B. neue OpenAI-kompatible Gateways, Router mit Budget-/Nutzer-Limits).
     - **RAG- / Wissens-Layer:** Vektor-DBs (Qdrant, alternativ Chroma, Weaviate, Milvus, pgvector), Parser (Tika, alternativ Docling, Unstructured), Embedding-Modelle, sowie fertige RAG-Frameworks.
     - **Anwendungen / Frontends / Agenten:** Automations- (n8n, Alternativen), Agenten- (Hermes, OpenCode, Alternativen), Chat-Frontends (Open WebUI, Alternativen), IDE-Plugins (Continue, Cline, Alternativen), Notiz-/Wissenssysteme (Obsidian, Alternativen).
     - **Betrieb / Sicherheit / Fernzugriff:** Prozess-/Container-Orchestrierung (systemd, Proxmox, Docker), Monitoring/Tracing (Langfuse, Alternativen), VPN (Tailscale/WireGuard, Alternativen), Reverse-Proxy/Auth-Lösungen.
     Kriterium: **breit genutzt, quelloffen bevorzugt, sinnvoll selbst hostbar.** Reine Nischen- oder Cloud-only-Tools nicht aufnehmen. Wesentliche Änderungen an der Architektur ebenfalls in der Fußzeile („alt → neu") vermerken.

3. **Aktualisiere in der HTML nur die geänderten Werte:** Preise, Modellnamen/Parameter, VRAM, Stromkosten, Gesamtkosten, Empfehlungen. Halte alle vier Modell-Tabellen spaltenkonsistent (11 Spalten; die letzte Spalte „Typische Einsatzbereiche“ bei neuen oder ersetzten Modellzeilen mitpflegen, als Orientierung kennzeichnen, nur belegte Angaben). Aktualisiere das Datum im Header, im Untertitel und in der Quellen-Fußzeile.

4. **Kennzeichne im Fußzeilen-Quellenteil kurz, was sich seit dem letzten Stand geändert hat** (1–3 Sätze „Änderungen in diesem Update").

5. **Prüfe die Tabellen technisch** (Header- vs. Zellenzahl je Modell-Tabelle müssen übereinstimmen, derzeit 11 Spalten) und dass valides HTML vorliegt.

6. **Deployen (direkt auf `main`).** Nur wenn Schritt 5 fehlerfrei ist:
   - Überschreibe `onsite-ki-modelle.html` in-place (gleicher Dateiname, gleicher Pfad – nicht doppelt anlegen).
   - `git add onsite-ki-modelle.html`
   - Commit mit Nachricht nach diesem Muster: `Update Onsite-KI-Aufstellung [MONAT JJJJ] – <1 Zeile wichtigste Änderung>`
   - `git push origin main`
   - Verändere niemals `update-prompt-onsite-ki.md` selbst.

7. **Abschlussbericht an Frank** (kurz, im Chat/Messenger): erledigt ja/nein, Commit-Hash bzw. -Nachricht, 3–5 Stichpunkte der wichtigsten Änderungen, und ausdrücklich alle Stellen, an denen die Recherche unsicher war.

## Fehler- & Sonderfälle

- **Recherche unsicher / widersprüchliche Preise:** Nicht raten. Den alten Wert stehen lassen, im Abschlussbericht als „unbestätigt – Prüfung nötig" markieren. Lieber ein Wert unverändert als ein falscher Wert.
- **Modell nicht real verifizierbar:** Nicht aufnehmen. Keine erfundenen Versionen (kein „Phi-5" o. Ä.).
- **Nichts hat sich geändert:** Kein Leer-Commit erzwingen; im Bericht „keine relevanten Änderungen in diesem Monat" melden.
- **`git push` schlägt fehl** (Auth, Konflikt, Netz): Änderungen lokal committed lassen, NICHT mehrfach blind neu versuchen. Frank mit der genauen Fehlermeldung informieren und auf manuelles Eingreifen warten.
- **Merge-Konflikt / Datei zwischenzeitlich geändert:** Erst `git pull --rebase`, Konflikt sauber lösen, dann erneut pushen. Im Zweifel abbrechen und Frank informieren.
- **Größere strukturelle Neuerung nötig** (neuer Cluster, neue Tabellen-Spalte): nicht eigenmächtig umbauen – vorschlagen und Freigabe von Frank abwarten.

## Grundregeln

- **Neuware-Preise** (keine Gebrauchtware).
- **SSD-Spiegel (RAID-1) + USV** bleiben in den Gesamtkosten enthalten.
- **Fernzugriff bleibt VPN-only.**
- Alle Preise als **gerundete Richtwerte inkl. MwSt. mit Datum**.
- **Unsicherheiten offen kennzeichnen.**
- **Kein „Phi-5" o. Ä. erfinden** – nur real belegte Modelle.
- **Neuere Hardware nur bei echter Marktverfügbarkeit übernehmen** (als Neuware in DE lieferbar), nicht bei bloßer Ankündigung. Wird eine Empfehlung durch eine neuere GPU/CPU/Workstation ersetzt, in der Fußzeile unter „Änderungen in diesem Update" ausdrücklich vermerken (alt → neu).
- **Im Zweifel konservativ:** Ein unveränderter, belegter Wert ist besser als eine unbelegte Aktualisierung. Alle Unsicherheiten in den Abschlussbericht an Frank aufnehmen.

---

### Checkliste der Abschnitte, die die Datei enthält (dürfen nicht verloren gehen)

1. Wichtiger Hinweis: Aktualität, Grenzen & fehlendes Benchmarking
2. Warum onsite? Risiken großer Cloud-KI
3. Rechtsrahmen: EU AI Act, DSGVO & Urheberrecht
4. IT-Sicherheit & Zertifizierung (BSI-Grundschutz, ISO 27001, ISO 42001)
5. Betriebssysteme im Überblick (Windows / Linux / macOS / Pi)
6. Gebrauchte Grafikkarten: worauf achten
7. Zur Kostenkalkulation (SSD-Spiegel & USV)
8. Cluster 0 – Raspberry Pi 5
9. Cluster 1 – Kleine Modelle
10. Cluster 2 – Mittlere Modelle
11. Cluster 3 – Große Modelle (inkl. Mac Studio M5 Max/Ultra)
12. Entscheidungshilfe nach Budget
13. Praxisbetrieb (Architektur, Admin, VPN, Mobile-Clients, Markdown-Arbeitsweise inkl. Link auf Karpathys „LLM Wiki“-Gist)
14. Coding-Agenten auf lokalen Modellen
15. CPU-Empfehlungen & Fertigrechner (Dell / ThinkStation)
16. Hosting-Alternative: GPU-Server mieten & Lastverteilung
17. Selbst trainieren / Feintuning (wann, Ablauf, Hardware Training vs. Inferenz)
18. Einrichtung Schritt für Schritt – Cluster 1 bis 3
19. Schlusstext „Vom Cloud-Dienst zum persönlichen KI-Begleiter"
20. Glossar
21. Impressum und Datenschutzerklärung (nicht inhaltlich verändern, nur auf Aktualität des Hostings/Texts achten)
22. Hinweise + Quellen-Fußzeile

Zusätzlich dürfen nicht verloren gehen: die Spalte „Typische Einsatzbereiche“ in den vier Modell-Tabellen, die JSON-LD-/SEO-Metadaten im `<head>` (bei jedem Update `dateModified`, `article:modified_time` und das `<time>`-Datum im Header auf das Update-Datum setzen) sowie der Link auf https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f im Abschnitt Praxisbetrieb.
