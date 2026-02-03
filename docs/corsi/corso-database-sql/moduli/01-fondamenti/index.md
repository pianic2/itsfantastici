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

Al termine di questo modulo lo studente sarà in grado di spiegare cos’è un database e perché è necessario, distinguendo tra database relazionali e non relazionali.

Saprà modellare correttamente entità e relazioni e comprenderà il ruolo di **primary key**, **foreign key** e dei principali vincoli per garantire l’integrità dei dati.

Inoltre, sarà in grado di leggere e valutare un modello dati, motivando le scelte progettuali, e di inquadrare SQL come uno strumento operativo al servizio del modello, non come un fine in sé.

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
- **Problema** — Comprendere cos’è un database e perché serve rispetto alla gestione tramite file.
- **Teoria** — Cos’è un database; perché i file non bastano; modello relazionale; entità, relazioni e vincoli; definizione del modello concettuale del progetto.
- **Esempi pratici** — inizializzare un nuovo database da zero; creare le prime tabelle.


👉 [Vai alla lezione](lezione-01.md)

---

### Lezione 02 — Primo contatto con SQL
- **Problema** — Passare dal modello concettuale a uno schema reale interrogabile.
- **Teoria** — Cos’è SQL e perché è dichiarativo; schema del database; tipi di dato (DB-agnostic); operazioni CRUD.
- **Esempi pratici** — Operazioni CRUD.

👉 [Vai alla lezione](lezione-02.md)

---
### Lezione 03 — Relazioni e JOIN
- **Problema** — Leggere dati distribuiti su più tabelle (post + autore, commenti + post, ecc.).
- **Teoria** — JOIN tramite chiavi (FK → PK); differenza tra `INNER JOIN` e `LEFT JOIN`; alias e naming.
- **Esempi pratici** — Post con autore (`JOIN users`); commenti con autore e post; post anche senza commenti (`LEFT JOIN` + `COUNT`).
- **Esercizi** — Progettare un database con **studenti**, **corsi** e **iscrizioni** (relazione molti-a-molti); creare tabelle, inserire dati, verificare con `SELECT`, e fare una query con JOIN per mostrare studente + corso.

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

