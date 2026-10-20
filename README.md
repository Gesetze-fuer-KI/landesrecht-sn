# Landesrecht Sachsen

<p>
  <a href="https://github.com/Gesetze-fuer-KI/landesrecht-sn/actions/workflows/sync.yml"><img alt="Nächtlicher Abgleich" src="https://github.com/Gesetze-fuer-KI/landesrecht-sn/actions/workflows/sync.yml/badge.svg"></a>
</p>

**Das Landesrecht von Sachsen für [Gesetze für KI](https://gesetze-fuer-ki.de):** Ihr KI-Assistent schlägt damit die aktuellen Landesgesetze nach. Alles zum Einrichten steht auf **[gesetze-fuer-ki.de](https://gesetze-fuer-ki.de)**.

---

<sub>Ab hier für Neugierige und alle, die mitmachen wollen.</sub>

## Was hier liegt

Alle Gesetze und Verordnungen des Freistaats Sachsen in der heute geltenden Fassung, eine Textdatei (Markdown) je Gesetz. Verwaltungsvorschriften, Bekanntmachungen und Satzungen sind nicht enthalten. Jede Nacht kommt als Commit hinzu, was sich geändert hat. Die Dateien sind auch für sich nutzbar: zum Lesen, Durchsuchen und Vergleichen von Fassungen.

## Quelle

| | |
|---|---|
| Land | Sachsen |
| Portal | [REVOSax](https://www.revosax.sachsen.de) (revosax.sachsen.de) |
| Betreiber | Sächsische Staatskanzlei, gemeinsam mit dem SV SAXONIA Verlag |
| Fassung | **nichtamtlich**, wie das Portal selbst sagt |

Die Texte sind die konsolidierten, **nichtamtlichen Fassungen** des Portals. Rechtlich maßgeblich ist allein, was im Sächsischen Gesetz- und Verordnungsblatt verkündet wurde.

## Wie der Abgleich läuft

Die [Action](.github/workflows/sync.yml) läuft jede Nacht um 01:52 UTC mit [`sync.py --land sn`](https://github.com/Gesetze-fuer-KI/gesetze-fuer-ki/blob/main/app/sync.py) aus [gesetze-fuer-ki](https://github.com/Gesetze-fuer-KI/gesetze-fuer-ki). Sie hält die robots.txt des Portals ein und stellt höchstens zwei Anfragen gleichzeitig.

Die Suche des Portals nennt zu jedem Gesetz, ab wann seine aktuelle Fassung gilt („Fassung gültig ab“). Neu geladen wird nur, was sich daran geändert hat. Zeigt das Portal schon eine künftige Fassung, wird sie erst an ihrem ersten Geltungstag übernommen.

Der **erste vollständige Abgleich** kann mehrere Nächte dauern. Jeder Lauf hört rechtzeitig vor dem Zeitlimit von GitHub auf, merkt sich in `.sync/state.json`, wie weit er gekommen ist, und committet den Zwischenstand; der nächste Lauf macht dort weiter. Bis der erste Durchgang fertig ist, steht Sachsen auf gesetze-fuer-ki.de als „im Aufbau“ und ist noch nicht durchsuchbar. Gesetze, die das Portal nicht mehr führt, werden erst nach einem vollständigen Durchgang gelöscht.

Hinweis für die Betreuung: GitHub pausiert geplante Workflows, wenn ein Repository 60 Tage lang keine Commits bekommt. Ein Lauf von Hand (**Actions → Sync → Run workflow**, `workflow_dispatch`) schaltet ihn wieder ein.

## Ein Gesetz finden

Die Dateien heißen nach dem Länderkürzel und der Kennung des Gesetzes auf dem Portal und liegen in einem Ordner nach den ersten zwei Zeichen dieser Kennung (`<ordner>/<kennung>.md`): `20/sn-20111.md` ist das Gesetz mit der Kennung 20111 auf dem Portal (`/vorschrift/20111`). Jede Datei beginnt mit Metadaten (Land, Abkürzung, Titel, Stand, Quelle mit Link aufs Portal); danach folgen Gliederung und Vorschriften als Überschriften, jeweils mit einem unsichtbaren Kommentar, der die Kennung der Vorschrift trägt.

Der Ordner `.sync/` gehört dem Abgleich: `state.json` (Fortschritt und was er sich über die Gesetze merkt) und `commit-message.txt` (die Nachricht des letzten Commits).

## Änderungen ansehen

Auf GitHub: eine Datei öffnen und **History** klicken. Lokal:

```bash
git log -p -- <ordner>/<kennung>.md
```

Die Commit-Nachricht nennt je geändertem Gesetz eine Zeile mit Abkürzung und neuem Stand.

## Herkunft und Lizenz

Das Portal nennt keine Lizenz und verbietet die Weiterverwendung nicht. Gesetze und Verordnungen sind amtliche Werke und nach § 5 UrhG gemeinfrei. Einzelheiten in [LIZENZ.md](LIZENZ.md).

Sollte das Land der Veröffentlichung hier widersprechen, nehmen wir die Texte heraus: [kontakt@gesetze-fuer-ki.de](mailto:kontakt@gesetze-fuer-ki.de).

Fehler der Umwandlung bitte als [Issue](https://github.com/Gesetze-fuer-KI/gesetze-fuer-ki/issues) melden, alles andere an [kontakt@gesetze-fuer-ki.de](mailto:kontakt@gesetze-fuer-ki.de). Mehr unter [Daten und Grenzen](https://gesetze-fuer-ki.de/daten/).

---

<sub>Keine Rechtsberatung: Der Dienst liefert Gesetzestexte; maßgeblich ist die amtliche Fassung. · [Unterstützen](https://gesetze-fuer-ki.de/unterstuetzen/) · [Impressum](https://gesetze-fuer-ki.de/impressum/) · [Datenschutz](https://gesetze-fuer-ki.de/datenschutz/)</sub>
