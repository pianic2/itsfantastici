---
title: Problema iniziale
---

# Problema iniziale

Il corso nasce dalla necessità di risolvere un problema concreto e realistico:

> progettare un sistema affidabile per la gestione di dati strutturati, interconnessi e soggetti a evoluzione nel tempo.

Non partiamo dal linguaggio SQL, ma dal **problema che rende necessario SQL**.

---

## Contesto

Immaginiamo di dover sviluppare una piattaforma che permetta a più utenti di:

- registrarsi e autenticarsi
- creare contenuti
- interagire con contenuti creati da altri utenti
- organizzare e classificare i contenuti

Il sistema deve funzionare:

- nel tempo
- con dati in crescita
- con più utenti simultanei
- senza perdere coerenza dei dati

---

## Approccio ingenuo (e perché fallisce)

Una prima soluzione potrebbe essere usare:

- file di testo
- file CSV
- file JSON

Questa soluzione fallisce rapidamente perché:

- non esiste un’identità univoca garantita
- le relazioni sono fragili e manuali
- i dati possono diventare incoerenti
- la ricerca diventa inefficiente
- la concorrenza non è gestibile

---

## Problema centrale

Il problema **non è salvare dati**, ma:

- modellare correttamente le informazioni
- definire relazioni affidabili
- garantire integrità e coerenza
- permettere interrogazioni efficienti
- supportare evoluzione e manutenzione

👉 Questo è esattamente ciò che un **database relazionale** risolve.

---

## Obiettivo del corso rispetto al problema

Il corso mostra **come risolvere questo problema passo dopo passo**, introducendo solo gli strumenti necessari nel momento in cui servono.

Non studiamo SQL “per capitoli”, ma **per esigenze reali** che emergono dal progetto.
