# oop-notes
## Lecture 2
- `final` är Java's version av `const`
- `import static java.lang.system.out` fixar så att man slipper `System` och bara kan göra `out.println(...)`
- `123 + 456 + "hi"` => `"579hi"`, `"hi" + 123 + 456` => `"hi123456"`
- `nextInt()` läser bara Int från strömmen, behåller kvar `\n` i strömmen!
  - kan bli problematiskt om man läser in String senare

---

- Program struktur: Först input, sedan "Process" (non-IO), sist output
- IntelliJ: Alt+Enter under hover => import suggestion
- `package <mapp>`, `<mapp>` ska vara mappen/path programmet ligger i
- `int / int` => heltalsdivision
  - använd cast `(double)` för vanlig division

---

- `rand.nextInt(100)` inkluderar ej 100, d.v.s. ger tal 0 t.o.m. 99
- konvention: `nGuesses` för number of guesses
- assignment `var = val` return:ar `val`
- `str == str2` kollar *adresserna*, inte värdena!
  - använd `str.equals(str2)` istället
- `{}` syntax for arrays
  - `int[] arr = {1, 2};` eller `int[] arr; arr = new int[]{1, 2};`
  - `int[] arr = new int[3]` <=> `int[] arr = {0, 0, 0}` (or null\*3 for pointers or false\*3 for booleans)
  - fixed size

## Lecture 3
- IntelliJ kör inte filen man har öppnad utan den som är vald uppe i högra hörnet bredvid play-knappen
- Tydligen kan man bara hålla 7 +- 2 fakta i arbetsminnet samtidigt enligt läraren?
- Gör test() som testar funktioner
  - `exit()` i slutet av `test` funktionen så att programmet slutar köra efter test
    - behövs bara om `test()` körs innanför programmet
  - `test` funktionen printar (helst) flera property results (true|false)
  - behåll denna funktionen, men du behöver inte alltid köra den
- Classes är lite som structs
  - Om man har `class Player {...}` initierar `Player p1 = new Player()` en ny Player
    - innehåller default data (0, null, etc.) om man inte har en initierare
  - `class Player {... Player(...) {...} ...}` tillåter `new Player(...)`
    - t.ex. `Player(String n, int p) {name = n; points = p}` tillåter `new Player("Olle", 3)`
 
## Lecture 4
- Fokusera på läsbarhet över performance
  - performance är ej ett krav i kursen
- Alla .class filer börjar med hex `CA FE BA BE` för att markera att det är bytecode
- Man kan skriva ints med underscore `1_000_000` syntax
- Med arrays kopieras referenser/adresser
  - Samma med cmp: `arr == arr2` jmf. endast adresserna!
- Referenser pekar alltid på objekt i Java
  - Kan ej peka på andra variabler som i C(++), Rust, etc.
- `final int[] arr` gör *adressen* const, inte själva `arr`!
- `new Object` blir en pekare till ett nytt `Objekt`
- `this` pekar på objektet man är i
  - t.ex. `this.name = name`: VL = objektets name, HL = input name

---

- IntelliJ: `class`: right-click -> generate -> constructure -> ...
- Pen&Paper: lär dig rita "Before" & "After" diagram
  - vad pekar variabler på, vilka värden har de, before & after
  - rita variabler som "lådor"
    - pekare blir lådor med en pil inuti som dras till något
    - array är pekare i låda till en ruta med en rad av lådor sammankopplade inuti
  - Operationer görs i mitten mellan "Before" och "After", separerat med linjer

---

- Primitiva typer är non-pointer, non-primitive är pointer (till objekt)
- String literals, i.e. `"hello"` är typ "anonyma" objekt
- Note: `s1 = "zzz"; s2 = "zzz"` optimeras till `s1 = "zzz"` så att `s1 == s2` => `s1 == s1`!
- `arr = null; arr[i]` => **N**ull **P**ointer **E**xception
- Automatisk deref i Java
  - Behövs inte `*`
  - Ingen pointer arithmetic, allt är implicit

## Lecture 5
- javac läser bara första raden av dekl/init innan den läser resten
  - så att man kan använda funktioner innan de är definierade
  - t.ex. läser `void program() {<program body>} void swap(...) {...}` först, sedan deras function bodys
    - `<program body>` kan t.ex. då innehålla `swap(...)`
  - inte direkt användbart för kursen men bra om du ska skriva en egen kompilator
  - notera att det här endast fungerar eftersom man bara kan köra kod inuti en funktion hela tiden

---

- Fisher-Yates shuffling
  - `for(int i = arr.length; i > 1; i--)`
  - Slumpa index j (`rand.nextInt(i)`), byt plats: `arr[j]` och `arr[i - 1]`
  - Slumpa index j igen, byt plats: `arr[j]` och `arr[i - 1]`
  - osv.

## Lecture 5+n
- `enum Enum { E1, E2, ...}`, `Enum e = Enum.E2`
- Enums också referenser som klasser, men:
  - varje "item" (t.ex. `E1`) är en referens till ett unikt objekt
  - betyder att man fortfarande kan göra `e == Enum.E2` eftersom `e` och `Enum.E2` är samma referens
- `Integer`, `Double`, etc. är "boxed" ints/doubles
  - d.v.s. referenser till ints/doubles
- Boxing & unboxing brukar ske automatiskt, men `==` är ett undantag
  - t.ex. `Integer i = 4; i++` boxar först 4 och sedan unboxar (deref) den i för att öka 4 till 5
  - `>=`, `<=`, `>`, etc. fixar fortfarande unboxing
  - `d1 == 1 * d2` unboxar också... så lite jobbigt som i JS tydligen ;-;
- **NOTE:** Optimisering i Java: Alla Integer objekt med värde under 128 är samma objekt
  - d.v.s. `Integer i = 127; Integer j = 127; i == j // true`

---

- Finns function overloading i Java
  - t.ex. `int f(int i) {...}` och `double f(double d)` kan både finnas
  - måste skilja i parametrarna, inte endast return-type
    - return-type kan dessutom vara samma så länge pars skiljer

---

- Generic methods
  - `<T> void shuffle(T[] arr) {...}`
  - T = any ref type
    - only ref types because byte, int, double, etc. different sizes while all ref types are 32/64-bit
- (type inference kan sägas "typ-härledning" på svenska)
- "Operator > not defined for T"
  - solve using `<T extends Comparable<T>>`

---

- Super & subtyper:
  - sub < super
    - t.ex. int: sub < double: super
      - "double = int|fraction"
  - subtyper har fler operationer än supertyper
    - alltså mer specialiserade, medan super är mer generell
  - type cast kan endast göra när det finns sub-super relation
    - i.e. `1 == (int) true` funkar inte
  - `Objekt` är super till allt
- ClassCastException (runtime)
- If `S <: T`, then `S[] <: T[]`
  - Problematiskt: `Object[] os = new Integer[123]; os[0] = 4.5` - kompilerar men runtime exception!

## Lecture 5+n+1
- Java fixar `.f()` om du gör `f(...) {...}` i class (ingen `self` behövs)
- Om du `return obj` i funktion kan du göra chaining: `obj.f().g().h()`
- Generic class: `class Class<T>`
- for in: `for(<type> item : arr)`

---

- `Character c = 'x'`
- `Character.isWhitespace(' ') == true`
- `StringBuilder` tillåter modifiering av String, t.ex. med `.append(...)`
  - alltså vanlig String är immutable
- `obj.toString()` is automatically called on obj print if defined

## Lecture 5+n+3
- Finns inga vanliga funktioner i Java, bara metoder
  - Alla tillhör objekt/klasser, men om man vill använda en metod inuti samma klass kan man skippa `this.` och bara skriva funktionsnamnet
- `list.removeIf(e -> cond)` - bra sätt att ta bort saker från lista
- `Collections` innehåller `shuffle`, `sort`, etc.
- HashMap fungerar genom att man genererar `hashCode()` från input string, vilket är ett heltal som är index i en lista.
  - T.ex. `hashmap.get("Nisse")` skulle kunna generare hashCode 97 och därför leta på index 97 efter "Nisse" entry.
  - Alla Object har hashCode, eftersom man kan ha andra objekt än String som keys

---

- Alla klasser `extends Object` även om det inte skrivs ut, så man har tillgång till Object metoder
- Kan inte anropa constructors inuti egna klassen, använd `this(arg1, arg2, ...)` istället
- T.sk. från Rust är instansvariabler public by default, så använd `private` när det behövs
- Getters & Setters
  - Vissa IDEs kan generera

---

- (Interface) Typen (VL) anger vilka operationer som är tillåtna; inte värdet
  - så t.ex. `Object[] arr = {1, 2, 3}` tillåter inte `arr[0]++` för `++` finns ej för `Object[]`

---

- Unified Modelling Language

## Lecture 5+n+4
- Bra att separera CLI från själva spelet, t.ex. ha CLI class och Game class
- Constructor for Game => easier to start different variants of Game (i.e. different amount of players)

---

- **static:** a *static* variable is shared across instances of a class
  - i.e. `private static int i;` in class `Class` => `(new Class()).i == (new Class()).i`
  - changing the variable in one instance of the class changes it for every instance
- Klasser sparas i RAM efter kompilering
  - `static` variabler pekar på en "klassvariabel" inuti klassen i RAM
  - (klassinstanser sparas också på ett annat ställe i RAM)
- `static` variabler laddas vid klassladdning istället för instansladdning
  - alltså laddas/skapas de bara en gång istället för varje instans (förutom referensen till klassvariabeln såklart)
- `static` methods kan anropas med `Class.method(...)` istället för `(new Class(...)).method(...)`
  - dessa metoder finns också i själva klassen
  - **note:** klassmetoder kan *inte* använda instansvariabler (för de kan ju variera från instans till instans)
- `public static void main(...)`: måste vara `static` för när programmet laddas finns inga instanser än; metoden kan bara kommas åt via klassen

## Lecture 5+n+5
- Checked exceptions kontrolleras compile-time
  - Alltså lite som i Rust, fast mycket jobbigare att hantera (throw-try-catch hela tiden)
- Om man inte hanterar error i en metod måste man göra `throws Exception` efter funktionsnamnet (inkl. args)
  - i.e. `readFile(Path path) throws IOException`

---

- OOP: Försök minska beroende (dependencies)
- Gemensama metoder & variabler till *basklass*
  - i.e. `class Pet`, `class [Dog|Cat] extends Pet`
  - `super(...)` inuti Dog/Cat anropar `Pet(...)`
    - behövs för vissa variabler finns nu i Pet, så vi behöver göra `public Cat(...) { super(...); this.uniqueVar = val; }`
- `null` är sub till allt (jmf. `new Object()` super till allt)
- `SubClass [implements|extends] SuperClass`
- Interfaces can cast:as utan super-sub, så t.ex. `interface1Impl = (Interface1) interface2Impl` funkar (men kan ge runtime error)
- `class B extends A implements IX, IY` funkar
  - impl flera interface finns, men går *inte* att göra `extends` flera gånger (förutom att allt `extends Object` by default)
- `obj instanceof Class`: `true` om `obj` är sub till `Class`
  - kollar under runtime
- Glöm ej att `@Override` inte är samma som (operator) overload!
  - Overload: Kompilatorn checkar med typen (`**Super** s = new Sub()`)
  - Override: Runtime checkar med själva objektet (`Super s = **new Sub()**`)
  - kolla `O4OverrideVsOverload.java` exempel-filen
- `this` är själva objektet som skapats
  - så som `B extends A` och vi gör `A a = new B()` och sedan `b.returnThis()` får vi ut instansen av `B`

---

- Flödesschema-ish:
  - `extends`: pil med ihåligt pilhuvud som pekar mot super
  - `implements`: samma som `extends` fast pilen är streckad

## Lecture 5+n+6
- `static` + `@Override` funkar inte (p.g.a. att `@Override` checkas runtime per objekt snarare än per klass)
  - blir shadowing istället om man ändå har samma metoder
- `abstract class`: förhindrar construction av klassen utanför subklasser
  - användbart t.ex. om man inte vill tillåta `new Pet(...)` men fortfarande `new Cat(...)` (`Pet` är då `abstract`)
  - tillåter också att man impl i subklasserna fast ändå har `AbstractClass implements ...`
- `Class::method` skapar en referens till ett anonymt objekt som innehåller metoden
  - `Class` kan vara `this` för denna klassen
  - i princip method references, så användbart för callbacks
  - **note:** annorlunda syntax, t.ex. `callback.accept(...)` istället för bara `callback(...)`

## Last Lecture (extra)
- Gör inget om man göra några små fel på tentan eller inte skriver exakt Java
  - fokus på logik, problemlösning snarare än syntax
- De bedömmer ca. 15 min. per fråga
  - Om de inte hinner får man 0p och "?" först men kan förklara för läraren och få poängen sen ändå
- Brukar inte krävas mer än 20 rader per deluppgift
- Man får bara använda appendix-metoder på vissa uppgifter
- **Glöm ej:** Heltalsdivision vs. double division!
- Integer, Double, etc. unboxas vid `==` endast om minst en av VL & HL är en unboxed/primitive value
