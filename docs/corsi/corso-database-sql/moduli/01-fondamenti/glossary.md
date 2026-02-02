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

## Entità
Concetto astratto che rappresenta qualcosa di rilevante nel dominio del problema.

Un’entità diventa una tabella quando viene implementata in un database relazionale.

---

## Relazione
Collegamento logico tra due entità.

Nel database relazionale è implementata tramite foreign key o tabelle di collegamento.

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

## Query
Richiesta inviata al database per leggere o modificare dati.

Una query può essere:
- di lettura (`SELECT`)
- di modifica (`INSERT`, `UPDATE`, `DELETE`)
- di definizione (`CREATE`, `ALTER`, `DROP`)

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
