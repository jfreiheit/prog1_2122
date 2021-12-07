# Die Klasse `Object`

Die Klasse `java.lang.Object` ist die Basisklasse (Elternklasse) aller in Java existierenden Klassen. `Object` wird häufig auch als *die Mutter aller Klassen* in Java bezeichnet. 
Eine Klasse kann entweder *explizit* von einer anderen Klasse erben (mithilfe von `extends`) oder sie erbt *implizit* von der Klasse `Object`. 
Das bedeutet, dass *jede* Klasse von der Klasse `Object` erbt. 

Betrachten wir nochmal zur Wiederholung unsere Vererbungshierarchie aus dem vorherigen Abschnitt [Vererbung](../vererbung/#vererbung): 

- Dort hatten wir zunächst die Klasse `Viereck` erstellt, die *explizit von keiner* Klasse geerbt hat. `Viereck` erbt somit *implizit*  von `Object`.  
- Die Klasse `Rechteck` erbt von `Viereck` und somit **auch von** `Object`. 
- Die Klasse `Quadrat` erbt von `Rechteck` und somit auch von `Viereck` und somit **auch von** `Object`. 

Wenn wir uns nun noch daran erinnern, dass wir beim [Erstellen der Konstruktoren](../vererbung/#der-konstruktor-von-rechteck-das-schlusselwort-super) gesagt haben, dass bei der Objekterzeugung auch immer ein Objekt der Elternklasse erzeugt wird, dann bedeutet das, dass für jedes Objekt auch immer ein Objekt der Klasse `Object` erzeugt wird. 

Wenn wir uns nun auch noch daran erinnern, dass in einer Vererbungshierarchie immer die *is-a*-Relation (*ist ein*) gilt (jedes `Rechteck` ist ein `Viereck`, jedes `Quadrat` ist ein `Rechteck` ist ein `Viereck`), dann gilt dass **jedes** Objekt auch ein Objekt vom Typ `Object` ist. Das bedeutet insbesondere, dass jedes Objekt alle Objekteigenschaften (Objektmethoden) der Klasse `Object` geerbt hat. 

> Jedes Objekt (egal von welchem Referenztyp) ist auch ein Objekt vom Typ `Object` und hat alle Objektmethoden von `Object` geerbt.

## Objektmethoden von `Object`

Jedes Objekt in Java hat also automatisch die [Methoden von `Object`](https://docs.oracle.com/en/java/javase/15/docs/api/java.base/java/lang/Object.html) geerbt. Einige davon betrachten wir nun etwas genauer:

|Objektmethode von `Object` |Bedeutung |
|----------------------------|------------|
|`getClass()`               |gibt den Laufzeittyp der Klasse zurück | 
|`toString()`	             |gibt einen `String` zurück --> sollte in jeder Klasse überschrieben werden, um eine geeignete textuelle Beschreibung der Objekte zu haben |
|`equals(Object)` |für den Vergleich zweier Objekte --> sollte in jeder Klasse überschrieben werden, um Gleichheit von Objekten zu beschreiben (default: Referenzvergleich) |
|`hashCode()`	|gibt einen HashCode (ein `int`) für ein Objekt zurück, wird benötigt zum Einsortieren in hashbasierten Containern --> später in Collections |
|`clone()` |gibt eine Kopie (einen Clone) des Objektes zurück | 
|`wait()`, `notify()`, `notifyAll()` |für Threads --> machen wir viel später | 
|`finalize()`|für die Garbage Collection --> ist seit Java 9 deprecated |

Die Objektmethoden aus den letzten beiden Zeilen der Tabelle betrachten wir hier nicht weiter. Die anderen Objektmethoden werden im Folgenden genauer untersucht. Wir beginnen mit `getClass()`. 

### Die Objektmethode `getClass()`

Angenommen, wir haben die Klassen `Viereck`, `Rechteck` und `Quadrat` aus dem vorherigen Kapitel [Vererbung](../vererbung/#vererbung) gegeben:

=== "Viereck.java"
	```java linenums="1"
	public class Viereck
	{
		protected int a,b,c,d;			// Seiten
		
		public Viereck(int a, int b, int c, int d)
		{
			this.a = a;
			this.b = b;
			this.c = c;
			this.d = d;
		}
		
		public int umfang()
		{
			return this.a + this.b + this.c + this.d;
		}
		
		public void print()
		{
			System.out.print("[ a=" + this.a + ", b=" + this.b 
					+ ", c=" + this.c + ", d=" + this.d + " ] ");
			System.out.println(" Umfang des Vierecks : " + this.umfang());
		}
	}
	```

=== "Rechteck.java"
	```java linenums="1"
	public class Rechteck extends Viereck
	{
		public Rechteck(int laenge, int breite)
		{
			super(laenge, breite, laenge, breite); 	// Aufruf des Konstruktors von Viereck
		}
		
		/*
		 *  neue Objektmethode
		 *  spezielle Eigenschaft fuer Rechteck 
		 *  gilt nicht für Viereck
		 *  
		 */
		public int flaecheninhalt()
		{
			return this.a * this.b;		// Zugriff moeglich wegen protected in Viereck
		}
		
		@Override
		public void print()
		{
			System.out.print("[ a=" + this.a + ", b=" + this.b 
					+ ", c=" + this.c + ", d=" + this.d + " ] ");
			System.out.print(" Umfang des Rechtecks : " + this.umfang());
			System.out.println(" Flaecheninhalt des Rechtecks : " + this.flaecheninhalt());
		}
	}
	```

=== "Quadrat.java"
	```java linenums="1"
	public class Quadrat extends Rechteck
	{
		Quadrat(int seite)
		{
			super(seite, seite);	// Aufruf des Konstruktors von Rechteck
		}
		
		@Override
		public void print()
		{
			System.out.print("[ a=" + this.a + ", b=" + this.b 
					+ ", c=" + this.c + ", d=" + this.d + " ] ");
			System.out.print(" Umfang des Quadrats : " + this.umfang());
			System.out.println(" Flaecheninhalt des Quadrats : " + this.flaecheninhalt());
		}
	}
	```

Wenn wir nun in z.B. einer `main()`-Methode folgende Anweisungen haben:

```java linenums="1"
Viereck v1 = new Viereck(10,20,30,40);
Rechteck r1 = new Rechteck(10, 20);
Quadrat q1 = new Quadrat(30);
```

, dann wissen wir, dass `v1` vom Typ `Viereck` ist, `r1` vom Typ `Rechteck` und `q1` vom Typ `Quadrat`. Die Deklarationen dieser Variablen geben den sogenannten *Compilertyp* an. Und tatsächlich haben wir ja im obigen Fall auch die dazu passenden Objekte erzeugt, die genau dem jeweiligen Typ entsprechen. Wenn wir nun also jeweils die `getClass()`-Methode aufrufen, dann bekommen wir die jeweiligen Typen zurückgegeben:

```java linenums="1"
Viereck v1 = new Viereck(10,20,30,40);
Rechteck r1 = new Rechteck(10, 20);
Quadrat q1 = new Quadrat(30);
System.out.println(v1.getClass());	// von Object geerbt
System.out.println(r1.getClass());	// von Viereck -> Object geerbt
System.out.println(q1.getClass());	// von Rechteck -> Viereck -> Object geerbt
```
Die Ausgaben sind:
```bash
class Viereck
class Rechteck
class Quadrat
```
Wichtig: `getClass()` gibt jedoch nicht den *Compilertyp*, sondern den *Laufzeittyp* zurück. 

#### Compilertyp vs. Laufzeittyp

Was sind *Compiler-* und *Laufzeittypen*? *Compilertyp* wissen wir schon. Bei der Deklaration einer Variablen geben wir den Compilertypen der Variablen an. Was wir aber auch wissen, ist, dass jedes `Rechteck` **ist auch ein** `Viereck`. Das erlaubt uns, auch Folgendes zu schreiben:

```java linenums="1"
Viereck v = new Rechteck(10, 20);
```

Jetzt ist `v` vom (Compiler-)Typ `Viereck`, aber vom *Laufzeittyp* `Rechteck`. Die Referenzvariable `v` zeigt auf ein `Rechteck`-Objekt. Mit `getClass()` erfragen wir den *Laufzeittyp*, d.h.

```java linenums="1"
Viereck v = new Rechteck(10, 20);		// Compilertyp von v ist Viereck
System.out.println(v.getClass());		// Laufzeittyp von v ist Rechteck
```
erzeugt die Ausgabe
```bash
class themen.vererbung.Rechteck
```

Wir können also auch soetwas machen:
```java linenums="1"
Viereck[] va = new Viereck[3];
va[0] = new Viereck(10,20,30,40);		// Compilertyp von va[0] ist Viereck, Laufzeittyp ist Viereck
va[1] = new Rechteck(10, 20);			// Compilertyp von va[1] ist Viereck, Laufzeittyp ist Rechteck
va[2] = new Quadrat(15);				// Compilertyp von va[2] ist Viereck, Laufzeittyp ist Quadrat

System.out.println(va[0].getClass());	// Viereck
System.out.println(va[1].getClass());	// Rechteck
System.out.println(va[2].getClass());	// Quadrat
```

Das bedeutet auch, dass sogar soetwas möglich ist:
```java linenums="1"
Object o1 = new Viereck(10,20,30,40);	// Compilertyp von o1 ist Object, Laufzeittyp ist Viereck
Object o2 = new Rechteck(10, 20);		// Compilertyp von o2 ist Object, Laufzeittyp ist Rechteck
Object o3 = new Quadrat(15);			// Compilertyp von o3 ist Object, Laufzeittyp ist Quadrat

System.out.println(o1.getClass());		// Viereck
System.out.println(o2.getClass());		// Rechteck
System.out.println(o3.getClass());		// Quadrat
```
> Der Compilertyp einer (Referenz-)Variablen wird durch die Deklaration bestimmt. Der Laufzeittyp wird bestimmt durch das konkrete Objekt, auf das die Referenzvariable zeigt. 

#### Welche Objektmethoden anwendbar? - Typecast

Wenn wir schonmal bei der Unterscheidung zwischen Compilertyp und Laufzeittyp sind, dann können wir gleich der Frage nachgehen, welche Objektmethoden anwendbar sind. Erinnern wir uns dazu nochmal an die Erweiterung der Klasse `Rechteck`. Dort hatten wir eine Objektmethode `flaecheninhalt()` definiert, die in der Klasse `Viereck` nicht existiert. 

Wir hatten folgenden Fall:
```java linenums="1"
Viereck v1 = new Viereck(10,20,30,40);
// System.out.println(v1.flaecheninhalt()); 	// flaecheninhalt() existiert für Viereck nicht
Rechteck r1 = new Rechteck(10, 20);
System.out.println(r1.flaecheninhalt()); 		// flaecheninhalt() existiert für Rechteck (=200)
```

Wenn wir nun 
```java linenums="1"
Viereck v = new Rechteck(10, 20);
```
haben, `v` also den Compilertyp `Viereck` hat und den Laufzeittyp `Rechteck`. Können wir dann 
```java linenums="1"
System.out.println(v.flaecheninhalt());		// Fehler!
```
aufrufen? Die Antwort ist **nein!** Das ist auch insofern logisch, als dass dieser Aufruf ja bereits zum Compilezeit möglich sein muss. Dem Typ `Viereck` steht diese Methode aber nicht zur Verfügung. Das geht also nicht. Was wir aber in diesem Fall machen können, ist eine [explizite Typkonvertierung](../variablen/#explizite-typkonvertierung). 
```java linenums="1"
Viereck v = new Rechteck(10, 20);
Rechteck r = (Rechteck)v; 			// geht, weil der Laufzeittyp Rechteck ist
System.out.println(r.flaecheninhalt());		// geht, weil der Compilertyp von r Rechteck ist
```

Nochmal im Detail: 

- In Zeile `1` definieren wir eine Referenzvariable `v` vom *Compilertyp* `Viereck`. 
- In Zeile `2` definieren wir eine Referenzvariable `r` vom *Compilertyp* `Rechteck`. 
- Weil `r` vom *Compilertyp* `Rechteck` ist, können wir für `r` die Objektmethode `flaecheninhalt()` aufrufen (für `v` nicht!). 
- Dass die Typkonvertierung in Zeile `2` auch tatsächlich gelingt, liegt (zur *Laufzeit*) daran, dass der *Laufzeittyp* von `v` `Rechteck` ist. Wäre das nicht der Fall, würde die Typkonvertierung scheitern - aber erst zur Laufzeit (mit einer `ClassCastException`). 

#### `instanceof` vs. `getClass()`

Wie gesagt, ermitteln wir mit `getClass()` den Laufzeittypen einer Referenzvariablen. Dafür gibt es auch noch ein anderes Schlüsselwort in Java, nämlich `instanceof`. Das ist ein Operator, mit dessen Hilfe wir einen Vergleich mit Typen anstellen können. Zunächst ein Beispiel:

```java linenums="1"
Viereck v = new Viereck(10,20,30,40);
if(v instanceof Viereck)
{
	System.out.println("v ist vom Typ Viereck");
}
```

In Zeile `2` sehen wir die Anwendung des `instanceof`-Operators. Er gibt ein `boolean` zurück, je nachdem die Variable vom angegebenen Typen ist oder nicht. Der obige Code erzeugt also die Ausgabe 
```bash
v ist vom Typ Viereck
```
auf der Konsole. Angenommen, wir haben nun folgendes Beispiel:
```java linenums="1"
Object o = new Quadrat(15);	// Compilertyp Object, Laufzeittyp Quadrat
if(o instanceof Object)		// true
{
	System.out.println("o ist vom Typ Object");
}
if(o instanceof Viereck)	// true
{
	System.out.println("o ist vom Typ Viereck");
}
if(o instanceof Rechteck)	// true
{
	System.out.println("o ist vom Typ Rechteck");
}
if(o instanceof Quadrat)	// true
{
	System.out.println("o ist vom Typ Quadrat");
}
```
, dann sind alle Bedingungen `true`, d.h. es wird folgende Ausgabe erzeugt:
```bash
o ist vom Typ Object
o ist vom Typ Viereck
o ist vom Typ Rechteck
o ist vom Typ Quadrat
```
`instanceof` prüft also jeden möglichen Laufzeittyp (wir wissen ja, dass ein Objekt vom Typ `Quadrat` **ist ein** Objekt vom Typ `Rechteck` **ist ein** Objekt vom Typ `Viereck` **ist ein** Objekt vom Typ `Object`). Das gleiche gilt auch für:
```java linenums="1"
Quadrat q = new Quadrat(15); // Compilertyp Quadrat, Laufzeittyp Quadrat
if(q instanceof Object)		// true
{
	System.out.println("q ist vom Typ Object");
}
if(q instanceof Viereck)	// true
{
	System.out.println("q ist vom Typ Viereck");
}
if(q instanceof Rechteck)	// true
{
	System.out.println("q ist vom Typ Rechteck");
}
if(q instanceof Quadrat)	// true
{
	System.out.println("q ist vom Typ Quadrat");
}
```
, dann sind alle Bedingungen `true`, d.h. es wird folgende Ausgabe erzeugt:
```bash
q ist vom Typ Object
q ist vom Typ Viereck
q ist vom Typ Rechteck
q ist vom Typ Quadrat
```

> Die Methode `getClass()` liefert also den **konkretesten (speziellsten)** Laufzeittypen zurück. Mit `instanceof` können **alle** Laufzeittypen abgefragt werden. Für eine beliebige Variable `var`, egal welchen Referenztyps, gilt immer, dass `var instanceof Object` `true` ergibt, d.h. jede Referenzvariable ist immer auch vom (Laufzeit-)Typ `Object`. 

### Die Objektmethode `toString()`

In jeder Klasse, die wir erstellen, erben wir von `Object` die Objektmethode `toString()`. Wenden wir diese Methode also einmal für unsere Klasse `Viereck`an:
```java linenums="1"
Viereck v = new Viereck(10,20,30,40);
System.out.println(v.toString());
```
Dann erhalten wir eine etwas kryptische Ausgabe:
```bash
Viereck@279f2327
```
wobei `Viereck` für die Klasse steht und `@279f2327` scheint irgendeine Referenzadresse zu sein. Interessant an der `toString()`-Methode ist, dass wir die gleiche Ausgabe auch dann erzielen, wenn wir nur 
```java linenums="1"
Viereck v = new Viereck(10,20,30,40);
System.out.println(v);
```
aufrufen, also der Methode `System.out.println()` nur `v` und nicht `v.toString()` übergeben. Das liegt daran, dass `System.out.println()` [überladen](../objekte/#uberladen-von-methoden) ist und - unter anderem - die beiden Implementierungen 
```java
System.out.println(String s) {}
System.out.println(Object o) {}
```
existieren. Wenn wir `System.out.println(v.toString());` aufrufen, wird die Implementierung von `System.out.println(String s) {}` verwendet (der `String s` wird ausgegeben). Wenn wir `System.out.println(v);` aufrufen, wird die Implementierung von `System.out.println(Object o) {}` verwendet und dabei wird nämlich `System.out.println(o.toString());` aufgerufen. 

Wenn wir nun also die Methode `toString()` **überschreiben** (ist ja von `Object` geerbt), dann gewinnen wir zwei Effekte:

1. wir erstellen eine textuelle Reprässentation unserer Objekte und
2. wir müssen `System.out.println()` nur noch die Referenzvariable `ref` auf unser Obejkt übergeben (und nicht `ref.toString()`)

Erweitern wir also die Klasse `Viereck` um eine Implementierung der `toString()`-Methode:
```java linenums="1" hl_lines="24-28"
public class Viereck
{
	protected int a,b,c,d;			// Seiten
	
	public Viereck(int a, int b, int c, int d)
	{
		this.a = a;
		this.b = b;
		this.c = c;
		this.d = d;
	}
	
	public int umfang()
	{
		return this.a + this.b + this.c + this.d;
	}
	
	public void print()
	{
		System.out.print(this.toString());		// siehe unten
		System.out.println(" Umfang des Vierecks : " + this.umfang());
	}
	
	@Override
	public String toString()
	{
		return "[ a=" + this.a + ", b=" + this.b + ", c=" + this.c + ", d=" + this.d + " ] ";
	}
}
```

Wir verwenden auch hier die `@Override`-Annotation, um dem Compiler zu sagen, dass wir die `toString()`-Methode von `Object` überschreiben wollen (nicht, dass wir z.B. ausversehen `tostring()` schreiben und somit eine neue Objektmethode erstellen). In der `toString()`-Methode implementieren wir eine geeignete Repräsentation des Objektes (hier die Seitenlängen des Vierecks). Nun erzeugen die Anweisungen
```java linenums="1"
Viereck v = new Viereck(10,20,30,40);
System.out.println(v);		// entspricht System.out.println(v.toString());
```
eine deutlich bessere Ausgabe, nämlich
```bash
[ a=10, b=20, c=30, d=40 ]
```

> Wir sollten uns angewöhnen, die `toString()`-Methode **immer**, d.h. in allen Klassen, die wir erstellen, zu überschreiben!


### Die Objektmethode `equals()`

Wir wiederholen zunächst nochmal in Kürze den Abschnitt über [Referenzvergleiche von Objekten](../methodenstack/#referenzvergleiche-mit). Angenommen, wir haben folgende Vierecke:
```java
Viereck v3 = new Viereck(10,20,30,40);
Viereck v4 = new Viereck(10,20,30,40);
System.out.println(v3==v4); 	// Referenzvergleich!! false - zwei Objekte
```
Wir könnten auf die Idee kommen, dass `v3==v4` `true` ergibt, weil für uns die beiden Objekte von `Viereck` gleich sind. Aber woher soll der Compiler oder die Laufzeitumgebung *wissen*, dass diese `Viereck`-Objekte gleich sind? 

> Der Operator `==` vergleicht nur die Referenzen und ist `false`, wenn die Referenzen auf zwei verschiedene Objekte zeigen. 

Mithilfe der `equals()`-Methode können wir definieren, wann Objekte der Klasse **gleich** sein sollen. Wir können aber nicht den Operator `==` überschreiben. Dieser bleibt für Referenztypen immer ein Referenzvergleich!

Wir wollen unsere Klasse `Viereck` also um eine `equals()`-Methode erweitern und in dieser `equals()`-Methode festlegen, wann zwei `Viereck`-Objekte gleich sein sollen (wenn ihre Seitenlängen gleich sind). Wir versuchen folgendes:

```java linenums="1" hl_lines="31-35"
public class Viereck
{
	protected int a,b,c,d;			// Seiten
	
	public Viereck(int a, int b, int c, int d)
	{
		this.a = a;
		this.b = b;
		this.c = c;
		this.d = d;
	}
	
	public int umfang()
	{
		return this.a + this.b + this.c + this.d;
	}
	
	public void print()
	{
		System.out.print(this.toString());		// siehe unten
		System.out.println(" Umfang des Vierecks : " + this.umfang());
	}
	
	@Override
	public String toString()
	{
		return "[ a=" + this.a + ", b=" + this.b 
		+ ", c=" + this.c + ", d=" + this.d + " ] ";
	}
	
	@Override
	public boolean equals(Viereck v)
	{
		// Implementierung von equals()
	}
}
```

Das führt leider zu einem Fehler. Der Compiler beschwert sich darüber, dass wir die geerbte `equals()`-Methode so gar nicht überschreiben. Tatsächlich erben wir nicht `equals(Viereck v)`, sondern `equals(Object o)` (woher sollte `Object` auch `Viereck` kennen?). Wir müssen also folgende Methode überschreiben:
```java
@Override
public boolean equals(Object o)
{
	// Implementierung von equals()
}
```

Natürlich erwarten wir, dass sich das aufrufende Viereck mit einem anderen Viereck vergleicht. Die Methode ist aber so implementiert, dass jedes beliebige Objekt als Parameter übergeben werden kann. Theoretisch wäre also z.B. folgender Aufruf möglich:
```java
Viereck v = new Viereck(10,20,30,40);
Point p = new Point(3,4);
Systems.out.println(v.equals(p));
```

Das soll natürlich `false` ergeben. Die Implementierung von `equals(Object o)` muss folgende Bedingungen erfüllen:

1. *Null-Akzeptanz:* für jede Referenz `x` ungleich `null` liefert `x.equals(null)` den Wert `false`
2. *Reflexivität:* für jede Referenz `x` ungleich `null` liefert `x.equals(x)` den Wert `true`
3. *Symmetrie:* wenn `x.equals(y)` `true` ergibt, dann muss auch `y.equals(x)` `true` ergeben (und umgedreht)
4. *Transitivität:* wenn `x.equals(y)` und `y.equals(z)` jeweils `true` ergeben, dann muss auch `x.equals(z)` `true` ergeben
5. *Konsistenz:* der Aufruf `x.equals(y)` muss immer den gleichen Wert ergeben

Das hört sich komplizierter an, als es ist. Wir werden sehen, dass wir bei der Implementierung von `equals(Object o)` immer gleich vorgehen. Wir führen zunächst ein paar Prüfungen durch:

1. prüfen, ob `null`-Referenzen vorliegen --> (wenn ja, dann `false`)
2. prüfen, ob keine identischen Objekte verglichen werden (dasselbe Objekt vergleicht sich mit sich selbst) --> (wenn ja, dann `true`)
3. prüfen, ob Objekte des gewünschten Typs verglichen werden --> (wenn nein, dann `false`)

```java linenums="1"
@Override
public boolean equals(Object other)
{
	if(other==null) return false; 		// Null-Akzeptanz
	if(this==other) return true; 		// Reflexivität
	if(this.getClass() != other.getClass()) return false; 			// ungleiche Typen

	// wenn wir hier die Methode noch nicht verlassen haben, dann
	// wissen wir, dass other vom Typ Viereck ist und auf ein 
	// Viereck-Objekt zeigt

}
```

- in Zeile `4` prüfen wir, ob das als Parameter übergebene Objekt überhaupt existiert. Wenn nicht (Referenz `null`), geben wir `false` zurück. 
- in Zeile `5` prüfen wir, ob das aufrufende Objekt dasselbe ist, wie das als Parameter übergebene Objekt (vergleich mit sich selbst). Wenn ja, geben wir `true` zurück. 
- in Zeile `6` prüfen wir, ob das aufrufende Objekt und das als Parameter übergebene Objekt den gleichen Typ haben (also hier `Viereck`). Wenn nicht, geben wir `false` zurück. 

Wenn diese Prüfungen alle `false` waren, dann wissen wir danach, dass `other` vom (Laufzeit-)Typ `Viereck` ist und auf ein `Viereck`-Objekt zeigt. Nun können wir den **eigentlichen Objektvergleich** durchführen. Dazu müssen wir jedoch `other` in den Typ `Viereck` konvertieren:

1. da beide Objekte vom gleichen Typ sind (`Viereck`), kann das Objekt aus dem Parameter in den vergleichenden Typ umgewandelt werden (z.B. `Object` nach `Viereck`)
2. dann können wir die Eigenschaften vergleichen, die für die „Gleichheit“ relevant sind (z.B. `radius` bei `Circle`, `kontonummer` bei `Konto`, `a` und `b` bei `Rectangle` usw. - hier: die vier Seiten des Vierecks `a`, `b`, `c` und `d`)

```java linenums="1"
@Override
public boolean equals(Object other)
{
	if(other==null) return false; 		// Null-Akzeptanz
	if(this==other) return true; 		// Reflexivität
	if(this.getClass() != other.getClass()) return false; 			// ungleiche Typen

	// wenn wir hier die Methode noch nicht verlassen haben, dann
	// wissen wir, dass other vom Typ Viereck ist und auf ein 
	// Viereck-Objekt zeigt

	// jetzt kommt der eigentliche Objektvergleich auf Gleichheit
	// damit wir ueberhaupt auf die Objektvariablen a, b, c, d von other
	// zugreifen können, muessen wir es nach Viereck konvertieren
	Viereck otherV = (Viereck)other;
	return this.a==otherV.a && this.b==otherV.b && this.c==otherV.c  && this.d==otherV.d;
}
```

- in Zeile `15` führen wir eine explizite Typkonvertierung durch. Wir wissen an dieser Stelle ja bereits (aus Zeile `6`), dass es sich bei `other` um den Laufzeittyp `Viereck` handelt. Die Konvertierung klappt also. Weil `other` den Compilertyp `Object` hat, können wir für `other` nicht auf die Objektvariablen `a`, `b`, `c`, `d` zugreifen. Wir müssen also konvertieren. 
- in Zeile `16` führen wir dann den eigentlichen Vergleich durch. Hier vergleichen wir die Seiten miteinander. Wir berücksichtigen nicht, dass Vierecke auch gedreht gleich sein können. Das ist Auslegungssache und Ihre Entscheidung, wann Objekte tatsächlich gleich sein sollen. 

Jetzt können wir die Gleichheit von zwei `Viereck`-Objekten mithilfe von `equals()` ermitteln:
```java
Viereck v3 = new Viereck(10,20,30,40);
Viereck v4 = new Viereck(10,20,30,40);
Viereck v5 = new Viereck(11,22,33,44);

System.out.println(v3.equals(v4)); 	// true
System.out.println(v3.equals(v3)); 	// true
System.out.println(v4.equals(v3)); 	// true
System.out.println(v3.equals(v5)); 		// false
System.out.println(v3.equals(null)); 	// false
```

!!! success
	Mithilfe der `equals()`-Methode haben wir eine einheitliche Möglichkeit, die Gleichheit von Objekten zu definieren. Die Implementierung der `equals()`-Methode folgt immer dem gleichen Schema. Wir führen zunächst die drei Prüfungen auf Null-Akzeptanz, Reflexivität und ungleiche Typen aus, konvertieren `other` dann in unseren Klassentyp und führen den eigentlichen Vergleich auf Gleichheit der Objekte durch. Wir sollten `equals()`, wie auch `toString()`, von nun an für alle unsere Klassen implmentieren. 

### Die Objektmethode `hashCode()`

Die Idee der `hashCode()`-Methode besteht darin, ein Objekt durch eine ganze Zahl zu repäsentieren. Diese Zahl wird verwendet, um Objekte in sogenannte *hashbasierte Container* einzusortieren. Das sind Datenstrukturen, in denen viele Objekte gespeichert werden und die Speicherung über einen *Hashwert* verteilt wird. Wir werden solche *hashbasierten Container* im 2. Semester kennenlernen, wenn wir uns mit *Collections* beschäftigen. Zum jetzigen Stand kümmern wir uns um diese Methode nicht weiter, wollen sie aber doch immer genau dann überschreiben, wenn wir die `equals()`-Methode implementieren. Es soll folgendes gelten:

> Wenn zwei Objekte laut `equals()`-Methode gleich sind, dann erzeugen sie auch den gleichen Hashcode mit der `hashCode()`-Methode. 

Es soll also gelten: wenn `x.equals(y)==true`, dann `x.hashCode()==y.hashCode()`. Wenn wir also die `equals()`-Methode überschreiben, dann überschreiben wir auch die `hashCode()`-Methode, um die genannte Bedingung zu erfüllen. Da wir für das `Viereck` die Seitenlängen verwendet haben, um die Gleichheit von zwei Vierecken zu definieren, können wir diese Seitenlängen auch verwenden, um einen HashCode zu erzeugen:

```java
@Override
public int hashCode()
{
	return this.a + this.b + this.c + this.d;
}
```

Mit dieser Implementierung ist gegeben, dass zwei Vierecke, die laut `equals()`-Methode gleich sind (haben die gleichen Seitenlängen), auch den gleichen HashCode haben. Es muss (zum Glück) nicht gelten, dass zwei Vierecke, die laut `equals()`-Methode ungleich sind, einen unterschiedlichen HashCode haben müssen. 

### Die Objektmethode `clone()`

Die Objektmethode `clone()` liefert einen identischen Clone (eine identische Kopie) des aufrufenden Objektes zurück. Wir wollen uns an dieser Stelle gar nicht weiter detailliert um `clone()` kümmern. Wir kommen darauf zurück, wenn wir im 2. Semester *Interfaces* kennenlernen. Die Methode `clone()` ist auch [nicht unumstritten](https://dzone.com/articles/java-cloning-copy-constructor-vs-cloning) - das aber nur zur Information, wie auch ein Beispiel für die folgende mögliche Implementierung der Methode in der Klasse `Viereck`. 

```java
@Override
protected Object clone()
{
	return new Viereck(this.a, this.b, this.c, this.d);
}
```

Das dient nur zum Verständinis der Idee von `clone()`. Im Gegensatz zu `toString()` und `equals()` (und also auch `hashCode()`) werden wir `clone()` nicht so oft überschreiben. 

!!! success
	Wir haben mit `Object` die *Mutter aller Klassen* in Java kennengelernt. Jede Klasse in Java erbt (implizit) von `Object`. Jede Referenzvariable ist somit (auch) vom Laufzeittyp `Object`. Für alle Klassen, die wir in Zukunft schreiben, werden wir die Objektmethoden `toString()` und `equals()` (und also auch `hashCode()`) überschreiben. 

## Polymorphie

*Polymorphie* gehört neben der Datenkapselung und der Vererbung zu den wesentlichen Konzepten der objektorientierten Programmierung. Die Grundidee der Polymorphie ist, dass es verschiedene Methoden gibt, die gleich heißen und dass entweder der Compiler (statisch) oder die Laufzeitumgebung (dynamisch) auswählt, welche dieser Methoden ausgeführt wird. Man unterscheidet zwischen *statischer* und *dynamischer Polymorphie*. 

### Statische Polymorphie

*Statische Polymorphie* haben wir in Verbindung mit dem **Überladen von Methoden**. Der Compiler kann (an der Methodensignatur) erkennen, welche Methode aufgerufen wird. Angenommen, wir haben folgende Methoden:
```java
public void printArray(int[] arr)
{
	// Ausgabe eines int[]-Arrays
}

public void printArray(char[] arr)
{
	// Ausgabe eines char[]-Arrays
}

public void printArray(double[] arr)
{
	// Ausgabe eines double[]-Arrays
}

public void printArray(String[] arr)
{
	// Ausgabe eines String[]-Arrays
}

public void printArray(Object[] arr)
{
	// Ausgabe eines Object[]-Arrays
}
```
, dann wird durch den Typs des als Parameter übergebenen Arrays klar, welche dieser Methoden aufgerufen wird. Es wird also unter vielen Implementierungen durch den Compiler die "richtige" ausgewählt. 

### Dynamische Polymorphie

*Dynamische Polymorphie* wird durch Vererbung und insbesondere durch das **Überschreiben von Methoden** ermöglicht. Wir betrachten folgendes Beispiel - gegeben sind drei Klassen `Base`, `Sub` und `SubSub`:

```java linenums="1"
public class Base 
{
	public void methodBase()
	{
		System.out.println("Base");
	}
}
```

```java linenums="1"
public class Sub extends Base 
{
	@Override
	public void methodBase()
	{
		System.out.println("Sub");
	}
}
```

```java linenums="1"
public class SubSub extends Sub 
{
	@Override
	public void methodBase()
	{
		System.out.println("SubSub");
	}
}
```

Die Klasse `Sub` erbt von `Base` und die Klasse `SubSub` erbt von `Sub`. In beiden Kindklassen wird die Methode `methodBase()` überschrieben, die in `Base` erstmalig definiert wird. Angenommen, wir haben nun folgende `main()`-Methode:

```java linenums="1"
public void main() 
{
	Base[] base = new Base[3];
	base[0] = new Base();		// Compilertyp Base, Laufzeittyp Base
	base[1] = new Sub();		// Compilertyp Base, Laufzeittyp Sub
	base[2] = new SubSub();		// Compilertyp Base, Laufzeittyp SubSub

	base[0].methodBase();		// Base
	base[1].methodBase();		// Sub
	base[2].methodBase();		// SubSub
}	
```

Wir erstellen uns also ein Array, deren Elemente vom Compilertyp `Base` sind. Das erste Element ist eine Referenz auf ein `Base`-Objekt, das zweite Element ist eine Referenz auf ein `Sub`-Objekt und das dritte zeigt auf ein `SubSub`-Objekt. Für alle drei Referenzvariablen wird nun die `methodBase()`-Methode aufgerufen. Es werden folgende Ausgaben erzeugt:

```bash
Base
Sub
SubSub
```

Das bedeutet, dass die Laufzeitumgebung von Java die *speziellstmögliche* Implementierung der Methode auswählt. Mit *speziellstmöglich* ist gemeint, dass die Implementierung des speziellsten Laufzeittypen ausgewählt wird. In der Vererbungshierarchie `SubSub`--> `Sub` --> `Base` ist `SubSub` der speziellste Typ, `Sub` ist spezieller als `Base`, aber allgemeiner als `Sub` und `Base` ist allgemeiner als `Sub` und erst recht als `SubSub`. 

- Der speziellste Laufzeittyp von `base[0]` ist `Base` und somit wird die `methodBase()`-Implementierung der Klasse `Base` verwendet. 
- Der speziellste Laufzeittyp von `base[1]` ist `Sub` und somit wird die `methodBase()`-Implementierung der Klasse `Sub` verwendet. 
- Der speziellste Laufzeittyp von `base[2]` ist `SubSub` und somit wird die `methodBase()`-Implementierung der Klasse `SubSub` verwendet. 

!!! success
	*Polymorphie* ist ein tolles Konzept der objektorientierten Programmierung. Der Nutzen von Polymorphie wird uns jetzt noch nicht vollständig deutlich. Wir werden aber immer wieder darauf hinweisen, wenn wir Polymorphie im Einsatz sehen. Vielleicht erkennen Sie ja jetzt besser, warum z.B. die Methode `System.out.println(Object o)` so funktioniert. Spätestens, wenn wir *Interfaces* behandeln, kommen wir auf dieses Konzept zurück. 

