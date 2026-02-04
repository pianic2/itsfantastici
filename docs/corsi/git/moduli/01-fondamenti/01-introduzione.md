---
title: Cos’è il versionamento
---

# Cos’è il versionamento

Prima di Git, prima dei comandi, prima di GitHub:  
**il problema è gestire il cambiamento**.

Il versionamento nasce per rispondere a una domanda semplice:

> Come posso modificare un progetto senza perdere controllo su ciò che cambia?

---

## Il problema dei file non versionati

Senza versionamento succedono sempre le stesse cose:

- copie multiple dello stesso progetto  
  (`progetto_finale`, `progetto_finale_v2`, `progetto_finale_definitivo`)
- paura di modificare codice che “funziona”
- impossibilità di tornare indietro
- nessuna traccia di *chi* ha cambiato *cosa* e *perché*

Questo approccio **non scala**:

- non scala nel tempo
- non scala in team
- non scala professionalmente

---

## Cos’è il versionamento del codice

Il versionamento è un sistema che:

- registra lo storico delle modifiche
- permette di tornare a uno stato precedente
- rende ogni cambiamento tracciabile
- consente di lavorare in sicurezza

Ogni modifica non è più un rischio, ma **un’operazione reversibile**.

---

## Versionamento come sistema di sicurezza

Un buon sistema di versionamento ti permette di:

- sperimentare senza paura
- isolare il lavoro in corso
- confrontare versioni diverse dello stesso progetto
- capire quando e perché è stato introdotto un bug

Il punto chiave è questo:

> Il versionamento riduce il costo dell’errore.

---

## Git nel contesto del versionamento

Git è un **sistema di versionamento distribuito**:

- lavora in locale
- funziona anche offline
- non dipende da un server centrale per operare

Questo lo rende:

- veloce
- affidabile
- adatto sia a progetti piccoli che a sistemi complessi

---

## Git NON è GitHub

È fondamentale separare i concetti:

- **Git**: strumento di versionamento
- **GitHub / GitLab**: piattaforme di hosting e collaborazione

Git è il motore.  
GitHub è l’infrastruttura attorno.

Confondere i due porta a usare Git in modo superficiale.

---

## Concetti chiave da fissare

Prima di andare avanti devi avere chiaro che:

- Git serve a gestire il cambiamento
- il versionamento è una garanzia, non un vincolo
- ogni modifica deve poter essere spiegata e, se serve, annullata

Nel prossimo file vedremo **come Git pensa**  
(non cosa scrivere nel terminale).
