---
title: Schleifen
teaching: 40
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Schreiben Sie eine Schleife, die einen oder mehrere Befehle separat auf jede Datei in
  einer Gruppe von Dateien anwendet.
- Verfolgen Sie die Werte, die eine Schleifenvariable während der Ausführung der
  Schleife annimmt.
- Erkläre den Unterschied zwischen dem Namen einer Variablen und ihrem Wert.
- Erkläre, warum Leerzeichen und einige Satzzeichen nicht in Dateinamen verwendet werden
  sollten.
- Demonstrieren Sie, wie Sie sehen können, welche Befehle kürzlich ausgeführt worden
  sind.
- Wiederholung kürzlich ausgeführter Befehle, ohne sie neu zu tippen.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich die gleichen Aktionen für viele verschiedene Dateien durchführen?

::::::::::::::::::::::::::::::::::::::::::::::::::

**Schleifen** sind ein Programmierkonstrukt, das es uns ermöglicht, einen Befehl oder
eine Reihe von Befehlen für jedes Element in einer Liste zu wiederholen. Als solche sind
sie der Schlüssel zur Produktivitätssteigerung durch Automatisierung. Ähnlich wie bei
Platzhaltern und der Tabulatorvervollständigung reduziert die Verwendung von Schleifen
auch die Anzahl der erforderlichen Eingaben (und damit die Anzahl der Tippfehler).

Angenommen, wir haben mehrere hundert Genomdateien mit den Namen `basilisk.dat`,
`minotaur.dat` und `unicorn.dat`. Für dieses Beispiel verwenden wir das Verzeichnis
`exercise-data/creatures`, das nur drei Beispieldateien enthält, aber die Prinzipien
können auf viele weitere Dateien gleichzeitig angewendet werden.

Die Struktur dieser Dateien ist die gleiche: der gemeinsame Name, die Klassifizierung
und das Aktualisierungsdatum werden in den ersten drei Zeilen angegeben, die
DNA-Sequenzen in den folgenden Zeilen. Schauen wir uns die Dateien an:

```bash
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```

Wir möchten die Klassifizierung für jede Art ausgeben, die in der zweiten Zeile jeder
Datei angegeben ist. Für jede Datei müssten wir den Befehl `head -n 2` ausführen und
diesen an `tail -n 1` weiterleiten. Wir werden eine Schleife verwenden, um dieses
Problem zu lösen, aber sehen wir uns zunächst die allgemeine Form einer Schleife an,
indem wir den folgenden Pseudocode verwenden:

```bash
# The word "for" indicates the start of a "For-loop" command
for thing in list_of_things 
#The word "do" indicates the start of job execution list
do 
    # Indentation within the loop is not required, but aids legibility
    operation_using/command $thing 
# The word "done" indicates the end of a loop
done  
```

und wir können dies auf unser Beispiel wie folgt anwenden:

```bash
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     echo $filename
>     head -n 2 $filename | tail -n 1
> done
```

```output
basilisk.dat
CLASSIFICATION: basiliscus vulgaris
minotaur.dat
CLASSIFICATION: bos hominus
unicorn.dat
CLASSIFICATION: equus monoceros
```

::::::::::::::::::::::::::::::::::::::::: callout

## Folgen Sie der Eingabeaufforderung

Der Shell-Prompt wechselt von `$` zu `>` und wieder zurück, während wir in unserer
Schleife tippen. Der zweite Prompt, `>`, ist anders, um uns daran zu erinnern, dass wir
noch nicht mit der Eingabe eines kompletten Befehls fertig sind. Ein Semikolon, `;`,
kann verwendet werden, um zwei Befehle zu trennen, die in einer einzigen Zeile stehen.


::::::::::::::::::::::::::::::::::::::::::::::::::

Wenn die Shell das Schlüsselwort `for` sieht, weiß sie, dass sie einen Befehl (oder eine
Gruppe von Befehlen) für jedes Element in einer Liste einmal wiederholen muss. Jedes
Mal, wenn die Schleife läuft (Iteration genannt), wird ein Eintrag in der Liste der
Reihe nach der **Variablen** zugewiesen, und die Befehle innerhalb der Schleife werden
ausgeführt, bevor zum nächsten Eintrag in der Liste übergegangen wird. Innerhalb der
Schleife fragen wir den Wert der Variable ab, indem wir ihr `$` voranstellen. Das `$`
weist den Shell-Interpreter an, die Variable als Variablennamen zu behandeln und ihren
Wert an ihrer Stelle zu ersetzen, anstatt sie als Text oder externen Befehl zu
behandeln.

In diesem Beispiel besteht die Liste aus drei Dateinamen: `basilisk.dat`,
`minotaur.dat`, und `unicorn.dat`. Jedes Mal, wenn die Schleife durchläuft, verwenden
wir zunächst `echo`, um den Wert auszugeben, den die Variable `$filename` gerade hat.
Dies ist für das Ergebnis nicht notwendig, aber für uns hier von Vorteil, um leichter
folgen zu können. Als Nächstes führen wir den Befehl `head` in der Datei aus, auf die
`$filename` gerade verweist. Beim ersten Durchlauf der Schleife ist `$filename`
`basilisk.dat`. Der Interpreter führt den Befehl `head` auf `basilisk.dat` aus und
leitet die ersten beiden Zeilen an den Befehl `tail` weiter, der dann die zweite Zeile
von `basilisk.dat` ausgibt. Bei der zweiten Iteration wird `$filename` zu
`minotaur.dat`. Dieses Mal lässt die Shell `head` auf `minotaur.dat` laufen und leitet
die ersten beiden Zeilen an den Befehl `tail` weiter, der dann die zweite Zeile von
`minotaur.dat` ausgibt. Bei der dritten Iteration wird `$filename` zu `unicorn.dat`,
also führt die Shell den Befehl `head` auf dieser Datei aus, und `tail` auf der Ausgabe
davon. Da die Liste nur drei Einträge enthielt, verlässt die Shell die `for`-Schleife.

::::::::::::::::::::::::::::::::::::::::: callout

## Gleiche Symbole, unterschiedliche Bedeutungen

Hier sehen wir, dass `>` als Shell-Prompt verwendet wird, während `>` auch zur Umleitung
der Ausgabe verwendet wird. In ähnlicher Weise wird `$` als Shell-Prompt benutzt, aber,
wie wir zuvor gesehen haben, wird es auch benutzt, um die Shell zu bitten, den Wert
einer Variablen zu erhalten.

Wenn die *Shell* `>` oder `$` ausgibt, erwartet sie, dass Sie etwas eingeben, und das
Symbol ist ein Prompt.

Wenn *Sie* selbst `>` oder `$` eintippen, ist das eine Anweisung von Ihnen, dass die
Shell die Ausgabe umleiten oder den Wert einer Variablen holen soll.


::::::::::::::::::::::::::::::::::::::::::::::::::

Bei der Verwendung von Variablen ist es auch möglich, die Namen in geschweifte Klammern
zu setzen, um den Variablennamen klar abzugrenzen: `$filename` entspricht `${filename}`,
ist aber anders als `${file}name`. Diese Schreibweise finden Sie vielleicht auch in
anderen Programmen.

Wir haben die Variable in dieser Schleife `filename` genannt, um ihren Zweck für den
menschlichen Leser zu verdeutlichen. Der Shell selbst ist es egal, wie die Variable
genannt wird; wenn wir diese Schleife so schreiben würden:

```bash
$ for x in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $x | tail -n 1
> done
```

oder:

```bash
$ for temperature in basilisk.dat minotaur.dat unicorn.dat
> do
>     head -n 2 $temperature | tail -n 1
> done
```

Es würde genau so funktionieren. *Tun Sie das nicht.* Programme sind nur dann nützlich,
wenn die Leute sie verstehen können, daher erhöhen bedeutungslose Namen (wie `x`) oder
irreführende Namen (wie `temperature`) die Wahrscheinlichkeit, dass das Programm nicht
das tut, was seine Leser denken, dass es tut.

In den obigen Beispielen hätte man den Variablen (`thing`, `filename`, `x` und
`temperature`) jeden anderen Namen geben können, solange er sowohl für die Person, die
den Code schreibt, als auch für die Person, die ihn liest, sinnvoll ist.

Beachten Sie auch, dass Schleifen für andere Dinge als Dateinamen verwendet werden
können, wie z.B. eine Liste von Zahlen oder eine Teilmenge von Daten.

::::::::::::::::::::::::::::::::::::::: challenge

## Schreiben Sie Ihre eigene Schleife

Wie würden Sie eine Schleife schreiben, die alle 10 Zahlen von 0 bis 9 als Echo ausgibt?

::::::::::::::: solution

## Lösung

```bash
$ for loop_variable in 0 1 2 3 4 5 6 7 8 9
> do
>     echo $loop_variable
> done
```

```output
0
1
2
3
4
5
6
7
8
9
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Variablen in Schleifen

Diese Übung bezieht sich auf das Verzeichnis `shell-lesson-data/exercise-data/alkanes`.
`ls *.pdb` gibt die folgende Ausgabe:

```output
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

Was ist die Ausgabe des folgenden Codes?

```bash
$ for datafile in *.pdb
> do
>     ls *.pdb
> done
```

Wie lautet nun die Ausgabe des folgenden Codes?

```bash
$ for datafile in *.pdb
> do
>     ls $datafile
> done
```

Warum geben diese beiden Schleifen unterschiedliche Ergebnisse aus?

::::::::::::::: solution

## Lösung

Der erste Codeblock gibt bei jeder Iteration der Schleife die gleiche Ausgabe. Bash
erweitert den Platzhalter `*.pdb` innerhalb des Schleifenkörpers (sowie vor dem Start
der Schleife), um alle Dateien zu finden, die auf `.pdb` enden, und listet sie dann mit
`ls` auf. Die erweiterte Schleife würde wie folgt aussehen:

```bash
$ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> do
>     ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> done
```

```output
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

Der zweite Codeblock listet bei jeder Schleifeniteration eine andere Datei auf. Der Wert
der Variable `datafile` wird mit `$datafile` ausgewertet und dann mit `ls` aufgelistet.

```output
cubane.pdb
ethane.pdb
methane.pdb
octane.pdb
pentane.pdb
propane.pdb
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Begrenzung von Dateimengen

Was wäre die Ausgabe, wenn die folgende Schleife im Verzeichnis
`shell-lesson-data/exercise-data/alkanes` ausgeführt würde?

```bash
$ for filename in c*
> do
>     ls $filename
> done
```

1. Es sind keine Dateien aufgelistet.
2. Alle Dateien sind aufgelistet.
3. Nur `cubane.pdb`, `octane.pdb` und `pentane.pdb` sind aufgeführt.
4. Nur `cubane.pdb` ist aufgeführt.

::::::::::::::: solution

## Lösung

4 ist die richtige Antwort.`*` passt auf null oder mehr Zeichen, so dass jeder
Dateiname, der mit dem Buchstaben c beginnt, gefolgt von null oder mehr anderen Zeichen,
gefunden wird.


:::::::::::::::::::::::::

Wie würde sich die Ausgabe unterscheiden, wenn stattdessen dieser Befehl verwendet
würde?

```bash
$ for filename in *c*
> do
>     ls $filename
> done
```

1. Die gleichen Dateien würden aufgelistet werden.
2. Diesmal werden alle Dateien aufgelistet.
3. Diesmal werden keine Dateien aufgelistet.
4. Die Dateien `cubane.pdb` und `octane.pdb` werden aufgelistet.
5. Es wird nur die Datei `octane.pdb` aufgelistet.

::::::::::::::: solution

## Lösung

4 ist die richtige Antwort.`*` passt auf null oder mehr Zeichen, also wird ein Dateiname
mit null oder mehr Zeichen vor dem Buchstaben c und null oder mehr Zeichen nach dem
Buchstaben c gefunden.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Speichern in einer Datei in einer Schleife - Teil eins

Was ist die Auswirkung dieser Schleife im Verzeichnis
`shell-lesson-data/exercise-data/alkanes`?

```bash
for alkanes in *.pdb
do
    echo $alkanes
    cat $alkanes > alkanes.pdb
done
```

1. Druckt `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, `pentane.pdb` und
   `propane.pdb`, und der Text von `propane.pdb` wird in einer Datei namens
   `alkanes.pdb` gespeichert.
2. Druckt `cubane.pdb`, `ethane.pdb` und `methane.pdb`, und der Text aus allen drei
   Dateien wird zusammengefügt und in einer Datei namens `alkanes.pdb` gespeichert.
3. Druckt `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`, und `pentane.pdb`,
   und der Text von `propane.pdb` wird in einer Datei namens `alkanes.pdb` gespeichert.
4. Keine der oben genannten.

::::::::::::::: solution

## Lösung

1. Der Text aus jeder Datei wird der Reihe nach in die Datei `alkanes.pdb` geschrieben.
   Allerdings wird die Datei bei jedem Schleifendurchlauf überschrieben, so dass der
   endgültige Inhalt von `alkanes.pdb` der Text aus der Datei `propane.pdb` ist.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Speichern in einer Datei in einer Schleife - Teil Zwei

Was wäre die Ausgabe der folgenden Schleife, ebenfalls im Verzeichnis
`shell-lesson-data/exercise-data/alkanes`?

```bash
for datafile in *.pdb
do
    cat $datafile >> all.pdb
done
```

1. Der gesamte Text von `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb` und
   `pentane.pdb` würde verkettet und in einer Datei namens `all.pdb` gespeichert.
2. Der Text von `ethane.pdb` wird in einer Datei namens `all.pdb` gespeichert.
3. Der gesamte Text von `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`,
   `pentane.pdb` und `propane.pdb` würde konkateniert und in einer Datei namens
   `all.pdb` gespeichert.
4. Der gesamte Text von `cubane.pdb`, `ethane.pdb`, `methane.pdb`, `octane.pdb`,
   `pentane.pdb` und `propane.pdb` würde auf dem Bildschirm ausgegeben und in einer
   Datei namens `all.pdb` gespeichert.

::::::::::::::: solution

## Lösung

3 ist die richtige Antwort. `>>` hängt an eine Datei an, anstatt sie mit der
umgeleiteten Ausgabe eines Befehls zu überschreiben. Da die Ausgabe des Befehls `cat`
umgeleitet wurde, wird nichts auf dem Bildschirm ausgegeben.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Lassen Sie uns mit unserem Beispiel im Verzeichnis
`shell-lesson-data/exercise-data/creatures` fortfahren. Hier ist eine etwas
kompliziertere Schleife:

```bash
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
```

Die Shell beginnt mit der Expansion von `*.dat`, um die Liste der zu verarbeitenden
Dateien zu erstellen. Der **Schleifenkörper** führt dann zwei Befehle für jede dieser
Dateien aus. Der erste Befehl, `echo`, gibt seine Befehlszeilenargumente auf der
Standardausgabe aus. Zum Beispiel:

```bash
$ echo hello there
```

druckt:

```output
hello there
```

Da die Shell in diesem Fall `$filename` als Name einer Datei expandiert, gibt `echo
$filename` den Namen der Datei aus. Beachten Sie, dass wir dies nicht so schreiben
können:

```bash
$ for filename in *.dat
> do
>     $filename
>     head -n 100 $filename | tail -n 20
> done
```

weil dann beim ersten Durchlauf der Schleife, wenn `$filename` zu `basilisk.dat`
expandiert, die Shell versuchen würde, `basilisk.dat` als Programm auszuführen.
Schließlich wählt die Kombination `head` und `tail` die Zeilen 81-100 aus der zu
verarbeitenden Datei aus (vorausgesetzt, die Datei hat mindestens 100 Zeilen).

::::::::::::::::::::::::::::::::::::::::: callout

## Leerzeichen in Namen

Leerzeichen werden verwendet, um die Elemente der Liste zu trennen, über die wir eine
Schleife laufen lassen wollen. Wenn eines dieser Elemente ein Leerzeichen enthält,
müssen wir es mit Anführungszeichen umgeben und dasselbe mit unserer Schleifenvariablen
tun. Angenommen, unsere Datendateien sind benannt:

```source
red dragon.dat
purple unicorn.dat
```

Um eine Schleife über diese Dateien zu ziehen, müssten wir doppelte Anführungszeichen
wie folgt hinzufügen:

```bash
$ for filename in "red dragon.dat" "purple unicorn.dat"
> do
>     head -n 100 "$filename" | tail -n 20
> done
```

Es ist einfacher, Leerzeichen (oder andere Sonderzeichen) in Dateinamen zu vermeiden.

Die obigen Dateien existieren nicht, wenn wir also den obigen Code ausführen, kann der
Befehl `head` sie nicht finden; die zurückgegebene Fehlermeldung zeigt jedoch den Namen
der erwarteten Dateien an:

```error
head: cannot open ‘red dragon.dat' for reading: No such file or directory
head: cannot open ‘purple unicorn.dat' for reading: No such file or directory
```

Versuchen Sie, die Anführungszeichen um `$filename` in der obigen Schleife zu entfernen,
um den Effekt der Anführungszeichen auf Leerzeichen zu sehen. Beachten Sie, dass wir ein
Ergebnis des Schleifenbefehls für unicorn.dat erhalten, wenn wir diesen Code im
Verzeichnis `creatures` ausführen:

```output
head: cannot open ‘red' for reading: No such file or directory
head: cannot open ‘dragon.dat' for reading: No such file or directory
head: cannot open ‘purple' for reading: No such file or directory
CGGTACCGAA
AAGGGTCGCG
CAAGTGTTCC
...
```

::::::::::::::::::::::::::::::::::::::::::::::::::

Wir möchten jede der Dateien in `shell-lesson-data/exercise-data/creatures` ändern, aber
auch eine Version der Originaldateien speichern. Wir wollen die Originaldateien in neue
Dateien mit den Namen `original-basilisk.dat` und `original-unicorn.dat` kopieren. Wir
können nicht verwenden:

```bash
$ cp *.dat original-*.dat
```

aus, denn das würde expandieren zu:

```bash
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
```

Dies würde unsere Dateien nicht sichern, stattdessen bekommen wir einen Fehler:

```error
cp: target `original-*.dat' is not a directory
```

Dieses Problem tritt auf, wenn `cp` mehr als zwei Eingaben erhält. Wenn das passiert,
erwartet es, dass die letzte Eingabe ein Verzeichnis ist, in das es alle Dateien
kopieren kann, die ihm übergeben wurden. Da es im Verzeichnis `creatures` kein
Verzeichnis namens `original-*.dat` gibt, erhalten wir einen Fehler.

Stattdessen können wir eine Schleife verwenden:

```bash
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
```

Diese Schleife führt den Befehl `cp` einmal für jeden Dateinamen aus. Beim ersten Mal,
wenn sich `$filename` zu `basilisk.dat` ausdehnt, führt die Shell ihn aus:

```bash
cp basilisk.dat original-basilisk.dat
```

Das zweite Mal lautet der Befehl:

```bash
cp minotaur.dat original-minotaur.dat
```

Das dritte und letzte Mal lautet der Befehl:

```bash
cp unicorn.dat original-unicorn.dat
```

Da der Befehl `cp` normalerweise keine Ausgabe erzeugt, ist es schwer zu überprüfen, ob
die Schleife korrekt funktioniert. Wir haben jedoch bereits gelernt, wie man
Zeichenketten mit `echo` ausgibt, und wir können die Schleife so modifizieren, dass sie
`echo` verwendet, um unsere Befehle auszugeben, ohne sie tatsächlich auszuführen. So
können wir prüfen, welche Befehle in der unveränderten Schleife ausgeführt werden
*würden*.

Das folgende Diagramm zeigt, was passiert, wenn die geänderte Schleife ausgeführt wird,
und demonstriert, dass die vernünftige Verwendung von `echo` eine gute Debugging-Technik
ist.

![](fig/shell_script_for_loop_flow_chart.svg){alt="Die for-Schleife "for filename in
.dat; do echo cp $filename original-$filename;done" weist der Variablen "$filename"
nacheinander die Namen aller ".dat"-Dateien in Ihrem aktuellen Verzeichnis zu und führt
dann den Befehl aus. Mit den Dateien "basilisk.dat", "minotaur.dat" und "unicorn.dat" im
aktuellen Verzeichnis wird die Schleife nacheinander dreimal den Befehl echo aufrufen
und drei Zeilen ausgeben: "cp basislisk.dat original-basilisk.dat", dann "cp
minotaur.datoriginal-minotaur.dat" und schließlich "cp
unicorn.datoriginal-unicorn.dat""}

## Nelle's Pipeline: Verarbeitung von Dateien

Nelle ist nun bereit, ihre Datendateien mit Hilfe von `goostats.sh` --- einem von ihrem
Betreuer geschriebenen Shell-Skript zu verarbeiten. Dieses Skript berechnet einige
Statistiken aus einer Protein-Probendatei und nimmt zwei Argumente entgegen:

1. eine Eingabedatei (die die Rohdaten enthält)
2. eine Ausgabedatei (um die berechneten Statistiken zu speichern)

Da sie immer noch lernt, wie man die Shell benutzt, beschließt sie, die benötigten
Befehle schrittweise aufzubauen. Ihr erster Schritt ist es, sicherzustellen, dass sie
die richtigen Eingabedateien auswählen kann --- erinnern Sie sich, das sind diejenigen,
deren Namen auf 'A' oder 'B' enden, und nicht auf 'Z'. Nelle wechselt in das Verzeichnis
`north-pacific-gyre` und tippt:

```bash
$ cd
$ cd Desktop/shell-lesson-data/north-pacific-gyre
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile
> done
```

```output
NENE01729A.txt
NENE01736A.txt
NENE01751A.txt

...
NENE02040B.txt
NENE02043B.txt
```

Ihr nächster Schritt besteht darin, zu entscheiden, wie die Dateien heißen sollen, die
das Analyseprogramm `goostats.sh` erstellen wird. Es scheint einfach zu sein, den Namen
jeder Eingabedatei mit "stats" voranzustellen, also modifiziert sie ihre Schleife, um
dies zu tun:

```bash
$ for datafile in NENE*A.txt NENE*B.txt
> do
>     echo $datafile stats-$datafile
> done
```

```output
NENE01729A.txt stats-NENE01729A.txt
NENE01736A.txt stats-NENE01729A.txt
NENE01751A.txt stats-NENE01729A.txt
...
NENE02040B.txt stats-NENE02040B.txt
NENE02043B.txt stats-NENE02043B.txt
```

Sie hat `goostats.sh` noch nicht wirklich ausgeführt, aber jetzt ist sie sicher, dass
sie die richtigen Dateien auswählen und die richtigen Ausgabedateinamen erzeugen kann.

Das wiederholte Eingeben von Befehlen wird jedoch mühsam, und Nelle hat Angst, Fehler zu
machen, also drückt sie, anstatt ihre Schleife erneut einzugeben, <kbd>↑</kbd>.
Daraufhin gibt die Shell die gesamte Schleife in einer Zeile wieder (mit Semikolons zur
Trennung der Teile):

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile stats-$datafile; done
```

Mit Hilfe des <kbd>←</kbd> navigiert Nelle zu dem Befehl `echo` und ändert ihn in `bash
goostats.sh`:

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
```

Wenn sie <kbd>Enter</kbd> drückt, führt die Shell den geänderten Befehl aus. Es scheint
jedoch nichts zu passieren - es gibt keine Ausgabe. Nach einem Moment wird Nelle klar,
dass sie, da ihr Skript nichts mehr auf dem Bildschirm ausgibt, keine Ahnung hat, ob es
läuft, geschweige denn wie schnell. Sie beendet den laufenden Befehl, indem sie
<kbd>Strg</kbd>\+<kbd>C</kbd> eintippt, verwendet <kbd>↑</kbd>, um den Befehl zu
wiederholen, und ändert ihn so ab, dass er lautet:

```bash
$ for datafile in NENE*A.txt NENE*B.txt; do echo $datafile;
bash goostats.sh $datafile stats-$datafile; done
```

::::::::::::::::::::::::::::::::::::::::: callout

## Anfang und Ende

Wir können an den Anfang einer Zeile in der Shell gehen, indem wir
<kbd>Strg</kbd>\+<kbd>A</kbd> eingeben und an das Ende mit
<kbd>Strg</kbd>\+<kbd>E</kbd>.


::::::::::::::::::::::::::::::::::::::::::::::::::

Wenn sie ihr Programm jetzt ausführt, produziert es alle fünf Sekunden oder so eine
Zeile an Ausgabe:

```output
NENE01729A.txt
NENE01736A.txt
NENE01751A.txt
...
```

1518 mal 5 Sekunden, geteilt durch 60, sagt ihr, dass ihr Skript etwa zwei Stunden für
die Ausführung brauchen wird. Als letzte Kontrolle öffnet sie ein weiteres
Terminalfenster, geht in `north-pacific-gyre` und benutzt `cat stats-NENE01729B.txt`, um
eine der Ausgabedateien zu untersuchen. Es sieht gut aus, also beschließt sie, sich
einen Kaffee zu holen und ihre Lektüre fortzusetzen.

::::::::::::::::::::::::::::::::::::::::: callout

## Diejenigen, die die Geschichte kennen, können wählen, sie zu wiederholen

Eine andere Möglichkeit, frühere Arbeiten zu wiederholen, ist die Verwendung des Befehls
`history`, um eine Liste der letzten paar hundert Befehle zu erhalten, die ausgeführt
wurden, und dann `!123` (wobei '123' durch die Befehlsnummer ersetzt wird) zu verwenden,
um einen dieser Befehle zu wiederholen. Wenn Nelle zum Beispiel dies tippt:

```bash
$ history | tail -n 5
```

```output
456  for datafile in NENE*A.txt NENE*B.txt; do   echo $datafile stats-$datafile; done
457  for datafile in NENE*A.txt NENE*B.txt; do echo $datafile stats-$datafile; done
458  for datafile in NENE*A.txt NENE*B.txt; do bash goostats.sh $datafile stats-$datafile; done
459  for datafile in NENE*A.txt NENE*B.txt; do echo $datafile; bash goostats.sh $datafile
stats-$datafile; done
460  history | tail -n 5
```

dann kann sie `goostats.sh` auf den Dateien erneut ausführen, indem sie einfach `!459`
eingibt.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Andere History-Befehle

Es gibt eine Reihe anderer Kurzbefehle, um auf die Historie zuzugreifen.

- <kbd>Strg</kbd>\+<kbd>R</kbd> schaltet in den History-Suchmodus 'reverse-i-search' und
  findet den letzten Befehl in Ihrer History, der mit dem Text übereinstimmt, den Sie
  als nächstes eingeben. Drücken Sie <kbd>Strg</kbd>\+<kbd>R</kbd> ein oder mehrere
  Male, um nach früheren Übereinstimmungen zu suchen. Sie können dann mit der linken und
  rechten Pfeiltaste diese Zeile auswählen und bearbeiten und dann <kbd>Return</kbd>
  drücken, um den Befehl auszuführen.
- `!!` ruft den unmittelbar vorhergehenden Befehl auf (Sie können dies bequemer finden
  als <kbd>↑</kbd>)
- `!$` holt das letzte Wort des letzten Befehls. Das ist öfter nützlich als man denkt:
  nach `bash goostats.sh NENE01729B.txt stats-NENE01729B.txt` kann man `less !$`
  eingeben, um sich die Datei `stats-NENE01729B.txt` anzusehen, was schneller ist als
  <kbd>↑</kbd> und die Befehlszeile zu bearbeiten.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Durchführung eines Trockenlaufs

Eine Schleife ist eine Möglichkeit, viele Dinge auf einmal zu tun --- oder viele Fehler
auf einmal zu machen, wenn sie das Falsche tut. Eine Möglichkeit zu überprüfen, was eine
Schleife tun *würde*, ist, die Befehle, die sie ausführen würde, zu `echo`, anstatt sie
tatsächlich auszuführen.

Angenommen, wir wollen eine Vorschau auf die Befehle, die die folgende Schleife
ausführen wird, ohne diese Befehle tatsächlich auszuführen:

```bash
$ for datafile in *.pdb
> do
>     cat $datafile >> all.pdb
> done
```

Was ist der Unterschied zwischen den beiden Schleifen unten, und welche würden wir
ausführen wollen?

```bash
# Version 1
$ for datafile in *.pdb
> do
>     echo cat $datafile >> all.pdb
> done
```

```bash
# Version 2
$ for datafile in *.pdb
> do
>     echo "cat $datafile >> all.pdb"
> done
```

::::::::::::::: solution

## Lösung

Die zweite Version ist die, die wir ausführen wollen. Sie gibt alles, was in den
Anführungszeichen steht, auf dem Bildschirm aus, wobei der Name der Schleifenvariablen
erweitert wird, da wir ihm ein Dollarzeichen vorangestellt haben. Sie *verändert* auch
nicht die Datei `all.pdb`, da `>>` wörtlich als Teil einer Zeichenkette und nicht als
Umleitungsanweisung behandelt wird.

Die erste Version hängt die Ausgabe des Befehls `echo cat $datafile` an die Datei
`all.pdb` an. Diese Datei enthält nur die Liste; `cat cubane.pdb`, `cat ethane.pdb`,
`cat methane.pdb` usw.

Probieren Sie beide Versionen aus, um die Ausgabe zu sehen! Öffnen Sie unbedingt die
Datei `all.pdb`, um ihren Inhalt zu sehen.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Verschachtelte Schleifen

Angenommen, wir wollen eine Verzeichnisstruktur einrichten, um einige Experimente zur
Messung der Reaktionsgeschwindigkeitskonstanten mit verschiedenen Verbindungen *und*
verschiedenen Temperaturen zu organisieren. Was wäre das Ergebnis des folgenden Codes:

```bash
$ for species in cubane ethane methane
> do
>     for temperature in 25 30 37 40
>     do
>         mkdir $species-$temperature
>     done
> done
```

::::::::::::::: solution

## Lösung

Wir haben eine geschachtelte Schleife, d.h. innerhalb einer anderen Schleife, so dass
für jede Art in der äußeren Schleife die innere Schleife (die geschachtelte Schleife)
über die Liste der Temperaturen iteriert und für jede Kombination ein neues Verzeichnis
erstellt.

Versuchen Sie, den Code selbst auszuführen, um zu sehen, welche Verzeichnisse erstellt
werden!



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Eine `for`-Schleife wiederholt die Befehle einmal für jedes Ding in einer Liste.
- Jede `for`-Schleife braucht eine Variable, die auf das Ding verweist, mit dem sie
  gerade arbeitet.
- Verwenden Sie `$name`, um eine Variable zu expandieren (d.h. ihren Wert zu erhalten).
  auch `${name}` kann verwendet werden.
- Verwenden Sie keine Leerzeichen, Anführungszeichen oder Platzhalterzeichen wie '\*'
  oder '?' in Dateinamen, da dies die Variablenexpansion erschwert.
- Geben Sie den Dateien konsistente Namen, die leicht mit Wildcard-Mustern
  übereinstimmen, um die Auswahl für die Schleife zu vereinfachen.
- Benutzen Sie die Pfeil-nach-oben-Taste, um durch die vorherigen Befehle zu blättern
  und sie zu bearbeiten und zu wiederholen.
- Verwenden Sie <kbd>Strg</kbd>\+<kbd>R</kbd>, um die zuvor eingegebenen Befehle zu
  durchsuchen.
- Verwenden Sie `history`, um die letzten Befehle anzuzeigen, und `![number]`, um einen
  Befehl nach Nummer zu wiederholen.

::::::::::::::::::::::::::::::::::::::::::::::::::



