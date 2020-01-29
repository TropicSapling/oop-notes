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
- `x = n` return:ar `n`
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
