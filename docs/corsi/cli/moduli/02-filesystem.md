---
title: Filesystem e Permessi
---

# Filesystem e Permessi

In questo modulo costruisci le basi per orientarti nel filesystem da riga di comando: capire *dove sei*, *cosa stai toccando* e *cosa succede* quando esegui un comando.

Quasi tutti i comandi della CLI lavorano su **file e directory**. Senza una mappa mentale della struttura e dei percorsi, i comandi si riducono a copia/incolla e gli errori diventano inevitabili.

Obiettivo: leggere e usare correttamente **path**, **gerarchia** e **contesto di lavoro** prima di passare ai permessi.

## Filesystem

### Cos’è il filesystem

Il **filesystem** è il modello logico con cui il sistema operativo:

- organizza i dati
- li rende accessibili
- gestisce permessi e proprietà

In sistemi UNIX-like il filesystem è:

- **gerarchico**
- **unificato**
- **radicato in `/`**

---

### File e directory

In UNIX:

- una **directory** è un *file speciale* che contiene un elenco di **nomi → inode** (cioè “etichette” che puntano ad altri file o directory)
- un **file** è, in sostanza, una **sequenza di byte** (testo, immagini, binari, ecc.)
- le **estensioni** (`.txt`, `.png`, `.pdf`) sono solo una **convenzione**: aiutano le persone e alcuni programmi, ma **non sono obbligatorie** né decisive

Quindi il “tipo” di un file non dipende dal nome, ma da:

1. **Contenuto** (formato reale)  
  Molti file hanno una *firma* interna (“magic number”). Per verificarlo si usa:
  ```bash
  file documento
  ```
2. **Metadati del filesystem** (permessi, proprietario, timestamp, ecc.)  

3. **Permessi di esecuzione**  


Conclusione: in UNIX **il nome è solo un nome**; ciò che conta è **cosa contiene** il file e **cosa ti è permesso farci**.

---

### Gerarchia standard

Tutto parte dalla directory radice e si ramifica in ulteriori directories:

```text
/
├── bin   # comandi essenziali
├── etc   # file di configurazione
├── home  # directory degli utenti
├── var   # dati variabili (log, cache)
└── tmp   # file temporanei
```

Non è una convenzione estetica:  
**ogni directory ha una funzione precisa**.

### Path (percorsi)

Un **path** identifica un file o una directory.

- **Path assoluto**: parte da `/`
  ```text
  /home/user/file.txt
  ```

- **Path relativo**: parte dalla directory corrente
  ```text
  ./file.txt
  ```

Un modo utile per pensarci:

- l’assoluto è “coordinate globali”
- il relativo è “coordinate locali” (dipendono da dove ti trovi)

---

### I riferimenti speciali: `.`, `..`, `~`

Nella maggior parte delle shell UNIX, questi simboli sono fondamentali:

- `.` = directory corrente
- `..` = directory padre
- `~` = home dell’utente

---

### Working directory (il “contesto”)

La **working directory** (directory di lavoro) è il posto in cui il sistema considera che tu sia “in questo momento”.

È fondamentale perché molti comandi:

- leggono file “relativi” al punto in cui sei
- creano nuovi file “qui” se non specifichi un path
- possono fare danni se eseguiti nella cartella sbagliata

Comandi base:

```bash
pwd     # stampa dove sei
ls      # mostra cosa c’è nella cartella
cd ...  # cambia cartella
```

Regola pratica:

> prima di un’operazione delicata (es. cancellazioni), esegui sempre `pwd` e `ls`.

---

## Muoversi nel filesystem

### Il prompt della shell (dove scrivi i comandi)

Quando apri il Terminale vedi una riga simile a:

```text
utente@macbook:~/progetti $
```

Quella parte finale (`$` oppure `#`) è il **prompt**: indica che la shell è pronta a ricevere un comando.

- `~` di solito significa “sei nella home”
- se vedi `#` spesso sei **root** (massimi permessi) → più rischioso

La cosa più importante da capire è: **ogni comando che scrivi viene eseguito “da” una directory corrente** (working directory). Per orientarti usi soprattutto `pwd`, `ls`, `cd`.

---

### Navigazione essenziale: `pwd`, `ls`, `cd`

#### `pwd` — “dove sono?”
`pwd` (*print working directory*) stampa il **percorso assoluto** della directory in cui ti trovi.

```bash
pwd
# /Users/pianic2/itsfantastici
```

È il comando da usare quando non sei sicuro del contesto (prima di operazioni delicate).

---

#### `ls` — “cosa c’è qui?”
`ls` (*abbreviazione per : list*) elenca file e directory nella cartella corrente (o in un path che gli passi).

```bash
ls
ls docs/
```

Opzioni comuni:

```bash
ls -l   # lista “lunga”: permessi, proprietario, dimensione, data
ls -a   # include i file nascosti (quelli che iniziano con .)
ls -la  # combinazione molto usata
```

`ls -la` è utile perché mostra:

- file “nascosti” (iniziano con `.`)
- permessi e proprietario (li vedremo nella parte sui permessi)

---

#### `cd` — “vai in un’altra cartella”
`cd` (*change directory*) cambia la directory corrente.

```bash
cd /          # vai alla root
cd ~          # vai alla home
cd ..         # vai alla cartella padre
cd -          # torna alla cartella precedente
cd docs/      # path relativo
cd /var/log   # path assoluto
```

Note pratiche:

- `cd` senza argomenti ti porta in `~` (home)
- i path **relativi** dipendono da dove sei (controlla con `pwd`)
- usa **TAB** per completare nomi di file/cartelle ed evitare errori

---

### Globbing (selezionare file con pattern)

La shell espande automaticamente alcuni pattern:

- `*` = qualsiasi sequenza di caratteri
- `?` = un singolo carattere

Esempi:

```bash
ls *.md
ls lezione-0?.md
```

Se un nome contiene spazi, usa le virgolette:

```bash
ls "File con spazi.txt"
```

## Creare, spostare ed eliminare file

In questa sezione vedi le operazioni fondamentali su file e directory:

- **creare**: `mkdir`, `touch`
- **copiare**: `cp`
- **spostare / rinominare**: `mv`
- **eliminare** (con attenzione): `rm`, `rmdir`

---

### Operazioni essenziali: `mkdir`, `touch`, `cp`, `mv`, `rm`

#### `mkdir` — “crea una directory”
`mkdir` (*make directory*) crea una nuova cartella.

```bash
mkdir appunti
```

Se vuoi creare **più livelli** in un colpo solo (e non avere errori se qualche cartella esiste già), usa `-p`:

```bash
mkdir -p corsi/cli/moduli
```

---

#### `touch` — “crea un file vuoto (o aggiorna il timestamp)”
`touch` crea un file vuoto se non esiste; se esiste, aggiorna data/ora di modifica.

```bash
touch note.md
```

---

#### `cp` — “copia”
`cp` (*copy*) copia file (e, con opzioni, directory).

Copiare un file (crea `copia.txt` oppure lo sovrascrive se esiste):

```bash
cp sorgente.txt copia.txt
```

Copiare una directory richiede `-r` (*recursive*):

```bash
cp -r cartella cartella-backup
```

Regola pratica: prima di una modifica “rischiosa”, fare una copia è spesso il modo più rapido per recuperare da un errore.

---

#### `mv` — “sposta o rinomina”
In UNIX, spostare e rinominare sono la stessa operazione: `mv` (*move*).

Rinominare un file:

```bash
mv vecchio.txt nuovo.txt
```

Spostare un file in una directory (eventualmente cambiandogli nome):

```bash
mv note.md appunti/note.md
```

Se la destinazione esiste già, `mv` può **sovrascrivere**. Per ridurre il rischio, usa la modalità interattiva:

```bash
mv -i sorgente.txt destinazione.txt
```

---

#### `rm` / `rmdir` — “elimina (attenzione)”
Eliminare è l’operazione più delicata: **di default non c’è cestino**.

Eliminare un file:

```bash
rm file.txt
```

Eliminare una directory **vuota**:

```bash
rmdir cartella-vuota
```

Eliminare una directory **con contenuto** (attenzione: rimuove tutto) richiede `-r`:

```bash
rm -r cartella
```

Modalità “interattiva” (chiede conferma):

```bash
rm -i file.txt
rm -ri cartella
```

Regola di sicurezza:

> prima fai una `ls` del path che vuoi colpire, poi esegui `rm`.

Esempio:

```bash
ls cartella
rm -r cartella
```

---

## Perché il contesto è fondamentale (la regola che evita errori)

Due comandi identici possono avere effetti completamente diversi a seconda di:

- dove sei (`pwd`)
- su quali file stai puntando (path relativo vs assoluto)
- quali pattern stai espandendo (`*`, `?`)

Esempio: questi due comandi NON sono equivalenti.

```bash
rm -r build
rm -r ./build
```

Il secondo rende esplicito che ti riferisci alla cartella `build` nella directory corrente.

