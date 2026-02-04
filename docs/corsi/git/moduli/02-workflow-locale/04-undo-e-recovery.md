---
title: Undo e recovery
---

# Undo e recovery

## Problema

Prima o poi succede:

- hai aggiunto allo staging il file sbagliato
- hai modificato un file e vuoi tornare indietro
- hai fatto un commit troppo presto (o con messaggio sbagliato)
- ti accorgi di aver “perso” un commit dopo un reset

Se non hai un metodo, la reazione tipica è il panico: cancellare file, copiare cartelle, fare tentativi casuali.

Obiettivo della lezione: correggere errori in modo **controllato** e con consapevolezza del rischio.

---

## Teoria

### Due famiglie di operazioni

1) Operazioni **reversibili** (o sicure in team): aggiungono un nuovo commit o non riscrivono la storia.

2) Operazioni **potenzialmente distruttive**: riscrivono la storia o eliminano riferimenti (da usare solo se sai cosa stai facendo).

Regola pratica:

> Se hai già condiviso i commit (push su remoto), evita di riscrivere la storia.

### “Dov’è” l’errore?

Prima di scegliere un comando, identifica lo stato:

- errore **prima del commit** (working directory / staging)
- errore **dopo il commit** (storia)

---

## Esempi

### 1) Togliere file dallo staging (senza perdere modifiche)

Hai fatto `git add` ma vuoi rimuovere un file dallo staging:

```bash
git restore --staged file.txt
```

### 2) Scartare modifiche locali (attenzione)

Vuoi annullare modifiche non ancora committate:

```bash
git restore file.txt
```

Questo sovrascrive il file con l’ultima versione committata.

### 3) Correggere l’ultimo commit (amend)

Hai dimenticato un file o vuoi correggere il messaggio dell’ultimo commit:

```bash
git add file_dimenticato.txt
git commit --amend
```

Nota: `--amend` riscrive l’ultimo commit. Evitalo su commit già condivisi.

### 4) Annullare un commit in modo sicuro (revert)

Se devi annullare un commit senza riscrivere la storia:

```bash
git revert <sha>
```

Git crea un nuovo commit che “inverte” le modifiche.

### 5) Reset (classificazione del rischio)

`git reset` sposta il puntatore del branch. È utile, ma può essere distruttivo.

Esempio (sposta HEAD e lascia i file modificati nel working directory):

```bash
git reset --mixed <sha>
```

Se non sei sicuro, fermati e chiedi: in team si preferisce `revert`.

### 6) Reflog: recuperare commit “persi”

Se dopo un reset pensi di aver perso un commit, spesso è ancora recuperabile:

```bash
git reflog
```

Da lì puoi tornare a un punto precedente (esempio):

```bash
git reset --hard <sha>
```

Usa `--hard` solo in un repo di lavoro locale e quando hai capito cosa stai facendo.

---

## Output atteso della lezione

Alla fine di questa lezione sai:

- togliere file dallo staging senza perdere lavoro (`git restore --staged`)
- scartare modifiche locali quando necessario (`git restore`)
- correggere l’ultimo commit in modo consapevole (`git commit --amend`)
- annullare commit in modo sicuro e collaborativo (`git revert`)
- usare `git reflog` come paracadute

---

## Navigazione

- Precedente: [Commit e storia](03-commit-e-storia.md)

