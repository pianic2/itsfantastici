---
title: Requisiti del progetto
---

# Requisiti del progetto

Questo documento descrive i requisiti funzionali e tecnici del progetto che accompagna il corso Git.

---

## Requisiti funzionali

### Versione 1.0 (baseline)
- aggiungere task con descrizione
- elencare tutti i task
- rimuovere task completati
- persistenza in file locale

### Versione 2.0 (feature intermediate)
- aggiungere priorità ai task (alta, media, bassa)
- filtrare task per priorità
- ricerca testuale tra i task
- aggiungere categorie/tag

### Versione 3.0 (feature avanzate)
- esportazione in JSON/CSV
- statistiche (task completati, in corso)
- reminder per task con scadenza
- integrazione con calendario

---

## Requisiti tecnici

### Linguaggio e struttura
- linguaggio: Python 3.8+
- struttura iniziale: singolo file `todo.py`
- struttura finale: package modulare
- configurazione: file `.ini` o `.toml`

### Testing
- unittest per funzioni core
- test di integrazione CLI
- coverage minima: 70%

### Documentazione
- README con istruzioni d'uso
- CHANGELOG con versioning semantico
- CONTRIBUTING per collaboratori
- docstring su funzioni pubbliche

### Repository
- `.gitignore` configurato per Python
- file di configurazione versionati
- separazione tra codice e dati utente
- gestione delle dipendenze (requirements.txt)

---

## Vincoli di progetto

### Vincoli tecnici
- nessun database esterno (solo file locali)
- interfaccia CLI (no GUI)
- cross-platform (Linux, macOS, Windows)
- dipendenze minime

### Vincoli didattici
- ogni feature deve introdurre problemi Git reali
- ogni modulo deve applicare concetti specifici
- il progetto deve rimanere comprensibile

---

## Requisiti Git

### Struttura repository
- branch `main` protetto
- branch `develop` per integrazione
- feature branch per ogni nuova funzionalità
- hotfix branch per bug critici

### Commit
- messaggi descrittivi e semantici
- commit atomici (una modifica logica per commit)
- sign-off per contributi esterni

### Workflow
- pull request obbligatorie per `main`
- code review su ogni PR
- CI/CD per test automatici
- versioning semantico per release

---

## Deliverable per modulo

### Modulo 01
- repository inizializzato
- file `todo.py` funzionante (versione 1.0)
- README di base
- almeno 5 commit significativi

### Modulo 02
- almeno 3 branch feature creati e mergiati
- gestione di almeno 1 conflitto
- storia pulita e lineare

### Modulo 03
- repository pubblicato su GitHub
- clone funzionante da remoto
- sincronizzazione con collaboratore
- gestione di divergenza

### Modulo 04
- implementazione di Git Flow o GitHub Flow
- almeno 2 pull request completate
- code review documentate

### Modulo 05
- storia linearizzata con rebase
- commit squashati dove opportuno
- almeno 1 cherry-pick eseguito

### Modulo 06
- almeno 1 hook configurato
- stash usato in scenario reale
- documentazione esterna gestita

---

## Criteri di successo

Al termine del corso, il progetto deve:

- essere completamente versionato
- avere una storia Git pulita e comprensibile
- essere sincronizzato con repository remoto
- seguire un workflow collaborativo
- essere documentato e manutenibile
- contenere test e CI/CD di base

---

## Navigazione

- [Home progetto](index.md)
- [Problema](problema.md)
- [Moduli](../moduli/index.md)
