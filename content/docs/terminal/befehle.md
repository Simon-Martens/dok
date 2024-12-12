---
weight: 3
Title: "Grundlegende Befehle"
bookToc: false
---

# Grundlegende Befehle

{{% columns %}}

## Arbeitsverzeichnis wechseln

```powershell
> cd <verzeichnis>
```
Mit `cd` (= change directory) kann man das Arbeitsverzeichnis wechseln. Der Pfad kann absolut (wie in `> cd C:/Users/User/Documents`) oder relativ zum Arbeitsverzeichnis (wie in `> cd Documents`) sein.

Besondere Bedutung haben die Pfade `.` und `..`.
`.` zeigt auf das aktuelle Verzeichnis, `> cd .` macht also nichts. `..` zeigt auf das übergeordnete Verzeichnis, `> cd ..` wechselt also in das übergeordnete Verzeichnis, beislpielsweise:

```powershell
C:\Users\User\Documents> cd ..
C:\Users\User>
```

## Neue (leere) Datei erstellen

{{% tabs %}}
{{% tab "Windows" %}}

```powershell
> ni <dateipfad>
```

{{% /tab %}}
{{% tab "Linux / Mac" %}}

```bash
$ touch <dateipfad>
```

{{% /tab %}}
{{% /tabs %}}

Erstellt eine leere Datei unter dem angegebenen Pfad.

Ist die Datei vorhanden, aktualisiert `touch` das Änderungsdatum der Datei auf die aktuelle Zeit, `ni` zeigt eine Fehlermeldung an.


## Datei od. Verzeichnis löschen

{{% tabs %}}
{{% tab "Windows" %}}

```powershell
> rm <pfad>
```

{{% hint info %}}
Windows zeigt eine Bestätigungsmeldung bei nicht-leeren Verzeichnissen an.
{{% /hint %}}

{{% /tab %}}
{{% tab "Linux / Mac" %}}

```bash
> rm [-r] [-f] <pfad>
```

Die Option `-r` löscht rekursiv auch Verzeichnisse und deren Inhalt, `-f` löscht ohne Rückfrage.


{{% /tab %}}
{{% /tabs %}}

{{% hint danger %}}
**Achtung!** Gelöschte Dateien  und Verzeichnisse landen nicht im Papierkorb und sind evtl. nicht
wiederherstellbar!
{{% /hint %}}


## Programme starten

Auch grafische Programme können aus dem Terminal heraus gestartet werden. Der Befehl wird erst beendet, wenn das Programm geschlossen wird.

```powershell
> start <programm> <parameter>
```

Beispielsweise öffnet `> start notepad++ file.txt` die Datei `file.txt` im
Editor Notepad++. Den aktuellen Ordner in Visual Studio Code öffnen: `> code .`.

Leider ist unter Windows die Syntax zum Starten von Programmen nach
Werkseinstellung nicht einheitlich.


<--->





## Verzeichnisinhalt anzeigen

{{% tabs %}}
{{% tab "Windows" %}}

```powershell
> dir [<verzeichnis>]
```

{{% /tab %}}
{{% tab "Linux / Mac" %}}

```bash
$ ls [-a] [-l] [-h] [<verzeichnis>]
```

Die Option `-a` zeigt auch versteckte Dateien an, `-l` zeigt eine detaillierte Liste (wie in Windows) an und `-h` zeigt die Größenangaben in einer menschenlesbaren Form an.

{{% /tab %}}
{{% /tabs %}}

Den Inhalt eines Verzeichnisses auflisten. Windows zeigt die Listenansicht standardmäßig an, Linux und Mac die Kurzansicht. Ohne angegebenes Verzeichnis wird das aktuelle Verzeichnis aufgelistet, `dir .` ist also äquivalent zu `dir`.



## Verzeichnis erstellen

{{% tabs %}}
{{% tab "Windows" %}}

```powershell
> mkdir <verzeichnis(se)>
```

{{% /tab %}}
{{% tab "Linux / Mac" %}}

```bash
$ ls [-p] [<verzeichnis>]
```

Die Option `-p` erstellt auch die übergeordneten Verzeichnisse, falls sie nicht existieren.

{{% /tab %}}
{{% /tabs %}}

Mit `mkdir` (= make directory) kann man ein neues Verzeichnis erstellen. Der Pfad kann absolut oder relativ sein. 


## Datei od. Verzeichnis verschieben

{{% tabs %}}
{{% tab "Windows" %}}

```powershell
> move <quellpfad> <zielpfad>
> Move-Item -Path <quellpfad> -Destination <zielpfad>
> git mv <quellpfad> <zielpfad>
```


{{% hint info %}}
Windows gibt bei gleichnamigen Dateien eine Fehlermeldung aus.
{{% /hint %}}

{{% /tab %}}
{{% tab "Linux / Mac" %}}

```bash
$ mv <quellpfad> <zielpfad>
$ git mv <quellpfad> <zielpfad>
```

{{% hint danger %}}
**Achtung!** Linux &amp; Mac überschreiben gleichnamige Dateien ohne Warnung!
{{% /hint %}}

{{% /tab %}}
{{% /tabs %}}

Einen Ordner oder eine Datei von `<quellpfad>` nach `<zielpfad>` verschieben.
Der entsprechende `git`-Befehl ist nur für Dateien im Git-Repository verfügbar
und führt zur einer nacvollziehbaren Nachverfolgung von Änderungen.

Der Befehl `mv` wird Umbenennen von Dateien und Verzeichnissen
verwendet. `> mv file.txt newfile.txt` benennt die Datei `file.txt` in
`newfile.txt` um.

## Inhalt einer Datei ausgeben

```powershell
> cat <dateipfad>
```

Gibt den Inhalt einer Datei im Terminal aus. 

## Terminal schließen

```powershell
> exit
```

{{% /columns %}}

