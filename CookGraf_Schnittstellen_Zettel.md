# CookGraf – Schnittstellen-Zettel

*Grundlage: 9 User Stories, 3 Epics. Jeder Service hat eine feste Eingabe/Ausgabe – Teams arbeiten gegen diese Zettel, nicht gegeneinander.*

---

## 🟢 Service 1: Property-Graph-Service

**Zweck:** Kennt alle Rezepte mit Zutaten, Methoden, Geräten, Kochzeit. Beantwortet "was passt zu meinen Zutaten?".

**Genutzt in:** US1, US2, US3

| Operation | Eingabe | Ausgabe |
|---|---|---|
| Rezepte nach Zutaten finden (US1) | Liste vorhandener Zutaten | Rezeptliste, sortiert nach Matching-% |
| Fehlende Zutaten ermitteln (US2) | Rezept-ID + vorhandene Zutaten | Liste fehlender Zutaten inkl. benötigter Menge |
| Nach Kochzeit filtern (US3) | Rezeptliste + Zeitgrenze (z. B. "< 30 Min") | Gefilterte Rezeptliste |

**Macht NICHT:** schlägt keine Alternativen/Ersatz vor (→ das macht Service 2), verwaltet keine Einkaufsliste (→ Service 3).

---

## 🟠 Service 2: Knowledge-Graph-Service

**Zweck:** Kennt Beziehungen zwischen Zutaten (Geschmack, Chemie) und zwischen Geräten (Kochmethoden). Beantwortet "was kann ich stattdessen nehmen?".

**Genutzt in:** US8, US9

| Operation | Eingabe | Ausgabe |
|---|---|---|
| Zutaten-Alternative finden (US8) | 1 fehlende Zutat | Liste von Alternativen + Begründung (z. B. "ähnliches Fettprofil") – oder ehrliche Fehlmeldung, falls keine passt |
| Geräte-Alternative finden (US9) | Fehlendes Gerät + geforderte Methode | Alternativgerät + angepasste Methode/Zeit + Hinweis auf mögliche Ergebnis-Änderung |

**Macht NICHT:** kennt keine konkreten Rezepte (→ Service 1 liefert die Basis-Zutat/-Gerät, dieser Service liefert nur den Ersatz dafür).

---

## 🟣 Service 3: Einkaufslisten-Service

**Zweck:** Sammelt, verwaltet und exportiert, was noch gekauft werden muss.

**Genutzt in:** US4, US5, US6, US7

| Operation | Eingabe | Ausgabe |
|---|---|---|
| Zur Liste hinzufügen (US4) | Fehlende Zutaten (aus Service 1) | Konsolidierte Liste (Duplikate zusammengeführt, Mengen summiert) |
| Als gekauft markieren (US5) | Listeneintrag + Status "gekauft" | Aktualisierter Eintrags-Status |
| Wochenplan konsolidieren (US6) | Ausgewählte Rezepte je Tag | Zusammengeführte Liste über alle Tage (nutzt intern US4-Logik) |
| Exportieren (US7) | Fertige Liste | Exportformat (z. B. Druckansicht, Textnachricht) |

**Macht NICHT:** entscheidet nicht, was fehlt (kommt von Service 1), schlägt keine Ersatz-Zutaten vor (kommt von Service 2 – falls Nutzer eine Alternative akzeptiert, meldet Service 2 das Ergebnis an diesen Service).

---

## Grundregel für alle Teams

> Eure Story braucht eine Eingabe von einem anderen Service? Nehmt das in der Tabelle oben stehende Beispiel als gegeben an. Ihr wartet nicht auf die andere Gruppe – ihr arbeitet gegen den Zettel.
