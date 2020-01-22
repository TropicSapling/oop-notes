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
