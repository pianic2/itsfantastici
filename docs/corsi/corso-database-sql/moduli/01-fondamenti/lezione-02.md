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

SQL è un linguaggio **dichiarativo**: quando scrivi una query descrivi **il risultato che vuoi** (quali righe/colonne), non i passaggi operativi per ottenerlo.

Questo significa che:

- tu specifichi **vincoli e condizioni** (`WHERE`, `JOIN`, `GROUP BY`, `ORDER BY`)
- il database decide **come** eseguire la richiesta nel modo più efficiente (piano di esecuzione: indici, ordine delle operazioni, strategie di join)

In altre parole, non dici “scorri tutte le righe una per una”, ma “dammi le righe che rispettano queste condizioni”.

Esempio (tu descrivi il risultato):

```sql
SELECT id, username
FROM users
WHERE born_year >= 1999
ORDER BY username;
```

Il DB stabilisce il “come” (se usare un indice, in che ordine leggere i dati, ecc.).

#### Famiglie di comandi che useremo

Nelle lezioni useremo e nomineremo queste famiglie di comandi SQL (in base al DB, alcune classificazioni possono variare):

- **DDL (Data Definition Language)**: definisce o modifica la **struttura** del database (schema)  
  Comandi tipici: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`  

- **DML (Data Manipulation Language)**: inserisce, aggiorna o elimina i **dati**  
  Comandi tipici: `INSERT`, `UPDATE`, `DELETE`, `MERGE` (non sempre disponibile)  

- **DQL (Data Query Language)**: interroga/legge i **dati** (spesso considerata parte della DML)  
  Comandi tipici: `SELECT` (+ `WHERE`, `JOIN`, `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`)  

- **TCL (Transaction Control Language)**: controlla le **transazioni** (atomicità/rollback)  
  Comandi tipici: `BEGIN`/`START TRANSACTION`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`  

- **DCL (Data Control Language)**: gestisce **permessi e sicurezza** (utenti/ruoli)  
  Comandi tipici: `GRANT`, `REVOKE`  

Regola pratica: 
- **DDL = struttura**,
- **DQL/DML = dati**,
- **TCL = coerenza delle operazioni**,
- **DCL = accessi**.  

> In genere: prima si crea lo schema (DDL), poi si lavora/interroga sui dati (DQL/DML), eventualmente dentro transazioni (TCL).

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

Usiamo **SQLite** (semplice e locale), ma cerchiamo di scrivere SQL **standard** e portabile quando possibile.

### Inserimento dei dati (INSERT)

`INSERT` serve a creare nuove righe in una tabella. La forma più comune è:

- `INSERT INTO <table> (<colonne>)` indica tabella e colonne da valorizzare
- `VALUES (<valori>)` indica i valori (nello **stesso ordine** delle colonne)

Esempio: inseriamo un utente.

```sql
INSERT INTO users (username, email)
VALUES ('alice', 'alice@example.com');
```

Il database:

- assegna automaticamente la **primary key** (se `id` è autoincrement)
- controlla i **vincoli** (es. `NOT NULL`, `UNIQUE`, `CHECK`)
- controlla le **foreign key** (se abilitate/attive)

Esempio: inseriamo un post collegato a un utente.

```sql
INSERT INTO posts (user_id, title, content)
VALUES (1, 'Primo post', 'Contenuto di esempio');
```

Se `user_id = 1` **non esiste** nella tabella `users` → errore di **integrità referenziale** (vincolo FK).

#### Inserire più righe in una sola query

È più efficiente e riduce il numero di query.

```sql
INSERT INTO users (username, email, born_year, born_month, born_day)
VALUES
  ('bob',   'bob@example.com',   1999, 10,  1),
  ('rob',   'rob@example.com',   1999,  1, 10),
  ('carlo', 'carlo@example.com', 2000,  7, 22),
  ('dina',  'dina@example.com',  1997, 11,  5),
  ('elena', 'elena@example.com', 2001,  1,  9),
  ('franco','franco@example.com',1995,  9, 30),
  ('giada', 'giada@example.com', 1996, 12, 14),
  ('luca',  'luca@example.com',  1999,  4,  2);
```

> Suggerimento: se stai inserendo dati “critici”, considera l’uso di **transazioni** (`BEGIN` / `COMMIT`) per rendere l’operazione atomica.

---

### Lettura dei dati (SELECT)

`SELECT` serve a leggere dati. Una query tipica è composta da:

- `SELECT <colonne>` quali colonne vuoi vedere (oppure `*` per tutte)
- `FROM <tabella>` da dove leggere
- `WHERE <condizioni>` filtri (opzionale)
- `ORDER BY <colonna> ASC|DESC` ordinamento (opzionale)
- `LIMIT <n>` massimo numero di righe (opzionale)
- `OFFSET <n>` salta le prime `n` righe (opzionale, utile per paginazione)

> Nota: la sintassi corretta è **`ORDER BY`**, non `ORDERED BY`.

#### Selezionare tutte le righe

```sql
SELECT * FROM users;
```

#### Selezionare colonne specifiche e usare alias (`AS`)

Mostriamo `title` e `content` rinominato come `description`:

```sql
SELECT
  title,
  content AS description
FROM posts;
```

`AS` è utile per rendere più leggibile l’output (o per nomi calcolati).

#### Filtrare con WHERE (logica booleana)

Esempio: tutti i post dell’utente con `user_id = 1`, ordinati alfabeticamente per titolo.

```sql
SELECT
  title,
  content AS description
FROM posts
WHERE user_id = 1
ORDER BY title ASC;
```

Operatori utili in `WHERE`:

- confronti: `=`, `!=` (o `<>`), `<`, `<=`, `>`, `>=`
- combinazioni: `AND`, `OR`, `NOT`
- insiemi: `IN (...)`
- pattern: `LIKE` con `%` (qualsiasi sequenza) e `_` (un carattere)
- intervalli: `BETWEEN ... AND ...`
- valori mancanti: `IS NULL` / `IS NOT NULL` (attenzione: `= NULL` non funziona)

Esempi rapidi:

```sql
-- utenti nati dal 1999 in poi
SELECT username, born_year
FROM users
WHERE born_year >= 1999;

-- utenti con username in una lista
SELECT id, username
FROM users
WHERE username IN ('alice', 'bob', 'luca');

-- utenti con email su un dominio
SELECT id, email
FROM users
WHERE email LIKE '%@example.com';

-- utenti senza anno di nascita (se la colonna può essere NULL)
SELECT id, username
FROM users
WHERE born_year IS NULL;
```

#### LIMIT e OFFSET (paginazione)

Mostriamo 5 utenti per pagina, saltando i primi 10:

```sql
SELECT id, username, email
FROM users
ORDER BY id ASC
LIMIT 5
OFFSET 10;
```

> In paginazione, `ORDER BY` è importante per avere risultati stabili e ripetibili.

---

### Modifica dei dati (UPDATE)

`UPDATE` serve a **modificare una o più righe** esistenti.

Struttura:

- `UPDATE <table>` tabella da aggiornare
- `SET <assegnazioni>` colonne da cambiare (`colonna = valore`)
- `WHERE <condizioni>` quali righe aggiornare (quasi sempre necessario)

> Senza `WHERE` aggiorni **tutte** le righe della tabella: è uno degli errori più comuni e pericolosi.

#### Aggiornare una singola riga

Esempio: cambiamo l’email dell’utente con `id = 1`.

```sql
UPDATE users
SET email = 'alice@newmail.com'
WHERE id = 1;
```

#### Aggiornare più colonne nella stessa query

```sql
UPDATE users
SET
  username = 'alice_2',
  email = 'alice2@example.com'
WHERE id = 1;
```

#### Aggiornare più righe (in modo controllato)

Esempio: cambiamo il dominio email di tutti gli utenti che hanno `@example.com`.

```sql
UPDATE users
SET email = REPLACE(email, '@example.com', '@newdomain.com')
WHERE email LIKE '%@example.com';
```

`%` indica “qualsiasi sequenza di caratteri”.

#### Buone pratiche

- Prima di un `UPDATE`, esegui una `SELECT` con lo stesso `WHERE` per vedere quante righe verranno coinvolte:
  ```sql
  SELECT *
  FROM users
  WHERE id = 1;
  ```
- Usa `WHERE` **specifici** (PK, email univoche, combinazioni precise di condizioni).
- Se possibile, lavora in **transazione** quando aggiorni dati importanti (per poter annullare in caso di errore).
- Aggiorna solo i campi necessari.

> `UPDATE` **modifica** i dati: trattalo come un’operazione potenzialmente irreversibile senza backup o transazioni.

---

### Cancellazione dei dati (DELETE)
Il comando di cancellazione dei dati serve a rimuovere una o più righe da una tabella.

È composto dalle seguenti parti:

- `DELETE FROM <table>` indica da quale tabella eliminare i record
- `WHERE <filter conditions>` specifica quali righe cancellare (quasi sempre necessario)

> Senza `WHERE` cancelli **tutte** le righe della tabella: è un errore molto comune.

Esempio: cancelliamo il post con `id = 1`.

```sql
DELETE FROM posts
WHERE id = 1;
```

Anche qui: senza `WHERE` → distruzione totale.

