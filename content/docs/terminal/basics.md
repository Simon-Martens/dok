---
weight: 1
Title: "Terminal Basics"
---

# Terminal Basics

## Hilfe

Kurzhilfe für die Verwendung eines Befehls kann man in der Regel auf unterschiedliche Art abfragen: <i class="ri-arrow-left-up-line"></i>

- <i class="ri-windows-fill"></i> `> git /?`
- Linux / <i class="ri-apple-fill"></i> `$ git --help` oder `$ git -h`

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


