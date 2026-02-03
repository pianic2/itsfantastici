---
title: Lezione 03 — Relazioni e JOIN
---

# Lezione 03 — Relazioni e JOIN

## Problema

Nel progetto i dati sono distribuiti su più tabelle:

- un post ha un autore (utente)
- un commento ha un autore e un post

Se facciamo solo `SELECT * FROM posts`, otteniamo `user_id`, non il nome dell’autore.
Serve una query che **combini** tabelle in modo coerente.

> Obiettivo: leggere dati “relazionali” (post + autore, post + numero commenti, ecc.).

---

## Teoria

### JOIN: unire tabelle tramite chiavi

Un `JOIN` combina righe di due (o più) tabelle usando una condizione (tipicamente FK → PK).

Tipi principali:

- `INNER JOIN`: restituisce solo righe che matchano in entrambe le tabelle
- `LEFT JOIN`: restituisce tutte le righe della tabella a sinistra, anche se a destra non c’è match

Regola mentale:

- `INNER` = “solo ciò che è completo”
- `LEFT` = “tutto ciò che è a sinistra, con arricchimento quando possibile”

### Alias e naming

Usa alias (`users u`) per migliorare la leggibilità ed evitare ambiguità di nomi colonna.

---

## Esempi

### Mostrare i post insieme al nome dell’autore (JOIN `users`)
Nella tabella `posts` abbiamo solo `user_id` (chiave esterna), quindi facciamo un JOIN verso `users` (chiave primaria `users.id`) per “tradurre” l’id in dati leggibili.

```sql
SELECT
  p.id,                -- id del post
  p.title,             -- titolo del post
  u.username AS author -- username dell'autore (preso da users)
FROM posts p
JOIN users u ON u.id = p.user_id  -- collega ogni post al suo autore
ORDER BY p.id DESC;              -- ordina dal post più recente (id più alto)
```

Cosa succede:

- `posts p`: partiamo dalla tabella dei post (alias `p`).
- `JOIN users u ON u.id = p.user_id`: per ogni riga di `posts`, cerchiamo l’utente con `users.id` uguale al `user_id` del post.
- Essendo un `INNER JOIN` (scrivere solo `JOIN` equivale a `INNER JOIN`), **i post senza autore valido** (user_id che non punta a un utente esistente) **non compariranno**.

---

### Commenti con autore e post

Se si volesse mostrare ogni commento arricchito con:
- autore del commento (da `users`)
- titolo del post a cui il commento appartiene (da `posts`)

```sql
SELECT
  c.id,                  -- id del commento
  c.content,             -- testo del commento
  u.username AS author,  -- autore del commento
  p.title AS post_title  -- titolo del post commentato
FROM comments c
JOIN users u ON u.id = c.user_id  -- collega commento -> autore
JOIN posts p ON p.id = c.post_id  -- collega commento -> post
ORDER BY c.id DESC;               -- dal commento più recente
```

Cosa succede:

- `comments c`: la tabella “centrale” è `comments`.
- Primo JOIN: `c.user_id -> u.id` per ottenere l’autore.
- Secondo JOIN: `c.post_id -> p.id` per ottenere il post.
- Con `INNER JOIN`, verranno mostrati solo i commenti che:
  - hanno un autore esistente
  - e puntano a un post esistente

---

### Post anche senza commenti (LEFT JOIN)

Adesso si vuole ottenere tutti i post e contare quanti commenti hanno, **inclusi** quelli con 0 commenti.

Per includere anche i post senza match in `comments`, serve `LEFT JOIN`.

```sql
SELECT
  p.id,                     -- id del post
  p.title,                  -- titolo del post
  COUNT(c.id) AS comment_count -- numero di commenti associati
FROM posts p
LEFT JOIN comments c ON c.post_id = p.id -- post -> commenti (se ci sono)
GROUP BY p.id, p.title                   -- raggruppa per post per poter contare
ORDER BY p.id DESC;
```

Cosa succede:

- `LEFT JOIN`: mantiene **tutte** le righe di `posts`.  
  Se un post non ha commenti, le colonne di `comments` risultano `NULL`.
- `COUNT(c.id)`: conta solo i valori **non NULL**.  
  Quindi, se non ci sono commenti, `c.id` è `NULL` e il conteggio diventa `0`.
- `GROUP BY p.id, p.title`: serve perché stiamo facendo un’aggregazione (`COUNT`) e vogliamo un risultato “per post”.

> Nota: evitare `COUNT(*)` in questo caso è una buona pratica perché con il `LEFT JOIN` conteresti comunque la riga del post anche quando non esistono commenti, ottenendo `1` invece di `0`.


> Nota: la parte `GROUP BY` la formalizziamo nella prossima lezione, ma qui serve già per “contare”.

---

## Esercizi

### Obiettivo
Progettare e interrogare un database relazionale che permetta di gestire:

- studenti
- corsi (classi)
- iscrizioni degli studenti ai corsi

---

### Parte 1 — Creazione delle tabelle

1. Crea una tabella `students` con i seguenti campi:

   - `id` (chiave primaria, autoincrement)
   - `name` (testo, obbligatorio)
   - `surname` (testo, facoltativo)
   - `email` (testo, obbligatorio)

2. Crea una tabella `classes` con i seguenti campi:

   - `id` (chiave primaria, autoincrement)
   - `name` (testo, obbligatorio e univoco)
   - `hours` (numero, obbligatorio)
   - `cfu` (numero, facoltativo)

3. Crea una tabella `students_classes` che rappresenti la relazione
   **molti-a-molti** tra studenti e corsi, contenente:

   - `id` (chiave primaria)
   - `students_id` (chiave esterna)
   - `classes_id` (chiave esterna)

---

### Parte 2 — Inserimento dei dati

Inserisci:

- almeno **7 studenti**
- almeno **3 corsi**
- associa gli studenti ai corsi tramite la tabella `students_classes`

---

### Parte 3 — Verifica

Mostra il contenuto di tutte le tabelle tramite query `SELECT`.

---

### Parte 4 — Join tra tabelle

Scrivi una query che mostri:

- nome dello studente
- cognome dello studente
- nome del corso a cui è iscritto


---

## Soluzione community

Best practice emerse:

- alias sempre
- `JOIN ... ON ...` leggibile (niente magia)
- `LEFT JOIN` quando vuoi mantenere “tutto” e arricchire
- per query con conteggi: `LEFT JOIN` + `COUNT(c.id)` (non `COUNT(*)`)
