# Sistema operativo 

---

## Esercizio 1 — Che SO sto usando?

**Obiettivo:** scoprire nome e versione del tuo sistema (e il *kernel*, il nucleo che sta sotto).

**Windows**:

premi `Win + R` poi:
```
winver
```

**macOS**:

menu  (mela) → *Informazioni su questo Mac*.

Oppure, da terminale:
```
sw_vers
```

**Linux**:

da terminale:
```
cat /etc/os-release
uname -r
```


## Esercizio 2 — Processi


### Passo 0 — Apri il gestore dei processi

- **Windows:**: premi `Ctrl + Maiusc + Esc` → scheda *Processi* (o *Dettagli*).
- **macOS:**: apri *Monitoraggio Attività* (`Cmd + Spazio`, scrivi "Monitoraggio").
- **Linux:**: in un terminale:
  ```
  top
  ```
  (esci con `q`). Se hai `htop`, è più leggibile:
  ```
  htop
  ```

## Domande 

* Quanti processi girano *ora* (approssimativamente)? Confrontalo col numero di finestre che hai aperte.
Dove sono tutti gli altri?

* Avvia lo **stesso** programma due volte e osserva **due righe con due PID diversi**.

  **Windows**: apri *due* finestre di Blocco note (cerca "Blocco note" due volte):
  vedrai due processi `notepad.exe`.
  
  **macOS / Linux**: apri *due* finestre di terminale e in **ognuna** incolla:
  ```
  sleep 120
  ```
  Nel gestore dei processi cerca `sleep`: ne vedrai due, con PID diversi.
  (Terminano da soli dopo 2 minuti; per fermarli prima premi `Ctrl + C`.)

* Ordina la lista per **CPU** (clic sull'intestazio**ne della colonna). 

* Vediamo il concetto di priorità: 
  
  **macOS / Linux**:
  
  avvia un processo a priorità bassa:
  ```
  nice -n 10 sleep 300 &
  ```
  **Windows**: 

  in Gestione attività: tasto destro su un processo → *Imposta priorità*. Osserva senza esagerare, poi riporta tutto a *Normale*.
  
  La priorità è la leva con cui il sistema decide chi va avanti per primo.

---

## L'estensione dei file è solo un'etichetta

**Obiettivo:** dimostrare che l'estensione dice al sistema *quale software* usare,
ma **non** è il contenuto del file.

> ⚠️ **Fai tutto su una COPIA di un file qualsiasi (es. una foto). Mai sull'originale.**

**1) Rendi visibili le estensioni**
- **Windows:** Esplora file → scheda *Visualizza* → spunta *Estensioni nomi file*.
- **macOS:** Finder → *Impostazioni* → *Avanzate* → spunta *Mostra tutte le estensioni dei documenti*.
- **Linux:** di solito già visibili.

**2) Duplica una foto**, per esempio `esempio.jpg` → `copia.jpg`.

**3) Rinomina la copia** in `copia.txt` (conferma l'avviso). L'icona cambia; se
provi ad aprirla vedrai caratteri illeggibili: ora il sistema la manda all'editor
di testo.

**4) Rinominala di nuovo** in `copia.jpg`: torna a essere un'immagine.

**Conclusione:** i byte non sono mai cambiati. Hai cambiato solo il *suggerimento*
che l'estensione dà al sistema su quale software usare.
