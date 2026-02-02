---
title: Lezione 02 — Primo contatto con SQL
---

# Lezione 02 — Primo contatto con SQL

## Problema

Abbiamo un modello concettuale. Ora dobbiamo trasformarlo in una struttura reale:

- creare lo schema (tabelle, colonne, vincoli)
- inserire dati di esempio
- interrogare e modificare quei dati in modo controllato

> Obiettivo: passare da “idea” a “sistema interrogabile”.
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

### SQL: linguaggio dichiarativo

SQL è dichiarativo: descrive *cosa* vuoi ottenere, non *come* ottenerlo.
In pratica lo useremo per:

- **DDL** (schema): `CREATE`, `ALTER`, `DROP`
- **DML** (dati): `INSERT`, `SELECT`, `UPDATE`, `DELETE`

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

Di seguito una tabella riepilogativa dei principali tipi di dato, con la corrispondenza tra SQLite, MySQL e PostgreSQL e un’indicazione della memoria occupata per campo.

| Tipo di dato | SQLite | MySQL | PostgreSQL | Memoria (indicativa) |
|---|---|---|---|---|
| BOOLEAN | `INTEGER` (0/1) | `BOOLEAN` | `BOOLEAN` | 1 byte |
| SMALLINT | `INTEGER` | `SMALLINT` | `SMALLINT` | 2 byte |
| INTEGER | `INTEGER` | `INT` | `INTEGER` | 4 byte |
| BIGINT | `INTEGER` | `BIGINT` | `BIGINT` | 8 byte |
| DECIMAL/NUMERIC | `REAL`/`NUMERIC` | `DECIMAL` | `NUMERIC` | variabile |
| REAL | `REAL` | `FLOAT` | `REAL` | 4 byte |
| DOUBLE | `REAL` | `DOUBLE` | `DOUBLE PRECISION` | 8 byte |
| CHAR | `TEXT` | `CHAR` | `CHAR` | fisso (n) |
| VARCHAR | `TEXT` | `VARCHAR` | `VARCHAR` | variabile (n) |
| TEXT | `TEXT` | `TEXT` | `TEXT` | variabile |
| DATE | `TEXT`/`REAL` | `DATE` | `DATE` | 4 byte (PG), variabile |
| TIME | `TEXT`/`REAL` | `TIME` | `TIME` | 8 byte (PG), variabile |
| DATETIME | `TEXT`/`REAL` | `DATETIME` | ❌ | variabile |
| TIMESTAMP | `TEXT`/`REAL` | `TIMESTAMP` | `TIMESTAMP` | 8 byte (PG), variabile |
| BLOB/BINARY | `BLOB` | `BLOB`/`BINARY` | `BYTEA` | variabile |
| JSON | `TEXT` | `JSON` | `JSON/JSONB` | variabile |
| UUID | `TEXT` | ❌ | `UUID` | 16 byte |

#### Foreign key (chiave esterna)

Una **foreign key** è un vincolo che collega una tabella a un’altra:

- indica quale colonna fa riferimento a una **primary key**
- garantisce l’**integrità referenziale** (niente riferimenti a record inesistenti)
- rende esplicite le relazioni tra entità (es. 1:N)

In pratica: puoi inserire un valore solo se esiste già nella tabella collegata.

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

> Partiamo con SQLite (semplice e locale), ma scriviamo SQL standard quando possibile.

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
