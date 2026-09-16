# IST-Aufnahme der Anwendungen – Neuhaus Wohn- und Pflegezentrum Wängi

Instrument zur IST-Aufnahme der Anwendungslandschaft, zugeschnitten auf ein Wohn- und
Pflegezentrum. Trägerin: Stiftung Neuhaus, Wängi.

Die Anwendung läuft vollständig im Browser. Es gibt keinen Server, keine Datenbank und
keine Anmeldung.

---

## Inhalt dieses Ordners

| Datei | Zweck |
|---|---|
| `index.html` | Die Anwendung. Enthält Katalog, Oberfläche und Synchronisation in einer einzigen Datei. |
| `.nojekyll` | Leere Datei. Verhindert, dass GitHub Pages die Dateien durch Jekyll verarbeitet. |

**Diese Datei (`README.md`) ist optional.** GitHub Pages würde sie als Startseite verwenden,
wenn keine `index.html` vorhanden wäre. Da `index.html` existiert, hat sie Vorrang — die
README wird nur im Repository angezeigt, nicht als Website.

---

## Erste Veröffentlichung

### 1. Repository anlegen

Auf GitHub ein neues Repository anlegen, zum Beispiel `ist-aufnahme-neuhaus`.

Bei einem kostenlosen Konto **muss das Repository öffentlich sein** — GitHub Pages lässt sich
am Gratis-Konto nur aus öffentlichen Repositories veröffentlichen. Private Repositories sind
zwar unbegrenzt kostenlos, aber ohne Pages.

> **Wichtig:** Diese Seite ist anschliessend öffentlich im Internet erreichbar, auch wenn das
> Repository privat wäre. Deshalb enthält die Anwendung **keine** echten Bewohner-, Personal-
> oder Vertragsdaten und **kein** Zugangstoken. Das ist Absicht und muss so bleiben.

### 2. Dateien hochladen

`index.html` und `.nojekyll` ins **Hauptverzeichnis** des Repositories legen.

Zu beachten:

- Der Dateiname muss **exakt klein** geschrieben sein: `index.html`. `Index.html` funktioniert nicht.
- Beide Dateien gehören auf die oberste Ebene, nicht in einen Unterordner.
- Die versteckte Datei `.nojekyll` wird von GitHub akzeptiert; beim Hochladen über die
  Weboberfläche einfach als Dateinamen `​.nojekyll` eingeben.

### 3. GitHub Pages einschalten

1. Im Repository auf **Settings**
2. Im Seitenmenü auf **Pages**
3. Unter *Build and deployment* → *Source*: **Deploy from a branch**
4. Branch **main**, Ordner **/(root)** wählen
5. **Save** klicken

### 4. Adresse

Nach etwa einer Minute bis zu zehn Minuten ist die Seite erreichbar unter:

```
https://<benutzername>.github.io/<repository-name>/
```

Den Link finden Sie jederzeit unter *Settings → Pages → Visit site*.

---

## Einrichtung der Synchronisation

Die Synchronisation legt jeden Erfassungsbogen als JSON-Datei in einem Repository ab. Jede
Speicherung wird dort zu einem Commit mit Verlauf und Wiederherstellung.

### Zuerst ohne Konto ausprobieren

In der Anwendung den Reiter **Synchronisation** öffnen und das Häkchen bei
**Demo-Modus (ohne GitHub-Konto erlebbar)** setzen. Dann **Verbindung prüfen**,
**Jetzt synchronisieren**, **Selbsttest** und **Konflikt erzeugen (Demo)** ausprobieren.
Alles verhält sich wie im Echtbetrieb, der Speicher liegt aber nur im Browser.

### Dann auf GitHub umstellen

**a) Daten-Repository anlegen** — ein **zweites, privates** Repository, nur für Daten.
Nicht dasselbe Repository wie die App, sonst wären die Erfassungsbögen öffentlich abrufbar.

**b) Token erzeugen**

GitHub → *Settings* (des eigenen Kontos) → *Developer settings* → *Personal access tokens*
→ *Fine-grained tokens* → *Generate new token*:

| Einstellung | Wert |
|---|---|
| Repository access | **Only select repositories** → das Daten-Repository |
| Permissions → Repository permissions → **Contents** | **Read and write** |
| Expiration | nach Wahl, zum Beispiel 90 Tage |

Nichts anderes aktivieren. Das Token gilt dann für genau ein Repository.

**c) In der Anwendung eintragen**

| Feld | Beispielwert |
|---|---|
| Eigentümer | `stiftung-neuhaus` |
| Repository (Daten) | `ist-aufnahme-daten` |
| Datenordner | `daten` |
| Branch | `main` |
| API-Adresse | `https://api.github.com` |
| Token | das eben erzeugte Token |

Danach **Verbindung prüfen**. Meldet die App *«Verbindung steht»*, ist alles bereit.

**d) Demo-Häkchen entfernen**, damit gegen GitHub gearbeitet wird.

---

## Für die zweite Person

Die Verbindungsdaten stehen **nicht** in der Datei, sondern im Browser-Speicher. Das heisst:

- Eigentümer, Repository, Ordner, Branch und API-Adresse sind bei jeder Person einmalig eintragen.
- **Jedes Token gehört einer Person.** Nicht weitergeben und nicht gemeinsam verwenden,
  damit im Verlauf erkennbar bleibt, wer was geändert hat.
- Nach einem Browserwechsel oder wenn der Browser-Speicher geleert wird, ist die Einrichtung
  erneut vorzunehmen.

---

## Täglicher Gebrauch

| Vorgang | Wo |
|---|---|
| Erfassen | Reiter **Erfassung je Anwendung**, Abschnitte 1 bis 9 |
| Auswerten und filtern | Reiter **Übersicht und Auswertung** |
| Übertragen | Reiter **Synchronisation** — automatisch 2,5 Sekunden nach der letzten Änderung, oder auf Knopfdruck |
| Zustand prüfen | Anzeige **Sync: …** oben rechts, dazu das Protokoll |
| Bericht erzeugen | Knopf **Drucken / PDF** — ergibt einen sauberen Ausdruck des aktuellen Bogens |
| Datensicherung | Knopf **Speichern** — JSON-Datei; **Laden** liest sie wieder ein |
| Weitergabe / Auswertung in Excel | **Export CSV** bzw. **Matrix als CSV** |

### Wenn ein Konflikt gemeldet wird

Das bedeutet: Im Repository liegt eine neuere Fassung, als dieser Rechner kennt. Die App
zeigt den Konflikt rot an und bietet zwei Wege:

- **Fremde Fassung übernehmen** — die andere Version gilt.
- **Meine Fassung durchsetzen** — die eigene Version wird hochgeladen und überschreibt die andere.

Nichts geht dabei verloren: Die überschriebene Fassung bleibt im Verlauf des Repositories
erhalten und lässt sich dort wiederherstellen. Bei zwei Personen mit getrennten Bögen
entsteht ein Konflikt praktisch nie.

---

## Sicherheit

- Das **Token liegt im Browser** der jeweiligen Person. Wer Zugriff auf diesen Rechner hat,
  kommt daran. Deshalb: Token auf ein einziges Repository begrenzen, Ablaufdatum setzen,
  bei Verlust sofort bei GitHub widerrufen.
- Das Token wird **ausschliesslich an die eingetragene API-Adresse** gesendet. Wird die
  Adresse von `https://api.github.com` abweichend gesetzt, zeigt die Anwendung eine rote
  Warnung.
- Das Token steht **in keiner Exportdatei und in keinem Ausdruck**.
- **Niemals echte Bewohner-, Gesundheits- oder Personaldaten in die App oder ins
  App-Repository aufnehmen.** Das Werkzeug und der Katalog sind unbedenklich; die
  ausgefüllten Bögen gehören ins private Daten-Repository.
- Bei mehreren gleichzeitig arbeitenden Personen oder gemeinsam genutzten Rechnern ist eine
  Datenbank mit Anmeldung (zum Beispiel Supabase) die geeignetere Lösung als ein Token im Browser.

---

## Wenn die Anwendung geändert werden soll

Die Anwendung wird aus `capabilities-neuhaus.json` erzeugt. Nach einer Änderung am Katalog
genügt auf dem eigenen Rechner:

```
node build-ist-aufnahme-neuhaus.js
```

Danach die neu entstandene `ist-aufnahme-neuhaus.html` als `index.html` ins Repository
hochladen. GitHub Pages veröffentlicht die Änderung automatisch.

Der Katalog umfasst 13 Domänen, 40 Fähigkeitsgruppen und 110 Fähigkeiten der
Leistungserbringung eines Wohn- und Pflegezentrums.

---

## Stand

| Angabe | Wert |
|---|---|
| Katalogversion | 1.0 |
| Gültig ab | 16.09.2026 |
| Trägerin | Stiftung Neuhaus, Wängi |
| Bezug | Wohn- und Pflegezentrum, 80 Bewohnerinnen und Bewohner, rund 115 Mitarbeitende |
