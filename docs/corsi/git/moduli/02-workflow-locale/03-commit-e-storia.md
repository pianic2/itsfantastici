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

### Leggere lo storico

```bash
git log
```

Ci aspettiamo un output del genere::

```output
Author: <username> <utente@example.com>
Date:   <date>

<testo del commit>
```

### Capire cosa stai per committare

Modifiche non in staging:

```bash
git diff
```

Modifiche già selezionate (staged):

```bash
git diff --staged
```

### Esempio di commit “buono”

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

