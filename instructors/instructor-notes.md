---
title: Hinweise für den Kursleiter
---


- Warum lernen wir, die Shell zu benutzen?
  - Ermöglicht es Benutzern, sich wiederholende Aufgaben zu automatisieren
  - Und erfassen Sie kleine Datenmanipulationsschritte, die normalerweise nicht
    aufgezeichnet werden, um die Forschung reproduzierbar zu machen
- Das Problem
  - Die Ausführung desselben Arbeitsablaufs für mehrere Proben kann unnötig
    arbeitsintensiv sein
  - Manuelle Manipulation von Datendateien:
    - ist oft nicht in der Dokumentation erfasst
    - ist schwer zu reproduzieren
    - ist schwer zu beheben, zu überprüfen oder zu verbessern
- Die Shell
  - Arbeitsabläufe können durch die Verwendung von Shell-Skripten automatisiert werden
  - Eingebaute Befehle ermöglichen eine einfache Datenmanipulation (z.B. sort, grep,
    etc.)
  - Jeder Schritt kann im Shell-Skript festgehalten werden und ermöglicht so die
    Reproduzierbarkeit und einfache Fehlersuche

## Insgesamt

Viele Leute haben sich gefragt, ob wir die Shell noch unterrichten sollten. Schließlich
kann jeder, der mehrere tausend Datendateien umbenennen möchte, dies leicht interaktiv
im Python-Interpreter tun, und jeder, der ernsthafte Datenanalysen durchführt, wird
wahrscheinlich den Großteil seiner Arbeit im IPython Notebook oder R Studio erledigen.
Warum also die Shell lehren?

Die erste Antwort lautet: "Weil so viel anderes davon abhängt." Das Installieren von
Software, das Konfigurieren Ihres Standard-Editors und das Steuern von entfernten
Rechnern setzt häufig eine grundlegende Vertrautheit mit der Shell und damit verbundenen
Begriffen wie Standardeingabe und -ausgabe voraus. Viele Werkzeuge verwenden auch ihre
Terminologie (zum Beispiel die magischen Befehle `%ls` und `%cd` in IPython).

Die zweite Antwort lautet: "Weil es eine einfache Möglichkeit ist, einige grundlegende
Ideen über den Umgang mit Computern zu vermitteln." Wenn wir den Teilnehmern beibringen,
wie man die Unix-Shell benutzt, bringen wir ihnen bei, dass sie den Computer dazu
bringen sollten, Dinge zu wiederholen (durch Tabulator-Vervollständigung, `!` gefolgt
von einer Befehlsnummer und `for`-Schleifen), anstatt sie selbst zu wiederholen. Wir
bringen ihnen auch bei, Dinge, die sie häufig tun, für eine spätere Wiederverwendung zu
speichern (über Shell-Skripte), Dingen sinnvolle Namen zu geben und ein wenig
Dokumentation zu schreiben (z. B. Kommentare am Anfang von Shell-Skripten), um das Leben
ihrer zukünftigen Selbst zu verbessern.

Die dritte Antwort lautet: "Weil sie die Nutzung vieler domänenspezifischer Werkzeuge
und Rechenressourcen ermöglicht, auf die Forscher sonst keinen Zugriff haben." Die
Vertrautheit mit der Shell ist sehr nützlich für den Fernzugriff auf Maschinen, die
Nutzung der Infrastruktur für Hochleistungsrechner und die Ausführung neuer
Spezialwerkzeuge in vielen Disziplinen. Wir lehren hier keine HPC- oder
domänenspezifischen Fähigkeiten, sondern legen den Grundstein für die weitere
Entwicklung dieser Fähigkeiten. Insbesondere das Verständnis der Syntax von Befehlen,
Flags und Hilfesystemen ist für domänenspezifische Tools nützlich und das Verständnis
des Dateisystems (und wie man darin navigiert) ist für den Fernzugriff nützlich.

Schließlich, und das ist vielleicht das Wichtigste, können wir den Teilnehmern durch das
Erlernen der Shell beibringen, über das Programmieren im Sinne der Funktionskomposition
nachzudenken. Im Fall der Shell nimmt dies die Form von Pipelines anstelle von
verschachtelten Funktionsaufrufen an, aber der Kerngedanke von "kleinen Stücken, lose
verbunden" ist derselbe.

Der gesamte Stoff kann in drei Stunden behandelt werden, sofern die Lernenden, die
Windows verwenden, nicht auf Hindernisse stoßen wie:

- nicht herausfinden können, wo ihr Home-Verzeichnis ist (besonders wenn sie Cygwin
  benutzen);
- nicht in der Lage, einen einfachen Texteditor auszuführen; und
- die Shell weigert sich, Skripte auszuführen, die DOS-Zeilenenden enthalten.

## Vorbereitung auf den Unterricht

- Verwenden Sie das Verzeichnis `data` für die Übungen im Workshop und die
  Live-Programmierbeispiele. Sie können das Verzeichnis shell-novice klonen oder die
  Schaltfläche *ZIP herunterladen* auf der rechten Seite verwenden, um das gesamte
  [Git-Repository] (https://github.com/swcarpentry/shell-novice) zu erhalten. Wir bieten
  jetzt auch eine Zip-Datei des `data`-Verzeichnisses auf der
  [Setup-Seite](../learners/setup.md).

- Website: Es wurden verschiedene Praktiken angewandt.

  - Option 1: Sie können den Lernenden vor der Lektion Links geben, damit sie folgen,
    aufholen und Übungen sehen können (besonders, wenn Sie dem Inhalt der Lektion ohne
    viele Änderungen folgen).
  - Option 2: Zeigen Sie den Lernenden die Website nicht während des Unterrichts, da
    dies ablenkend wirken kann: Die Schüler lesen vielleicht, anstatt zuzuhören, und ein
    weiteres geöffnetes Fenster stellt eine zusätzliche kognitive Belastung dar.
  - Stellen Sie auf jeden Fall sicher, dass Sie auf die Website als Referenz nach dem
    Workshop verweisen.

- Inhalt: Wenn Sie nicht wirklich viel Zeit haben (4+ Stunden), werden Sie
  wahrscheinlich nicht ALLE Inhalte dieser Lektion in einer einzigen halbtägigen Sitzung
  behandeln können. Planen Sie im Voraus, was Sie auslassen könnten, was Sie wirklich
  betonen wollen, usw.

- Übungen: Überlegen Sie sich im Voraus, wie Sie die Übungen während des Unterrichts
  behandeln wollen. Wie werden Sie sie zuweisen (Website, Folie, Handout)? Sollen alle
  die Aufgabe lösen und Sie zeigen dann die Lösung? Lassen Sie einen Lernenden die
  Lösung zeigen? Lassen Sie die Gruppen jeweils eine andere Übung machen und ihre
  Lösungen präsentieren?

- Die [Referenzseite](../learners/reference.md) kann ausgedruckt und den Studenten als
  Referenz gegeben werden, ganz wie Sie wollen.

- Andere Vorbereitungen: Es steht Ihnen frei, eigene Beispiele oder Kommentare
  hinzuzufügen, aber Sie sollten wissen, dass dies nicht notwendig ist: Die Themen und
  Befehle können so unterrichtet werden, wie sie auf den Lektionsseiten angegeben sind.
  Wenn Sie der Meinung sind, dass die Lektion an einer Stelle fehlt, können Sie gerne
  einen Fehler melden oder einen Pull-Request einreichen.

## Lehrnotizen

- Super coole Online-Ressource! [http://explainshell.com/](https://explainshell.com/)
  zerlegt jeden Shell-Befehl, den Sie eingeben, und zeigt zu jedem Teil einen Hilfetext
  an. Ein weiteres nettes Handbuch-Tool ist [http://tldr.sh/](https://tldr.sh/) mit
  kurzen, sehr anschaulichen Handbüchern für Shell-Befehle, nützlich vor allem unter
  Windows bei der Verwendung von Git BASH, wo `man` nicht funktioniert.

- Eine weitere supercoole Online-Ressource ist
  [http://www.shellcheck.net](https://www.shellcheck.net), die Shell-Skripte (sowohl
  hochgeladene als auch eingetippte) auf häufige Fehler überprüft.

- Ressourcen zum "Aufteilen" Ihrer Shell, damit die letzten Befehle im Blick bleiben:
  [https://github.com/rgaiacs/swc-shell-split-window](https://github.com/rgaiacs/swc-shell-split-window).

- Tabulatorvervollständigung klingt wie eine Kleinigkeit: ist es aber nicht. Die
  Wiederholung alter Befehle mit `!123` oder `!wc` ist auch keine Kleinigkeit, ebenso
  wenig wie Wildcard-Expansion und `for`-Schleifen. Jede dieser Möglichkeiten ist eine
  Gelegenheit, eine der großen Ideen des Software Carpentry zu wiederholen: Wenn der
  Computer sie wiederholen *kann*, wird irgendein Programmierer irgendwo mit ziemlicher
  Sicherheit einen Weg gefunden haben, damit der Computer sie wiederholen *kann*.

- Das Erstellen einer Pipeline mit vier oder fünf Schritten, das anschließende Einfügen
  in ein Shell-Skript zur Wiederverwendung und das Aufrufen dieses Skripts innerhalb
  einer `for`-Schleife ist eine gute Gelegenheit, um zu zeigen, wie "sieben plus oder
  minus zwei" mit dem Programmieren zusammenhängt. Sobald wir herausgefunden haben, wie
  wir etwas einigermaßen Kompliziertes machen können, machen wir es wiederverwendbar und
  geben ihm einen Namen, damit es nur einen Platz im Arbeitsspeicher einnimmt und nicht
  mehrere. Es ist auch eine gute Gelegenheit, über exploratives Programmieren zu
  sprechen: Anstatt ein Programm im Voraus zu entwerfen, können wir ein paar nützliche
  Dinge tun und dann im Nachhinein entscheiden, welche davon es wert sind, für die
  zukünftige Wiederverwendung gekapselt zu werden.

- Wenn alles gut läuft, können Sie darauf hinweisen, dass Dateierweiterungen im
  Wesentlichen dazu da sind, Computern (und menschlichen Lesern) zu helfen, den Inhalt
  von Dateien zu verstehen, und keine Voraussetzung für Dateien sind (kurz behandelt in
  [Navigieren in Dateien und Verzeichnissen](../episodes/02-filedir.md)). Dies kann im
  Abschnitt [Pipes und Filter](../episodes/04-pipefilter.md) geschehen, indem Sie
  zeigen, dass Sie die Standardausgabe in eine Datei ohne die Erweiterung .txt umleiten
  können (z.B. Längen), und dass die resultierende Datei immer noch eine vollkommen
  brauchbare Textdatei ist. Weisen Sie darauf hin, dass der Computer Sie bei einem
  Doppelklick in der grafischen Benutzeroberfläche wahrscheinlich fragen wird, was Sie
  tun wollen.

- Aus Zeitgründen müssen wir viele wichtige Dinge weglassen, darunter
  Dateiberechtigungen, Job Control und SSH. Wenn die Lernenden den grundlegenden Stoff
  bereits verstehen, können diese Themen stattdessen anhand der Online-Lektionen
  behandelt werden. Diese Einschränkungen haben auch Konsequenzen für die Folgekurse:

- Es ist schwer, über `#!` (shebang) zu diskutieren, ohne zuerst über Berechtigungen zu
  sprechen, was wir nicht tun. `#!` ist auch [ziemlich kompliziert][shebang], also
  selbst wenn wir Berechtigungen diskutieren würden, würden wir wahrscheinlich immer
  noch nicht `#!` diskutieren wollen.

- Die Installation der Bash und eines vernünftigen Satzes von Unix-Befehlen unter
  Windows ist immer mit etwas Tüftelei und Frustration verbunden. Bitte sehen Sie sich
  die neuesten Installationsrichtlinien an und probieren Sie es selbst aus, *bevor* Sie
  eine Klasse unterrichten.

- Standardmäßig haben Sie möglicherweise eine lange Reihe von Informationen an Ihre
  Eingabeaufforderung in Git Bash angehängt. Um das "Rauschen" zu reduzieren und mit
  einer übersichtlicheren Eingabeaufforderung fortzufahren, geben Sie den Befehl ein:

  ```bash
  PS1='$ '
  ```

- Auf Windows-Rechnern, auf denen `nano` nicht ordnungsgemäß mit dem [Software Carpentry
  Windows Installer][windows-installer] installiert wurde, ist es möglich, `notepad` als
  Alternative zu verwenden. Es wird eine GUI-Schnittstelle geben und Zeilenenden werden
  anders behandelt, aber ansonsten können `notepad` und `nano` für die Zwecke dieser
  Lektion fast austauschbar verwendet werden.

- Unter Windows sieht es so aus:

  ```bash
  $ cd
  $ cd Desktop
  ```

  wird immer jemanden auf seinen Desktop setzen (es sei denn, sein Rechner ist mit dem
  OneDrive des Unternehmens gesichert, siehe nächster Punkt). Lassen Sie sie das
  Beispielverzeichnis für die Shell-Übungen dort anlegen, damit sie es leicht finden und
  seine Entwicklung beobachten können.

- Wenn ein Windows-Rechner mit OneDrive gesichert ist, kann es sein, dass der
  GUI-Desktop aus einem Ordner in OneDrive gerendert wird, der nicht mit dem Inhalt von
  `~/Desktop` übereinstimmt. Der OneDrive-Desktop sollte mit einem der folgenden Befehle
  aufgerufen werden können (wenn der Name des Unternehmens nicht klar ist, sehen Sie
  sich die Ausgabe von `ls` an, um den richtigen Ordner zu finden):

  ```bash
  $ cd "~/OneDrive - Name Of Enterprise/Desktop"
  $ cd "C:/Users/Username/OneDrive - Name Of Enterprise/Desktop"
  ```

  Eine Möglichkeit, zu erkennen, ob der Computer diese Art von Konfiguration verwendet,
  ist, sich Dateien, Ordner oder Verknüpfungen auf dem Desktop anzusehen. Normalerweise
  enthält das Symbol eine Verknüpfung/ein Pfeilsymbol, wenn es sich um einen Link
  handelt, oder nur das einfache Symbol, wenn die Datei nur im Ordner `Desktop`
  gespeichert ist. Mit OneDrive synchronisierte Dateien enthalten ein zusätzliches
  Symbol, das den Synchronisierungsstatus anzeigt (typischerweise blaue Pfeile für
  "Synchronisierung ausstehend" oder ein grünes Häkchen für "synchronisiert").

- Bleiben Sie innerhalb der POSIX-kompatiblen Befehle, wie es alle Lehrmaterialien tun.
  Ihre spezielle Shell verfügt möglicherweise über Erweiterungen, die über POSIX
  hinausgehen und auf anderen Rechnern nicht zur Verfügung stehen, insbesondere bei den
  Standard-Bash-Emulatoren für macOS und Windows. Zum Beispiel hat POSIX `ls` keine
  `--ignore=` oder `-I` Option, und POSIX `head` nimmt `-n 10` oder `-10`, aber nicht
  die lange Form von `--lines=10`.

## Windows

Die Installation der Bash und eines vernünftigen Satzes von Unix-Befehlen unter Windows
ist immer mit etwas Tüftelei und Frustration verbunden. Bitte sehen Sie sich die
neuesten Installationsrichtlinien an und probieren Sie es selbst aus, *bevor* Sie eine
Klasse unterrichten. Zu den von uns untersuchten Optionen gehören:

1. [msysGit](https://msysgit.github.io/) (auch "Git Bash" genannt),
2. [Cygwin](https://www.cygwin.com/),
3. unter Verwendung einer virtuellen Desktop-Maschine, und
4. Die Lernenden müssen sich mit einem entfernten Unix-Rechner (typischerweise eine VM
   in der Cloud) verbinden.

Cygwin war bis Mitte 2013 die bevorzugte Option, aber als wir anfingen, Git zu
unterrichten, erwies sich msysGit als besser geeignet. Virtuelle Desktop-Maschinen und
Cloud-basierte VMs eignen sich gut für technisch versierte Lernende und können den
Installations- und Konfigurationsaufwand zu Beginn des Workshops verringern, aber:

1. Sie funktionieren nicht gut auf leistungsschwachen Rechnern,
2. Sie sind verwirrend für Anfänger (weil einfache Dinge wie Kopieren und Einfügen
   anders funktionieren),
3. Lernende verlassen den Workshop ohne eine Arbeitsumgebung auf dem Betriebssystem
   ihrer Wahl, und
4. Es kann vorkommen, dass Teilnehmer auftauchen, ohne die VM heruntergeladen zu haben,
   oder dass das WLAN während des Unterrichts ausfällt (oder überlastet wird).

Was auch immer Sie verwenden, bitte *testen Sie es selbst* auf einem Windows-Rechner
*vor* Ihrem Workshop: Es kann sich immer etwas hinter Ihrem Rücken geändert haben seit
Ihrem letzten Workshop. Und nutzen Sie bitte auch unseren [Software Carpentry Windows
Installer][windows-installer].

[shebang]: https://www.in-ulm.de/~mascheck/various/shebang/
[windows-installer]: https://github.com/swcarpentry/windows-installer




