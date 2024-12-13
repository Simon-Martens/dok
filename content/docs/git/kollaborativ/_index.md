---
weight: 3
Title: "Git Kollaborativ"
bookToc: false
---

{{< figure src="/images/GitCollaborative.png" link="/images/GitCollaborative.png" alt="Arbeitsablauf Git-Kollaborativ, Schematische Darstellung" class="invertable" >}}

Im Grunde funktioniert `git` dezentral, das heißt, dass prinzipell jeder Client gleichberechtigt ist, und keine:r der Teilnehmer:innen eines Projekts Autorität über den gerade gültigen Stand eines Repositories besitzt. In der Praxis wird jedoch immer ein zentrales Repository als Referenz genutzt. Ein Server hostet den de facto gültigen Status eines Projekts, der zwar gewaltsam überschrieben werden kann, aber nie sollte (mehr dazu unten). 

Weil Server, im Gegensatz zu einzelnen Rechnern, immer eingeschaltet sind und im offenen Netz stehen, benutzt man in der Regel einen Anbieter, der das autoritative Repository hostet. Die bekanntesten Anbieter sind [GitHub](https://github.com), [GitLab](https://gitlab.com) und [Bitbucket](https://bitbucket.org). Software wie [Gitea](https://gitea.io) oder [Gogs](https://gogs.io) ermöglichen es auch, eigene Git-Server zu betreiben, was aber wegen des hohen Aufwands und der geringen Vorteile nur von sehr großen oder firmeninternen Projekten gemacht wird.

## Begriffe

### remote/origin

Remote ist ein Verweis auf ein entferntes Repository, das auf einem Server liegt. Der Standardname für das entfernte Repository ist `origin`. Mit `git remote` können alle entfernten Repositories angezeigt werden, mit `git remote -v` werden auch die URLs angezeigt. Mit `git remote add <name> <url>` kann ein neues entferntes Repository hinzugefügt werden, mit dem synchronisiert werden kann.


### merge

Falls mehere Teilnehmer:innen gleichzeitig an einem Projekt arbeiten, kann es passieren, dass *upstream* commits bereitstellt, die lokal nicht vorhanden sind.
In diesem Fall muss ein merge durchgeführt werden, um die Änderungen zusammenzuführen. 
`git` versucht, den merge automatisch durchzuführen, und erstellt einen neuen commit, der die Änderungen vereint. 
In der Regel ist das kein Problem, da die meisten Teilnehmer:innen an verschiedenen Teilen des Projekts (beispielsweise unterschiedliche Dateien, oder ganz andere Zeilen innerhalb einer Datei) arbeiten. 
Manchmal kann es aber bei widersprüchlichen Änderungen zu Konflikten kommen, die manuell gelöst werden müssen (s.u. [Merge-Workflow](/docs/git/kollaborativ/merge)).
## Befehle

[pull](#git-pull) | [push](#git-push) | [clone](#git-clone)

{{% columns %}}

### git clone

```bash
git clone <url>
```

`git clone` erstellt initial eine Kopie eines entfernten Repositories auf dem lokalen Rechner. Der Standardname für das entfernte Repository ist `origin`. Der erstellte Ordner trägt den Namen des Repositories. Jede:r Teilnehmer:in erhält eine eigene Kopie des Repositories, mit allen jemals daran getätigten Änderungen. Die lokale Version funktioniert unabhängig und offline von der öffentlichen.


### git pull

```bash
git pull <pfad>
```

`git pull` lädt alle Änderungen aus dem entfernten Repository herunter und führt die Änderungen, falls nötig, zusammen.

{{% hint warning %}}
Bei einem `pull` kann es zu einem [Merge-Konflikt](/docs/git/kollaborativ/merge) kommen.

Es ist sinnvoll, vor jeder Arbeit einen pull durchzuführen, um unnötige Konflikte zu vermeiden. 
{{% /hint %}}

<--->

### git push

```bash
git push
```

`git push` lädt alle lokalen commits in das entfernte Repository hoch und veröffentlicht sie. Der Befehl `git push` wird manchmal mit dem Namen des entfernten Repositories und des Branches kombiniert, z.B. `git push origin master`. 

`git push` kann auch mit `--tags` kombiniert werden, um Tags zu veröffentlichen.

{{% hint info %}}
commits, die einmal veröffentlicht wurden, können nur sehr schwer und verbunden mit der Unterbrechung aller Arbeiten am Repository geändert werden. Es gibt fast keine Fälle, in denen es ratsam ist, commits zu löschen oder zu ändern, nachdem sie veröffentlicht wurden. 
{{% /hint %}}


{{% hint danger %}}
Manchmal wird  in Foren ein `git push --force` zur Lösung eines Problems angeraten. Der Server wird damit angewiesen, seine history mit der lokalen zu überschreiben. 

Normalerweise hat es aber einen einfachen Grund, dass der Server einen push ablehnt: jemand hat in der Zwischenzeit ebenfalls commits gepusht. Ein einfacher `git pull` und ein merge commit beheben in 99.9% aller Fälle das Problem. 

Manchmal muss ein Administrator einen solchen force-push durchführen, um beispielsweise unabsichtlich eingecheckte Zugangsdaten aus der history zu tilgen.  Ein `git push --force` sollte nur in Ausnahmefällen und nach Absprache mit allen Beteiligten durchgeführt werden.
{{% /hint %}} 

{{% /columns %}}

## Hinweise

### Wie können Änderungen rückgängig gemacht machen?

{{% hint info %}}

```bash
git restore [--source <tree-like>] <pfad>
```

`restore` ist ein neuerer, ungefährlicher Befehl, der dazu dient, Änderungen in Dateien zurückzusetzen. Meistens, wenn man einen früheren Dateistand wiederherstellen möchte, ist `restore` der gesuchte Command.

`restore` wird primär dazu genutzt, Änderungen von einzelnen Dateien aus dem Stageing-Bereich zu entfernen und wird von `git status` dazu empfohlen. Mithilfe von `restore` können auch commits rückgängig gemacht werden, aber so, dass die history nicht neu geschrieben wird. Dabei wird ein commit erstellt, der Änderungen rückgängig macht.

{{% /hint %}}

{{% hint info %}}

```bash
git revert <commit>
```

Auch mit `revert` kann man relativ ungefährdet einen früheren Dateizustand wiederherstellen. Wie mit `restore` oben kann mit `revert` ein neuer commit erstellt, der die Änderungen eines früheren commits im Ganzen rückgängig macht. `revert` ist ein sicherer Weg, um Änderungen rückgängig zu machen, ohne die history zu verändern.

`restore` und `revert` unterscheiden sich darin, dass `restore` Änderungen in Dateien zurücksetzt und sich ohne Angabe von `--source` auf den Stageing-Bereich bezieht, während `revert` ganze commits rückgängig macht.

{{% /hint %}}

{{% hint warning %}}
```bash
git checkout <pfad | tree-like>
```

Wenn Änderungen in den Dateien zurückgesetzt werden sollen, die noch nicht in einem commit sind, kann `git checkout` benutzt werden. So werden alle Dateien eines Verzeichnisses beispielsweise mit `git checkout .` in den Zustand des letzten commits zurückgesetzt. Dieser Befehl wird oft benutzt, wenn man kurzfristig etwas kaputt gemacht hat, aber jetzt nicht das Repo neu clonen möchte. 

**Achtung!** Dabei gehen Änderungen an Dateien verloren, die nicht committed wurden.


{{% /hint %}}

{{% hint danger %}}
```bash
git reset [--soft | --hard] <commit-like>
```

`reset` kann die History neu schreiben. Früher wurde `reset` u.a. dazu benutzt, Änderungen aus dem Index zu entfernen und von `git status` dazu empfohlen. Heute wird `git restore` empfohlen, um Änderungen aus dem Stageing-Bereich zu nehmen. `reset` sollte nur in Ausnahmefällen und nach Absprache mit allen Beteiligten durchgeführt werden.

{{% /hint %}}

### Git Rebase

{{% hint warning %}}
```bash
git rebase <branch>
```

 `rebase` ist ein mächtiges Werkzeug, um die history zu bereinigen und zu vereinfachen. So kann eine vielverzweigte hisory damit "gestrafft" werden. `rebase` sollte aber nur in den eigenen branches und niemals in branches, die mit anderen geteilt werden, durchgeführt werden. Ein `rebase` impliziert fast immer einen `force-push` und sollte nur nach Absprache mit allen Beteiligten durchgeführt werden.
{{% /hint %}}


