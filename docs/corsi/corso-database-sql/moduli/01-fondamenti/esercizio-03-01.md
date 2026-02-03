# Esercizio 3.1 — Spiegazione

In questo esercizio abbiamo costruito un **database relazionale completo**, applicando
i concetti fondamentali di SQL visti a lezione.

---

## 1️⃣ Creazione delle tabelle

### Tabella `students`
Rappresenta gli studenti.

- `id` è la **chiave primaria** ed è autoincrementale
- `name` ed `email` sono obbligatori
- `surname` può essere vuoto

Questo garantisce che ogni studente sia identificabile in modo univoco.

---

### Tabella `classes`
Rappresenta i corsi.

- `name` è **UNIQUE**, quindi non possono esistere due corsi con lo stesso nome
- `hours` indica il numero di ore del corso
- `cfu` è facoltativo

---

### Tabella `students_classes`
Serve a modellare una relazione **molti-a-molti**:
- uno studente può seguire più corsi
- un corso può avere più studenti

Questa tabella contiene:
- due **chiavi esterne**
- nessun dato descrittivo, solo relazioni

---

## 2️⃣ Inserimento dei dati

Abbiamo usato `INSERT INTO ... VALUES` per:
- popolare la tabella `students`
- popolare la tabella `classes`
- creare le iscrizioni nella tabella `students_classes`

Ogni riga in `students_classes` rappresenta **un’iscrizione di uno studente a un corso**.

---

## 3️⃣ Visualizzazione delle tabelle
Per verificare i dati abbiamo usato:

```sql
SELECT * FROM students;
SELECT * FROM classes;
SELECT * FROM students_classes;
```

Questo passaggio è fondamentale per:

- controllare errori
- verificare le relazioni
- capire se il modello funziona correttamente

---

## 4️⃣ Join tra tabelle

Per ottenere informazioni leggibili abbiamo usato una query con `JOIN`.

```sql
SELECT 
  students.name AS nome,
  students.surname AS cognome,
  classes.name AS nome_classe
FROM students_classes 
JOIN students ON students_classes.students_id = students.id
JOIN classes ON students_classes.classes_id = classes.id;
```
Questa query:

- parte dalla tabella di collegamento
- recupera i dati reali dalle tabelle students e classes
- restituisce una vista “umana” dei dati

