# Was ist Programmieren?

Zunächst ein bisschen Motivation: 

- [**10 Gründe, Programmieren zu lernen**](https://itgirls.de/10-gruende-programmieren-zu-lernen/) und 
- [**Bericht einer ehemaligen FIW-Studentin**](https://itgirls.de/100-frauenanteil-im-informatikstudium/).

---

Ehe wir uns weiter mit Java und Programmierkonzepten beschäftigen, wollen wir uns bewusst werden, was Programmieren überhaupt ist. Prinzipiell lösen wir beim Programmieren ein Problem mithilfe einer Programmiersprache. Dabei stellt sich die Frage, welche Probleme mithilfe eines Computers lösbar sind und welche nicht. Dazu gibt es umfangreiche theoretische Untersuchungen - viele davon werden Sie in den "Grundlegenden Konzepten der Informatik" diskutieren. Ein wesentlicher Begriff dabei ist *Algorithmus*. Ein Algorithmus ist eine eindeutige Handlungsvorschrift, die aus endlich vielen einzelnen Schritten besteht und ein Problem löst. 

Algorithmen sind also auch Kochrezepte oder Bauanleitungen, wenn sie denn "eindeutig" sind. Wir kennen alle das Problem, dass Handlungsanweisungen nicht immer eindeutig sind - man kann es manchmal so oder so machen. In der Programmierung darf eine solche Mehrdeutigkeit natürlich nicht vorkommen. Der Algorithmusbegriff wurde deshalb detailliert und folgende Eigenschaften müssen für eine Handlungsanweisung für einen Computer gelten, um ein Algorithmus zu sein:

1. **Finitheit** Das Verfahren muss in einem **endlichen** Text (Programm) eindeutig beschreibbar sein.
2. **Ausführbarkeit** Jeder einzelne Schritt des Verfahrens muss auch tatsächlich ausführbar sein.
3. **Dynamische Finitheit** Das Verfahren darf zu jedem Zeitpunkt nur endlich viel Speicherplatz benötigen.
4. **Terminierung** Das Verfahren muss irgendwann enden, d.h. darf nur endlich viele Ausführungsschritte benötigen.
5. **Determiniertheit** Das Verfahren muss bei denselben Voraussetzungen das gleiche Ergebnis liefern.
6. **Determinismus** Die nächste anzuwendende Regel im Verfahren ist zu jedem Zeitpunkt (in jedem Zustand) eindeutig definiert.

### Beispiel: Euklidischer Algorithmus

Mit dem euklidischen Algorithmus[^4] kann der *größte gemeinsame Teiler (ggT)* zweier Zahlen berechnet werden. In seinen *Elementen* hat Euklid diesen Algorithmus ungefähr so formuliert:

[^4]: Benannt nach Euklid von Alexandria, einem Mathematiker aus dem 3. Jahrhundert, Autor der *Elemente* - einem Kompendium des Wissens der Mathematik seiner Zeit. 

!!! quote "Euklidischer Algorithmus"
	Wenn CD aber AB nicht misst, und man nimmt bei AB, CD abwechselnd immer das kleinere vom größeren weg, dann muss (schließlich) eine Zahl übrig bleiben, die die vorangehende misst.

Hm, das ist recht schwierig zu verstehen. Euklid betrachtet die beiden Zahlen, von denen der größte gemeinsame Teiler ermittelt werden soll, als Strecken (`AB` und `CD`). Er zieht wiederholt die kleinere der beiden Strecken von der größeren ab. Er wiederholt dies solange, bis die beiden Strecken gleich lang sind - genauer: er wiederholt dies solange, solange die beiden Strecken nicht gleich lang sind (*... CD aber AB nicht misst...*).

Beispiel: ggT von 24 und 40

1. AB: 40, CD: 24, AB größer als CD --> 40 - 24 = 16 
2. AB: 16, CD: 24, CD größer als AB --> 24 - 16 =  8
3. AB: 16, CD: 8,  AB größer als CD --> 16 -  8 =  8  
4. AB:  8, CD: 8,  AB gleich CD --> Ende --> ggT ist 8

Wir versuchen, den Algorithmus in eine verständlichere und genauere Sprache zu überführen, ohne bereits eine *Programmiersprache* zu verwenden. Wir benutzen sogenannten *Pseudocode*:

Angenommen, die beiden Zahlen, von denen wir den *ggT* berechnen wollen, sind `a` und `b`:

```bash linenums="1"
solange a ungleich b ist, wiederhole
	wenn a größer ist als b, dann:
		ziehe b von a ab und weise das Ergebnis a zu
	andernfalls:
		ziehe a von b ab und weise das Ergebnis b zu
wenn a gleich b ist, dann:
	a (oder auch b) ist der gesuchte ggT
``` 

Wichtig ist, dass das Einrücken hier eine Bedeutung hat (eine *Semantik*). In Zeile `1` formulieren wir, dass sich etwas wiederholen soll, solange eine bestimmte Bedingung gilt. Das, was sich wiederholen soll, ist in den Zeilen `2` bis `5` formuliert. Zeile `1` formuliert eine *Schleife* und in den Zeilen `2`-`5` befindet sich der *Schleifeninhalt*. Die Zeilen `2`-`5` formulieren ein eigenes Konstrukt, nämlich eine Auswahl zwischen Alternativen, abhängig von einer Bedingung. Die Bedingung ist, ob `a` größer ist als `b`. Wenn das der Fall ist, dann wird die Alternative `ziehe b von a ab und weise das Ergebnis a zu` ausgeführt (In der Programmierung werden das später als `a = a - b` schreiben - das sieht für uns jetzt noch sehr "falsch" aus). Ist jedoch `a` nicht größer als `b`, dann wird die Alternative `ziehe a von b ab und weise das Ergebnis b zu` (`b = b - a`) ausgeführt. Ein solches Konstrukt wird *Selektion* (oder auch *bedingte Alternative*) genannt. Nachdem entweder Zeile `3` oder Zeile `5` ausgeführt wurde (es wird genau eins von beiden ausgeführt), wird erneut in Zeile `1` geprüft, ob `a ungleich b` ist. Wenn ja, wird die Selektion wiederholt. Wenn nicht, dann ist die Schleife beendet und Zeile `6` wird ausgeführt. Die in Zeile `6` formulierte Bedingung `wenn a gleich b ist`, ist eigentlich unnötig. 

!!! question "Frage"
	Warum ist die Bedingung `wenn a gleich b ist` in Zeile `6` unnötig?

Wir betrachten nochmals die im obigen Algorithmus betrachteten Konstrukte (wir sprechen vom *Kontrollfluss* von *Anweisungen*): 

1. *Iteration*: die Schleife, die in Zeile `1` formuliert wird und die als Schleifeninhalt die Zeilen `2`-`5` hat, beschreibt einen *iterativen* (sich wiederholenden) *Kontrollfluss*.
2. *Selektion*: die *bedingte Alternative*, die eine Bedingung prüft (Zeile `2`) und dann, je nachdem, ob die Bedingung richtig oder falsch ist, jeweils eine alternative Anweisung ausführt (entweder Zeile `3` oder Zeile `4`), wird *Selektion* genannt (siehe Zeilen `2`-`5`).
3. *Sequenz*: die Anweisungen werden hintereinander ausgeführt, erst Zeile `1`, dann Zeile `2`, dann entweder Zeile `3`oder Zeile `4` usw. Das Hintereinanderausführen von Anweisungen wird *Sequenz* genannt. 

Schauen wir uns für unseren Algorithmus nochmal die Eigenschaften eines Algorithmus an: 

1. **Finitheit** unsere Beschreibung des Algorithmus ist endlich (siehe oben).
2. **Ausführbarkeit** jeder einzelne Schritt kann ausgeführt werden.
3. **Dynamische Finitheit** über den Speicherplatz können wir noch nicht viel sagen, aber wir müssen nur einige wenige Zahlen speichern. Das sollte klappen.
4. **Terminierung** Wann endet unser Algorithmus? Was muss gelten? Wissen wir, ob der Algorithmus irgendwann stoppt?
5. **Determiniertheit** Es ist sicherlich nicht so leicht zu sehen, ob bei gleicher Eingabe (die Zahlen `a`und `b`) auch stets der gleiche größte gemneinsame Teiler berechnet wird. Dazu müssten wir uns erstmal überlegen, wie wir das prüfen können. 
6. **Determinismus** Wir werden unseren Algorithmus nochmal an einem Beispiel *durchspielen*, um ein Gefühl dafür zu bekommen, dass wir stets wissen, welche Anweisung als nächstes ausgeführt wird. 

### Beispielzahlen für den euklidischen Algorithmus

Wir nehmen die Zahlen `a=40` und `b=24` und spielen damit unseren Algorithmus durch:

Zeile `1`: `a (40) ist ungleich b (24)`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `a ist größer als b`, also wird Zeile `3` ausgeführt (und genau nicht Zeilen `4` und `5`)
Zeile `3`: das Ergebnis von `a-b` ist 16. Der neue Wert von `a` ist 16.
Zeile `1`: wegen *wiederhole* (Iteration): `a (16) ist ungleich b (24)`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `a ist nicht größer als b`, also wird Zeile `5` ausgeführt (und genau nicht Zeile `3`)
Zeile `5`: das Ergebnis von `b-a` ist 8. Der neue Wert von `b` ist 8.
Zeile `1`: wegen *wiederhole* (Iteration): `a (16) ist ungleich b (8)`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `a ist größer als b`, also wird Zeile `3` ausgeführt (und genau nicht Zeile `5`)
Zeile `3`: das Ergebnis von `a-b` ist 8. Der neue Wert von `a` ist 8.
Zeile `1`: wegen *wiederhole* (Iteration): `a (8) ist nicht ungleich b (8)`, also wird der Schleifeninhalt **nicht** ausgeführt
Zeile `6`: `a (8) ist gleich b (8)`
Zeile `7`: der gesuchte `ggT` ist `8`
Ende

Für dieses Beispiel war stets eindeutig, welche Anweisung als nächstes ausgeführt wird. Der Algrorithmus hat auch terminiert, d.h. er wurde beendet und es sollte auch klar sein, dass das Ergebnis für die die Eingabe `a=40` und `b=24` stets `8` ist. 

!!! question "Fragen"
	 * Was ändert sich, wenn am Anfang `a=24` und `b=40` sind?
	 * Was ändert sich, wenn am Anfang `a=-40` und `b=24` sind?
	 * Was ändert sich, wenn am Anfang `a=0` und `b=24` sind?
	 * Was ändert sich, wenn am Anfang `a=24` und `b=24` sind?

### Beispiel: (3n+1)-Vermutung (Collatz-Problem)

Wir betrachten noch einen weiteren Algorithmus: Als Eingabe bekommen wir eine positive natürliche Zahl, z.B. `5`. Der Algorithmus berechnet eine Folge von Zahlen und zwar nach folgender Vorschrift: ist die Zahl ungerade, dann wird ihr Nachfolger dadurch berechnet, dass die Zahl mit 3 multipliziert und dann 1 addiert wird. Ist die Zahl gerade, dann wird ihr Nachfolger dadurch berechnet, dass die Zahl durch 2 geteilt wird. Der Algorithmus stoppt, wenn der Nachfolger `1` ist. 

Angenommen, die eingegebene positive natürliche Zahl ist `n`:

```bash linenums="1"
solange n ungleich 1 ist, wiederhole
	wenn n ungerade, dann:
		berechne 3*n +1 und weise das Ergebnis n zu
	andernfalls:
		berechne n/2 und weise das Ergebnis n zu
``` 

Wir begeben uns also in eine *Schleife* und berechnen so lange einen Nachfolger für die Zahl bis der NAchfolger `1`ist. Betrachten wir den Algorithmus für die EIngabe von `n=5`:

Zeile `1`: `n (5) ist ungleich 1`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `n ist ungerade`, also wird Zeile `3` ausgeführt (und genau nicht Zeilen `4` und `5`)
Zeile `3`: das Ergebnis von `3*5+1` ist `16`. Der neue Wert von `n` ist 16.
Zeile `1`: wegen *wiederhole* (Iteration): `n (16) ist ungleich 1`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `n ist nicht ungerade`, also wird Zeile `5` ausgeführt (und genau nicht Zeile `3`)
Zeile `5`: das Ergebnis von `16/2` ist `8`. Der neue Wert von `n` ist 8.
Zeile `1`: wegen *wiederhole* (Iteration): `n (8) ist ungleich 1`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `n ist nicht ungerade`, also wird Zeile `5` ausgeführt (und genau nicht Zeile `3`)
Zeile `5`: das Ergebnis von `8/2` ist `4`. Der neue Wert von `n` ist 4.
Zeile `1`: wegen *wiederhole* (Iteration): `n (4) ist ungleich 1`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `n ist nicht ungerade`, also wird Zeile `5` ausgeführt (und genau nicht Zeile `3`)
Zeile `5`: das Ergebnis von `4/2` ist `2`. Der neue Wert von `n` ist 2.
Zeile `1`: wegen *wiederhole* (Iteration): `n (2) ist ungleich 1`, also wird der Schleifeninhalt ausgeführt
Zeile `2`: `n ist nicht ungerade`, also wird Zeile `5` ausgeführt (und genau nicht Zeile `3`)
Zeile `5`: das Ergebnis von `2/2` ist `1`. Der neue Wert von `n` ist 1.
Zeile `1`: wegen *wiederhole* (Iteration): `n (1) ist nicht ungleich 1`, also wird der Schleifeninhalt **nicht** ausgeführt
Ende

Auch für dieses Beispiel war erneut stets eindeutig, welche Anweisung als nächstes ausgeführt wird. Der Algrorithmus hat auch terminiert, d.h. er wurde beendet und es sollte auch klar sein, dass das Ergebnis für die Eingabe `n=5` stets `1` ist. 

!!! question "Fragen"
	 * Spielen Sie den Algorithmus ruhig einmal für `n=7` durch oder auch für andere `n`
	 * Denken Sie, dass der Algorithmus für jede beliebige positive natürliche Zahl `n` terminiert?
	 * Wenn ein Algorithmus für eine konkrete Eingabe stets ein eindeutiges Ergebnis (und zwar immer das gleiche) liefert, wie können dann Zufallszahlen berechnet werden?

!!! success
    Wir haben ein Verständnis über den *Algorithmus*-Begriff erlangt und wissen, was *Finitheit*, *Determiniertheit*, *Determinismus* und *Terminierung* bedeuten. 

## Programmablaufstrukturen

Interessanterweise gibt es nur *drei* verschiedene Ablaufstrukturen in Programmen bzw. Algorithmen. Alle drei haben wir bereits verwendet. Mit Ablaufstrukturen meinen wir die Abarbeitungsreihenfolge von Anweisungen. Man sagt auch *Kontrollfluss* dazu. Die drei Ablaufstrukturen, die es gibt, sind:

- die *Sequenz*: die Anweisungen werden in sequenzieller Abfolge, d.h. hintereinander ausgeführt
- die *Iteration*: die Abläufe werden wiederholt ausgeführt, also in einer Schleife
- die *Selektion*: die Abläufe werden *selektiv*, d.h. unter einer bestimmten Bedingung ausgeführt. Man nennt diese Struktur auch *Verzweigung*  oder *bedingte Alternative*

Wir schauen uns alle drei Kontrollstrukturen einmal genauer an.

### Die Sequenz

Bei der Sequenz handelt es sich einfach um hintereinander ausgeführte Anweisungen. Es wird stets erst die eine Anweisung vollständig abgearbeitet, ehe die andere begonnen wird.

=== "Sequenz von 3 Anweisungen"
	```bash
	Anweisung1
	Anweisung2
	Anweisung3
	```

Ein Beispiel (mit 2 Anweisungen) wäre:

```bash
berechne 3*n und weise das Ergebnis n zu
berechne n+1 und weise das Ergebnis n zu 
```

Zur Visualisierung von Kontrollstrukturen werden auch sogannnte *Programmablaufdiagramme* oder *Programmablaufpläne* verwendet. Für eine Sequenz sähe ein solches Ablaufdiagramm so aus:

![sequenz](./files/07_sequenz.png)

So ein Diagramm wird von oben nach unten gelesen. Es wird also erst `Anweisung1` ausgeführt, dann `Anweisung2` und zuletzt `Anweisung3`. Innerhalb einer Sequenz gilt immer *single entry*/*single exit*, d.h. keine der Anweisungen innerhalb einer Sequenz kann mehrere Ausgänge oder mehrere Eingänge haben. Es wäre ansonsten *nicht-deterministisch*  und somit ein Verstoß gegen unseren Algorithmusbegriff.

![sequenz](./files/08_sequenz.png)

### Die Iteration

Bei der *Iteration* handelt es sich um eine wiederholte Ausführung einer Anweisung bzw. einer Sequenz von Anweisungen. Wie oft eine Iteration ausgeführt wird, hängt von einer Bedingung ab. In der Programmierung sprechen wir bei der Iteration auch von einer *Schleife*. 

Bedingungen für eine solche Schleife haben wir bereits kennengelernt:

```bash
solange a ungleich b ist, wiederhole
	hier die Anweisung 
	oder die Anweisungen, die wiederholt werden, solange die Bedingung gilt
```

bzw.

```bash
solange n ungleich 1 ist, wiederhole
	hier die Anweisung 
	oder die Anweisungen, die wiederholt werden, solange die Bedingung gilt
```

Wichtig ist, dass es auch hier eine strikte Reihenfolge der Abarbeitung der Anweisungen gibt:

- es wird zunächst geprüft, ob die Bedingung erfüllt (wahr) ist, also ob z.B. `a ungleich b ist` oder ob `n ungleich 1`. Wenn diese Bedingung erfüllt (also wahr) ist, dann werden die Anweisung(en) innerhalb der Schleife nacheinander (sequenziell) abgearbeitet. Erst wenn alle Anweisungen innerhalb der Schleife abgearbeitet wurden, wird die Schleifenbedingung erneut geprüft. Ist sie wieder wahr, werden die Anweisungen innerhalb der Schleife erneut abgearbeitet usw. Ist sie nicht wahr, also wenn z.B. `a gleich b ist` oder `n gleich 1 ist`, dann wird die Schleife beendet und die Anweisungen innerhalb der Schleife **nicht** (erneut) abgearbeitet. 

Das Ablaufdiagramm einer Schleife (Iteration) sieht so aus:

![iteration](./files/09_iteration.png)

Die eigentliche Iteration ist grün dargestellt. Wir kommen von einer anderen Anweisung und prüfen die Bedingung. Ist sie wahr, wird `Anweisung1` ausgeführt.

!!! info "Beachte"
	`Anweisung1` muss nicht zwingend nur genau eine Anweisung sein. Bei `Anweisung1` kann es sich auch um eine Sequenz von Anweisungen oder eine Selektion oder sogar selbst um eine Iteration (Schleife in der Schleife - *verschachtelte* Schleife) handeln!

Nach jeder Ausführung von `Anweisung1` wird die Bedingung erneut geprüft. Ist sie (immernoch) wahr, wird `Anweisung1` erneut ausgeführt. Ist die Bedingung jedoch falsch, dann wird `Anweisung1` nicht (mehr) ausgeführt, sondern die Schleife wird verlassen und die Anweisung, die der Schleife folgt, wird ausgeführt (`Anweisung2`) oder das Programm ist dann zu Ende.

!!! info "Beachte"
	Es kann sein, dass `Anweisung1` gar nicht ausgeführt wird, weil die Bedingung bereits bei der ersten Prüfung falsch ist. Es ist also nicht gesagt, dass sich eine Iteration wirklich *wiederholt*. Es kann sein, dass `Anweisung1` gar nicht oder nur genau ein Mal ausgeführt wird (wenn die Bedingung nach der ersten Ausführung falsch ist). Das ist kein Problem! 
	Ein Problem ist es jedoch, wenn die Bedingung niemals falsch wird und die Schleife unendlich oft hintereinander ausgeführt wird. Das ist ein Verstoß gegen die **Terminierung** eines Algorithmus. In einem solchen Fall werden wir irgendwann einen Fehler bei der Programmausführung erhalten (aber erst zur Ausführungszeit, nicht bereits beim Compilieren). 

Wir werden uns ausführlich mit Schleifen auseinandersetzen, da sie logisch recht anspruchsvoll und dadurch häufig fehleranfällig sein können. 

### Die Selektion

Bei der *Selektion* handelt es sich, im Gegensatz zur Iteration, um eine einmalige Ausführung einer (oder mehrerer) Anweisung(en). Jedoch ist diese Ausführung, im Gegensatz zur Sequenz, von einer Bedingung abhängig. Wir hatten eine solche Selektion jeweils in obigen Beispielalgorithmen. Selektion aus dem euklidischen Algorithmus:

```bash
wenn a größer ist als b, dann:
	ziehe b von a ab und weise das Ergebnis a zu
andernfalls:
	ziehe a von b ab und weise das Ergebnis b zu
``` 

Selektion aus der (3n+1)-Vermutung (dem Collatz-Problem):

```bash
wenn n ungerade, dann:
	berechne 3*n +1 und weise das Ergebnis n zu
andernfalls:
	berechne n/2 und weise das Ergebnis n zu
``` 

Es gibt also immer eine Bedingung (z.B. `wenn a größer ist als b`) und abhängig vom Wert dieser Bedingung (wahr oder falsch), wird entweder die eine Anweisung (z.B. `ziehe b von a ab und weise das Ergebnis a zu`)  oder die andere (z.B. `ziehe a von b ab und weise das Ergebnis b zu`) ausgeführt. 

Das Ablaufdiagramm einer Selektion sieht so aus:

![selektion](./files/10_selektion.png)

!!! info "Beachte"
	`Anweisung1` und auch `Anweisung2` müssen nicht zwingend jeweils nur genau eine Anweisung sein. Bei beiden kann es sich auch um eine Sequenz von Anweisungen oder eine Selektion oder um eine Iteration handeln!

### Verschachteln von Kontrollstrukturen

Mehr als diese drei genannten Kontrollstrukturen gibt es nicht. Aber diese Kontrollstrukturen können beliebig ineinander verschachtelt werden. Überall dort, wo eine Anweisung steht (z.B. `Anweisung1`) kann auch eine komplette Kontrollstruktur eingesetzt werden, also eine Sequenz von Anweisungen oder eine Iteration oder eine Selektion. Die kann dann beliebig fortgeführt werden. So entstehen komplexe Strukturen - und somit komplexe Programme. 

Ein (immernoch recht einfaches) Beispiel für eine etwas komplexere Struktur:

![komplex](./files/11_komplex.png)

??? note "Übung Programmablaufpläne"
	Erstellen Sie sowohl für den euklidischen Algorithmus als auch für die (3n+1)-Vermutung einen Programmablaufplan!

??? note "Übung Algorithmus und Programmablaufplan"
	Ein Jahr ist ein Schaltjahr, wenn es sich durch 4 teilen lässt. Außer, es lässt sich durch 100 teilen. Dann ist es doch kein Schaltjahr. Außer, es lässt sich durch 400 teilen. Dann ist es doch ein Schaltjahr. Beschreiben Sie diese Vorschrift als einen Algorithmus in der Form, in der auch der euklidische Algorithmus und die (3n+1)-Vermutung beschrieben wurden. Erstellen Sie dann den dazugehörigen Programmablaufplan. 

!!! success
    Wir wissen nun, dass es nur drei verschiedene Programmablaufstrukturen gibt: die Sequenz, die Iteration und die Selektion. Wir haben ein Verständnis davon, was die drei Programmablaufstrukturen ausmacht, welchen Zweck sie haben und was sie voneinander unterscheidet. Wir wissen, dass sich diese Strukturen beliebig ineinander verschachteln lassen. 

