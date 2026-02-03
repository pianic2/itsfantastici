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
| 1 | alice | alice@example.com |

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
### Relazioni tra tabelle (logica in SQL)

In un database relazionale, una *relazione* tra due “entità” non è un collegamento “magico”: viene rappresentata **tramite valori** e **vincoli**.

1. **Prima ragioniamo a livello logico (modello)**
  - identifichiamo le entità (es. `users`, `posts`, `comments`)
  - decidiamo le cardinalità (1:1, 1:N, N:M)
  - scegliamo quali dati identificano un record (**Primary Key**)

2. **Poi traduciamo il modello in SQL (implementazione)**
  - usiamo **Primary Key (PK)** per identificare univocamente le righe
  - usiamo **Foreign Key (FK)** per “puntare” a una PK di un’altra tabella
  - applichiamo vincoli per evitare stati incoerenti (es. FK che punta a un record inesistente)

Di fatto, **la relazione è il fatto che una colonna contiene l’identificatore (PK) di un’altra tabella**, e il database può far rispettare questa regola con una FK.

---

#### One-to-One (1:1)
**Idea logica:** un record di A corrisponde a *al massimo* un record di B (e viceversa).  
**In SQL:** si usa una FK con vincolo `UNIQUE` (oppure si condivide la stessa PK).

Esempio (profilo utente separato):

```sql
CREATE TABLE user_profiles (
  user_id INTEGER PRIMARY KEY,
  bio TEXT,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

Qui `user_id` è anche PK: garantisce **un solo profilo per utente**.

---

#### One-to-Many (1:N)
**Idea logica:** un record di A può essere associato a molti record di B, ma ogni record di B appartiene a un solo record di A.  
**In SQL:** la FK sta nella tabella “molti”.

Esempio (un utente può avere molti post):

```sql
CREATE TABLE posts (
  id INTEGER PRIMARY KEY,
  user_id INTEGER NOT NULL,
  title TEXT NOT NULL,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

`posts.user_id` collega ogni post a **un** utente, mentre lo stesso utente può comparire in molte righe di `posts`.

---

#### Many-to-Many (N:M)
**Idea logica:** molti record di A possono essere associati a molti record di B.  
**In SQL:** non si mette una FK “diretta” da una parte all’altra: si crea una **tabella ponte** (junction table) con **due FK**.

Esempio (utenti che mettono “like” ai post):

```sql
CREATE TABLE post_likes (
  user_id INTEGER NOT NULL,
  post_id INTEGER NOT NULL,
  PRIMARY KEY (user_id, post_id),
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (post_id) REFERENCES posts(id)
);
```

- ogni riga rappresenta una singola associazione *(utente, post)*
- la `PRIMARY KEY (user_id, post_id)` impedisce duplicati (stesso like ripetuto)

---

**Nota importante:** le FK servono a mantenere l’integrità (coerenza) dei dati; le query (`JOIN`) servono a *leggere* le relazioni combinando le tabelle quando ti serve. 

---

## Esempi

### Esempio: creare un nuovo database sqlite

Per aggiornare gli indici dei pacchetti e installare SQLite su Ubuntu:

```bash
sudo apt update
sudo apt install -y sqlite3
```

Dopo l’installazione puoi verificare la versione:

```bash
sqlite3 --version
```

```bash
sqlite3 nome_database.db
```

Il file `nome_database.db` verrà creato nella cartella corrente se non esiste.  
All’interno della shell di SQLite puoi verificare con:

```sql
.databases
```

Per uscire:

```sql
.exit
```

### Esempio: struttura dati del progetto

Nel nostro progetto iniziale gestiremo:

- utenti
- post
- commenti

#### Tabella `users`
Creiamo la tabella utenti.

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  username TEXT NOT NULL UNIQUE,
  email TEXT NOT NULL UNIQUE,
  born_year INTEGER,
  born_month INTEGER,
  born_day INTEGER
);
```
Qui:

* `id` identifica univocamente l’utente
* `UNIQUE` e `NOT NULL` sono **vincoli**
* il database impedisce stati invalidi


#### Tabella `posts`
Creiamo la tabella posts.

```sql
CREATE TABLE posts (
  id INTEGER PRIMARY KEY,
  user_id INTEGER NOT NULL,
  title TEXT NOT NULL,
  content TEXT,
  FOREIGN KEY (user_id) REFERENCES users(id)
);
```

La **foreign key** rende esplicita la relazione 1:N.

#### Tabella `Commments`
Creiamo la tabella commenti.

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