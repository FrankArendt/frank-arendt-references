# frank-arendt-references

Referenzunterlagen von Frank Arendt (Diplominformatiker, Bretten): Konzepte, Studien und Aufstellungen aus den Bereichen Digitalisierung, KI und Energie. Stand dieser Übersicht: 19.10.2026.

Alle Dokumente sind Entwürfe oder Orientierungshilfen, keine Rechts-, Steuer- oder Anlageberatung. Zahlen sind, soweit nicht anders vermerkt, Modellrechnungen oder Herstellerangaben.

## Übersicht

| Projekt | Dokumente | Kurzbeschreibung | Stand |
|---|---|---|---|
| [Onsite-KI](#onsite-ki) | [onsite-ki-modelle.html](onsite-ki-modelle.html) | Praxisleitfaden für lokal betriebene KI-Modelle (Hardware, Kosten, Recht, IT-Sicherheit) | Okt. 2026 |
| [SCORE](#score) | [Anforderungsdokument](SCORE%20Anforderungsdokument.pdf), [Konzept-Deck](SCORE_%E2%80%94_Smart_Cost-Optimized_Recognition_%26_Evaluation_Engine%202.pdf), [Beratungsdokumentation](SCORE_Beratungsdokumentation_Arendt.pdf) | Lernender Prozess zur Belegerkennung mit kostengesteuerter Verfahrenswahl | Juli bis Okt. 2026 |
| [Smart Grid Eigenheim](#smart-grid-eigenheim) | [Anforderungsdokument](Digitalisierungsprojekt%20Smart%20Grid%20v1%204.html), [Kundenpräsentation](Smart_Grid_Eigenheim.pdf) | Energiemanagementsystem für ein Wohnhaus mit PV, Speicher, E-Auto und Wallbox | Juli 2026 |
| [Power on Rails](#power-on-rails) | [Power on Rails.pdf](Power%20on%20Rails.pdf) | Machbarkeitsbetrachtung: Batterien auf Güterwagen als Brücke im Netzausbau | Okt. 2026 (Fassung 2.1) |
| [PROJECT HELIOS](#project-helios) | [PROJECT HELIOS Studie.pdf](PROJECT%20HELIOS%20Studie.pdf) | Konzeptstudie: global verteiltes, erneuerbar versorgtes Rechenzentrumsnetz für KI-Training | Juli 2026 |

---

## Onsite-KI

**Datei:** `onsite-ki-modelle.html` (einzelne HTML-Seite, online unter https://onsite-ki.de/)

**Worum es geht:** Aufstellung und Leitfaden für Privatpersonen und KMU, die KI-Modelle lokal statt in der Cloud betreiben wollen.

**Management Summary**
- **Modelle nach Hardware:** Open-Weight-Modelle in vier Clustern (Raspberry Pi, kleine, mittlere, große Modelle) mit Speicherbedarf, passender Hardware, Stromkosten und Gesamtkosten inklusive gespiegelter SSD und USV; je Modell die typischen Einsatzbereiche (u. a. OCR) als Orientierung
- **Hardware-Preise:** Neuware-Richtwerte für den deutschen Markt (Stand 19.10.2026); GPU- und Mac-Studio-Preise sind 2026 deutlich gestiegen, unbestätigte Werte sind im Dokument markiert
- **Betrieb:** Architektur-Schichten (Runtime, Gateway, Wissensbasis, Anwendungen), Fernzugriff nur über VPN, Mobile-Clients, Markdown-Arbeitsweise (inkl. Verweis auf das „LLM Wiki"-Muster von Andrej Karpathy), Coding-Agenten auf lokalen Modellen
- **Recht und Sicherheit:** EU AI Act, DSGVO, Urheberrecht, BSI-Grundschutz, ISO 27001 und 42001, OWASP-Hinweise, Patch-Disziplin
- **Zusätzlich:** GPU-Server mieten (Anbietervergleich DE/EU), Selbst trainieren bzw. Feintuning (wann, Ablauf, Hardware Training gegenüber Inferenz), Schritt-für-Schritt-Einrichtung für Windows, Linux und macOS
- **Grenzen:** Momentaufnahme ohne eigenes Benchmarking; Preise ändern sich schnell und sind vor einer Kaufentscheidung zu prüfen

---

## SCORE

**Smart Cost-Optimized Recognition & Evaluation Engine**

**Dokumente:** Anforderungsdokument (52 Seiten, Version 1.5, Juli 2026), Konzept-Deck (12 Folien, Juli 2026), Beratungsdokumentation (25 Seiten, Oktober 2026)

**Management Summary**
- **Problem:** Belege sind heterogen; ein starrer, teurer OCR-/IDP-Dienst und viele manuelle Klärfälle machen die Belegverarbeitung aufwendig
- **Ansatz:** Ein lernender Prozess wählt pro Beleg das günstigste Verfahren, das voraussichtlich ausreicht. Eine statische Bildanalyse vor der OCR liefert Messgrößen; daraus wird eine Startstufe vorhergesagt. Darauf folgt eine Eskalation von lokaler OCR bis zu Cloud-LLMs mit fester Kostenobergrenze. Plausibilitäts-, Rechen- und Sicherheitsprüfungen sowie eine Klärfall-Prüfoberfläche sichern das Ergebnis ab. Jeder Fall fließt in die Wissensbasis ein, das Modell wird regelmäßig neu trainiert
- **Bausteine:** n8n, DuckDB, Tesseract, Docling, Ollama, Claude Haiku, LightGBM, Redis
- **Entwicklung der Konzeption:** Die Konzeptdokumente (Juli 2026) beschreiben eine Fuzzy-Distanz auf bis zu 60 Messgrößen; die Beratungsdokumentation (Oktober 2026) beschreibt den späteren Stand mit LightGBM als Startstufen-Prognose, 49 Belegarten und Rechenprüfung
- **Ergebnisse laut Beratungsdokumentation** (Testdaten öffentlich oder synthetisch): Massentest mit 1.000 Belegen: 93,4 % ohne Klärfall, rund 0,1 Cent Gesamtkosten je Beleg; Red-Team-Test zum Schutz vor Prompt Injection: alle 18 Angriffe erkannt
- **Ehrliche Einschränkungen:** Feldrichtigkeit auf Testkassenbons nur 41–71 %; einige Prüfungen laufen noch im Shadow-Modus; ein Pilot mit echten deutschen Belegen steht aus
- **Empfehlung:** vierwöchiger Pilot, danach schrittweise Ablösung des bisherigen Verfahrens

**Hinweis:** Das Dashboard im Konzept-Deck zeigt Beispielwerte (Mockup), keine Messwerte.

---

## Smart Grid Eigenheim

**Dokumente:** Anforderungsdokument (HTML, Version 1.4, Entwurf), Kundenpräsentation (12 Folien, 23.07.2026)

**Management Summary**
- **Ziel:** Ein Energiemanagementsystem (EMS) für einen deutschen Haushalt mit PV-Anlage, Batteriespeicher, Elektroauto und Wallbox: möglichst hoher Eigenverbrauch, netzdienlicher Betrieb nach § 14a EnWG und Kostenoptimierung über dynamische Börsenstrompreise
- **Umfang:** Funktionale Anforderungen und REST-API (Wetter- und PV-Prognose, Strombörse, Wechselrichter, Fahrzeug, Wallbox), Steuerungsregeln, iPhone-App, nicht-funktionale und rechtliche Anforderungen, Schichtenarchitektur
- **Zielwerte:** Autarkie 75–90 % im Jahresmittel, Prognoseabweichung höchstens 15 %, Verfügbarkeit des EMS-Kerns mindestens 99,5 %
- **Umsetzungsplan:** 22 Wochen in sechs Meilensteinen
- **Stand:** Anforderungsdokument im Entwurf (Version 1.4); die Kundenpräsentation fasst dasselbe Projekt nicht-technisch zusammen

---

## Power on Rails

**Datei:** `Power on Rails.pdf` (Fassung 2.1, 24 Seiten; ursprüngliche Fassung 1.0 vom 31.07.2024)

**Management Summary**
- **Idee:** Güterwagen, deren Nutzlast aus Batteriesystemen besteht, werden im Norden mit Überschussstrom geladen und im Süden entladen, als temporäre Brücke, solange Übertragungsleitungen fehlen und Bahnkapazitäten aus dem Kohleausstieg frei werden
- **Ergebnis der Rechnung:** Im Basisfall (Einzelwagenverkehr, DB-Cargo-Preisliste 2026) liegen die Vollkosten bei rund 280 ct/kWh, etwa das Siebzehnfache des Industriestrompreises. Selbst im günstigsten Fall (Ganzzug, hohe Energiedichte) bleiben rund 43 ct/kWh. Fassung 2.0 war noch von rund 500 ct/kWh ausgegangen; der Unterschied kommt aus dem leeren Rücklauf, den die Preisliste deutlich günstiger tarifiert
- **Kernbefund:** Nicht die Energiedichte, sondern die Auslastung des eingesetzten Kapitals ist der begrenzende Faktor. Ein stationärer Speicher nutzt dieselbe Batterie etwa fünfmal häufiger
- **Größenordnung:** Als Ersatz für eine Übertragungsleitung (z. B. ein SuedLink-System mit 2 GW) wären rund 173 Ganzzüge pro Tag und Richtung nötig, betrieblich nicht darstellbar
- **Tragfähiger Kern:** netzferne oder temporäre Bedarfe, Überbrückung verzögerter Netzanschlüsse, Doppelnutzung mit ohnehin vorzuhaltender Notstromversorgung, am ehesten mit Containern statt Ganzzug
- **Offene Punkte:** belastbarer Ganzzugtarif, Gefahrgutrecht (UN 3536), Volumen- gegen Massenbegrenzung; Ganzzugwerte beruhen auf Annahmen
- **Stand:** Entwurf zur fachlichen Diskussion; das PDF entstand aus einer HTML-Umsetzung der Word-Fassung (Layout und Inhaltsverzeichnis weichen von der Word-Fassung ab)

---

## PROJECT HELIOS

**Datei:** `PROJECT HELIOS Studie.pdf` (30 Seiten, 18.07.2026)

**Management Summary**
- **Thema:** Konzeptstudie für ein global verteiltes Rechenzentrumsnetz, das große Sprachmodelle dort trainiert, wo gerade erneuerbarer Strom verfügbar ist („Follow the Renewables")
- **Inhalt:** Standortwahl und politische Stabilität, Energieversorgung mit Batteriepuffern, Verlagerung von Trainingszwischenständen (Checkpoints) zwischen Standorten, modellierte Verfügbarkeit, Kostenmodell im Vergleich zu gasversorgten Rechenzentren, Abgrenzung von Training und Inferenz
- **Eckpunkte des Konzepts:** sechs Standorte, 12 GW IT-Leistung
- **Bewertung:** Das Papier ist ein Konzept, keine Investitionsempfehlung; alle Ergebnisse sind modellbasierte Schätzungen. Empfohlen wird eine vertiefte, standortspezifische Machbarkeitsstudie

---

## Hinweise

- Dokumente mit Version und Datum im Titel sind Momentaufnahmen; maßgeblich ist jeweils der Stand im Dokument
- Preise und Marktdaten ändern sich schnell und sind vor Entscheidungen zu prüfen
- Die Zusammenfassungen oben sind absichtlich auf Projektebene gehalten
