---
weight: 2
Title: "Glossar, Tipps & Tricks"
---

## Glossar

{{% details "Arbeitsverzeichnis" true %}}

### Arbeitsverzeichnis

Alle Programme und Befehle, die im Terminal ausgeführt werden, bekommen automatisch das aktuelle Verzichnis als Arbeitsverzeichnis übergeben. Das Arbeitsverzeichnis ist das Verzeichnis, in dem sich der Benutzer gerade befindet. Es wird auch als "current working directory" bezeichnet und in der Kommandozeile vorn angezeigt. 

Der Befehl `pwd` (print working directory) gibt das Arbeitsverzichnis aus. Der Befehl `cd` (change directory) wechselt das Arbeitsverzeichnis. 

{{% /details %}}

{{% details "Befehl" true %}}

### Befehl

Ein Befehl ist eine Anweisung, die an ein Programm oder das Betriebssystem gerichtet wird und die grundlegende Funktionen ausführt. 

Befehle sind von der Struktur

{{% tabs %}}
{{% tab "Windows" %}}
```powershell
befehl [</option(en)>] [<parameter>]
```
{{% /tab %}}
{{% tab "Linux / Mac" %}}

```bash
befehl [<-optionen>] [<parameter>]
```

{{% /tab %}}
{{% /tabs %}}

Optionen oder Flags manipulieren die Arbeitsweise des Befehls. Beispielsweise gibt der Befehl `ls -l` eine detaillierte Liste der Dateien im aktuellen Verzeichnis aus, während `ls` nur die Dateinamen auflistet. Die Optionen `-l -a` würde eine detaillierte Liste aller Dateien, inklusive aller versteckten, im aktuellen Verzeichnis ausgeben.

Parameter sind textuelle oder numerische Werte, die der Befehl benötigt, um seine Funktion auszuführen. Beispielsweise benötigt der Befehl `mkdir <verzeichnis>` einen Parameter, der den Namen des zu erstellenden Verzeichnisses angibt (ohne den Namen des Verzeichnisses würde der Befehl keinen Sinn ergeben).

{{% /details %}}

{{% details "Pfade, absolute und relative" true %}}

### Pfade, absolute und relative

Ein Pfad ist eine Zeichenfolge, die den Speicherort einer Datei oder eines Verzeichnisses auf einem Dateisystem angibt. Es gibt zwei Arten von Pfaden: absolute und relative Pfade.

Ein *absoluter* Pfad beginnt immer am Stammverzeichnis des Dateisystems und enthält den vollständigen Pfad zur Datei oder zum Verzeichnis (in Windows inklusive des Laufwerksbuchstabens), so wie etwa `C:\Users\User\.gitconfig` oder `/etc/passwd`.

Ein *relativer* Pfad beginnt im aktuellen Arbeitsverzeichnis und enthält nur den Pfad zur Datei oder zum Verzeichnis relativ zum aktuellen Arbeitsverzeichnis, z.B. `Documents\file.txt` oder `../Pictures/photo.jpg`.

Alle Befehle, die einen Pfad benötigen, können i.d.R. sowohl absolute als auch relative Pfade verwenden. 
{{% /details %}}

{{% details "Skript" true %}}

### Skript

Ein Shell-Skript ist eine Datei, die eine Abfolge von Terminal-Befehlen enthält. Diese Befehle werden nacheinander ausgeführt, wenn das Skript ausgeführt wird. Shell-Skripte werden häufig verwendet, um wiederkehrende Aufgaben zu automatisieren, und können sehr komplex werden. In Windows können die Skripte die Endungen `.bat`, `.cmd` oder `.ps1` bzw. `.ps2` haben. Unter Linux wird normalerweise die Endung `.sh` verwendet.

Vorsicht! Weil Shell-Kommandos direkt auf dem System ausgeführt werden, können Skripte auch Schaden anrichten. Verwenden Sie nur Skripte, die Sie verstehen und denen Sie vertrauen. 

{{% /details %}}



## Tipps &amp; Tricks

{{% tipp %}}

{{% tipp-head %}}

### Tab-Taste

{{% /tipp-head %}}

{{% tipp-body %}}

Damit man im Teminal nicht alles eintippen muss, vervollständigt die TAB-Taste automatisch Befehle und vor allem Datei- und Verzeichnispfade, wenn ein Teil des Pfades eingegeben wurde. Beispiel: Steht im aktuellen Terminal

```powershell
> C:\Users\User\>cd Doc
```

vervollständigt die TAB-Taste den Befehl automatisch zu 

```powershell
> C:\Users\User\>cd Documents\
```

{{% /tipp-body %}}
{{% /tipp %}}

{{% tipp %}}

{{% tipp-head %}}

### Leerzeichen in &lt;Parametern&gt;

{{% /tipp-head %}}

{{% tipp-body %}}

Manchmal enthalten Parameter &ndash; wie Datei- oder Verzeichnisnamen &ndash; Leerzeichen.
Weil das Leerzeichen in der Shell aber zur Trennung von Argumenten verwendet
weird, kommt es zu Konfliken. Man kann zur klaren Abgrenzum im Terminal seine
Parameter in Anführungszeichen setzen. Beispiel:

```powershell
> cd "C:\Program Files"
```

{{% /tipp-body %}}
{{% /tipp %}}

