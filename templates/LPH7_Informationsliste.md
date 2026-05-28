# LPH 7 — Informationsliste

## Quelle der Felder — Projektanalyse

| Feldgruppe | Herkunft aus Projektanalyse |
|---|---|
| Vergabesummen je Gewerk | Implizit in (Projekt-Nr.), (Projekt-Nr.) (Schlussrechnungen erlauben Rückschluss auf Auftragssummen) |
| Bauzeitenplan | Standardpraxis + Referenz-Projekt B (Sporthalle) (gewerkweise Zuordnung) |
| Grundleistungen | HOAI § 34 LB 7 (7.1–7.10 Grundleistungen) |

**Hinweis:** LPH 7 war in den analysierten Projekten am schlechtesten separat dokumentiert — Inhalte liegen meist im `09 Austausch` oder in Angebotsordnern der einzelnen Gewerke.

## Pflicht-Quellen im Projektordner

| Quelle | Suchpfad | Zweck |
|---|---|---|
| LPH 6 Report | `**/LPH6_Report*.html` | Brücke |
| Ausschreibungsstand | `**/Ausschreibungsstand.xlsx` | Vergabesummen eintragen |
| Angebote der Bieter | `**/06 Gewerk*/*/Angebote/*.pdf`, `**/09 Austausch/**/Angebot*.pdf` | 7.2/7.3 |
| Preisspiegel | `**/*Preisspiegel*.xlsx`, `**/*Preisvergleich*.pdf` | 7.2 |
| Vergabeprotokolle | `**/*Vergabe*Protokoll*.pdf`, `**/*Zuschlag*.pdf` | 7.4/7.6 |
| Zuschlagsschreiben | `**/*Zuschlagsschreiben*.pdf`, `**/*Auftragsvergabe*.docx` | 7.6 |
| Bauzeitenplan | `**/*Bauzeit*.pdf`, `**/*GANTT*.pdf`, `**/*MS Project*.mpp` | 7.9 |
| Beteiligtenliste | `**/*Beteiligte*.xlsx` (vollständig, inkl. beauftragter AN) | 7.6 |

## Platzhalter-Referenz → Herkunft

| Platzhalter | Datenquelle | Typ |
|---|---|---|
| Basis-Platzhalter | LPH 6 | Text |
| `{{7_1_STAMMDATEN_TEXT}}` | LPH 6 + Projektstand | Fließtext |
| `{{7_1_VERGABE_TABELLE}}` | Vergabeübersicht | HTML `<table>`: Gewerk, Vergabeverfahren, Submission, Status |
| `{{7_2_SUBMISSION_TEXT}}` | Submissionsprotokolle | Fließtext |
| `{{7_2_PREISSPIEGEL_TABELLE}}` | Preisspiegel je Gewerk | HTML `<table>`: Gewerk, Bieter 1..n, Angebotssumme; Bestangebot markiert mit `class="price-best"` |
| `{{7_3_PRUEFUNG_TEXT}}` | Prüfberichte | Fließtext: Vorgehen rechnerisch/technisch/wirtschaftlich |
| `{{7_3_PRUEFUNG_TABELLE}}` | Prüfvermerke | HTML `<table>`: Gewerk, Bieter, Rechn., Techn., Wirtsch., Eignung, Gesamt |
| `{{7_4_VERHANDLUNG_TEXT}}` | Verhandlungsprotokolle | Fließtext |
| `{{7_4_VERHANDLUNG_TABELLE}}` | Verhandlungsprotokolle | HTML `<table>`: Gewerk, Bieter, Gegenstand, Ergebnis, Nachlass |
| `{{7_5_EMPFEHLUNG_TEXT}}` | Vergabevorschläge | Fließtext |
| `{{7_5_EMPFEHLUNG_TABELLE}}` | Vergabevorschläge | HTML `<table>`: Gewerk, empf. Bieter, Summe, Begründung, AG-Freigabe |
| `{{7_6_VERGABE_TEXT}}` | Zuschlagsschreiben | Fließtext |
| `{{7_6_VERGABE_TABELLE}}` | Auftragsvergaben | HTML `<table>`: Gewerk, AN, Vergabesumme netto/brutto, Zuschlagsdatum, Bauzeit |
| `{{7_7_KOSTEN_TEXT}}` | Kostenprognose | Fließtext max. 5 Sätze |
| `{{7_7_KOSTEN_TABELLE}}` | Kostenanschlag aktualisiert | HTML `<table>` KGR 100–700 |
| `{{7_7_KOSTEN_VERGLEICH}}` | Vergleich LPH 6 vs. LPH 7 | HTML `<table>`: KGR, KAS LPH 6, Vergabesumme, Δ, Δ% |
| `{{7_8_VERTRAG_TEXT}}` | Vertragsunterlagen | Fließtext |
| `{{7_8_VERTRAG_TABELLE}}` | Vertragschecklisten | HTML `<table>`: Gewerk, LV, BVB, Pläne, Fristen, Sicherheit, Unterschrift |
| `{{7_9_BAUZEIT_TEXT}}` | Bauzeitenplan | Fließtext |
| `{{7_9_BAUZEIT_TABELLE}}` | Bauzeitenplan | HTML `<table>`: Gewerk, Beginn, Ende, Vorgänger, Meilenstein |
| `{{7_10_OFFEN_TEXT}}` / `{{7_10_OFFEN_TABELLE}}` | Protokolle | Fließtext + HTML Tabelle |
| `{{ABSCHLUSS_TEXT}}`, `{{DATEILISTE}}` | Standard | Text / `<li>` |

## Stil-Vorgaben

- Fachbegriffe: VOB/A §§ 12–19, VOB/B § 2, § 16 VOB/A (Angebotswertung), BGB § 631 ff.
- Preise konsistent in netto/brutto mit MwSt-Angabe
- Bei öffentlichen Vergaben auf VgV / GWB Bezug nehmen
