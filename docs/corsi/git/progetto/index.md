---
title: Progetto del corso
---

# Progetto del corso

Questo documento descrive il progetto che accompagna l'intero corso Git.

Il progetto **non è un esercizio teorico**: è un repository reale che evolve lezione dopo lezione, introducendo problemi concreti che richiedono l'uso progressivo degli strumenti Git.

---

## Obiettivo del progetto

Costruire e mantenere un **repository di codice funzionale**, simulando scenari realistici:

- sviluppo di feature in parallelo
- correzione di bug urgenti
- collaborazione con altri sviluppatori
- integrazione di contributi esterni
- gestione di release e versioni

---

## Perché un progetto unico

Un progetto unico garantisce:

- **continuità logica**: ogni modulo estende il precedente
- **contesto reale**: i problemi emergono naturalmente, non sono artificiali
- **riproducibilità**: tutti lavorano sullo stesso caso, facilitando confronto e discussione

---

## Contesto del progetto

Stiamo costruendo una **applicazione CLI per gestire task personali** (todo list).

Il progetto:
- parte da un singolo file Python
- evolve con feature aggiuntive (ricerca, categorie, priorità)
- viene refactorizzato per migliorare la struttura
- riceve contributi da più collaboratori
- viene rilasciato con versioning semantico

---

## Requisiti tecnici

- linguaggio: Python (semplice, non richiede setup complesso)
- struttura: inizialmente monolitica, poi modulare
- test: introdotti nel corso per simulare sviluppo reale
- documentazione: README, CHANGELOG, CONTRIBUTING

---

## Evoluzione del progetto per modulo

### Modulo 01 — Fondamenti
- creazione del repository
- primo commit
- aggiunta di file iniziale (todo.py)
- esplorazione della storia

### Modulo 02 — Branching e merging
- creazione di branch per feature (add, list, remove)
- merge di branch completati
- primo conflitto e risoluzione

### Modulo 03 — Repository remoti
- pubblicazione su GitHub
- clone da remoto
- sincronizzazione con collaboratori
- gestione di divergenze

### Modulo 04 — Workflow collaborativi
- implementazione di Git Flow
- creazione di pull request
- review del codice
- merge di feature da fork esterni

### Modulo 05 — Storia e refactoring
- rebase per linearizzare la storia
- squash di commit per pulizia
- ammend di commit con errori
- cherry-pick di hotfix tra branch

### Modulo 06 — Strumenti avanzati
- uso di stash per context switching
- bisect per trovare bug
- hooks per automazione test
- gestione di documentazione separata (submodules)

---

## Come usare il progetto

1. **Segui il corso in ordine**: ogni lezione introduce nuove operazioni sul progetto
2. **Lavora sul tuo repository**: crea il tuo repository locale e applicaci le operazioni descritte
3. **Confronta con le soluzioni**: ogni modulo include lo stato atteso del repository
4. **Contribuisci**: proponi miglioramenti al progetto didattico tramite pull request

---

## Navigazione

- [Home corso](../index.md)
- [Moduli](../moduli/index.md)
- [Problema](problema.md)
- [Requisiti](requisiti.md)
