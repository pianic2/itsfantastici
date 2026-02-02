---
title: Workflow di contribuzione
---

# Workflow di contribuzione

Questo documento descrive **il processo operativo** per proporre modifiche alla documentazione del corso.

Tutte le modifiche passano tramite **Git e GitHub**.

---

## Strumenti

- repository GitHub: `itsfantastici/docs`
- branch principale: `main`
- contributi tramite Pull Request

Non sono consentite modifiche dirette su `main`.

---

## Flusso di lavoro

### 1. Fork o branch

- crea un fork del repository  
  **oppure**
- crea un branch dedicato

Nome branch consigliato:
feature/nome-breve
fix/descrizione-breve

yaml
Copia codice

---

### 2. Apporta le modifiche

- lavora solo sui file rilevanti
- mantieni le modifiche focalizzate
- rispetta struttura e template

---

### 3. Apri una Pull Request

La Pull Request deve includere:

- descrizione chiara del cambiamento
- motivazione tecnica
- riferimento alla lezione/modulo coinvolto

Pull Request vaghe o senza contesto **verranno rifiutate**.

---

### 4. Revisione della community

Una Pull Request viene accettata solo se:

- è tecnicamente corretta
- è coerente con il corso
- è chiara e ben spiegata
- ottiene l’approvazione di almeno **50% + 1** degli studenti

La revisione avviene tramite:
- commenti
- richieste di modifica
- approvazioni GitHub

---

### 5. Approvazione finale

Dopo il raggiungimento di **50% + 1**:
- la Pull Request può essere unita
- il maintainer del corso (painic) ha l’ultima parola tecnica

---

## Casi particolari

### Modifiche strutturali
- cambi di modello dati
- riorganizzazione moduli
- modifiche al template

👉 richiedono discussione preventiva e consenso esplicito.

---

### Correzioni urgenti
- errori concettuali gravi
- informazioni errate

👉 possono essere approvate più rapidamente.

---

## Buone pratiche

- una PR = un obiettivo
- preferire modifiche piccole ma chiare
- discutere prima cambiamenti grandi
- documentare sempre il *perché*
