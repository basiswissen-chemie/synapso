# Synapso für iPhone / iPad (kostenlos, ohne App Store)

Apple erlaubt keine freie App-Installation wie Android. Der kostenlose Weg ist
eine **PWA**: Die App wird einmal ins Web gestellt und von den Nutzern in
**Safari** über „Zum Home-Bildschirm" wie eine App abgelegt. Sie läuft danach
im Vollbild und – nach dem ersten Laden – **offline**.

## Inhalt dieses Ordners

```
Synapso-PWA/
  index.html              ← Startseite, verlinkt beide Varianten
  synapso/                ← Variante MIT Startsätzen
    index.html, manifest.webmanifest, sw.js, icon-180/192/512.png
  synapso-ohne/           ← Variante OHNE Startsätze
    index.html, manifest.webmanifest, sw.js, icon-180/192/512.png
```

Beide Varianten sind eigenständig und funktionieren auch einzeln.

---

## Schritt 1 – Online stellen (eine der beiden Optionen)

### Option A: Netlify (am schnellsten, ohne Konto-Gefummel)

1. Auf <https://app.netlify.com/drop> gehen.
2. Den **ganzen Ordner `Synapso-PWA`** in das Browserfenster ziehen.
3. Netlify vergibt sofort eine HTTPS-Adresse, z. B.
   `https://zufallsname.netlify.app/`.
   - Startseite: `…netlify.app/`
   - Nur „mit": `…netlify.app/synapso/`
   - Nur „ohne": `…netlify.app/synapso-ohne/`

> Kostenloses Netlify-Konto erlaubt, die Seite dauerhaft zu behalten und einen
> hübscheren Namen zu vergeben.

### Option B: GitHub Pages (dauerhaft, kostenlos)

1. GitHub-Konto anlegen (falls nicht vorhanden): <https://github.com>.
2. Neues **Repository** erstellen, z. B. `synapso`.
3. Den Inhalt von `Synapso-PWA` hochladen (Weboberfläche: „Add file →
   Upload files", Ordner per Drag&Drop).
4. Im Repository **Settings → Pages**: Branch `main`, Ordner `/ (root)`,
   speichern.
5. Nach 1–2 Minuten ist die Seite erreichbar unter
   `https://DEIN-NAME.github.io/synapso/`
   - „mit": `…/synapso/synapso/`
   - „ohne": `…/synapso/synapso-ohne/`

**Wichtig:** Die Adresse muss mit **https://** beginnen – sonst funktioniert die
„App"-Installation und der Offline-Modus nicht. (Beide Optionen liefern HTTPS.)

---

## Schritt 2 – Auf dem iPad/iPhone als App ablegen

1. Den Link in **Safari** öffnen (nicht Chrome/Firefox – nur Safari kann das).
2. Variante antippen (oder direkt die Variantenadresse öffnen).
3. Unten/oben auf das **Teilen-Symbol** (Quadrat mit Pfeil nach oben) tippen.
4. **„Zum Home-Bildschirm"** wählen → **„Hinzufügen"**.
5. Es erscheint das **Synapso-Icon** auf dem Home-Bildschirm. Beim Start läuft
   die App im Vollbild.

Diesen Schritt macht jede Nutzerin / jeder Nutzer einmal pro Gerät.

---

## Wichtig: Lernfortschritt sichern

Der Fortschritt wird wie im Browser lokal gespeichert (`localStorage`).
**iOS-Safari kann diese Daten löschen**, wenn die App länger nicht benutzt wird.
Deshalb:

- Regelmäßig über **„Exportieren"** ein JSON-Backup erstellen (landet bei iOS in
  „Dateien" / kann geteilt werden).
- Nach Bedarf über **„Importieren"** wiederherstellen.

Das ist kein Fehler der App, sondern eine Einschränkung von iOS für
Web-Apps.

---

## App aktualisieren

Neue HTML einspielen: die jeweilige `synapso/index.html` bzw.
`synapso-ohne/index.html` ersetzen und erneut hochladen. Damit die Geräte die
neue Version laden, in der zugehörigen `sw.js` die Zeile
`const CACHE = 'synapso-mit-v1';` (bzw. `…-ohne-v1`) auf eine neue Nummer
erhöhen (z. B. `-v2`). Beim nächsten Start mit Internet aktualisiert sich die
App dann automatisch.
