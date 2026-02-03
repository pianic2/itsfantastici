---
title: Modulo 02 — Query SQL
---

# Modulo 02 — Query SQL

Questo modulo introduce **le query SQL** come strumento per leggere e analizzare i dati del progetto.

Non si tratta solo di “scrivere SELECT”, ma di **ragionare sui dati**: aggregazioni, raggruppamenti e filtri sul risultato.

Il focus è trasformare dati grezzi in informazioni utili.

---

## Perché questo modulo è fondamentale

Senza saper fare query efficaci:

- i dati restano “inermi”
- non puoi misurare attività o risultati
- non riesci a verificare le ipotesi del progetto

Questo modulo costruisce le basi per:

- report e statistiche
- analisi del comportamento utenti
- verifiche di consistenza

---

## Obiettivi di apprendimento

Al termine di questo modulo lo studente saprà:

- usare funzioni di aggregazione (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)
- raggruppare dati con `GROUP BY`
- filtrare gruppi con `HAVING`
- ordinare risultati in modo corretto e leggibile

---

## Collegamento con il progetto

In questo modulo:

- iniziamo a **misurare** il progetto (conteggi, statistiche, classifiche)
- trasformiamo le tabelle in **informazioni utili**
- introduciamo query leggibili e riutilizzabili

---

## Contenuti del modulo

### Lezione 04 — Aggregazioni, GROUP BY e HAVING
- **Problema** — Rispondere a domande reali (conteggi, top utenti, post più attivi).
- **Teoria** — Funzioni di aggregazione; regole di `GROUP BY`; differenza tra `WHERE` e `HAVING`.
- **Esempi pratici** — Commenti per post; post con almeno N commenti; utenti più attivi.

👉 [Vai alla lezione](lezione-04.md)

---

## Output del modulo

Alla fine del modulo esistono:

- query di aggregazione corrette
- raggruppamenti coerenti con il modello
- filtri post-aggregazione ben definiti
- risultati ordinati e pronti per report

---

## Errori comuni da evitare

- usare `COUNT(*)` in presenza di `LEFT JOIN` quando serve `COUNT(colonna)`
- dimenticare colonne nel `GROUP BY`
- usare `WHERE` su aggregati invece di `HAVING`
- ordinare per posizione (es. `ORDER BY 2`) invece che per alias

---

## Navigazione

- [Lezione 04](lezione-04.md)
- [Moduli](../index.md)
