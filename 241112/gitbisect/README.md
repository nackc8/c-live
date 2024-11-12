# git bisect

## Exempel: Hitta den commit som bryter ett skript med `git bisect`

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
   ```

2. Markera den nuvarande commiten som dålig:
   ```bash
   git bisect bad
   ```

3. Markera den senaste kända bra commiten:
   ```bash
   git bisect good <commit-hash>
   ```

4. Kör `git bisect` med det ignorerade testskriptet för att automatisera processen:
   ```bash
   git bisect run ./ignored-test
   ```

`git bisect` kommer att köra `ignored-test` automatiskt vid varje steg för att avgöra om den aktuella commiten är bra eller dålig. När `git bisect` hittar den första dåliga commiten, kommer den att visa detaljer om den commiten.

## Förklaring av skript

### `upper`
```bash
#!/bin/bash
# Skript som konverterar en fils innehåll till versaler
if [ -f "$1" ]; then
    cat "$1" | tr '[:lower:]' '[:upper:]'
else
    echo "Fil saknas eller har inte angetts."
    exit 1
fi
```

### `ignored-test`
```bash
#!/bin/bash
# Testskript för upper
echo "Detta är ett test." > testfile.txt
./upper testfile.txt > result.txt

if grep -q '[a-z]' result.txt; then
    echo "Test misslyckades: Utdata innehåller små bokstäver."
    exit 1
else
    echo "Test godkänt: Utdata är i versaler."
    exit 0
fi
```

Använd detta exempel för att lära dig hur `git bisect` kan hjälpa till att hitta den commit som orsakar ett fel i din kodbas.
