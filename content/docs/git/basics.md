---
weight: 1
Title: "Git Basics"
---

# Git Basics

{{< figure src="https://imgs.xkcd.com/comics/git.png" link="https://xkcd.com/1597/" alt="Comic from xkcd.com. Click to view." caption="Git-Realität" >}}

## Zweck

Der Einsatz von Git verfolgt in der Regel hauptsächlich drei Zwecke:

- Textdateien zu tracken und Dateistände adressierbar zu machen *(Versionierung)*
- *Kollaboratives Arbeiten* an Dateien ohne Datei-Locking oder Datenverluste zu ermöglichen
- Die Integration von zuverlässigen *[CI/CD](https://en.wikipedia.org/wiki/CI/CD)-Pipelines* in den Arbeitsablauf

Man muss die Funktionsweise von Git nicht vollständig verstehen, um es effektiv zu nutzen. Für 99% aller Einsätze reichen eine handvoll grundlegender Befehle aus.


## Installation und Hilfe

Git kann über die [offizielle Website](https://git-scm.com/) heruntergeladen werden.

{{% tabs %}}

{{% tab "Windows" %}}

```powershell
git help [<subcommand>]
```

{{% /tab %}}

{{% tab "Linux & Mac" %}}

```bash
man git[-<subcommand>]
```

{{% /tab %}}

{{% /tabs %}}

Das Handbuch zum Befehl `git` und allen Sub-Commands kann im Terminal oder [online](https://git-scm.com/docs) gelesen werden.
Die Einführug in Git orientiert sich an `giteveryday` und `gitessentials` ([online](https://git-scm.com/docs/giteveryday)). 
Auf der offiziellen Website gibt es auch das Buch [Pro Git 2](https://git-scm.com/book/en/v2) zur kostenlosen Lektüre, dass
eine umfassende Einführung in die Funktionsweise von Git bietet, und auch kapitelweise gelesen werden kann.

## Einrichtung

Vor der ersten Verwendung von Git müssen einige Konfigurationen vorgenommen werden. Diese sind global und betreffen alle Repositories auf dem Rechner, können aber auch je Repository überschrieben werden.

```bash
git config --global user.name "Max Mustermann"
git config --global user.email "maxmustermann@provider.de"
```

Setzt den Namen und die E-Mail-Adresse des Benutzers. Diese Informationen werden in den Commits gespeichert und sind für die Zusammenarbeit mit anderen Benutzern wichtig. 

{{% hint info %}}
Benutzt man Hosting-Services wie GitHub oder GitLab, dann ist es hilfreich, die E-Mail-Adresse zu verwenden, die auch dort hinterlegt ist. So werden die commits dem richtigen Benutzer zugeordnet.
{{% /hint %}}
