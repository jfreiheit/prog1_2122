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

![review](./files/12_review.png)

## Aufgaben

#### Aufgabe 1 (Abgabe bis 25.10.2021 24:00 Uhr)
??? "Aufgabe1 - Square mit Circles"
	- Verwenden Sie BlueJ und öffnen Sie das Projekt `picture` aus dem `examples`-Ordner von BlueJ. Speichern Sie das Projekt als Projekt `aufgabe1` ab. Die Klasse `Picture` können Sie wie folgt anpassen:
		```java
		/**
		 * Aufgabe 1
		 * 
		 */
		public class Picture
		{
		    /**
		     * Constructor for objects of class Picture
		     */
		    public Picture()
		    {// nothing to do... instance variables are automatically set to null
		        
		    }

		    /**
		     * Draw this picture.
		     */
		    public void draw()
		    {
		        Square s1 = new Square();		        
		        Circle c1 = new Circle();
		        Circle c2 = new Circle();
		        Circle c3 = new Circle();  
		        Circle c4 = new Circle();
		        // hier die Implementierung
		    }
		}
		```
	 - Programmieren Sie die `draw()`-Methode so, dass folgendes Bild gezeichnet wird:
	 	![aufgabe1](./files/21_aufgabe1.png)
	 	
	 	Die Größen bleiben Ihnen überlassen, aber die vier Kreise sollen das gelbe Quadrat vollständig ausfüllen. Den Titel des Fensters müssen Sie nicht ändern (geht aber in der Klasse `Canvas`).

	 - Erstellen Sie sich eine Testklasse `PictureTest`, in der es eine Testmethode `testDraw()` gibt, die die `draw()`-Methode für ein `Picture`-Objekt ausführt. 
	 - Zippen Sie Ihr Projekt `aufgabe1` und laden es in Moodle hoch. 


#### Aufgabe 2 (Abgabe bis 01.11.2021 24:00 Uhr)
??? "Aufgabe2 - Methoden und Ausgaben"
	- Erstellen Sie sich ein neues Projekt `aufgabe2` und darin eine neue Klasse `Aufgabe2`, die wie folgt aussieht:
		```java
					
		public class Aufgabe2
		{
		    public Aufgabe2()
		    {
		        
		    }

		    public void start()
		    {
		        // rufen Sie hier Ihre Methoden auf:
		        
		    }
		}

		```
	- Implementieren Sie eine Methode `computeSum(double number1, double number2)`, die die Summe der beiden Zahlen `number1` und `number2` als `double` *zurückgibt*. 
	- Implementieren Sie eine Methode `printSum(double number1, double number2`, die die Summe der beiden Zahlen `number1` und `number2` in der folgenden Form *ausgibt*. Die Ausgabe sieht für die Beispielwerte `number1 = 4.0` und `number2 = 5.0` so aus:
		```bash
		4.0 + 5.0 = 9.0
		```
		Rufen Sie in der `printSum(double number1, double number2`-Methode die Methode `computeSum(double number1, double number2)` auf!
	- Implementieren Sie ähnliche Methoden auch für die Subtraktion, Multiplikation und Division von zwei `double`-Zahlen. Verwenden Sie jeweils die `computeXXX()`-Methoden in den `printXXX()`-Methoden. 
	- Erstellen Sie eine Methode `printComputations(double number1, double number2)`, in der alle vier `printXXX()`-Methoden aufgerufen werden, so dass durch den Aufruf der `printComputations(double number1, double number2)`-Methode folgende Ausgabe erscheint (Beispielwerte `4.0` und `5.0`):
		```bash
		4.0 + 5.0 = 9.0
		4.0 - 5.0 = -1.0
		4.0 * 5.0 = 20.0
		4.0 / 5.0 = 0.8
		```
	- Zippen Sie Ihr Projekt `aufgabe2` und laden es in Moodle hoch. 


#### Aufgabe 3 (Abgabe bis 08.11.2021 24:00 Uhr)
??? "Aufgabe3 - Rechteck"
	- Erstellen Sie sich ein neues Projekt `aufgabe3` und darin eine neue Klasse `Aufgabe3`, die wie folgt aussieht:
		```java
					
		public class Aufgabe3
		{
		    public Aufgabe3()
		    {
		        
		    }

		    public void start()
		    {
		        // rufen Sie hier Ihre Methoden auf:
		        
		    }
		}

		```
	- Implementieren Sie eine Methode `public void printRectangle(int width, int height, boolean filled){}`
	- Ist der Parameterwert von `filled` `true`, dann soll ein Rechteck wie folgt auf die Konsole ausgegeben werden (Beispielausgabe für `width=11` und `height=5`):
		```bash
		***********
		***********
		***********
		***********
		***********
		```
	- Ist der Parameterwert von `filled` `false`, dann soll das Rechteck ungefüllt sein, also so:
		```bash
		***********
		*		  *
		*		  *
		*		  *
		***********
		```
	- Die obere Ausgabe ist also durch die Anweisung `printRectangle(11, 5, true);` und die untere durch die Anweisung `printRectangle(11, 5, false);` entstanden.
	- **Tipp:**: Schreiben Sie sich zwei weitere Methoden `public void printRectangleFilled(int width, int height){}` und `public void printRectangleUnfilled(int width, int height){}`, die Sie entsprechend des Wertes von `filled` aufrufen. In der einen Methode erstellen Sie das ausgefüllte Rechteck und in der anderen das ungefüllte. Dann wird Ihr Programm nicht zu unübersichtlich. Fangen Sie am besten mit der ausgefüllten an, die ist etwas leichter. 
	- Das Programm soll für beliebige (nicht so große - max. Werte für `width` und `height` je `100`) positive Zahlen (also `> 0`) funktionieren. Insbesondere sind die Tests für `width=1` und `height=1` bzw. `height=2` interessant. 
	- Zippen Sie Ihr Projekt `aufgabe3` und laden es in Moodle hoch. Viel Spaß und viel Erfolg!



#### Aufgabe 4 (Abgabe bis 15.11.2021 24:00 Uhr)
??? "Aufgabe4 - Rhombus"
	- Erstellen Sie sich ein neues Projekt `aufgabe4` und darin eine neue Klasse `Aufgabe4`, die wie folgt aussieht:
		```java
					
		public class Aufgabe4
		{
		    public Aufgabe4()
		    {
		        
		    }

		    public void start()
		    {
		        // rufen Sie hier Ihre Methoden auf:
		        
		    }
		}

		```
	- Implementieren Sie eine Methode `public static void printRhombus(int upperHalf, boolean filled){}`
	- Ist der Parameterwert von `filled` `true`, dann soll ein Rhombus (eine Raute) wie folgt auf die Konsole ausgegeben werden:
		```bash
		      *
		     ***
		    *****
		   *******
		  *********
		 ***********
		  *********
		   *******
		    *****
		     ***
		      *
		```
	- Ist der Parameterwert von `filled` `false`, dann soll der Rhombus ungefüllt sein, also so:
		```bash
		      *
		     * *
		    *   *
		   *     *
		  *       *
		 *         *
		  *       *
		   *     *
		    *   *
		     * *
		      *
		```
	- der Wert für `upperHalf` gibt die Höhe einer Hälfte des Rhombus an. Die Gesamthöhe des Rhombus berechnet sich aus `
		```java
		int height = 2 * upperHalf +1;
		```
	- In unserem oben gezeigten Beispiel ist der Wert von `upperHalf` `5` und die Gesamthöhe des Rhombus `11`. 
	- Die obere Ausgabe ist also durch die Anweisung `printRhombus(5, true);` und die untere durch die Anweisung `printRhombus(5, false);` entstanden.
	- Die Berechnung der Höhe aus dem Parameterwert `upperHalf` hat die Vorteile, 
		- dass die Höhe dadurch immer eine ungerade Zahl ist (was notwendig ist) und 
		- dass Sie den Wert `upperHalf` gut verwenden können (was ebenfalls notwendig ist, wie Sie merken werden)
	- **Tipp:**: Schreiben Sie sich zwei weitere Methoden `public static void printRhombusFilled(int upperHalf){}` und `public static void printRhombusUnfilled(int upperHalf){}`, die Sie entsprechend des Wertes von `filled` aufrufen. In der einen Methode erstellen Sie die ausgefüllte Raute und in der anderen die ungefüllte. Dann wird Ihr Programm nicht zu unübersichtlich. Fangen Sie am besten mit der ausgefüllten an, die ist etwas leichter. 
	- Das Programm soll für beliebige (nicht so große - max. Wert `100`) positive Zahlen (also `> 0`) von `upperHalf` funktionieren. Insbesondere sind die Tests für `upperhalf == 1` interssant. 
	- Zippen Sie Ihr Projekt `aufgabe4` und laden es in Moodle hoch. Viel Spaß und viel Erfolg!


