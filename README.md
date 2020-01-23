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
