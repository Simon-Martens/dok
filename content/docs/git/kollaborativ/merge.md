---
title: "Merge-Workflow"
bookToc: false
---

{{< figure src="/images/GitWorkflowCollaborative.png" link="/images/GitWorkflowCollaborative.png" alt="Arbeitsablauf Git-Kollaborativ, Schematische Darstellung" class="invertable" >}}

# Git Merge-Workflow

Der Merge-Workflow ist der von `git` standardmäßig vorgeschlagene und eingestellte Arbeitsablauf zur Synchronisation zwischen lokalen und entfernten Repositories und eignet sich sehr gut für kleine Branches, an denen eine [Handvoll an Entwickler:innen](https://en.wikipedia.org/wiki/The_Mythical_Man-Month) arbeiten, die sich gegenseitig vertrauen.
Alternativ zum Merge-Workflow kann man auch den [Rebase](https://git-scm.com/book/en/v2/Git-Branching-Rebasing) verwenden. 
Ein ganz anderer und im Kontext von Open Source oft genutzter Arbeitsablauf ([Patch-Workflow](https://git-scm.com/docs/gitworkflows")) sieht vor, Änderungen nur durch Integratoren (via *pull-requests* oder per mail eingesendete *patches*) einpflegen zu lassen.

Bei einem Merge-Workflow können bei einem `git pull` mehrere Dinnge passieren:

## 1. Lokal keine commits | Remote keine commits

Hier zeigt `git` eine Meldung, dass alles aktuell ist und es passiert gar nichts.

## 2. Lokal keine commits <i class="ri-arrow-left-line"></i> Remote neue commits

Hier findet ein *fast-forward* statt. 
Das bedeutet, dass die neuen commits einfach auf den aktuellen Stand aufgesetzt werden. 
Das ist möglich, weil die neuen commits auf dem aktuellen Stand basieren. Das ist der einfachste und häufigste Fall, wenn man vor dem Arbeiten schnell einen `git pull` durchführt. Es gibt keinen Merge-Commit.

## 3. Lokal neue commits <i class="ri-arrow-right-line"></i> Remote keine commits

Hier kann man einfach `git push` ausführen. 
Dabei passiert ein *fast-forward* auf dem Remote-Repository. Es gibt keinen neuen Merge-Commit. 
Oder man arbeitet lokal weiter und pusht später.

## 4. Lokal neue commits <i class="ri-expand-horizontal-s-line"></i> Remote neue commits

Hier muss ein Merge-Commit erstellt werden. 
Dabei passiert ein sog. *three-way-merge*. 
Der heißt so, weil `git` drei commits miteinander vergleicht: den letzten gemeinsamen commit zwischen lokal und remote, den aktuellen Stand des lokalen Repositories und den aktuellen Stand des Remote-Repositories.

### Fall 1: Automatischer Merge

In den allermeisten Fällen ist die Arbeit so aufgeteilt, dass sich Änderungen nicht gegenseitig überschreiben. Die Teilnehmer:innen arbeiten an unterschiedlichen Dateien oder an unterschiedlichen Stellen in den Dateien. In diesem Fall kann `git` den intendierten Zustand der Dateien leicht erkennen und erstellt automatisch einen Merge-Commit. Man muss nur noch die Commit-Nachricht schreiben (oder die Standard-Message übernehmen) und pushen.

### Fall 2: Konflikte

Wenn sich Änderungen überschneiden, kann `git` nicht automatisch entscheiden, welche der Änderungen autoritativ ist. 
In diesem Fall gibt es einen Merge-Konflikt. 
`git` zeigt die betroffenen Dateien an und markiert die Stellen, an denen Konflikte aufgetreten sind.
Git schreibt beide Versionen einer Stelle, die sich gegenseitig widersprechen, in die Datei:

```
<<<<<<< HEAD:file.txt
# Änderung aus dem lokalen Repository
=======
# Änderung aus dem Remote-Repository
>>>>>>> 77976da35a11db4580b80ae27e8d65caf5208086:file.txt
```

Der Konflikt muss händisch aufgelöst werden. 
Dabei wird jede konfligierende Datei einfach so bearbeitet, wie sie am Ende aussehen soll und gespeichert. 
Sind alle Konflikte zur Zufriedenheit gelöst, führt man einfach `git add .` und `git commit` aus, und hat damit den merge-Commit selbst durchgeführt.

{{% hint info %}}

### Merge-Konflikte vermeiden

Es gibt einige Praktiken, um Merge-Konflikte zu vermeiden, die in den allermeisten Fällen dann auch funktionieren:

#### Kleine Commits, häufiges Pushen

Es ist einfacher, Änderungen zu mergen, wenn sie in kleinen, in sich geschlossenen Commits vorliegen. Es ist sinnvoll, Änderungen, die lokal vorliegen, häufig zu pushen, damit möglichst alle anderen Teilnehmer:innen bei Beginn ihrer Arbeitden aktuellen Stand bekommen.

#### Sinnvolle Arbeitsteilung

Es ist sinnvoll, dass die Teilnehmer:innen an unterschiedlichen Dateien oder an unterschiedlichen Stellen in den Dateien arbeiten. Das reduziert die Wahrscheinlichkeit, dass sich Änderungen überschneiden. **Achtung beim Suchen und Ersetzen in ganzen Dateien**: bei größeren *Refactories*, bei denen viele Dateien und sehr unterschiedliche Stellen quer durch eine Repo betroffen sind, sollten sich die Teilnehmer:innen absprechen, um Konflikte zu vermeiden.

#### Vor dem Arbeiten: `git pull`

Es ist am Besten, die eigenen commits basierend auf dem aktuellsten Stand des Remote-Repositories zu machen. Das reduziert die Wahrscheinlichkeit von Konflikten. Daher vor dem Arbeiten: immer einen `git pull` ausführen.

{{% /hint %}}

