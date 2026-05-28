---
name: lph7
description: Erstellt einen vollstaendigen LPH 7 Bericht Mitwirkung bei der Vergabe (HOAI Paragraph 34, Gebaeude und Innenraeume) fuer ein beliebiges Architekturprojekt. Durchsucht alle Dateien im Projektordner, extrahiert Daten und befuellt das standardisierte HTML-Template. Baut auf der LPH 6 Dokumentation auf.
user-invocable: true
---

# LPH 7 Mitwirkung bei der Vergabe — Automatische Generierung

## OUTPUT-KONVENTION (verbindlich)

**WICHTIGSTE REGEL: Es wird ein EINZIGER Ordner namens `Claude/` im Projekt-Root erzeugt. ALLE Outputs landen dort drin. NIRGENDS sonst im Projekt.**

```
<Projekt-Root>/                           <- bleibt unveraendert
├── (die existierenden Projektordner)       (welche Struktur auch immer)
│
└── Claude/                               <- EINZIGER Ordner den wir anlegen
    ├── Projekt_Historie.md                 <- kumulative Wissensbasis
    ├── LPH_1/LPH1_Report_YYYY-MM-DD.html
    ├── LPH_2/LPH2_Report_YYYY-MM-DD.html
    ├── ... bis LPH_8/
    ├── Dashboard/Projekt_Dashboard_YYYY-MM-DD.html
    └── Fachplaner-Analyse/Fachplaner_Analyse_YYYY-MM-DD.md
```

**Dein konkreter Output-Pfad fuer diesen Skill:**
```
<Projekt-Root>/Claude/LPH_7/LPH7_Report_YYYY-MM-DD.html
```

**Pflichten beim Schreiben:**
1. Wenn `<Projekt-Root>/Claude/` nicht existiert: anlegen (mkdir)
2. Wenn `<Projekt-Root>/Claude/LPH_7` nicht existiert: anlegen
3. Datums-Format im Dateinamen: `YYYY-MM-DD` (z.B. 2026-05-27)
4. Bei jedem Aufruf: NEUE Datei mit aktuellem Datum (keine Ueberschreibung)

**NIEMALS schreibst du:**
- In andere Ordner des Projekts (00 Aktennotiz/, 11 Doku/, etc.) - keine Verschmutzung der Projekt-Struktur
- In den Projekt-Root direkt - nur in `Claude/` Unterstruktur
- In `~/.claude/plugins/` - das ist Read-only Plugin-Code
- In versteckte Ordner (.claude/) - nutze ausschliesslich `Claude/` (sichtbar)

---

## WISSENSBASIS NUTZEN

Falls `<Projekt-Root>/Claude/Projekt_Historie.md` existiert:
- ZUERST diese Datei lesen - sie enthaelt chronologisch alle E-Mails, Aktennotizen, Beschluesse
- Spart Zeit + Tokens (statt das ganze Projekt jedes Mal neu zu scannen)

Falls die Datei NICHT existiert:
- Empfehle dem User: "Tipp: Fuer aktuelle Daten zuerst /projekt-historie ausfuehren"
- Trotzdem das Projekt direkt scannen (Fallback)

---


## Template

Zentrale Ablage:
```
<via Plugin-Distribution geladen - Template liegt im Plugin selbst>
```

Kopiere nach `{Projekt}\13 Dokumentationen\Dokumentation LPH 7\LPH7_Report.html`.
Referenzen: `LPH7_Checkliste.md`, `LPH7_Informationsliste.md`.

## Ablauf — 6 Schritte

### Schritt 1: LPH 6 Dokumentation finden (PFLICHT)
- Suche nach `*LPH6*`, `*Vorbereitung*Vergabe*`, `*Ausschreibung*`
- Extrahiere: Vergabeeinheiten, Kostenanschlag, Bieterlisten, Submissionstermine

### Schritt 2: Projektordner durchsuchen
- **Angebote**: `**/*Gewerk*/*/Angebote/*.pdf`, `**/*Austausch*/**/Angebot*.pdf`
- **Preisspiegel**: `**/*Preisspiegel*.xlsx`, `**/*Preisvergleich*.pdf`
- **Vergabeprotokolle**: `**/*Vergabe*Protokoll*.pdf`, `**/*Zuschlag*.pdf`
- **Zuschlagsschreiben**: `**/*Zuschlagsschreiben*.pdf`, `**/*Auftragsvergabe*`
- **Bauzeitenplan**: `**/*Bauzeit*.pdf`, `**/*GANTT*`, `**/*MSProject*.mpp`
- **Aktualisierter Ausschreibungsstand** (mit Vergabesummen): `**/Ausschreibungsstand.xlsx`

### Schritt 3: Daten extrahieren
Siehe `LPH7_Informationsliste.md`:
- **Submissionsergebnisse**: je Gewerk alle Bieter mit Angebotssummen
- **Preisspiegel**: Tabelle Gewerk x Bieter, Bestangebot markiert
- **Angebotspruefung**: rechnerisch, technisch, wirtschaftlich, Eignung
- **Verhandlungsprotokolle**: Aufklaerung, Nachlaesse, Bauzeit
- **Vergabevorschlaege**: je Gewerk empfohlener Bieter + Begruendung
- **Vergabeentscheidungen**: AN, Vergabesumme netto/brutto, Zuschlagsdatum
- **Kostenanschlag aktualisiert**: Vergabesummen pro KGR, Vergleich LPH 6 vs. LPH 7
- **Vertragsunterlagen**: LV, BVB, Plaene, Fristen, Sicherheiten
- **Bauzeitenplan nach Vergabe**: Meilensteine, Reihenfolge, Puffer
- **Offene Punkte**: Noch zu vergebende Gewerke, AG-Freigaben

### Schritt 4: Template kopieren und befuellen
1. Kopiere `LPH7_Template.html` ins Projekt
2. Ersetze ALLE `{{PLATZHALTER}}`
3. Preisspiegel: Bestangebot je Gewerk mit CSS-Klasse `.price-best` hervorheben
4. Sidebar `{{DATEILISTE}}`

### Schritt 5: Wirtschaftlichkeitsempfehlung
- Δ Kostenanschlag LPH 6 vs. Vergabesumme
- Gewerke mit hoher Preisabweichung analysieren
- Bonitaetspruefung / Eignungsnachweise
- Nachtragsrisiken bei Billigangeboten diskutieren (§ 16d EU VOB/A)

### Schritt 6: Qualitaetspruefung
- PowerShell `Select-String` auf `{{`
- Alle Preise netto/brutto/MwSt konsistent
- Fachbegriffe: VOB/A §§ 12-19, § 16 (Angebotswertung), VgV / GWB bei oeff. Vergabe
- Stil sachlich, technisch, passiv

## Design-Regeln
- Schwarz `#1a1a1a`, A4 quer, contenteditable, randlos
- Bestangebot in Preisspiegel: `<td class="price-best">` (gruene Markierung)

## Platzhalter-Referenz
Siehe `LPH7_Informationsliste.md`. Hauptfelder:
Basis + 7.1 bis 7.10 + Abschluss
(`{{7_1_STAMMDATEN_TEXT}}`, `{{7_1_VERGABE_TABELLE}}`, `{{7_2_SUBMISSION_TEXT}}`, `{{7_2_PREISSPIEGEL_TABELLE}}`, `{{7_3_PRUEFUNG_*}}`, `{{7_4_VERHANDLUNG_*}}`, `{{7_5_EMPFEHLUNG_*}}`, `{{7_6_VERGABE_*}}`, `{{7_7_KOSTEN_*}}`, `{{7_7_KOSTEN_VERGLEICH}}`, `{{7_8_VERTRAG_*}}`, `{{7_9_BAUZEIT_*}}`, `{{7_10_OFFEN_*}}`, `{{ABSCHLUSS_TEXT}}`, `{{DATEILISTE}}`).
