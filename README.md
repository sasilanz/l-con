# l-con.ch

Schlanke Visitenkarte der l-con GmbH, gehostet auf GitHub Pages.

- `index.html`: die ganze Seite (Deutsch und Englisch, Umschaltung über `#en` / `#de`, ohne JavaScript)
- `static/css/style.css`: Stil, angelehnt an [dieti-it.ch](https://github.com/sasilanz/dieti-it-support)
- `ZIEL.md`: Planung und Ablauf des Umzugs

## Lokal anschauen

```sh
python3 -m http.server 8000
```
Dann im Browser <http://localhost:8000> öffnen. Die englische Version ist unter <http://localhost:8000/#en> erreichbar.

## Veröffentlichen

Jeder Push auf `main` wird automatisch von GitHub Pages veröffentlicht.
