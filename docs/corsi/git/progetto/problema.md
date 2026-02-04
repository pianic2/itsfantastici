---
title: Problema del progetto
---

# Problema del progetto

## Situazione iniziale

Abbiamo un'applicazione CLI per gestire task personali (todo list).

Il codice:
- funziona
- viene modificato regolarmente
- ha bisogno di nuove feature
- deve essere manutenuto e corretto

Ma:
- non abbiamo uno storico delle modifiche
- non possiamo tornare a versioni precedenti
- non possiamo sviluppare feature in parallelo senza sovrascrivere
- non possiamo collaborare con altri sviluppatori senza conflitti continui
- non abbiamo modo di tracciare *chi* ha fatto *cosa* e *perché*

---

## Perché è un problema reale

Senza version control:

- **perdita di codice**: una modifica sbagliata può distruggere ore di lavoro
- **impossibilità di sperimentare**: ogni modifica è rischiosa
- **collaborazione caotica**: file copiati, versioni finali-finali-definitive
- **bug non riproducibili**: non sappiamo quale versione ha introdotto il problema
- **nessuna documentazione delle decisioni**: il codice cambia, ma non sappiamo perché

---

## Scenario reale

Stai sviluppando una feature (aggiunta di priorità ai task).

Nel frattempo:
- un collega deve correggere un bug urgente
- un altro sta refactorizzando il codice
- tu stesso vuoi provare un'implementazione alternativa

Come fare senza:
- bloccare il lavoro degli altri?
- perdere le modifiche in corso?
- creare caos nella codebase?

---

## La soluzione: Git

Git risolve questi problemi fornendo:

- **storia completa**: ogni modifica è tracciata e reversibile
- **branching**: sviluppo parallelo e isolato
- **merging**: integrazione controllata delle modifiche
- **collaborazione distribuita**: ogni sviluppatore ha una copia completa
- **tracciabilità**: chi, cosa, quando, perché

---

## Obiettivo finale del progetto

Alla fine del corso, il progetto sarà:

- versionato correttamente
- sviluppato con branch isolati
- sincronizzato con repository remoto
- documentato con commit chiari
- gestito con workflow professionale
- pronto per rilascio e manutenzione

---

## Navigazione

- [Home progetto](index.md)
- [Requisiti](requisiti.md)
- [Moduli](../moduli/index.md)
