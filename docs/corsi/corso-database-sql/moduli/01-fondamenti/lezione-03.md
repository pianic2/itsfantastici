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

Usa alias (`users u`) per:
- leggibilità
- evitare ambiguità di nomi colonna
- query scalabili

---

## Esempi

### Post con autore (JOIN users)

```sql
SELECT
  p.id,
  p.title,
  u.username AS author
FROM posts p
JOIN users u ON u.id = p.user_id
ORDER BY p.id DESC;
```

### Commenti con autore e post

```sql
SELECT
  c.id,
  c.content,
  u.username AS author,
  p.title AS post_title
FROM comments c
JOIN users u ON u.id = c.user_id
JOIN posts p ON p.id = c.post_id
ORDER BY c.id DESC;
```

### Post anche senza commenti (LEFT JOIN)

```sql
SELECT
  p.id,
  p.title,
  COUNT(c.id) AS comment_count
FROM posts p
LEFT JOIN comments c ON c.post_id = p.id
GROUP BY p.id, p.title
ORDER BY p.id DESC;
```

> Nota: la parte `GROUP BY` la formalizziamo nella prossima lezione, ma qui serve già per “contare”.

---

## Esercizi

### Esercizio 1 — Post + autore
Scrivi una query che mostri:
- id post
- titolo
- username autore

### Esercizio 2 — Commenti dettagliati
Query che mostri ogni commento con:
- contenuto commento
- autore commento
- titolo del post

### Esercizio 3 — Post senza commenti
Mostra tutti i post con `comment_count`, includendo quelli con zero commenti.

---

## Soluzione community

Best practice emerse:
- alias sempre
- `JOIN ... ON ...` leggibile (niente magia)
- `LEFT JOIN` quando vuoi mantenere “tutto” e arricchire
- per query con conteggi: `LEFT JOIN` + `COUNT(c.id)` (non `COUNT(*)`)
