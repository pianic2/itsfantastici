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

### Commit = unità logica

Un commit non è “un salvataggio qualsiasi”. È una unità logica che dovrebbe rappresentare:

- un obiettivo chiaro
- uno stato coerente del progetto
- una motivazione (spiegata dal messaggio)

Regola pratica:

> un’idea = un commit

### Staged vs unstaged

Git ti fa lavorare su due livelli:

- **unstaged**: modifiche presenti nei file, ma non selezionate per il prossimo commit
- **staged**: modifiche selezionate (staging area) che entreranno nel prossimo commit

Questa distinzione è ciò che ti permette uno storico pulito.

### Diff e log

- `git diff` mostra differenze tra working directory e staging
- `git diff --staged` mostra differenze tra staging e ultimo commit
- `git log` mostra la storia dei commit

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

