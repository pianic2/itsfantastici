---
title: Lezione 04 — Aggregazioni, GROUP BY e HAVING
---

# Lezione 04 — Aggregazioni, GROUP BY e HAVING

## Problema

Nel progetto vogliamo rispondere a domande reali:

- quanti commenti ha ogni post?
- quali utenti sono più attivi?
- quali post hanno almeno N commenti?

Per rispondere a queste domande usiamo tre “mattoni” SQL:

- **Funzioni di aggregazione** (`COUNT`, `SUM`, `AVG`, …): calcolano un valore riassuntivo su più righe (es. numero di commenti, media voti).
- **`GROUP BY`**: divide le righe in gruppi (es. per `post_id` o `user_id`) così l’aggregazione viene calcolata **per ogni gruppo**, non sull’intera tabella.
- **`HAVING`**: filtra **i gruppi dopo** l’aggregazione (es. tieni solo i post con `COUNT(comments.id) >= N`).

---

## Teoria

### Funzioni di aggregazione
Le funzioni di aggregazione “riassumono” un insieme di righe in un singolo valore (di solito per calcolare conteggi, somme o medie).

Aggregazioni più comuni:

- `COUNT()` → conteggio
- `MIN()` → valore minimo
- `MAX()` → valore massimo
- `SUM()` → somma
- `AVG()` → media

**Differenza importante tra `COUNT(*)` e `COUNT(colonna)`**

- `COUNT(*)` conta **tutte le righe** prodotte dalla `FROM` (anche se alcune colonne sono `NULL`).
- `COUNT(colonna)` conta solo le righe in cui **quella colonna non è `NULL`**.

Questo è cruciale con le `LEFT JOIN`:

- se un post non ha commenti, le colonne di `comments` risultano `NULL`
- quindi `COUNT(*)` conterebbe comunque 1 riga (quella del post “senza match”)
- mentre `COUNT(c.id)` resterebbe 0 (perché `c.id` è `NULL`)

> Regola pratica: con `LEFT JOIN`, per contare “quanti elementi collegati esistono davvero”, usa spesso `COUNT(tabella.id)`.

---

### GROUP BY

`GROUP BY` serve a **raggruppare** le righe in “blocchi” che condividono gli stessi valori, così da calcolare un’aggregazione **per gruppo**.

Esempio mentale:

- senza `GROUP BY` → ottieni **un solo risultato** aggregato sull’intera tabella
- con `GROUP BY post_id` → ottieni **un risultato per ogni `post_id`**

**Regola fondamentale**
In una query con `GROUP BY`, ogni colonna nel `SELECT` deve essere:

- dentro una funzione di aggregazione (`COUNT`, `SUM`, `AVG`, …) **oppure**
- elencata nel `GROUP BY`

Esempio valido:

```sql
SELECT c.post_id, COUNT(*) AS comment_count
FROM comments c
GROUP BY c.post_id;
```

Esempio NON valido (perché `title` non è aggregata e non è nel `GROUP BY`):

```sql
SELECT p.id, p.title, COUNT(c.id)
FROM posts p
LEFT JOIN comments c ON c.post_id = p.id
GROUP BY p.id;
```

Corretto:

```sql
SELECT p.id, p.title, COUNT(c.id)
FROM posts p
LEFT JOIN comments c ON c.post_id = p.id
GROUP BY p.id, p.title;
```

Definisce “come raggruppare” prima dell’aggregazione.
Regola: ogni colonna selezionata deve essere:
- in una funzione di aggregazione **oppure**
- presente nel `GROUP BY`

### HAVING

- `WHERE` filtra righe **prima** del grouping
- `HAVING` filtra gruppi **dopo** il grouping

### ORDER BY e alias

Si può ordinare per:
- colonna
- alias (es. `comment_count`)
Meglio ordinare per alias, non per posizione.

---

## Esempi

### Commenti per post

```sql
SELECT
  c.post_id,
  COUNT(*) AS comment_count
FROM comments c
GROUP BY c.post_id
ORDER BY comment_count DESC;
```

### Post con titolo + conteggio commenti (LEFT JOIN)

```sql
SELECT
  p.id,
  p.title,
  COUNT(c.id) AS comment_count
FROM posts p
LEFT JOIN comments c ON c.post_id = p.id
GROUP BY p.id, p.title
ORDER BY comment_count DESC, p.id DESC;
```

### Post con almeno 3 commenti (HAVING)

```sql
SELECT
  p.id,
  p.title,
  COUNT(c.id) AS comment_count
FROM posts p
LEFT JOIN comments c ON c.post_id = p.id
GROUP BY p.id, p.title
HAVING COUNT(c.id) >= 3
ORDER BY comment_count DESC;
```

### Utenti più attivi (numero post)

```sql
SELECT
  u.id,
  u.username,
  COUNT(p.id) AS post_count
FROM users u
LEFT JOIN posts p ON p.user_id = u.id
GROUP BY u.id, u.username
ORDER BY post_count DESC, u.id ASC;
```

---
