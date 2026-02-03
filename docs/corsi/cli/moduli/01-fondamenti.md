---
title: Fondamenti della CLI
---
# Fondamenti della CLI
## Introduzione alla CLI

La **Command Line Interface (CLI)** è il metodo più antico e potente per interagire con un sistema operativo.

Prima delle interfacce grafiche (GUI), **tutti i sistemi** venivano controllati tramite comandi testuali.
Ancora oggi:

- i server
- i sistemi embedded
- l’infrastruttura cloud
- il mondo DevOps

si basano **quasi esclusivamente sulla CLI**.

---

## Distinzione Tra CLI, Terminale e Shell
Uno degli errori più comuni è confondere questi concetti:

- **CLI:** è il linguaggio di interazione
- **Terminale:** è solo un contenitore
- **Shell:** è l’interprete

Sono **cose diverse**.

### Cos’è la CLI

La **CLI (Command Line Interface)** è un **paradigma di interazione**:
- l’utente scrive comandi testuali
- il sistema risponde con output testuale

Non è un programma specifico.
È un **modo di lavorare**.

### Cos’è il terminale

Il **terminale** è un’applicazione che:
- fornisce una finestra
- riceve input da tastiera
- mostra output testuale

Esempi:
- GNOME Terminal
- iTerm2
- Windows Terminal

Il terminale **non interpreta i comandi**.

---

## La Shell

La **shell** è il programma che:
- legge i comandi
- li interpreta
- li esegue

È il **cuore operativo della CLI**.

## Cosa fa una shell

Una shell:

- interpreta il testo digitato
- espande variabili
- gestisce redirection e pipe
- avvia processi
- restituisce un exit code

Quando scrivi un comando, **non stai parlando direttamente al sistema**, ma alla shell.

## Shell comuni

Alcuni esempi:

- `sh` – shell storica
- `bash` – la più diffusa
- `zsh` – moderna e avanzata
- `fish` – orientata all’usabilità

Nel corso useremo **bash** come riferimento concettuale.

## Prompt

Il **prompt** è la parte di testo che la shell mostra per indicare che è pronta a ricevere un comando. In pratica è un “segnale di attesa” e, spesso, contiene informazioni utili sul contesto in cui stai lavorando.

Di solito può includere:

- **utente** corrente
- **nome della macchina** (host)
- **cartella** in cui ti trovi (directory corrente)
- un **simbolo finale** che indica il tipo di utente

**Esempio:**
```bash
user@machine:~$
```

Come si legge:

- `user` = nome utente
- `machine` = computer/server su cui stai lavorando
- `~` = home directory dell’utente (es. `/home/user`)
- `$` = utente normale  
  (`#` di solito indica l’utente **root**/amministratore)

Il prompt può cambiare a seconda della shell e della configurazione, e può mostrare anche altre informazioni (ad esempio il ramo Git o lo stato di un ambiente virtuale).
