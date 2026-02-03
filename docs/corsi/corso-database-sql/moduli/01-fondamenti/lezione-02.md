---
title: Lezione 02 — Primo contatto con SQL
---

# Lezione 02 — Primo contatto con SQL

## Problema

Abbiamo un modello concettuale ed abbiamo creato le tabelle utenti, posts e commenti. Ora dobbiamo trasformarlo in una struttura reale:

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

I tipi di dato in DB-agnostic sono:
- INTEGER
- TEXT


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

### Inserimento dei dati (INSERT)
Il comando di inserimento dei dati è composto dalle seguenti parti:

- `INSERT INTO <table> (<fields>)` specifica la tabella per inserire i dati
- `VALUES (<values>)` valori da inserire

```sql
INSERT INTO users (username, email)
VALUES ('alice', 'alice@example.com');
```

Il database:

* assegna automaticamente la primary key
* verifica i vincoli


```sql
INSERT INTO posts (user_id, title, content)
VALUES (1, 'Primo post', 'Contenuto di esempio');
```
Se `user_id = 1` non esiste → **errore**.
Questa è integrità referenziale.

Per inserire più righe in un’unica istruzione, puoi usare una lista di valori separati da virgole. È più efficiente e mantiene i dati coerenti.

```sql
INSERT INTO users (username, email, born_year, born_month, born_day)
VALUES
  ('bob', 'bob@example.com', 1999, 10, 1),
  ('rob', 'rob@example.com', 1999, 1, 10),
  ('carlo', 'carlo@example.com', 2000, 7, 22),
  ('dina', 'dina@example.com', 1997, 11, 5),
  ('elena', 'elena@example.com', 2001, 1, 9),
  ('franco', 'franco@example.com', 1995, 9, 30),
  ('giada', 'giada@example.com', 1996, 12, 14),
  ('luca', 'luca@example.com', 1999, 4, 2);
```

---

### Lettura dei dati (SELECT)
Il comando di lettura dei dati è composto dalle seguenti parti:

- `SELECT <fields>` indica quali fields selezionare
- `FROM <table>` indica su quale tabella cercare i dati
- `WHERE <filter conditions>` impone filtri alla selezione usando la logica booleana
- `ORDERED BY <field> <order(DESC | ASC)>` ordina i dati per i valori di una specifica colonna
- `LIMIT <int value>` se specificato indica quante entries mostrare per ogni pagina
- `OFFSET <int value> <order(DESC | ASC)>` indica da quale entry mostrare in modo esclusivo (mostra dal `n+1` esimo elemento). 

> I selettori `LIMIT` e `OFFSET` saranno in seguito usati per la paginazione.

Iniziamo creando una query che seleziona e mostra tutte le entries all'interno della tabella users.

```sql
SELECT * FROM users;
```

Proviamo ora a mostrare titolo e contenuto di tutti i posts che sono relazionati all'utente con valore di `user_id = 1`, ordinati per titolo in ordine alfabetico.

```sql
SELECT 
  title,
  content AS "description"
  FROM posts
WHERE user_id = 1
ORDERED BY title ASC;
```
In SQL esiste l'alias `AS` per visualizzare una colonna con un nome più leggibile nel risultato della query.

La query non modifica i dati: **li interroga**.

---

### Modifica dei dati (UPDATE)
Il comando di modifica dei dati è composto dalle seguenti parti:

- `UPDATE <table>` indica in quale tabella eseguire la modifica
- `SET <assegnations>` uno o più campi e rispettivi valori da modificare
- `WHERE <filter conditions>` una o più condizioni booleane che indicano a quali entries applicare la modifica.
Senza `WHERE` → modificheresti **tutte le righe**.
Questo è uno degli errori più comuni.

```sql
UPDATE users
SET email = 'alice@newmail.com'
WHERE id = 1;
```

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
