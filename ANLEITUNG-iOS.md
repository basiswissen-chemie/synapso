# Synapso für iPhone / iPad (kostenlos, ohne App Store)

Apple erlaubt keine freie App-Installation wie Android. Der kostenlose Weg ist
eine **PWA**: Die App wird einmal ins Web gestellt und von den Nutzern in
**Safari** über „Zum Home-Bildschirm“ wie eine App abgelegt. Sie läuft danach
im Vollbild und – nach dem ersten Laden – **offline**.

> **Stand:** 10.09.2026, App-Version **1.4** – entspricht
> `..\Working\Synapso_ohne_Startsätze.html` (Cache-Name `synapso-v1.4-2`).
> Es gibt nur noch **eine** Variante (ohne eingebaute Startsätze); Kartensätze
> werden separat als JSON-Dateien zum Import bereitgestellt.

## Inhalt dieses Ordners

```
Synapso-PWA/
  index.html              ← Startseite, verlinkt die App
  synapso/                ← die App
    index.html, manifest.webmanifest, sw.js, icon-180/192/512.png
```

Die frühere Variante „mit Startsätzen“ (alter Inhalt von `synapso/`) und die
alte Fassung „ohne“ (`synapso-ohne/`) liegen unter
`..\Archiv - Version mit Startsatz\`.

---

## Schritt 1 – Online stellen (eine der beiden Optionen)

### Option A: Netlify (am schnellsten, ohne Konto-Gefummel)

1. Auf <https://app.netlify.com/drop> gehen.
2. Den **ganzen Ordner `Synapso-PWA`** in das Browserfenster ziehen.
3. Netlify vergibt sofort eine HTTPS-Adresse, z. B.
   `https://zufallsname.netlify.app/`.
   - Startseite: `…netlify.app/`
   - App direkt: `…netlify.app/synapso/`

> Kostenloses Netlify-Konto erlaubt, die Seite dauerhaft zu behalten und einen
> hübscheren Namen zu vergeben.

### Option B: GitHub Pages (dauerhaft, kostenlos)

1. GitHub-Konto anlegen (falls nicht vorhanden): <https://github.com>.
2. Neues **Repository** erstellen, z. B. `synapso`.
3. Den Inhalt von `Synapso-PWA` hochladen (Weboberfläche: „Add file →
   Upload files“, Ordner per Drag&Drop).
4. Im Repository **Settings → Pages**: Branch `main`, Ordner `/ (root)`,
   speichern.
5. Nach 1–2 Minuten ist die Seite erreichbar unter
   `https://DEIN-NAME.github.io/synapso/`
   - App direkt: `…/synapso/synapso/`

**Wichtig:** Die Adresse muss mit **https://** beginnen – sonst funktioniert die
„App“-Installation und der Offline-Modus nicht. (Beide Optionen liefern HTTPS.)

**Beim Umstellen auf eine Variante:** Den Ordner `synapso-ohne/` auf dem Server
**löschen** (GitHub: Ordner im Repository entfernen), damit dort nur noch
`index.html` und `synapso/` liegen.

---

## Schritt 2 – Auf dem iPad/iPhone als App ablegen

1. Den Link in **Safari** öffnen (nicht Chrome/Firefox – nur Safari kann das).
2. Auf der Startseite „Synapso“ antippen (oder direkt die App-Adresse öffnen).
3. Unten/oben auf das **Teilen-Symbol** (Quadrat mit Pfeil nach oben) tippen.
4. **„Zum Home-Bildschirm“** wählen → **„Hinzufügen“**.
5. Es erscheint das **Synapso-Icon** auf dem Home-Bildschirm. Beim Start läuft
   die App im Vollbild.

Diesen Schritt macht jede Nutzerin / jeder Nutzer einmal pro Gerät.

### Bestehende Installationen

- Wer die frühere Variante **„Synapso“** (mit Startsätzen) unter `…/synapso/`
  installiert hat, bekommt beim nächsten Start mit Internet automatisch die
  neue Fassung. Karten und Lernstand bleiben erhalten (bereits geladene
  Startsatz-Karten bleiben als normale Karten in der Sammlung).
- Wer **„Synapso o. S.“** unter `…/synapso-ohne/` installiert hat, behält eine
  funktionierende, aber nicht mehr aktualisierbare App. Umstieg: in der alten
  App **„Karten → Exportieren → Alles inkl. Lernstand“**, dann die neue App
  von der Startseite hinzufügen, dort importieren und die alte vom
  Home-Bildschirm löschen. (iOS gibt jeder Home-Bildschirm-App einen eigenen
  Speicher – deshalb der Umweg über Export/Import.)

---

## Wichtig: Lernfortschritt sichern

Der Fortschritt wird wie im Browser lokal gespeichert (`localStorage`).
**iOS-Safari kann diese Daten löschen**, wenn die App länger nicht benutzt wird.
Deshalb:

- Regelmäßig über **„Karten“ → Exportieren → „Alles inkl. Lernstand“** ein
  JSON-Backup erstellen (landet bei iOS in „Dateien“ / kann geteilt werden).
- Nach Bedarf über **„Importieren“ → „Datei auswählen …“** wiederherstellen.

Das ist kein Fehler der App, sondern eine Einschränkung von iOS für
Web-Apps.

---

## App aktualisieren

**Achtung – nicht einfach die Datei aus `Working\` darüberkopieren.** Die
`synapso/index.html` hier ist die App-HTML **plus einem PWA-Kopfblock** (Zeilen
6–20: `theme-color`, `manifest`, Apple-Metas und die Registrierung des Service
Workers). Ohne diesen Block gibt es kein Home-Bildschirm-Symbol und keinen
Offline-Betrieb.

Richtiges Vorgehen:

1. Die neue App-HTML aus `..\Working\Synapso_ohne_Startsätze.html` nehmen.
2. Den PWA-Kopfblock direkt **nach** der `viewport`-Zeile wieder einsetzen –
   am einfachsten aus der bisherigen `synapso/index.html` herauskopieren
   (`apple-mobile-web-app-title` ist `Synapso`).
3. In `synapso/sw.js` den Cache-Namen ändern, Schema
   `synapso-v<App-Version>-<Upload-Nr.>`: z. B. `synapso-v1.4-3` beim nächsten
   Hochladen derselben App-Version, `synapso-v1.5-1` bei einer neuen. **Ohne
   diese Änderung behalten bereits installierte PWAs dauerhaft die alte
   Fassung**, denn der Service Worker liefert zuerst aus dem Cache.
4. Alles neu hochladen. Beim nächsten Start mit Internet aktualisiert sich die
   App dann automatisch.
