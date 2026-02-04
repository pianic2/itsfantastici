---
title: Commit e storia
---

# Commit e storia

## Problema

Stai usando Git ogni giorno, ma succede spesso che:

- lo storico è pieno di commit “update” / “fix” senza significato
- non capisci cosa è cambiato tra due versioni
- non sai distinguere cosa è già pronto (staged) da cosa è ancora “in lavorazione”
- quando c’è un bug, non sai **dove** è entrato

Se non sai leggere la storia, Git diventa solo “un posto dove spingi codice”, non uno strumento di controllo.

---

## Teoria

### Commit = unità logica (non “salvataggio”)

Un commit non è “uno snapshot a caso”: è una **unità logica** che racconta una modifica completa e comprensibile. Idealmente, un commit permette a chi legge lo storico (anche te tra 2 settimane) di capire:

- **che obiettivo** introduce (feature/bugfix/refactor)
- **cosa cambia** in modo coerente
- **perché** è stato fatto (quando serve contesto)

Regole pratiche:

- **un’idea = un commit** (atomicità)
- se una modifica contiene *due motivi diversi*, separala in due commit
- un commit dovrebbe lasciare il progetto in uno stato “sano” (test/build ok, se applicabile)

**Messaggio di commit**
Un buon messaggio non descrive *il comando*, descrive *l’intento*.

- evita: `fix`, `update`, `changes`
- preferisci: “Corregge X quando Y”, “Aggiunge validazione input in Z”, “Rimuove duplicazione in …”

Struttura utile (facoltativa, ma efficace):

- **titolo breve** (cosa fa)
- **dettagli** (perché/come) nel corpo, se necessario

---

### Staged vs unstaged (working directory e staging area)

Git tiene separati due livelli di modifica:

- **unstaged (working directory)**: modifiche presenti nei file, ma **non ancora selezionate** per il prossimo commit
- **staged (staging area / index)**: modifiche **selezionate** che entreranno nel prossimo commit

Perché è importante: lo staging ti permette di creare commit **puliti e mirati**, evitando “commit omnibus” con dentro cambiamenti non correlati.

Operazioni tipiche:

- aggiungere allo staging:
    - `git add <file>`
    - `git add .` (tutto in blocco)
- rimuovere dallo staging (senza perdere le modifiche):
    - `git restore --staged <file>`

**Selezionare solo parte di un file (consigliato quando un file contiene più modifiche)**
- `git add -p` (interactive patch): scegli *hunk* per *hunk* cosa va nel commit

Questa pratica è una delle chiavi per uno storico leggibile.

---

### Diff e log (gli strumenti per “leggere” cosa sta succedendo)

#### `git diff`: capire cosa è cambiato

- `git diff`  
    mostra le differenze tra **working directory** (unstaged) e **staging**

- `git diff --staged` (o `--cached`)  
    mostra le differenze tra **staging** e **ultimo commit**  
    → è la verifica più importante **prima di committare**

Comandi utili aggiuntivi:

- `git diff <commit1> <commit2>`: confronta due commit
- `git diff <commit> -- <path>`: confronta un commit con lo stato attuale per un file/cartella
- `git diff --stat`: riepilogo per file (meno rumore, utile per farsi un’idea rapida)

#### `git log`: leggere lo storico

`git log` mostra la sequenza dei commit. Varianti pratiche:

- `git log --oneline`: vista compatta (hash breve + titolo)
- `git log --graph --oneline --decorate`: utile per capire rami/merge
- `git log -p`: mostra anche le patch (cosa è cambiato)
- `git log -- <path>`: storico relativo a un file/cartella
- `git show <commit>`: dettagli completi di un singolo commit

Obiettivo: usare diff e log per rispondere rapidamente a domande tipiche:

- “cosa sto per committare?”
- “quando è stata introdotta questa modifica?”
- “quale commit ha cambiato questo file e perché?”

---

## Esempi
### Leggere lo storico `git log`

Per capire *cosa è successo* nel progetto, il comando base è:

```bash
git log
```

Ogni commit è una “tessera” della storia e contiene sempre alcune informazioni chiave:

- **chi** ha fatto la modifica (**Author**)
- **quando** è stata fatta (**Date**)
- **perché / cosa** è cambiato (il **messaggio di commit**)

Un output tipico (semplificato) assomiglia a questo:

```output
Author: <username> <utente@example.com>
Date:   <date>

<testo del commit>
```

> **Suggerimento pratico**: quando lo storico è lungo, l’obiettivo non è “leggerlo tutto”, ma **scorrere e trovare rapidamente** i punti in cui sono state introdotte modifiche importanti.

---

### Capire cosa stai per committare `git diff`

Prima di fare un commit, conviene controllare *esattamente* quali modifiche stai includendo. Qui entra in gioco `git diff`, che ti aiuta a distinguere tra:

- **unstaged**: modifiche presenti nei file, ma **non ancora aggiunte** allo staging
- **staged**: modifiche **già pronte** per finire nel prossimo commit

**Modifiche non in staging (working directory vs staging):**

```bash
git diff
```

Usalo per rispondere alla domanda: **“cosa ho modificato, ma non ho ancora deciso di committare?”**

**Modifiche già selezionate (staging vs ultimo commit):**

```bash
git diff --staged
```

Usalo per rispondere alla domanda: **“cosa finirà nel commit se lo faccio adesso?”**

Regola pratica: prima di committare, controlla sempre `git diff --staged` per evitare di includere cambiamenti **non intenzionali**.

---

### Esempio di commit “buono”

Un commit “buono” di solito è:

- **piccolo** (fa una cosa principale)
- **coerente** (tutte le modifiche vanno nella stessa direzione)
- **spiegato bene** (il messaggio dice l’**intento**, non solo l’azione)

Esempio:

```bash
git add .
git commit -m "Aggiunge validazione input nel comando add"
```

Perché funziona:

- il messaggio spiega **cosa cambia** (*validazione input*)
- chiarisce **dove** (*nel comando add*)
- rende più facile capire lo storico e individuare regressioni o bug in futuro

```bash
git add .
git commit -m "Aggiunge validazione input nel comando add"
```

Il messaggio descrive l’intento, non il comando.

---

## Output atteso della lezione

Alla fine di questa lezione sai:

- leggere la storia (`git log`) in modo utile
- distinguere staged/unstaged con `git diff` e `git diff --staged`
- scrivere commit piccoli, coerenti e descrittivi

---

## Navigazione

- Precedente: [Workflow locale quotidiano](02-workflow-quotidiano.md)
- Successivo: [Undo e recovery](04-undo-e-recovery.md)

