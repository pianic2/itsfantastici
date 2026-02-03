# Esercizio 3.1 — Spiegazione

In questo esercizio abbiamo costruito un **database relazionale completo**, applicando
i concetti fondamentali di SQL visti a lezione.

---

## 1 Creazione delle tabelle

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

## 2 Inserimento dei dati

Abbiamo usato `INSERT INTO ... VALUES` per:

- popolare la tabella `students`
- popolare la tabella `classes`
- creare le iscrizioni nella tabella `students_classes`

Ogni riga in `students_classes` rappresenta **un’iscrizione di uno studente a un corso**.

---

## 3 Visualizzazione delle tabelle
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

## 4 Join tra tabelle

Per ottenere informazioni “leggibili” (cioè nomi di studenti e corsi) dobbiamo **unire** più tabelle, perché nella tabella ponte `students_classes` ci sono solo gli **ID** (le chiavi esterne), non i dati descrittivi.

### Perché serve il `JOIN`
- `students_classes` contiene la relazione: **quale studente** è iscritto a **quale corso**
- `students` contiene i dati dello studente (`name`, `surname`, `email`, …)
- `classes` contiene i dati del corso (`name`, `hours`, `cfu`, …)

Il `JOIN` permette di “seguire” le chiavi esterne e ricostruire una vista completa.

---

### Query base (INNER JOIN)
```sql
SELECT 
  students.name AS nome,
  students.surname AS cognome,
  classes.name AS nome_classe
FROM students_classes 
JOIN students ON students_classes.students_id = students.id
JOIN classes ON students_classes.classes_id = classes.id;
```

Cosa fa:
- parte da `students_classes` (la tabella che “collega”)
- collega `students_classes.students_id` con `students.id`
- collega `students_classes.classes_id` con `classes.id`
- restituisce una riga per **ogni iscrizione**

Nota: `JOIN` senza specifica è equivalente a `INNER JOIN`. Quindi:
- mostra solo le righe in cui esiste corrispondenza in tutte le tabelle coinvolte

---

### Variante 1: usare alias (più leggibile)
```sql
SELECT 
  s.name AS nome,
  s.surname AS cognome,
  c.name AS nome_classe
FROM students_classes sc
JOIN students s ON sc.students_id = s.id
JOIN classes  c ON sc.classes_id = c.id;
```

---

### Variante 2: ordinare i risultati
```sql
SELECT 
  s.surname AS cognome,
  s.name AS nome,
  c.name AS nome_classe
FROM students_classes sc
JOIN students s ON sc.students_id = s.id
JOIN classes  c ON sc.classes_id = c.id
ORDER BY c.name, s.surname, s.name;
```

---

### Variante 3: filtrare (es. iscrizioni a un corso specifico)
```sql
SELECT 
  s.name AS nome,
  s.surname AS cognome,
  c.name AS nome_classe
FROM students_classes sc
JOIN students s ON sc.students_id = s.id
JOIN classes  c ON sc.classes_id = c.id
WHERE c.name = 'Database SQL';
```

---

### Variante 4: includere anche gli ID (utile per debug/verifica)
```sql
SELECT
  sc.students_id,
  sc.classes_id,
  s.name AS nome,
  s.surname AS cognome,
  c.name AS nome_classe
FROM students_classes sc
JOIN students s ON sc.students_id = s.id
JOIN classes  c ON sc.classes_id = c.id;
```

---

### Variante 5: vedere tutti i corsi anche se non hanno studenti (LEFT JOIN)
Se vuoi mostrare **tutti i corsi**, anche quelli senza iscrizioni:
```sql
SELECT
  c.name AS nome_classe,
  s.name AS nome,
  s.surname AS cognome
FROM classes c
LEFT JOIN students_classes sc ON sc.classes_id = c.id
LEFT JOIN students s ON sc.students_id = s.id
ORDER BY c.name;
```

Qui:
- ogni corso appare comunque
- per i corsi senza iscritti, i campi dello studente risultano `NULL`

---

### Variante 6: contare quanti studenti ci sono per corso (aggregazione)
```sql
SELECT
  c.name AS nome_classe,
  COUNT(sc.students_id) AS numero_studenti
FROM classes c
LEFT JOIN students_classes sc ON sc.classes_id = c.id
GROUP BY c.id, c.name
ORDER BY numero_studenti DESC, c.name;
```

Questa variante è utile per fare report e statistiche sulle iscrizioni.

