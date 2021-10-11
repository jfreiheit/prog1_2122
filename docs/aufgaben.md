# Aufgaben

Hier finden Sie die Aufgaben. Die Abgabefristen der einzelnen Aufgaben stehen [hier](../#planung-vorlaufig-kann-sich-noch-andern). Beachten Sie die nachfolgenden Hinweise zum Hochladen der Aufgaben. 

## Hinweise zur Abgabe der Aufgaben

Die Aufgaben laden Sie in [Moodle](https://moodle.htw-berlin.de/course/view.php?id=29156) unter dem Reiter "Aufgaben" hoch. Dort ist für jede Aufgabe eine Moodle-Aufgabe erstellt. Beachten Sie, dass ein Hochladen nach Ablauf der Abgabefrist nicht mehr möglich ist. 


### BlueJ vs. Eclipse

Die ersten Wochen verwenden wir als Entwicklungsumgebung BlueJ. Für die Aufgaben, die wir mit BlueJ lösen, werde ich Ihnen jeweils Hinweise zur Abgabe für jede Aufgabe einzeln geben. 

Sobald wir Eclipse verwenden, gelten die folgenden Hinweise: 

- Achten Sie darauf, dass Sie die Quelldateien (also die `.java`-Dateien aus dem `src`-Verzeichnis) hochladen. 
- Ihre Klassen erstellen Sie immer in einem package `aufgaben.aufgabeX`. Das heißt, Aufgabe1 ist im package `aufgaben.aufgabe1`, Aufgabe2 im package `aufgaben.aufgabe2` usw. 
- In Ihrem `workspace`gibt es dann einen Ordner für Ihr Java-Projekt, z.B. `WS21` (je nachdem, wie Sie Ihr Java-Projekt genannt haben) und darin befindet sich ein `bin`- und ein `src`-Ordner. In dem `src`-Ordner befindet sich dann ein Ordner `aufgaben` und darin ein Ordner `aufgaben1` (für Aufgabe1). Darin befindet sich Ihre `.java`-Datei, die Sie hochladen sollen. Angenommen, Sie haben Ihre Klasse `Aufgabe1` genannt, dann heißt die Klasse also `Aufgabe1.java`. Sie folgen also dem Pfad `workspace`--> *Java-Projekt* (z.B. `WS21`) --> `src` --> `aufgaben` --> `aufgabe`*X*.
- Wenn Ihre Lösung aus mehreren Klassen (mehreren `.java`-Dateien) besteht, können Sie entweder die Dateien einzeln hochladen oder Sie zippen Ihre Dateien (am besten dann den `aufgabeX`-Ordner und laden das `.zip`-File hoch. 
- In Ihrer Lösung (Ihrer/n Klasse/n) fügen Sie direkt oberhalb Ihrer Klassendefinition einen JavaDoc-Kommentar ein (`/** ... */`). Dieser enthält ein `@author`-Tag. dahinter schreiben Sie Ihren Namen. Das sieht dann z.B. so aus:
	```java
	package aufgaben.aufgabe1;

	/**
	 * 
	 * @author Jörn Freiheit
	 * 
	 * Diese Klasse gibt auf die Konsole ein Rhombus (eine Raute) aus.
	 * Der Rhombus ist entweder gefuellt oder ungefuellt. 
	 *
	 */
	public class Aufgabe1
	{
		// hier Ihre Implementierung
	}
	```
- Sie können Ihre Aufgaben zu zweit lösen. Tragen Sie dann hinter das `@author`-Tag beide Namen ein und **laden Sie bitte beide** die Lösung in Moodle hoch!

## Code Review

Für jede abgegebene Aufgabe wird Ihnen die Lösung einer Kommilitonin zum Review zugewiesen. Analysieren Sie den Code Ihrer Kommilitonin und geben Sie ihr dazu eine Rückmeldung!  Es genügen 2 bis 3 Review-Kommentare.
Zur offiziellen Abgabe einer Aufgabe gehören also

- das Hochladen der eigenen Lösung,
- das Analysieren/Kommentieren einer fremden Lösung.

#### Hinweise zum Review:

- Es geht nicht darum, das Programm zu überarbeiten, sondern darum es nachzuvollziehen und Ihrer Kommilitonin eine Rückmeldung und eventuell Anregungen zu geben.
- Weisen Sie sowohl auf Stärken als auch auf Schwächen des Quelltexts hin.
- Worauf Sie u.a. achten können:
	- Ist der Quelltext gut strukturiert und verständlich?
	- Haben Variablen und Methoden passende Namen? Werden die Namen konsistent verwendet?
	- Werden Konventionen eingehalten? Beispiel: Klassennamen starten immer mit Großbuchstaben, Objektnamen immer mit Kleinbuchstaben
	- Ist das Programm übersichtlich formatiert? Beispiel: kein horizontales Scrolling nötig
- Machen Sie ggf. Vorschläge für (alternative) Lösungen.
- Gehen Sie respektvoll miteinander um, es gibt keinen Grund, unhöflich zu sein.
- Lesen Sie Ihre Kommentare noch einmal durch, bevor Sie sie an Ihre Kommilitonin weitergeben.



## Aufgaben