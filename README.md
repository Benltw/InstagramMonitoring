# Instagram-Monitoring · Bundestagsfraktionen

Tägliches, öffentlich zugängliches Monitoring der Instagram-Aktivität aller
MdB-Accounts der fünf Bundestagsfraktionen (AfD, CDU/CSU, SPD, Grüne, Linke).

ausschließlich für den internen Gebrauch.

## Inhalt

Diese GitHub-Pages-Site zeigt die aktuelle Tagesgalerie mit:

- **Summary Statistics** — Posts, Bild/Video/Sidecar, Likes, Kommentare, Views pro Fraktion
- **Interaktive Galerie** mit allen 433 Posts als Instagram-Embeds
- **Filter** nach Fraktion und nach Themenkategorie (14 Kategorien, z. B. Attestpflicht/Gesundheit, Wohnen/Miete, Merz-Kritik/CDU)
- **Sortierung** nach Likes, Relevanz-Score, Kommentaren, Views

Design nach dem offiziellen [CDU Corporate Design Manual (Stand: September 2023)](https://www.cdu.de/):
Cadenabbia-Türkis, Rhöndorf-Blau, Union-Gold, Bogen in Schwarz-Rot-Gold,
Inter Extrabold und IBM Plex Serif als Hausschriften.

## Deployment (GitHub Pages)

1. **Repository anlegen** — z. B. `fraktions-briefing` (privat empfohlen, da vertraulich).
2. **Diesen Ordner (`deploy/`) hochladen** — die Datei `index.html` ist das Deployment-Artefakt.
3. **GitHub Pages aktivieren** — Settings → Pages → Branch `main`, Folder `/` (root) oder `/docs`.
4. **URL abrufen** — verfügbar unter `https://<user>.github.io/<repo>/`.

Alternativ als einfache statische Site auf Vercel/Netlify:
`vercel deploy` bzw. Drag&Drop auf netlify.com.

### Empfohlene Repository-Struktur

```
fraktions-briefing/
├── index.html            # aktuelle Tagesgalerie
├── README.md
├── .nojekyll             # unterdrückt Jekyll-Rendering auf GitHub Pages
├── .gitignore
└── archive/              # optional: ältere Tagesausgaben
    ├── 2026-07-01.html
    ├── 2026-07-02.html
    └── ...
```

## Datenquelle

Instagram-Posts werden täglich um 07:00 Uhr über den Apify-Actor
`apify/instagram-post-scraper` gescrapt. Die Rohdaten werden gefiltert
(nur Posts des Vortags), dedupliziert und in `filtered_all.json` konsolidiert.
Aus diesen Rohdaten baut das Python-Skript `build_full_gallery.py` das
statische HTML — kein Backend, keine Datenbank, keine Cookies.

Der Scrape läuft als geplante Aufgabe im Cowork-Setup; das Ergebnis wird
manuell in dieses Repo committed und deployed.

## Sicherheit & Datenschutz

- Alle Instagram-Embeds werden **direkt vom Nutzer-Browser** von instagram.com nachgeladen.
  Der GitHub-Pages-Server liefert nur die HTML-Datei aus, keine Nutzerdaten.
- Diese Site setzt selbst **keine Cookies**. Instagram kann per Embed Cookies setzen
  (siehe Meta/Instagram-Datenschutzerklärung).
- Google Fonts (`Inter`, `IBM Plex Serif`) werden per `<link>` von Google geladen.
  Für DSGVO-konformen Betrieb siehe Hinweise im CDU Corporate Design Manual (4.1/4.2)
  bzw. Fonts lokal in `/fonts/` einbinden.
- **Meta-Tag `robots: noindex,nofollow`** ist gesetzt — die Seite wird von Suchmaschinen
  nicht indexiert. Ergänzend bitte GitHub-Pages-Zugriff über einen privaten Repo-Access
  absichern oder hinter Basic Auth (z. B. via Cloudflare Access) stellen.



## Kontakt

CDU Deutschlands · Bundesgeschäftsstelle
