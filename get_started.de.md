# Zähme die Klammern - Starten mit Clojure

## (like-parentheses?)

Der erste ins Auge stechende Unterschied von Clojure zu C-Sprachen sind die runden Klammern. Für manche gibt's davon einfach zu viele, obwohl der Stil eigentlich nicht *so* ungewohnt ist wie man an einem Beispiel sieht:

```python
println("hello world")
```

ist gültiges Python 3 während Clojure es so macht

```clojure
(println "hello world")
```

Clojure geht dann noch einen Schritt weiter und wendet das gleiche Prinzip auf so ziemlich alles an z.B. Funktions-Deklarationen:

```clojure
(defn fun [param]
  "result")
```

## (watch talk)

Um einen besseren Eindruck davon zu bekommen ob Clojure was für dich ist, schlage ich vor den großartigen Vortrag [Clojure, made simple](https://www.youtube.com/watch?v=VSdnJDO-xdg) vom Macher der Sprache Rich Hickey zu sehen.

Bei der [TUI Infotec](http://www.tui-infotec.com/) habe ich letztens im Team einen Vortrag mit Demo über die Sprache und ihre Anwendunge für Web-Entwicklung gehalten. Natürlich habt ihr nicht viel von dem Demos ohne Video, wenn ihr nicht dort wart, aber vielleicht habt ihr trotzdem was davon kurz durchzublättern: [Clojure - The Average Joe's Lisp](https://kossmoboleat.github.io/clojure_intro). Mein Ziel war zu zeigen, dass weit vom Stereotyp der akademische esoterische funktionalen Programmiersprache entfernt ist. Heute kann man damit auch als Normalsterblicher elegant Probleme lösen.

Ein paar andere Leute haben auch versucht das zu vermitteln. Zum Beispiel der Clean-Code-Guro Robert C. Martin oder Uncle Bob, der darüber gebloggt hat: [Clojure Is the New C](https://www.infoq.com/presentations/clojure-c), [Why Clojure?](http://thecleancoder.blogspot.de/2010/08/why-clojure.html)

## (try)

Wenn du praktische einsteigen willst geht das am Simpelsten mit einem Online-Interpreter (oder [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop)) [tryclj.com](http://www.tryclj.com/) (das gibt's auch für [ClojureScript](http://himera.herokuapp.com/index.html)) oder löse eins der Anfänger-Probleme beim ebenfalls interaktiven [4clojure.com](http://www.4clojure.com/problem/66). Beim letzten Link geht's darum den Algorithmus zum Finden des größten gemeinsamen Teilers zu implementieren, der ja auch ein schöner rekursiver Algorithmus ist. Ein bisschen einfacher startet es sich vielleicht mit den Basis-Konstrukten der Sprache wie dem [hier](http://www.4clojure.com/problem/14)). Ähnlich sind die Katas von [codewars.com](https://www.codewars.com) bei dem man noch zusätzlich mit Gamification motiviert wird. Damit habe ich den Einstieg geschafft. Die Seite hat übrigens auch nette Probleme für Javascript, Python, Ruby, Java oder Haskell falls man das besser lernen möchte.

Nach dem Einstieg in die Sprach-Basics hilft's immer sich an einem konkrete Beispiel-Projekt entlangzuhangeln, um die Sprache zu verinnerlichen. Als erstes solltest du dafür ein [JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) und dann das Build-Tool [Leinigen](http://leiningen.org/) installieren. So einfach kannst du es auf unixoiden Betriebssystem zum Laufen bringen (Für Windows schaut unter dem Link nach):

```shell
$ wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
# verschieb es in ein Verzeichnis auf dem $PATH, wie ~/bin
$ mv lein ~/bin
# mach es ausführbar
$ chmod a+x ~/bin/lein
# Führe es einmal aus, damit es sich selbst installiert
$ lein
```

Um einzusteigen ist der für sich alleine auch schon beeindruckende Editor [Light Table](http://lighttable.com/) zu empfehlen und wer ein richtiges Projekt aufsetzen möchte ist mit dem IDE-Plugin [cursive](https://cursive-ide.com/) für Intellij gut bedient.

Um in die Web-Entwicklung einzusteigen empfehle ich  [Luminus](http://www.luminusweb.net/). Das ist ein Micro-Framework, das die besten Web-Bibliotheken zusammenpackt und einfach ein Start-Projekt generiert. So ähnlich wie bei [JHipster](https://jhipster.github.io/) ein nettes [Spring Boot](https://projects.spring.io/spring-boot/) + AngularJS Projekt generiert. Schreib dazu ins Terminal und schon läuft eine App mit Beispiel unter [localhost:3000](http://localhost:3000). Ähnlich wie bei JHipster kann auch noch Optionen dazuwählen um z.B. Authentifizierung einzubinden.

```shell
$ lein new luminus my-app
$ cd my-app
$ lein run
Started server on port 3000
```

Obwohl ich eher skeptisch gegenüber großen Frameworks bin, gibt es doch eins das vielversprechend aussieht. [Arachne](http://arachne-framework.org/) wird von sehr findigen Leuten gemacht und kommt hoffentlich bald raus ohne zu seher frameworky zu sein.

## (read)

Wenn ihr so weit kommt, schaut euch ein paar sehr gut geschiebene Bücher über Clojure an:
- [Programming Clojure by Stuart Halloway](https://pragprog.com/book/shcloj/programming-clojure)
- [Web Development with Clojure by Dmitri Sotnikov](https://pragprog.com/book/dswdcloj2/web-development-with-clojure-second-edition)
- [Clojure Applied From Practice to Practitioner by Bend Vandgrift and Alex Miller](https://pragprog.com/book/vmclojeco/clojure-applied)
