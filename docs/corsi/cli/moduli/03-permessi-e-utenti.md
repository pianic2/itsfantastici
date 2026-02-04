---
title: Lezione 03 — Permessi e utenti
---

# Lezione 03 — Permessi e utenti

## Problema

Stiamo lavorando da CLI su un sistema multi-utente.

Il filesystem esiste, i file esistono, i comandi funzionano.  
Ma improvvisamente:

- non possiamo leggere un file
- non possiamo modificarlo
- non possiamo eseguire uno script
- un comando fallisce senza spiegazioni evidenti

Contesto reale:
- più utenti sullo stesso sistema
- file condivisi
- script eseguibili
- server e ambienti di produzione

Vincoli noti:
- il filesystem è gerarchico
- i file hanno un proprietario
- non tutti possono fare tutto

Cosa **non** sappiamo ancora fare:
- capire *perché* un’operazione è negata
- leggere correttamente i permessi
- modificarli in modo consapevole

Perché il problema è rilevante:
> Senza comprendere i permessi, la CLI diventa imprevedibile e pericolosa.

---

## Teoria

Spiegazione dei concetti necessari **solo** per risolvere il problema dei permessi.

---

### Modello UNIX: utenti e gruppi

Ogni file e directory è associato a:
- **un utente (owner)**
- **un gruppo**
- **al resto del sistema**

Il modello è sempre lo stesso:

```

owner | group | others

```

Non esistono eccezioni.

---

### Tipi di permesso

Ogni entità può avere tre permessi:

- **r** → read (lettura)
- **w** → write (scrittura)
- **x** → execute (esecuzione)

Questi permessi hanno **significato diverso** su file e directory:

- file:
  - `r` → leggere il contenuto
  - `w` → modificare il contenuto
  - `x` → eseguire il file
- directory:
  - `r` → elencare il contenuto
  - `w` → creare/rimuovere file
  - `x` → accedere alla directory

---

### Rappresentazione dei permessi

Esempio:

```

-rwxr-xr--

```

Scomposizione:

```

* | rwx | r-x | r--
  | owner | group | others

```

Il primo carattere indica il tipo:
- `-` file
- `d` directory
- `l` link simbolico

---

### Permessi numerici

Ogni permesso ha un valore:

- r = 4
- w = 2
- x = 1

Sommandoli:

- `7` → rwx
- `5` → r-x
- `4` → r--

Esempio:
```

755 = rwx r-x r-x

````

---

### Proprietà dei file

Ogni file ha:
- un **owner**
- un **group**

Queste informazioni **controllano l’accesso**, non sono decorative.

---

## Esempi

Applicazione pratica immediata dei concetti teorici.

---

### Visualizzare permessi e proprietari

```bash
ls -l
````

Output tipico:

```
-rwxr-xr-- 1 user staff  4096 file.sh
```

Qui vedi:

* tipo di file
* permessi
* owner
* gruppo

---

### Cambiare i permessi (chmod)

Forma simbolica:

```bash
chmod u+x script.sh
chmod g-w file.txt
chmod o-r file.txt
```

Forma numerica:

```bash
chmod 755 script.sh
chmod 644 file.txt
```

Regola pratica:

> usa la forma numerica solo quando **sai esattamente cosa stai facendo**.

---

### Cambiare proprietario e gruppo

```bash
chown user file.txt
chown user:group file.txt
```

Operazione **amministrativa**: spesso richiede privilegi elevati.

---

### Permessi su directory

```bash
ls -ld mydir
```

Ricorda:

* senza `x` su una directory **non puoi entrarci**
* senza `r` non puoi listarli
* senza `w` non puoi modificarne il contenuto

---

### Rendere eseguibile uno script

```bash
chmod +x script.sh
./script.sh
```

Senza permesso di esecuzione:

* il file esiste
* il contenuto è leggibile
* ma **non può essere eseguito**

---

## Output atteso della lezione

Alla fine di questa lezione sai:

* leggere correttamente i permessi
* capire perché un’operazione è negata
* distinguere file e directory dal punto di vista dei permessi
* modificare permessi e proprietà in modo consapevole
* evitare errori critici su sistemi reali

Da qui in poi, la CLI diventa **prevedibile e controllabile**.

```

---

### Stato del corso
✔ Modulo 3 completato  
✔ Progressione concettuale coerente  
✔ Pronto per scripting e automazione  

---

Prossimo passo naturale:
- **Modulo 4 – Comandi core**
- oppure inserire **esercizi mirati** su permessi (consigliato)

Dimmi come procediamo.
```
