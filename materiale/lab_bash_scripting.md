# Esercizi Bash scripting

Ricorda che tutti gli script iniziano con `#!/bin/bash`

Puoi creare gli script da terminale con `nano <nome_script>.sh` oppure da un editor di testo (tipo il blocco note) salvando con estensione `.sh` 

## Esercizio 1 — Organizzatore di file per estensione

Crea una cartella `disordine/` che contiene questi file:

```
foto1.jpg  foto2.jpg  appunti.txt  relazione.txt
canzone.mp3  presentazione.pdf  note.pdf  README
```

Scrivi uno script `organizza.sh`, utilizzando i comandi bash che conosci, che:

1. Crea tre cartelle: `immagini`, `documenti`, `altro`;
2. Sposta tutti i file `.jpg` e `.png` dentro `immagini`;
3. Sposta tutti i file `.txt` e `.pdf` dentro `documenti`;
4. Sposta il file `README` (senza estensione) dentro `altro`;
5. Alla fine, verifica stampando il contenuto delle tre cartelle. 

**Comandi coinvolti:** `mkdir` (con più argomenti), `mv` con wildcard (`*.jpg`), `echo`, `ls`, redirezione dell'output.

---

## Esercizio 2 — Monitor di log semplificato

Hai un file di log `access.log` con righe di questo tipo (crealo a popolalo con `nano`):

```
2026-09-20 10:15:32 INFO avvio sistema
2026-09-20 10:16:01 WARNING spazio disco basso
2026-09-20 10:20:14 ERROR utente non trovato
2026-09-20 10:22:45 INFO login effettuato
2026-09-20 10:25:03 ERROR connessione al database fallita
```

Scrivi uno script `analizza_log.sh`, utilizzando i comandi bash che conosci, che:

1. Conta quante righe ci sono per ciascun livello di log (`INFO`, `WARNING`, `ERROR`);
2. Stampa le 3 righe di `ERROR` più recenti (assumendo che il file sia ordinato cronologicamente);

**Comandi coinvolti:** `grep`, `grep -c`, `tail`, `wc -l`, pipe (`|`).

---

## Bignami dei comandi

### `mkdir` — crea directory
```bash
mkdir cartella                        # crea una singola cartella
mkdir cartella1 cartella2 cartella3   # crea più cartelle in un colpo solo
mkdir -p percorso/annidato/profondo   # crea anche le cartelle intermedie mancanti
```

### `mv` — sposta o rinomina file/cartelle
```bash
mv file.txt destinazione/       # sposta un file in una cartella
mv vecchio.txt nuovo.txt        # rinomina un file
mv *.jpg immagini/              # sposta tutti i file con estensione .jpg
mv file1.txt file2.pdf cartella/  # sposta più file insieme
```
⚠️ Se il pattern (es. `*.jpg`) non trova corrispondenze, bash lo lascia invariato come stringa letterale e il comando darà un errore tipo "No such file or directory".

### `ls` — elenca il contenuto di una cartella
```bash
ls                # elenca la cartella corrente
ls cartella/      # elenca una cartella specifica
ls -l             # formato "lungo": permessi, proprietario, dimensione, data
ls -a             # mostra anche i file nascosti (che iniziano con .)
```

### `echo` — stampa testo a schermo
```bash
echo "Ciao mondo"
echo "Valore: $variabile"        # interpola una variabile
echo "Riga di log" >> report.txt # aggiunge una riga a un file (append)
```

### `grep` — cerca testo dentro file
```bash
grep "ERROR" access.log          # stampa le righe che contengono "ERROR"
grep -c "ERROR" access.log       # conta quante righe contengono "ERROR"
grep -n "ERROR" access.log       # mostra anche il numero di riga
grep -i "error" access.log       # ricerca case-insensitive
```

### `tail` — mostra le ultime righe di un file
```bash
tail access.log         # ultime 10 righe (default)
tail -n 3 access.log    # ultime 3 righe
```

### `wc -l` — conta le righe
```bash
wc -l access.log             # conta le righe di un file
grep "INFO" access.log | wc -l   # conta quante righe contengono "INFO"
```

### `read` — legge input dall'utente
```bash
echo "Inserisci una parola chiave:"
read parola
echo "Hai scelto: $parola"
```

### `|` (pipe) — collega l'output di un comando all'input del successivo
```bash
grep "ERROR" access.log | tail -n 3
grep "ERROR" access.log | wc -l
```

### Redirezione dell'output
```bash
comando > file.txt     # scrive l'output su file, SOVRASCRIVENDO il contenuto
comando >> file.txt    # aggiunge l'output alla fine del file (append)
```