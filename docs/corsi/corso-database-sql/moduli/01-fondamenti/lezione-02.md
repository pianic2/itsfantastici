---
title: Lezione 02 — Primo contatto con SQL
---

# Lezione 02 — Primo contatto con SQL

## Problema

Abbiamo:

- un problema reale
- dei requisiti chiari
- un modello dati concettuale

Ora sorge una nuova esigenza concreta:

> come trasformiamo il modello concettuale in una struttura reale, interrogabile e modificabile?

Dobbiamo passare **dall’idea al sistema**.  
Questo significa introdurre **SQL** come strumento operativo.

---

## Teoria

### Cos’è SQL

**SQL (Structured Query Language)** è il linguaggio standard usato per:

- definire la struttura del database
- inserire dati
- leggere dati
- modificarli
- cancellarli

SQL **non è un linguaggio di programmazione generale**, ma un linguaggio dichiarativo:
> dici *cosa* vuoi ottenere, non *come* ottenerlo.

---

### Il concetto di schema

Lo **schema** rappresenta la struttura del database:

- tabelle
- colonne
- tipi di dato
- vincoli
- relazioni

È il passaggio formale dal **modello logico** all’**implementazione fisica**.

---

### Tipi di dato (DB-agnostic)

Ogni colonna deve avere un tipo di dato.  
I tipi indicano:
- che valori sono ammessi
- come vengono memorizzati
- quali operazioni sono possibili

Categorie principali:

- numerici
- testuali
- booleani
- temporali

Nel corso useremo **tipi comuni a tutti i database**.

---

### CRUD

Le operazioni fondamentali sui dati sono quattro:

| Operazione | Significato | SQL |
|----------|------------|-----|
| Create | inserire dati | `INSERT` |
| Read | leggere dati | `SELECT` |
| Update | modificare dati | `UPDATE` |
| Delete | cancellare dati | `DELETE` |

Ogni sistema informativo, senza eccezioni, ruota attorno a queste operazioni.

---

### Query

Una **query** è una richiesta fatta al database.

Caratteristiche:
- è deterministica
- produce un risultato
- può leggere o modificare dati

La query più comune è `SELECT`.

---

## Esempi

> Useremo **SQLite** come ambiente iniziale, ma **scrivendo SQL standard**.

---

### Creazione delle tabelle (CREATE)

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY,
  username TEXT NOT NULL UNIQUE,
  email TEXT NOT NULL UNIQUE
);
```

Qui:

* `id` identifica univocamente l’utente
* `UNIQUE` e `NOT NULL` sono **vincoli**
* il database impedisce stati invalidi

---

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

---

### Inserimento dei dati (INSERT)

```sql
INSERT INTO users (username, email)
VALUES ('alice', 'alice@example.com');
```

Il database:

* assegna automaticamente la primary key
* verifica i vincoli

---

```sql
INSERT INTO posts (user_id, title, content)
VALUES (1, 'Primo post', 'Contenuto di esempio');
```

Se `user_id = 1` non esiste → **errore**.
Questa è integrità referenziale.

---

### Lettura dei dati (SELECT)

```sql
SELECT * FROM users;
```

```sql
SELECT title, content
FROM posts
WHERE user_id = 1;
```

La query non modifica i dati: **li interroga**.

---

### Modifica dei dati (UPDATE)

```sql
UPDATE users
SET email = 'alice@newmail.com'
WHERE id = 1;
```

Senza `WHERE` → modificheresti **tutte le righe**.
Questo è uno degli errori più comuni.

---

### Cancellazione dei dati (DELETE)

```sql
DELETE FROM posts
WHERE id = 1;
```

Anche qui: senza `WHERE` → distruzione totale.

---

## Esercizi

### Esercizio 1 — Traduzione del modello

Prendi il modello dati definito nel progetto e:

* individua tutte le entità
* scrivi le `CREATE TABLE` corrispondenti
* specifica PK, FK e vincoli

Obiettivo: passare dal **concetto alla struttura**.

---

### Esercizio 2 — CRUD controllato

Scrivi le query per:

1. inserire un nuovo utente
2. inserire due post dello stesso utente
3. recuperare tutti i post di un utente
4. aggiornare il titolo di un post
5. cancellare un commento

Motiva ogni `WHERE`.

---

### Esercizio 3 — Errori intenzionali

Prova a:

* inserire due utenti con la stessa email
* inserire un post con `user_id` inesistente

Osserva e spiega **perché il database rifiuta l’operazione**.

---

## Soluzione community

### Principio guida

Le soluzioni migliori:

* rispettano i vincoli
* sono leggibili
* spiegano *perché* funzionano

---

### Esempio commentato

```sql
INSERT INTO users (username, email)
VALUES ('bob', 'bob@example.com');

SELECT p.title
FROM posts p
WHERE p.user_id = 1;
```

Motivazione:

* nessuna duplicazione
* query semplice
* pieno rispetto del modello

---

## Concetti introdotti in questa lezione

* SQL come linguaggio dichiarativo
* schema del database
* tipi di dato
* CRUD
* query
* integrità referenziale

Questi concetti verranno **usati continuamente** da ora in avanti.

---

## Conclusioni

Ora siamo in grado di:

* creare una struttura reale partendo da un modello
* inserire e interrogare dati
* capire perché il database blocca operazioni scorrette

👉 Nella prossima lezione inizieremo a **combinare dati da più tabelle** (`JOIN`).
