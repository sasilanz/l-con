# l-con.ch – Zieldokument

*Stand: 2026-09-28 · Status: Seite live auf l-con.ch (GitHub Pages), Mail über Proton. Offen: `www`, Aufräumen nach Ablauf von `mobosupe` am 5.10.2026.*

## 1. Ziel

- **Hosting-Kosten senken:** Das Hostpoint-Hosting-Paket `mobosupe` wird gekündigt. Bei Hostpoint bleiben nur die Domain-Registrierungen.
- **l-con.ch wird eine schlanke Visitenkarte der l-con GmbH (Variante A):** Die GmbH ist im Handelsregister eingetragen, aber inaktiv. Die Seite zeigt, wer die Firma ist, und verweist auf das aktive Angebot unter **dieti-it.ch**.
- **Hosting gratis auf GitHub Pages**, gleich aufgebaut wie dieti-it.ch und astridkreativ.ch.
- **Mail `info@l-con.ch` zieht zu Proton** (Proton Unlimited ist vorhanden, dieti-it.ch läuft schon dort).

## 2. Ist-Zustand

| Domain | Registriert bei | Web | Mail |
|---|---|---|---|
| l-con.ch | Hostpoint | Hostpoint (`mobosupe`), 217.26.52.218 | Hostpoint **+ SimpleLogin gemischt** (Überbleibsel) |
| dieti-it.ch | Hostpoint | GitHub Pages ✔ | Proton ✔ |
| astridkreativ.ch | Hostpoint | GitHub Pages ✔ (nur zum Anschauen) | keine |
| asiarch.net | Hostpoint | – | – |

Die DNS-Zonen aller Domains werden bei Hostpoint verwaltet (`ns*.hostpoint.ch`).

**Folgerung:** l-con.ch ist das Letzte, was `mobosupe` noch wirklich nutzt.

## 3. Soll-Zustand

| Domain | Web | Mail |
|---|---|---|
| l-con.ch | GitHub Pages (Repo `sasilanz/l-con`, public) | Proton, nur `info@l-con.ch` |

- `astrid@l-con.ch` fällt weg.
- SimpleLogin wird für l-con.ch entfernt.
- `mobosupe` wird gekündigt.

## 4. Die Webseite

### Inhalt (Deutsch und Englisch)
1. **Kopf:** l-con GmbH, eine Zeile, worum es geht
2. **Kurztext:** Die Firma ist eingetragen, das aktuelle Angebot läuft über IT-Support Dietikon, mit Link zu dieti-it.ch
3. **Kontakt:** `mailto:info@l-con.ch` (kein Formular)
4. **Impressum:** Firmenname (l-con GmbH), Adresse, UID
5. **Datenschutz-Kurzhinweis:** keine Cookies, kein Tracking, kein Formular. Hinweis, dass GitHub Pages als Hoster technische Zugriffsdaten (IP-Adresse) protokolliert.

**Fällt weg (bestätigt):** Kontaktformular, Portfolio-PDF, CS50-Zertifikat, Bankdaten (IBAN), alte Dienstleistungs-Beschreibungen. Die Beschreibung wird neu formuliert, zuerst mit einem Platzhaltertext.

### Technik
- **Eine Datei `index.html`** mit CSS in `static/css/style.css` (wie bei dieti-it-support). Kein Framework, kein Build-Schritt.
- **Zweisprachig ohne JavaScript:** Deutsch ist die Standardsprache, ein Link „EN“ schaltet auf Englisch um (Anker-Link). Die Details legen wir beim Bauen fest.
- **Design angelehnt an dieti-it.ch:** Vorlage ist das Repo [`sasilanz/dieti-it-support`](https://github.com/sasilanz/dieti-it-support) (`index.html` und `static/css/landing.css`). Gleicher Verlauf im Kopfbereich (`#2575fc` → `#6a29ae`), gleiche Akzentfarbe `#6a29ae`, gleicher schlichter Aufbau. Man soll sehen, dass beide Seiten zusammengehören.
- Die Seite muss auf dem Handy gut lesbar sein.

### Repo-Struktur
```
l-con/
├── index.html      # die Seite
├── static/css/style.css   # gleiche Struktur wie dieti-it-support
├── favicon.svg     # optional
├── CNAME           # enthält: l-con.ch
├── README.md       # kurz: was, wie deployen
├── ZIEL.md         # dieses Dokument
└── ziel.md         # ursprüngliche Notiz
```
Deployment: GitHub Pages aus Branch `main`, Ordner `/`.

## 5. DNS (bei Hostpoint)

### Web, wie bei dieti-it.ch
| Name | Typ | Wert |
|---|---|---|
| `l-con.ch` | A | 185.199.108.153 · 185.199.109.153 · 185.199.110.153 · 185.199.111.153 |
| `www` | CNAME | `sasilanz.github.io.` |

Die alte A-Adresse 217.26.52.218 fällt weg. Danach in GitHub „Enforce HTTPS“ aktivieren. Empfohlen: die Domain im GitHub-Konto verifizieren, damit sie niemand anders für eine eigene Pages-Seite übernehmen kann.

### Mail, wie bei dieti-it.ch
Proton zeigt die genauen Werte beim Hinzufügen der Domain an:
- TXT-Eintrag zur Verifizierung bei Proton
- MX: `mail.protonmail.ch` (10), `mailsec.protonmail.ch` (20)
- SPF (TXT): `v=spf1 include:_spf.protonmail.ch ~all`
- DKIM: 3 CNAME-Einträge von Proton
- DMARC (TXT `_dmarc`)
- **Entfernen:** die MX-Einträge von Hostpoint und SimpleLogin sowie alte SPF- und DKIM-Einträge von Hostpoint und SimpleLogin

## 6. Reihenfolge der Umstellung

Die Seite und die Mail sollen nie gleichzeitig ausfallen. Alle Schritte lassen sich einzeln rückgängig machen, bis in Schritt 6 gekündigt wird.

0. **Sichern:**
   - Mails aus `info@` und `astrid@` anschauen, aufräumen und bei Bedarf exportieren (per IMAP, z. B. mit Thunderbird, oder mit dem Proton Import Assistant)
   - Webspace und Datenbanken von `mobosupe` prüfen, ob noch etwas gebraucht wird
   - Impressums-Angaben von der alten Seite notieren
1. **Repo:** den lokalen Ordner mit `git init` anlegen, mit `git@github.com:sasilanz/l-con.git` verbinden, ersten Commit pushen
2. **Seite bauen** und lokal im Browser testen
3. **GitHub Pages aktivieren**, zuerst ohne eigene Domain testen (`sasilanz.github.io/l-con`)
4. **Mail zu Proton:** Domain in Proton hinzufügen, `info@l-con.ch` anlegen, DNS-Einträge setzen, Senden und Empfangen testen. Das Hostpoint-Postfach bleibt vorerst bestehen, als Sicherheitsnetz.
5. **Web umstellen:** `CNAME`-Datei ins Repo, DNS-Einträge setzen, HTTPS aktivieren, testen (mit und ohne www, http und https)
6. **Beobachten, ca. 1–2 Wochen,** dann **`mobosupe` kündigen.** Vorher bei Hostpoint abklären:
   - Bleiben die DNS-Zonen aller Domains verwaltbar, wenn das Hosting-Paket weg ist?
   - astridkreativ.ch ist im Panel noch `mobosupe` zugeordnet (Web und Mail). Das ist falsch: Die Domain braucht nur DNS von Hostpoint. **Astrid löst die Zuordnung vor der Kündigung.**
7. **Aufräumen:** die Domain aus dem SimpleLogin-Konto entfernen, alte Einträge löschen, dieses Dokument abschliessen

## 7. Kosten

| | Vorher | Nachher |
|---|---|---|
| Hosting `mobosupe` | ca. CHF 250 / Jahr | 0 |
| Domains (Hostpoint) | unverändert | unverändert |
| Proton Unlimited | schon vorhanden | schon vorhanden |
| GitHub Pages | – | 0 |

## 8. Risiken

| Risiko | Gegenmassnahme |
|---|---|
| Mails gehen während der Umstellung verloren | MX erst umstellen, wenn Proton verifiziert ist. Hostpoint-Postfach bis Schritt 6 behalten. |
| Die Kündigung von `mobosupe` betrifft die DNS-Zonen | Vor der Kündigung bei Hostpoint nachfragen (Schritt 6) |
| HTTPS-Zertifikat kommt nicht | Braucht nach der DNS-Umstellung etwas Zeit. Bei Problemen die Custom Domain in GitHub entfernen und neu eintragen. |
| Die Seite erfüllt die Pflichtangaben nicht | Impressum mit vollständigen Firmendaten, dazu Datenschutz-Kurzhinweis |

## 9. Offene Punkte

- [x] Impressum-Umfang: Firmenname (l-con GmbH), Adresse, UID
- [x] Impressum-Werte eintragen (von der alten Seite: Krokusstrasse 8, 8953 Dietikon, CHE-472.791.905). Auf uid.admin.ch gegenprüfen.
- [x] Kurztext Deutsch und Englisch (Variante 2)
- [x] Downloads, Bankdaten und alte Service-Liste fallen weg
- [x] Entscheidung: DNS bleibt bei Hostpoint (kein Cloudflare). Domain state wird **nicht** manuell umgestellt (Redirect/Parking würden vermutlich eigene A-Einträge setzen, Disable löscht die Zone).
- [x] `mobosupe` gekündigt (läuft am **5.10.2026** aus)
- [ ] Antwort vom Hostpoint-Support abwarten (Anfrage vom 28.9.2026: Domain state, DNS nach Ablauf, www-CNAME). „Parking“ wird bei eigenen A-Einträgen abgelehnt („Conflicting IP addresses found“).
- [ ] Nach dem 5.10.: Zonen von l-con.ch und astridkreativ.ch mit den Sicherungen vergleichen (`~/dev/l-con.ch.txt`, `~/dev/astridkreativ.ch.txt`, Stand 28.9.2026)
- [x] `www.l-con.ch` als CNAME → `sasilanz.github.io` angelegt (28.9.2026). Hostpoint hat das blockiert, bis alles aus `mobosupe` entfernt war:
  1. Website-Alias `www.l-con.ch` gelöscht
  2. Die alte „Sites“-Webseite auf `mobosupe.myhostpoint.ch` umgehängt und dann gelöscht
  3. Die Mail-Konten `info@` und `astrid@` bei Hostpoint gelöscht
  4. Die separat angelegte Subdomain `www.l-con.ch` gelöscht, das war der eigentliche Blocker
  Danach liess sich der CNAME anlegen. Um das Zertifikat für `www` auszulösen, wurde die Custom Domain in GitHub einmal entfernt und neu gesetzt.
- [ ] Nach dem 5.10.: prüfen, ob der automatisch angelegte Wildcard-MX `*.l-con.ch → mail.protonmail.ch` verschwunden ist, sonst löschen
- [x] HTTPS für l-con.ch erzwungen (Let's Encrypt, wird automatisch verlängert). Für `www` stellt GitHub das Zertifikat aus, sobald der CNAME steht.
- [ ] DKIM: In Proton prüfen, ob der Reiter grün ist, und eine Test-Mail auf `dkim=pass` prüfen
- [x] Kosten `mobosupe`: ca. CHF 250 / Jahr, fallen ab 5.10.2026 weg
- [x] Vorlage für das Design: `sasilanz/dieti-it-support`
