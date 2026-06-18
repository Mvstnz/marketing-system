# Spezifikation: Marketing-System für Skincare-Freelancerin

> Interne Bau-Spezifikation. Working-Doc auf Deutsch.
> Alle *benutzerseitigen* Texte im fertigen Produkt sind **Englisch** (die Freelancerin spricht nur Englisch).
> Stand: 2026-06-18 — abgeleitet aus der Grilling-Session (Fragen F1–F23 + Bild-Verfeinerung).

---

## 1. Zweck & Kontext

Ein Assistenz-System, mit dem eine **Marketing-Freelancerin** (arbeitet für ein Skincare-Unternehmen)
markenkonforme Marketing-Inhalte mit minimaler Eingabe erstellt.

- **Werkstatt (Entwicklung):** Gerät des Auftraggebers — Claude Code (Windows)
- **Ziel-Plattform (Produktion):** Laptop der Freelancerin — **nur Codex**, **Windows**
- **Designprinzip:** so einfach wie möglich, ein Bedienpfad, plattform-neutral

---

## 2. Grundarchitektur

| Aspekt | Entscheidung | Ref |
|---|---|---|
| Form | Set aus Agent-Skills (Markdown), keine Web-App, kein Hosting | F1 |
| Einstieg | **Ein** Befehl `/marketing` → geführte Auswahl | F2 |
| Bau-Philosophie | **Orchestrierung (B)**: `/marketing` dirigiert die installierte Bibliothek | F17/F21 |
| Bibliothek | `coreyhaines31/marketingskills` (öffentlich, MIT, Codex-kompatibel) | F21 |
| Plattform | **plattform-neutral**, Codex ist Pflicht → keine Claude-Code-only-Funktionen | F21 |

### Skills im Lieferumfang (eigene)
1. `/marketing-setup` — einmaliger Aufbau des Brand Kit
2. `/marketing` — Haupt-Erstellungsfluss (orchestriert die Bibliothek)
3. `/marketing-update` — Selbstpflege des Brand Kit

---

## 3. Zwei Sprachebenen (wichtig!)

- **Bediensprache = Englisch** — alle Menüs, Fragen, Optionen, Tuning-Hinweise sprechen die Nutzerin auf Englisch an.
- **Content-Sprache = pro Kanal** (automatisch gesetzt, überschreibbar):

| Kanal | Content-Sprache |
|---|---|
| Blog | Deutsch |
| Instagram (Post / Carousel / Story) | Englisch |
| Newsletter / E-Mail / Betreffzeilen | Deutsch |
| Produktbeschreibung (Shopify) | Deutsch **+** Englisch |

> Beispiel: Das System erklärt ihr auf Englisch, dass es einen deutschen Newsletter schreibt,
> und liefert den Newsletter-Content auf Deutsch.

---

## 4. Bedienung (UX)

- **Geführte Fragen mit nummerierten Optionen** (`1) … 2) … 3) … – type a number`), Codex-tauglich. F7
  - Pflicht-Rückfragen, aber als **auswählbare Optionen** statt Freitext.
  - Optionen werden **dynamisch** aus Brand Kit + Eingabe der Nutzerin generiert.
- **Sprache automatisch pro Asset-Typ** gesetzt — wird nicht jedes Mal gefragt. F13
- **Überarbeitung (Tuning):** nach jedem Entwurf nummerierte Schnell-Optionen
  (`1) Shorter  2) Punchier  3) Different angle  4) New variant`) **plus** freies Nachtippen. F18
- **Output:** Anzeige im Chat **+** automatische Datei-Ablage als Archiv. F8

---

## 5. Fundament: Brand Kit

> **Architektur-Schwenk (F25):** Kein Produktkatalog vorab. Die Marke hat ~800 Produkte —
> niemand trägt 800 Links zusammen. Stattdessen **„Link pro Erstellung"**: Setup baut nur
> das dauerhafte Marken-Wissen (Tonfall + Zielgruppen); einzelne Produkte werden bei der
> Erstellung aus einem eingefügten Link **live geholt** (und optional in `products.md`
> als Cache gespeichert). Produkt-URLs sind die Hauptquelle; CSV/Screenshots/Text als
> Fallback. Setzt Web-Zugriff im Agenten voraus (beim Testlauf prüfen).

Aufgebaut durch `/marketing-setup`:

- **Tonfall:** **kuratierte Beispiel-Posts** (10–20 repräsentative) → abgeleitet, einmal von der Nutzerin gegengelesen. F6
- **Zielgruppen:** ein paar Stichworte → `audience.md`.
- **Produkte:** **optional** — kein Pflicht-Katalog; `products.md` ist nur ein Cache. F25

### Datei-Struktur `brand/`
```
brand/
  voice-de.md      # Tonfall Deutsch (Newsletter, Blog) – robuste Regeln, engine-unabhängig
  voice-en.md      # Tonfall Englisch (Instagram)
  products.md      # Produktkatalog aus Shopify-CSV
  audience.md      # Zielgruppen-Profile (mehrere Segmente)
  samples/         # die kuratierten Beispiel-Posts (Input fürs Voice-Kit)
```

- **Voice-Kit zweisprachig** (DE + EN), weil Tonfall sich nicht 1:1 überträgt. F13
- **Robuste Regeln** statt „klinge wie Claude" — Output kommt bei ihr aus einem OpenAI-Modell (Codex). F21
- **Keine eingebaute Compliance-/Claim-Prüfung** — rechtliche Kontrolle liegt bei der Nutzerin/dem Unternehmen. F16

---

## 6. Asset-Typen

### Eigenständige Menüpunkte (F15)
- Instagram-Post (EN)
- Instagram-Carousel (EN)
- Instagram-Story (EN)
- Newsletter (DE)
- Promo-E-Mail (DE)
- Blogpost (DE)
- Produktbeschreibung (DE + EN)
- Kampagnenidee
- Bild-Prompt (siehe §7)
- Content-Kalender (siehe §8)
- Reel / Short-Video-Skript (EN) — *nachträglich ergänzt (F24)*, liefert Dreh-Skript + Caption

**Facebook** (F24): kein eigener Typ — IG-Feed-Posts werden 1:1 als Cross-Post auf Facebook
genutzt; der IG-Post-Output enthält einen entsprechenden Hinweis.

**Content-Kalender** nutzt den realen Wochen-Rhythmus der Marke als Standard-Schablone
(Mo Story · Di Blog+Educational/Carousel · Mi Product+Newsletter · Do Reel · Fr Blog+Promo;
Stories Mo–Fr).

### Automatische Folge-Aktionen (kein eigener Menüpunkt) (F15)
- **A/B-Varianten** — angeboten nach jedem Asset
- **Betreffzeilen** (mehrere) — angeboten nach E-Mail/Newsletter

---

## 7. Bild-Prompt-Schmied (Sonderfall)

Kein API-Zugang, keine Kosten — das System ist reiner **Prompt-Schmied**. F9–F11

- **Input:** echtes Produktfoto (liefert sie immer mit) + Stichworte.
- **Frage:** `Generate in → 1) Nano Banana  2) ChatGPT` → liefert einen **tool-optimierten Edit-Prompt**
  (die Tools reagieren unterschiedlich auf Prompt-Stil). F-Bild
- **Canva-Finishing-Hinweise:** was danach in Canva ergänzt wird (Textoverlay, Logo, IG-Format/Crop);
  der Prompt **lässt bewusst Raum** dafür (z. B. „negative space oben für Text").
- Sie führt den Prompt selbst in ihrer App aus (Nano Banana / ChatGPT), Nachbearbeitung in Canva.

---

## 8. Content-Kalender (Sonderfall)

- **Plan/Überblick als Tabelle** (kein fertiger Content auf einmal). F12
- Plan wird im Datei-Archiv abgelegt.
- **Brücke:** einzelne Einträge füttern später den normalen `/marketing`-Fluss als Kontext
  („erstell mir Punkt 3 aus dem Kalender").

---

## 9. Wartung

- `/marketing-update` — Selbstpflege: neue Shopify-CSV einwerfen → Produktkatalog aktualisiert;
  neue Top-Posts ergänzen → Voice nachgeschärft. F19
- **Inline-Korrektur:** fällt im Arbeiten etwas auf („Produkt fehlt / Ton stimmt nicht"),
  kann sie es im Fluss korrigieren → System schreibt zurück ins Brand Kit. F19
- Macht die Nutzerin unabhängig vom Entwickler.

---

## 10. Deployment

- **Auslieferung:** **ein GitHub-Repo (C)** mit allem (eigene Skills + Brand-Kit-Gerüst + Auto-Setup). F22
- **Bibliothek-Install:** `npx skills add coreyhaines31/marketingskills` (ein Befehl). F21
- **Ziel:** Windows-Laptop, **nur Codex**, Nutzerin technisch unerfahren. F23
- **Installations-Anleitung auf Englisch**, wasserdicht, Schritt für Schritt. F23
  - **Node-Check zuerst:** läuft Codex schon, ist Node.js wahrscheinlich bereits da
    (Codex CLI ist ein npm-Paket) → schwierigster Schritt entfällt evtl.
- **Updates später:** `git pull`.

### Install-Sequenz (Ziel-Ablauf für die Nutzerin)
1. Node.js prüfen / ggf. installieren
2. Repo klonen
3. `/marketing-setup` starten (zieht Bibliothek via `npx` nach, legt Brand-Kit-Gerüst an)
4. Daten einspeisen (CSV + Beispiel-Posts), Voice-Kit gegenlesen

---

## 11. Bau-Reihenfolge (MVP zuerst, F20)

1. **Repo-Gerüst + `/marketing-setup` + Brand-Kit-Vorlagen**
2. **IG-Post (EN) + Newsletter (DE)** — testet das zweisprachige Konzept sofort
3. **Bild-Prompt-Schmied**
4. **Restliche Asset-Typen** (folgen alle derselben Schablone)
5. **Englische Windows-Installations-Anleitung**

---

## 12. Benötigte Echtdaten (für Testlauf bei der Entwicklung)

Nicht zum Bauen nötig — erst für den ersten `/marketing-setup`-Testlauf:
- 📦 Shopify-Produkt-CSV (Products → Export)
- 📸 10–20 typische IG-Captions (Englisch)
- ✉️ 2–3 Newsletter/E-Mails (Deutsch)
- 📝 1–2 Blogposts (Deutsch), falls vorhanden
- 👥 Stichworte zur Zielgruppe (wer kauft, Alter, Hautanliegen)

---

## 13. Bewusst NICHT im Scope

- Keine weiteren Kanäle (kein TikTok/Pinterest/Facebook/Ads/Amazon). F14
- Keine echte Bild-API / Bildgenerierung im System (nur Prompts). F9–11
- Keine Direkt-Postings in Tools (Instagram-Scheduler, Mailchimp …). F8
- Keine eingebaute Compliance-/Rechtsprüfung. F16
- Keine echte Mehrsprachigkeit über die Kanal-Matrix hinaus. F13
