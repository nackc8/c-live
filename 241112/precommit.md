# pre-commit Hook

`pre-commit`-hooken är en av de viktigaste klient-sidiga Git-hooks eftersom den körs innan en commit skapas. Detta gör att den kan stoppa commit-processen om vissa villkor inte är uppfyllda, vilket hjälper till att upprätthålla kodkvalitet och konventionsregler i projektet.

## Exempel: Kontrollera att commit-meddelanden inte slutar med punkt

Här är ett exempel på en `pre-commit`-hook som kollar att commit-meddelandet inte slutar med en punkt. Om commit-meddelandet gör det, avbryts commit-processen och ett felmeddelande visas.

### Bashkod för `pre-commit`-hooken

```bash
#!/bin/bash
# Hook för att kontrollera att commit-meddelandet inte slutar med en punkt.

# Läser commit-meddelandet från standardplatsen
commit_msg_file=$(git rev-parse --git-dir)/COMMIT_EDITMSG

# Kollar om commit-meddelandet slutar med en punkt
if [[ $(tail -n 1 "$commit_msg_file") =~ \.$ ]]; then
    echo "Fel: Commit-meddelandet får inte sluta med en punkt."
    exit 1
fi

# Om kontrollen passerar, fortsätt med commit
exit 0
```

### Användning

1. Spara koden ovan i `.git/hooks/pre-commit`.
2. Gör filen körbar:
   ```bash
   chmod +x .git/hooks/pre-commit
   ```

När denna hook är på plats kommer den att kontrollera commit-meddelandet varje gång en commit skapas. Om meddelandet slutar med en punkt, stoppas commit-processen med ett felmeddelande.
