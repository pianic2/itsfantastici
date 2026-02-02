---
title: Modulo 01 — Fondamenti dei database
---

# Modulo 01 — Fondamenti dei database

Questo modulo introduce i **concetti fondamentali** necessari per comprendere e progettare un database relazionale.

Non si parte dalla sintassi, ma dalla **struttura mentale corretta**:  
capire *cosa* stiamo costruendo prima di imparare *come* interrogarlo.

Tutto ciò che verrà fatto nei moduli successivi **dipende direttamente** da questo modulo.

---

## Perché questo modulo è fondamentale

Senza una comprensione chiara di:
- entità
- relazioni
- vincoli
- integrità dei dati

qualsiasi utilizzo di SQL diventa:
- fragile
- difficile da mantenere
- impossibile da scalare

Questo modulo serve a **prevenire errori strutturali**, non a imparare comandi a memoria.

---

## Obiettivi di apprendimento

Al termine di questo modulo lo studente sarà in grado di:

- spiegare cos’è un database e perché è necessario
- distinguere database relazionali e non relazionali
- modellare entità e relazioni in modo corretto
- comprendere il ruolo di:
  - primary key
  - foreign key
  - vincoli
- leggere, valutare e motivare un modello dati
- comprendere il ruolo di SQL come strumento, non come fine

---

## Collegamento con il progetto

In questo modulo:

- viene introdotto il **problema iniziale**
- vengono definiti **requisiti e vincoli**
- viene costruito il **modello dati iniziale**
- si realizza la **prima implementazione reale** dello schema

Il progetto nasce qui e **non verrà mai resettato**.

---

## Contenuti del modulo

### Lezione 01 — Introduzione ai database
- problema: comprendere cos’è un database e perché serve oltre ai file
- teoria:
  - cos’è un database
  - perché i file non bastano
  - modello relazionale
  - entità, relazioni e vincoli
  - definizione del modello concettuale del progetto
- esempi pratici:
  - confronto tra file e database
  - esempio di entità e relazioni del progetto
- esercizi:
  - identificare entità e relazioni dal problema
  - definire i vincoli principali
- soluzione community e best practice

👉 [Vai alla lezione](lezione-01.md)

---

### Lezione 02 — Primo contatto con SQL
- problema: passare dal modello concettuale a uno schema reale interrogabile
- teoria:
  - cos’è SQL e perché è dichiarativo
  - schema del database
  - tipi di dato (DB-agnostic)
  - operazioni CRUD
- esempi pratici:
  - `CREATE` per tabelle del progetto
  - `INSERT` di dati di esempio
  - `SELECT` mirate
  - `UPDATE` e `DELETE` con `WHERE`
- esercizi:
  - definire lo schema completo del progetto
  - scrivere query CRUD con vincoli corretti
  - verificare errori di integrità referenziale
- soluzione community e best practice

👉 [Vai alla lezione](lezione-02.md)

---

### Lezione 03 — Relazioni e JOIN
- problema: perché servono le JOIN
- teoria:
  - `INNER JOIN` e `LEFT JOIN`
  - alias e naming
- esempi pratici:
  - post con autore
  - commenti con autore e post
  - post anche senza commenti (`LEFT JOIN` + `COUNT`)
- esercizi:
  - post + autore
  - commenti dettagliati
  - post senza commenti
- soluzione community e best practice

👉 [Vai alla lezione](lezione-03.md)

---

## Output del modulo

Alla fine del modulo esistono:

- un problema ben definito
- un insieme di requisiti espliciti
- un modello dati coerente
- una prima implementazione reale
- un linguaggio tecnico condiviso tra tutti i partecipanti

Questi elementi costituiscono la **base tecnica comune** dell’intero corso.

---

## Errori comuni da evitare

- saltare la modellazione per “andare subito su SQL”
- confondere tabelle con entità concettuali
- ignorare i vincoli pensando di gestirli “a codice”
- duplicare dati per comodità
- pensare che SQL sia solo sintassi

Questo modulo serve a **costruire fondamenta solide**.

---

## Navigazione

- [Progetto](../../progetto/index.md)
- [Lezione 01](lezione-01.md)
- [Lezione 02](lezione-02.md)
- [Lezione 03](lezione-03.md)
- [Glossario](glossary.md)
- [Moduli](../index.md)
