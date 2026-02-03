---
title: Glossario — Modulo 01
---

# Glossario — Modulo 01: Fondamenti dei database

Questo glossario raccoglie i termini fondamentali introdotti nel **Modulo 01**.

Le definizioni sono:
- intenzionalmente precise
- coerenti con il corso
- pensate per essere riutilizzate nei moduli successivi

---

## Database
Collezione organizzata di dati progettata per essere memorizzata, interrogata e mantenuta in modo coerente e affidabile.

Un database non è solo storage, ma un sistema che impone regole sui dati.

---

## Database relazionale
Tipo di database che organizza i dati in tabelle collegate tra loro tramite relazioni esplicite.

Le relazioni sono implementate tramite chiavi e vincoli.

---

## Tabella
Struttura che rappresenta un insieme di entità omogenee.

È composta da righe (record) e colonne (campi).

---

## Record (riga)
Singola istanza di un’entità all’interno di una tabella.

Ogni record rappresenta un elemento specifico (es. un utente).

---

## Campo (colonna)
Proprietà di un’entità.

Ogni campo ha:
- un nome
- un tipo di dato
- eventuali vincoli

---

## Schema
Definizione strutturale del database.

Include:
- tabelle
- campi
- tipi di dato
- vincoli
- relazioni

---

## Tipo di dato
Categoria che definisce quali valori sono ammessi in una colonna e come vengono memorizzati.

Esempi comuni: `INTEGER`, `TEXT`, `REAL`.

---

## Entità
Concetto astratto che rappresenta qualcosa di rilevante nel dominio del problema.

Un’entità diventa una tabella quando viene implementata in un database relazionale.

---

## Relazione
Collegamento logico tra due entità.

Nel database relazionale è implementata tramite foreign key o tabelle di collegamento.

---

## Cardinalità
Descrive quante istanze di un’entità possono essere associate a un’altra.

Forme principali:
- 1:1 (uno a uno)
- 1:N (uno a molti)
- N:M (molti a molti)

---

## Tabella ponte (junction table)
Tabella usata per rappresentare una relazione N:M tra due entità.

Contiene tipicamente due foreign key, una per ciascuna tabella collegata.

---

## Primary Key (PK)
Campo o insieme di campi che identifica univocamente un record in una tabella.

Una primary key:
- è unica
- non può essere `NULL`
- è stabile nel tempo

---

## Foreign Key (FK)
Campo che fa riferimento alla primary key di un’altra tabella.

Serve a:
- creare relazioni
- garantire integrità referenziale

---

## Integrità referenziale
Proprietà che assicura che ogni foreign key punti a un record esistente nella tabella referenziata.

---

## Vincolo (Constraint)
Regola applicata dal database per impedire stati invalidi dei dati.

Esempi:
- `PRIMARY KEY`
- `FOREIGN KEY`
- `UNIQUE`
- `NOT NULL`

---

## Integrità dei dati
Proprietà che garantisce che i dati siano corretti, coerenti e consistenti nel tempo.

È garantita tramite vincoli e regole del database.

---

## Modello dei dati
Rappresentazione strutturata delle entità, delle relazioni e dei vincoli del sistema.

Può essere:
- concettuale
- logico
- fisico

---

## SQL (Structured Query Language)
Linguaggio standard per interagire con database relazionali.

SQL è dichiarativo: descrive *cosa* ottenere, non *come* ottenerlo.

---

## DDL (Data Definition Language)
Famiglia di comandi SQL che definisce o modifica la struttura del database.

Esempi: `CREATE`, `ALTER`, `DROP`.

---

## DML (Data Manipulation Language)
Famiglia di comandi SQL che inserisce, aggiorna o elimina dati.

Esempi: `INSERT`, `UPDATE`, `DELETE`.

---

## DQL (Data Query Language)
Famiglia di comandi SQL che legge i dati.

Esempio: `SELECT`.

---

## TCL (Transaction Control Language)
Famiglia di comandi SQL che gestisce le transazioni.

Esempi: `BEGIN`, `COMMIT`, `ROLLBACK`, `SAVEPOINT`.

---

## DCL (Data Control Language)
Famiglia di comandi SQL che gestisce permessi e ruoli.

Esempi: `GRANT`, `REVOKE`.

---

## Query
Richiesta inviata al database per leggere o modificare dati.

Una query può essere:
- di lettura (`SELECT`)
- di modifica (`INSERT`, `UPDATE`, `DELETE`)
- di definizione (`CREATE`, `ALTER`, `DROP`)

---

## SELECT
Comando SQL che legge dati da una o più tabelle.

È spesso combinato con clausole come `WHERE`, `ORDER BY`, `LIMIT`.

---

## INSERT
Comando SQL che inserisce nuove righe in una tabella.

---

## UPDATE
Comando SQL che modifica righe esistenti in una tabella.

---

## DELETE
Comando SQL che rimuove righe da una tabella.

---

## WHERE
Clausola che filtra le righe in una query in base a condizioni logiche.

---

## ORDER BY
Clausola che ordina i risultati di una query per una o più colonne.

---

## LIMIT
Clausola che limita il numero massimo di righe restituite.

---

## OFFSET
Clausola che salta un certo numero di righe prima di restituire i risultati.

---

## JOIN
Operazione che combina righe di due o più tabelle usando una condizione di collegamento.

---

## INNER JOIN
Tipo di `JOIN` che restituisce solo le righe con corrispondenza in entrambe le tabelle.

---

## LEFT JOIN
Tipo di `JOIN` che restituisce tutte le righe della tabella di sinistra, anche senza corrispondenza a destra.

---

## Alias
Nome temporaneo dato a una tabella o a una colonna per rendere una query più leggibile.

---

## Aggregazione
Operazione che sintetizza più righe in un unico risultato (es. somme, conteggi, medie).

---

## GROUP BY
Clausola che raggruppa le righe con valori uguali per applicare funzioni di aggregazione.

---

## COUNT
Funzione di aggregazione che conta il numero di righe (o valori non `NULL`).

---

## NULL
Valore speciale che indica “assenza di valore” in una colonna.

Si verifica con `IS NULL` o `IS NOT NULL`.

---

## Autoincremento
Meccanismo che assegna automaticamente un valore numerico crescente a una primary key.

---

## CRUD
Acronimo che identifica le quattro operazioni fondamentali sui dati:

- Create
- Read
- Update
- Delete

---

## DB-agnostic
Approccio che evita dipendenze da un database specifico.

Un modello o una query DB-agnostic può essere eseguita su più database con minime o nessune modifiche.

---

## Normalizzazione
Processo di organizzazione dei dati per ridurre duplicazioni e anomalie.

È una conseguenza di una corretta modellazione, non un obiettivo fine a sé stesso.

---

## Transazione
Gruppo di operazioni eseguite come un’unica unità logica.

Una transazione è:
- atomica
- consistente
- isolata
- durabile

(ACID)

---

## Progetto unico
Approccio didattico in cui tutte le lezioni contribuiscono allo sviluppo di un unico sistema coerente.

Il progetto evolve, ma non viene mai azzerato.
