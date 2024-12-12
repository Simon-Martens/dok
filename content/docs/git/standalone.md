---
weight: 2
Title: "Git Lokal"
bookToc: false
---

{{< figure src="/images/GitStandalone.png" link="/images/GitStandalone.png" alt="Arbeitsablauf Git-Lokal, Schematische Darstellung" class="invertable" >}}

## Begriffe

### Repository

Ein Verzeichnis und die Geschichte aller Änderungen (Commits) und Verzweigungen (branches) an getrackten Ordnern und Dateien.

### Commit

Ein Speicherpunkt für einen spezifischen Dateistand. Ein Commit enthält verpflichtend:

- Einen *SHA1-Hash*, der den commit eindeutig identifiziert.
- Angaben zum Autor des commits (*Name, email-Adresse und Zeitstempel mit Zeitzone*).
- Eine Nachricht, die optimalerweise den commit kurz beschreibt.
- Eine Referenz auf den vorherigen commit (*parent-commit*). Ausnahme: Der erste commit in einem Repository und sog. *dangling commits* haben keinen Parent-commit. Außerdem kann ein commit mehrere parent-commits haben, wenn es sich um einen merge-commit handelt, der mehrere Verzweigungen zusammenführt.
- Eine Referenz auf einen spezifischen Stand eines Verzeichnisbaumes.

Da die meisten dieser Felder von `git` generiert werden oder global konfiguriert sind, muss meist nur eine kurze commit message angegeben werden.

Optional kann ein commit auch enthalten:

- Comitter und Autor eines commits können differenziert werden, auch mit unterschiedlichen Zeitstempeln. Bei sehr großen Projekten kann es vorkommen, dass commits eingereicht werden und nur Maintainer oder Integratoren commits letztendlich in das Repository einpflegen.
- Eine Referenz auf einen *tag*, der den commit markiert, i.d.R. sind das Markierungen von funktional abgeschlossenen Zuständen eines Repositories (z.B. 2.16, 0.1-alpha).
- Eine längere Beschreibung des commits, genannt Notiz od. *note*.

### Stage

Oft wird der Stageing-Bereich auch *Index* genannt. Der Stageing-Bereich ist eine Hilfe für Entwickler:innen um Änderungen an Dateien zu sammeln, die dann zusammen in den nächsten commit einfließen.

{{< figure src="/images/GitWorkflowStandalone.png" link="/images/GitWorkflowStandalone.png" alt="Arbeitsablauf Git-Lokal, Schematische Darstellung" class="invertable" >}}

## Befehle

[init](#git-init) | [status](#git-status) | [log](#git-log) | [add](#git-add) | [commit](#git-commit)

{{% columns %}}

### git init

```bash
git init [<pfad>]
```

Erstellt ein neues Git-Repository (im aktuellen Verzeichnis, sofern kein Pfad angegeben wurde).
Alle Daten, die `git` benötigt, um das Repository zu verwalten, werden im (versteckten) Verzeichnis `.git` gespeichert.

### git status

```bash
git status
```

Zeigt den Status des Repositories und des Stageing-Bereichs an. Es wird angezeigt, welche Dateien geändert wurden, welche Dateien neu hinzugefügt wurden und welche Dateien für den nächsten commit bereit sind. Außerdem gibt `git status` Hinweise, wie Dateien in den Stageing-Bereich oder aus dem Stageing-Bereich entfernt werden können, oder was bei Konflikten zu tun ist.

{{% hint info %}}

`git status` ist ein sehr hilfreicher Befehl, um zu sehen, was sich im Repository getan hat und was als nächstes zu tun ist. Der Befehl schlägt niemals destrukive Aktionen vor.

{{% /hint %}}


### git log

```bash
git log [--graph] [--oneline] [--since=<datum>] [--author=<name>] [-p]
```

Zeigt die Historie der commits an. Mit `--graph` wird die Historie als Graph dargestellt, mit `--oneline` wird die Historie in einer Zeile je commit dargestellt. Mit `--since=<datum>` können nur commits ab einem bestimmten Datum angezeigt werden, mit `--author=<name>` können nur commits eines bestimmten Autors angezeigt werden. Mit `-p` werden die Änderungen an den Dateien in jedem commit detailliert angezeigt.

{{% hint info %}}
`git log` zeigt nur commits an, die lokal verfügbar und heruntergeladen sind. Um auch die commits aus einem Remote-Repository anzuzeigen, muss zuvor `git fetch` ausgeführt werden.
{{% /hint %}}


<--->



### git add

```bash
git add <pfad>
```

Fügt eine Datei oder ein Verzeichnis dem Stageing-Bereich hinzu. Die Datei wird für den nächsten Commit vorbereitet. Wenn ein Verzeichnis hinzugefügt wird, werden alle Dateien in diesem Verzeichnis und in allen Unterverzeichnissen hinzugefügt. Oft genutzt wird `git add .`, um alle Änderungen im aktuellen Verzeichnis und in allen Unterverzeichnissen hinzuzufügen. Manchmal wird der Befehl auch übersprungen und direkt `git commit -a` genutzt, um alle Änderungen in einem Schritt zu committen.

{{% hint warning %}}
Am Besten werden sinnvolle Einheiten an Änderungen zu einem commit zusammengefügt. Für CI/CD-Pipelines ist es wichtig, unvollständige oder fehlerhafte commits zu vermeiden.
{{% /hint %}}

{{% hint warning %}}
`git commit -a` fügt nur Dateien hinzu, die bereits von `git` getrackt werden, eine Falle, in die man sehr leicht tappen kann. Neue Dateien müssen zuerst explizit mit `git add` hinzugefügt werden.
{{% /hint %}}


### git commit

```bash
git commit [-a] [-m "Nachricht"]
```

Erstellt einen neuen Commit mit den Dateien, die sich im Stageing-Bereich befinden. Mit `-a` werden alle Dateien, die bereits von `git` getrackt werden, automatisch hinzugefügt. Mit `-m "Nachricht"` kann eine commit-Nachricht direkt beim commit angegeben werden. Wenn dies nicht geschieht, öffnet sich ein Editor, in dem die Nachricht eingegeben werden kann, mit einem Speichern und Schließen des Editors wird dann der Commit erstellt.

{{% hint info %}}
Es ist empfehlenswert, eine kurze, aussagekräftige Commit-Nachricht zu schreiben ("Einpflegung Brief 343", "Kollation Ms. 12.4") und allgemeine Nachrichten ("kleine Änderung", "Nochmal") so gut es geht zu vermeiden.
{{% /hint %}}

{{% hint danger %}}
Der Befehl `git commit --amend` kann genutzt werden, um den letzten commit zu ändern, so bespielsweise einen Rechtschreibfehler in einer commit-Message. Das sollte jedoch nur gemacht werden, wenn der commit noch nicht gepusht wurde. Ansonsten wird die History des Repositories verändert, was zu Problemen bei kollaborierenden Entwickler:innen führt.
{{% /hint %}}

{{% /columns %}}
