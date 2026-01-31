---
title: Modello dei dati
---

# Modello dei dati

Questa sezione introduce il **modello dei dati iniziale**, che verrà esteso progressivamente durante il corso.

Il modello **non è definitivo**: evolve insieme alle competenze acquisite.

---

## Entità principali

In base al problema e ai requisiti individuiamo le seguenti entità fondamentali.

### Utente (`users`)
Rappresenta una persona che utilizza la piattaforma.

Attributi principali:

- identificatore univoco
- username
- email

---

### Contenuto (`posts`)
Rappresenta un contenuto creato da un utente.

Attributi principali:

- identificatore univoco
- autore
- titolo
- testo

Relazione:

- ogni contenuto appartiene a **un solo utente**
- un utente può creare **più contenuti**

---

### Commento (`comments`)
Rappresenta un’interazione su un contenuto.

Attributi principali:

- identificatore univoco
- autore
- contenuto testuale

Relazioni:

- ogni commento è associato a un utente
- ogni commento è associato a un contenuto

---

### Categoria (`categories`)
Serve per classificare i contenuti.

Relazione:

- un contenuto può appartenere a più categorie
- una categoria può essere associata a più contenuti

Questo richiede una **relazione many-to-many**.

---

## Relazioni tra entità

| Entità A | Entità B | Tipo |
|--------|----------|------|
| users  | posts    | 1 : N |
| users  | comments | 1 : N |
| posts  | comments | 1 : N |
| posts  | categories | N : M |

---

## Considerazioni di modellazione

- ogni entità ha una primary key
- le relazioni sono esplicite tramite foreign key
- le relazioni N:M usano una tabella di collegamento
- nessuna informazione è duplicata inutilmente

Questo modello segue i principi della **normalizzazione** e può essere implementato su qualsiasi database relazionale.

---

## Evoluzione del modello

Durante il corso il modello verrà esteso con:

- metadati
- gestione temporale
- ottimizzazioni di performance
- adattamenti per database diversi

Il modello è un **oggetto vivo**, non un diagramma statico.
