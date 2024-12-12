---
weight: 3
Title: "Git Kollaborativ"
bookToc: false
---

{{< figure src="/images/GitCollaborative.png" link="/images/GitCollaborative.png" alt="Arbeitsablauf Git-Kollaborativ, Schematische Darstellung" class="invertable" >}}

Eigentlich arbeitet `git` dezentral, das heißt, dass prinzipell jeder Client gleichberechtigt wird, und keine:r der Teilnehmer:innen eines Projekts Autorität über den gerade gültigen Stand des Repositories besitzt. In der Praxis wird jedoch immer ein zentrales Repository (*upstream*) als Referenz genutzt. Dieser Server hostet den quasi gültigen Status der history eines Projekts, die nie gewaltsam überschrieben werden sollte (mehr dazu unten). 

Weil Server, im Gegensatz zu einzelnen Rechnern, immer eingeschaltet sind und im offenen Netz stehen, benutzt man in der Regel einen Anbieter, der das autoritative Repository hostet. Die bekanntesten Anbieter sind [GitHub](https://github.com), [GitLab](https://gitlab.com) und [Bitbucket](https://bitbucket.org). Software wie [Gitea](https://gitea.io) oder [Gogs](https://gogs.io) ermöglichen es auch, eigene Git-Server zu betreiben, was aber wegen des hohen Aufwands und der geringen Vorteile nur von sehr großen oder firmeninternen Projekten gemacht wird.

## Begriffe

### remote/origin

Remote ist ein Verweis auf ein entferntes Repository, das auf einem Server liegt. Der Standardname für das entfernte Repository ist `origin`. Mit `git remote` können alle entfernten Repositories angezeigt werden, mit `git remote -v` werden auch die URLs angezeigt. Mit `git remote add <name> <url>` kann ein neues entferntes Repository hinzugefügt werden, mit dem synchronisiert werden kann.


### merge

Falls mehere Teilnehmer:innen gleichzeitig an einem Projekt arbeiten, kann es passieren, dass *upstream* commits bereitstellt, die lokal nicht vorhanden sind.
In diesem Fall muss ein merge durchgeführt werden, um die Änderungen zusammenzuführen. 
`git` versucht, den merge automatisch durchzuführen, und erstellt einen neuen commit, der die Änderungen vereint. 
In der Regel (>95% aller Fälle) ist das kein Problem, da die meisten Teilnehmer:innen an verschiedenen Teilen des Projekts (beispielsweise unterschiedliche Dateien, oder ganz andere Zeilen innerhalb einer Datei) arbeiten. 
`git` erkennt automatisch, welche Teile des Projekts von wem stammen und wie angepasst werden müssen, um einen konsistenten Dateistand herzustellen.

Manchmal kann es aber auch zu Konflikten kommen, die `git` nicht automatisch zusammenführen kann, oft, wenn Teilnehmer:innen an der gleichen Datei und derselben Stelle Änderungen vorgenommen haben. 
In diesem Fall muss der merge manuell durchgeführt werden; dabei wird die Datei in einen Konfliktzustand versetzt, und die Konflikte müssen manuell gelöst werden. 
Der jeweils mergende entscheidet dabei, welche Änderungen übernommen werden sollten &ndash; und welche Geschichte sind.

Sind die Probleme gelöst, führt der mergende einen `git add` und einen `git commit` durch, um den merge abzuschließen, und schon ist die Ordung wieder hergestellt.


{{< figure src="/images/GitWorkflowCollaborative.png" link="/images/GitWorkflowCollaborative.png" alt="Arbeitsablauf Git-Kollaborativ, Schematische Darstellung" class="invertable" >}}

## Befehle

{{% columns %}}


### git pull

```bash
git pull <pfad>
```

{{% hint warning %}}
Es ist sinnvoll, vor jeder Arbeit einen pull durchzuführen, um unnötige Konflikte zu vermeiden. 
{{% /hint %}}

`git pull` lädt alle Änderungen aus dem entfernten Repository herunter und führt einen merge, falls nötig, durch. 

{{% hint info %}}
Bei einem pull kann es zu merge-Konfilkten kommen. Grundsätzlich muss ein merge durchgeführt werden, wenn remote commits von anderen Teilnehmer:innen vorliegen, die nicht lokal verfügbar sind, also meinst, wenn vor dem Arbeiten nicht gepullt wurde. Meistens allerdings ist das Projekt so aufgeteilt, dass andere Teilnehmer:innen an anderen Teilen arbeiten, und es keine Konflikte gibt. In dem Falle wird ein automatischer merge-commit erstellt.
{{% /hint %}}

### git clone

```bash
git clone <url>
```

`git clone` erstellt initial eine Kopie eines entfernten Repositories auf dem lokalen Rechner. Der Standardname für das entfernte Repository ist `origin`. Der erstellte Ordner trägt den Namen des Repositories. Jede:r Teilnehmer:in erhält eine eigene Kopie des Repositories, mit allen jemals daran getätigten Änderungen, die unabhängig und offline funktioniert.

<--->

### git push

```bash
git push
```

`git push` lädt alle lokalen commits in das entfernte Repository hoch und veröffentlicht sie. Der Befehl `git push` wird manchmal mit dem Namen des entfernten Repositories und des Branches kombiniert, z.B. `git push origin master`. Der Befehl `git push` kann auch mit `--tags` kombiniert werden, um Tags zu veröffentlichen.

{{% hint info %}}
commits, die einmal veröffentlicht wurden, können nur sehr schwer und verbunden mit der Unterbrechung aller Arbeiten am Repository geändert werden. Es gibt fast keine Fälle, in denen es besser ist, commits zu löschen oder zu ändern, nachdem sie veröffentlicht wurden. 
{{% /hint %}}


{{% hint danger %}}
Manchmal wird  in Foren ein `git push --force` zur Lösung eines Problems angeraten. Der Server wird damit angewiesen, seine history mit der eigenen zu überschreiben. 

Normalerweise hat es aber einen einfachen Grund, dass der Server einen push ablehnt: in der Regel hat jemand anderes in der Zwischenzeit ebenfalls commits gepusht. Ein einfacher `git pull` und ein merge commit behebt in 99.9% aller Fälle das Problem. 

Manchmal muss ein Administrator einen solchen force-push durchführen, um beispielsweise unabsichtlich eingecheckte Zugangsdaten aus der history zu tilgen.  Ein `git push --force` sollte nur in Ausnahmefällen und nach Absprache mit allen Beteiligten durchgeführt werden.
{{% /hint %}} 

{{% /columns %}}

## Hinweise

{{% hint warning %}}
```bash
git rebase
```

 `rebase` ist ein mächtiges Werkzeug, um die history zu bereinigen und zu vereinfachen. So kann eine vielverzweigte hisory damit "gestrafft" werden. Es sollte aber nur in den eigenen branches und niemals in branches, die mit anderen geteilt werden, durchgeführt werden. Ein `rebase` impliziert fast immer einen `force-push` und sollte nur nach Absprache mit allen Beteiligten durchgeführt werden.
{{% /hint %}}


{{% hint warning %}}
```bash
git reset 
```

`reset` kann ebenfalls die History neu schreiben. Früher wurde `reset` u.a. dazu benutzt, Änderungen aus dem Index zu entfernen und von `git status` dazu empfohlen. Heute wird `git restore` empfohlen, um Änderungen aus dem Stageing-Bereich zu entfernen. `reset` sollte nur in Ausnahmefällen und nach Absprache mit allen Beteiligten durchgeführt werden.

{{% /hint %}}


{{% hint info %}}
```bash
git restore
```

`restore` ist ein relativ ungefährlicher Befehl, der dazu dient, Änderungen in Dateien zurückzusetzen. Meistens, wenn man Dateien oder Änderungen zu einem früheren Zeitpunkt zurücksetzen möchte, ist `restore` der Befehl, den man dazu braucht.

Der Befehl kann auch dazu benutzt werden, Änderungen aus dem Stageing-Bereich zu entfernen und wird von `git status` dazu empfohlen. Mit `restore` können auch commits rückgängig gemacht werden, aber so, dass die history nicht neu geschrieben wird. Dabei wird ein commit erstellt, der Änderungen rückgängig macht.

{{% /hint %}}

