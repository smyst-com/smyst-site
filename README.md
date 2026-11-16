# smyst-site
Auslieferung der Website smyst.com (kein Quellcode)

## Was ist das?
Dieses Projekt enthält **keinen Quellcode**. Es liefert nur die fertige Website aus.
Das private Projekt `smyst-app` baut die Website und legt sie als Paket im Speicher
IDrive e2 ab (Bucket `smyst-site-releases`, Datei `site/current.tar.zst`).
Der Ablauf `.github/workflows/deliver.yml` holt dieses Paket, prüft es und stellt es
über GitHub Pages auf smyst.com.

- Alle 30 Minuten wird nur **verglichen**: neues Paket in e2 oder schon live?
- **Automatisch ausgeliefert** wird nur, wenn die Repo-Variable
  `SMYST_SITE_AUTO_DEPLOY` auf `true` steht (Standard: aus).
- **Von Hand:** Actions → „Auslieferung smyst.com“ → „Run workflow“ → `deploy` anhaken.
  Ohne Haken wird nur geprüft und nichts verändert.
- Vor dem Ausliefern werden Prüfsumme, `index.html`, `404.html`, `CNAME`, `release.json`,
  Dateianzahl und Größe geprüft. Danach ein kurzer Test der Live-Seite.
- Solange die Pages-Quelle auf „Deploy from a branch“ (main) steht, liefert der Ablauf
  **nichts** aus – dann bleibt die Wartungsseite (`index.html` in diesem Zweig) live.

## Rückweg
1. Zuerst `SMYST_SITE_AUTO_DEPLOY` auf `false` stellen (sonst kommt der neue Stand
   beim nächsten Zeitplan-Lauf wieder).
2. Actions → „Auslieferung smyst.com“ → „Run workflow“ → `deploy` anhaken,
   `slot` = `previous` → liefert den vorherigen Stand aus.
3. Notfall: Settings → Pages → Source auf „Deploy from a branch“, Zweig `main`, Ordner `/ (root)`
   → die Wartungsseite aus diesem Zweig ist wieder live.
