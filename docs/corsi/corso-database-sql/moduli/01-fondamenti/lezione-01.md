---
title: Lezione 01 — Introduzione ai database
---

# Lezione 01 — Introduzione ai database

## Problema

Stiamo sviluppando un sistema informatico che deve gestire dati reali:
- utenti
- contenuti creati dagli utenti
- relazioni tra utenti e contenuti

All’inizio potremmo pensare di usare semplici file (`.txt`, `.csv`, `.json`), ma emergono subito problemi concreti:

- come garantiamo che i dati siano coerenti?
- come evitiamo duplicazioni?
- come gestiamo più utenti che accedono agli stessi dati?
- come modelliamo relazioni complesse (es. utenti → post → commenti)?

**Problema centrale:**  
> come memorizzare, organizzare e interrogare dati in modo strutturato, scalabile e affidabile?

Questa lezione introduce lo strumento che useremo per risolvere il problema: **il database**.

---

## Teoria

### Cos’è un database

Un **database** è una collezione organizzata di dati progettata per:
- memorizzare informazioni in modo strutturato
- permettere accesso efficiente ai dati
- garantire coerenza e integrità
- supportare accesso concorrente

Un database **non è solo storage**, ma un sistema che impone regole.

---

### Perché non bastano i file

L’uso di file presenta limiti strutturali:

- nessuna garanzia di unicità
- relazioni gestite “a mano”
- difficoltà di accesso concorrente
- ricerca inefficiente su grandi volumi di dati
- assenza di vincoli formali

Un database introduce **regole esplicite** che impediscono stati inconsistenti.

---

### Tipi di database

#### Database relazionali (SQL)
- dati organizzati in **tabelle**
- struttura definita (schema)
- relazioni esplicite tra dati
- linguaggio SQL per interrogazione

Esempi: SQLite, MySQL, PostgreSQL.

#### Database non relazionali (NoSQL)
- struttura più flessibile
- modelli diversi (documenti, key-value, grafi)
- utili in contesti specifici

👉 In questo corso useremo **database relazionali**.

---

### Tabelle, righe e colonne

Una **tabella** rappresenta un insieme di entità omogenee.

- **Riga (record)**: una singola entità
- **Colonna (campo)**: una proprietà dell’entità

Esempio concettuale:

| id | username | email |
|----|----------|-------|

---

### Chiavi e vincoli

#### Primary Key (PK)
- identifica univocamente ogni riga
- non può essere `NULL`
- non può duplicarsi

Serve per:
- distinguere i record
- creare relazioni

#### Foreign Key (FK)
- riferimento a una PK di un’altra tabella
- impone coerenza tra tabelle

#### Vincoli
Regole applicate dal database:
- `PRIMARY KEY`
- `FOREIGN KEY`
- `UNIQUE`
- `NOT NULL`

Obiettivo: **integrità dei dati**.

---

### Relazioni tra tabelle

- **One-to-One (1:1)**  
  un record ↔ un record

- **One-to-Many (1:N)**  
  un record ↔ molti record  
  (es. utente → post)

- **Many-to-Many (N:M)**  
  molti ↔ molti  
  richiede una tabella di collegamento

---

## Esempi

### Esempio: struttura dati del progetto

Nel nostro progetto iniziale gestiremo:
- utenti
- post
- commenti

#### Tabella `users`
```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  username TEXT NOT NULL UNIQUE,
  email TEXT NOT NULL UNIQUE
);
```

#### Tabella `posts`
```sql
CREATE TABLE posts (
  id INTEGER PRIMARY KEY,
  user_id INTEGER NOT NULL,
  title TEXT NOT NULL,
  content TEXT,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

#### Tabella `Commments`
```sql
CREATE TABLE comments (
  id INTEGER PRIMARY KEY,
  user_id INTEGER NOT NULL,
  post_id INTEGER NOT NULL,
  content TEXT NOT NULL,
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (post_id) REFERENCES posts(id)
);
```