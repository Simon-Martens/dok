---
weight: 1
Title: "Terminal Basics"
---

# Terminal Basics

## Unterschiede zwischen Windows, Mac und Linux

Das Terminal oder auch die *Shell* ist ein sehr mächtiges textbasiertes Werkzug und für viele Entwickler das Mittel der Wahl, um mit dem Computer zu interagieren. Dabei gibt es jedoch Unterschiede in der Verwendung und Verfügbarkeit von Befehlen in verschiedenen Betriebssystemen.

{{% columns %}}

### <i class="ri-windows-fill"></i> Windows

#### Programme

Unter Windows ist die sogenannte `PowerShell` vorinstalliert. Beide haben unterschiedliche Befehle und Syntax.
Im [Windows-Store](https://apps.microsoft.com/detail/9n0dx20hk701?rtc=1&hl=de-DE&gl=DE) oder auf über [GitHub](https://github.com/microsoft/terminal/releases) kann man sich das neue Windows Terminal herunterladen, das die PowerShell, die Eingabeaufforderung und Linux-Terminals in einer Anwendung vereint. Windows 11 hat das i.d.R. bereits integriert.

#### Kommandozeile

```powershell
C:\Users\username> 
```

Windows verwendet den *Laufwerksbuchstaben* und das *Arbeitsverzeichnis* als Prompt. Normalerweise startet die PowerShell im Benutzerverzeichnis.
Von hier aus kann man seine Dokumente, Downloads und andere Verzeichnisse erreichen.

#### Flags &amp; Parameter

```powershell
> befehl /flag parameter
```

Windows verwendet den Schrägstrich `/` als Flag-Präfix und trennt Flags und Parameter durch Leerzeichen.

#### Pfade

```powershell
C:\Users\username\Documents
```

Absolute Pfade in Windows beginnen mit dem Laufwerksbuchstaben und einem Doppelpunkt `C:\`. Relative Pfade beginnen mit dem Verzeichnisnamen. Zum Trennen von Pfadelementen wird der Backslash `\` verwendet.

<--->

### <i class="ri-apple-fill"></i> Mac / Linux

#### Programme

Unter Mac steht mit der `Terminal`-App ein vollwertiges `zsh`-Terminal zur Verfügung. Unter Linux gibt es verschiedene Emulatoren, wie `gnome-terminal`, `konsole` oder `xterm`, wobei meistens `bash` als Shell verwendet wird.

#### Kommandozeile

```bash
username@hostname:~$
username@hostname ~ %
```

Linux und Mac verwenden den *Benutzernamen*, den *Rechnernamen* und das *Arbeitsverzeichnis* als Prompt. Normalerweise startet die Shell im Benutzerverzeichnis. Besonderheit: das Home-Verzeichnis des gerade angemeldeten Benutzers wird mit `~` (=`/home/user/`) abgekürzt. Auch hier kann man von hier aus seine Dokumente, Downloads und andere Verzeichnisse erreichen.

#### Flags &amp; Parameter

```bash
$ befehl --flag -f parameter
```

Linux und Mac verwenden den Doppel-Bindestrich `--` (ausgeschrieben) oder `-` (abgekürzt) als Flag-Präfix und trennen Flags und Parameter durch Leerzeichen.

#### Pfade

```bash
/home/username/Documents
```

Absolute Pfade in Linux und Mac beginnen mit dem Wurzelverzeichnis `/`. Relative Pfade beginnen mit dem Verzeichnisnamen. Zum Trennen von Pfadelementen wird der Schrägstrich `/` verwendet.

{{% /columns %}}


## Hilfe

Kurzhilfe für die Verwendung eines Befehls kann man in der Regel auf unterschiedliche Art abfragen:

- <i class="ri-windows-fill"></i> `> git /?`
- <i class="ri-apple-fill"></i> / Linux `$ git --help` oder `$ git -h`

Linux und Max bieten zudem auch Handbücher zu vielen Befehlen im Terminal an, sogenannte *manpages*. Diese können mit dem Befehl `man <befehl>` aufgerufen werden, beispielsweise `man git`.


## Syntax
In der Hilfe und an dieser Stelle wird die Benutzung eine Befehls oft in einer formalen, aber einfachen [Syntax](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap12.html#tag_12_01) angegeben, die sich an folgendem Muster orientiert:

```bash
befehl [optional] <platzhalter>
```

Optionale Flags und Parameter werden in eckigen Klammern angegeben. Für Platzhalter, die in der Benutzung durch entsprechend eigene Werte zu ersetzen wären, stehen spitze Klammern. Beispiel:

```bash
git [-v | --version] [-h | --help] <command> [<args>]
```

Bedeutet, dass `git` mit den Flags `-v` oder `--version` und `-h` oder `--help` aufgerufen werden kann, sowie einem Befehl (wie `commit`, `add` etc.) und optionalen Argumenten.


