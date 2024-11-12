# Exempel: Hitta den commit som bryter ett skript med `git bisect`

Detta projekt innehåller ett skript, `upper`, som tar en fil och konverterar dess innehåll till versaler. Syftet med detta exempel är att visa studenter hur man använder `git bisect` för att hitta den commit som introducerade ett fel.

## Beskrivning av filer

- **`upper`**: Ett Bash-skript som läser en fil och skriver ut innehållet i versaler.
- **`ignored-test`**: Ett testskript som verifierar att resultatet från `upper` är i versaler. Det är inkluderat i `.gitignore` för att inte spåras i Git.
- **`.gitignore`**: Fil som ser till att `ignored-test` inte läggs till i versionskontrollen.

## Hur man använder `git bisect` för att hitta ett fel

Följ dessa steg för att hitta den commit som introducerade felet:

1. Börja `git bisect`:
   ```bash
   git bisect start
