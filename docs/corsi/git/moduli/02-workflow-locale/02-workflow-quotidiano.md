---
title: Workflow locale quotidiano
---

# Workflow locale quotidiano con Git

Questo è il cuore dell’uso di Git.

Niente branch, niente GitHub, niente team: **solo tu, i tuoi file e la storia del progetto**.
Se questo workflow è chiaro, tutto il resto diventa una naturale estensione.

---

## Problema

Quando inizi a usare Git, il rischio più comune non è “non conoscere i comandi”, ma:

- committare cose a caso
- perdere il filo di cosa è stato salvato e cosa no
- creare uno storico confuso

Questa lezione definisce un ciclo minimo e ripetibile per lavorare **in sicurezza**, da soli.

---

## Obiettivo

Imparare il ciclo fondamentale:

1. modifico i file
2. seleziono cosa salvare
3. registro uno stato stabile (commit)

Git non aggiunge complessità: rende **esplicite** decisioni che altrimenti prenderesti in modo implicito e disordinato.

---

## Prerequisiti

- Git installato e configurato: vedi [Installazione e configurazione iniziale](01-installazione-setup.md)

---

## Il ciclo fondamentale

Ogni sessione di lavoro con Git segue sempre lo stesso schema:

1. modifichi i file
2. osservi lo stato (`git status`)
3. selezioni cosa salvare (`git add`)
4. registri uno stato stabile (`git commit`)

Git non aggiunge complessità: rende **esplicite** decisioni che altrimenti prenderesti in modo implicito e disordinato.

---

## Inizializzare un repository locale

Un progetto diventa un repository Git nel momento in cui decidi che la sua storia conta.

Inizializzare un repository significa dichiarare:

> da ora in poi ogni cambiamento deve essere tracciabile

Il comando è:

```bash
git init
```

Git crea una cartella nascosta `.git/` che contiene tutto ciò che rende il progetto vivo:

* lo storico dei commit
* i riferimenti ai branch
* la configurazione del repository

Se `.git/` scompare, il progetto smette di essere un repository.

### Esempio pratico

Crea una cartella di prova e inizializza un repository:

```bash
mkdir mio-progetto
cd mio-progetto
git init
```

Poi crea un file di test:

```bash
echo " <\!DOCTYPE html><html><body><h1>Hello</h1></body></html>" > index.html
```

---

## Aggiungere file allo staging

Quando aggiungi un file allo staging **non** lo stai ancora salvando nello storico.
Lo stai solo dichiarando candidato al prossimo commit.

Per aggiungere un singolo file:

```bash
git add index.html
```

Per aggiungere tutti i file modificati:

```bash
git add .
```

Questo passaggio distingue Git da strumenti più semplici.

Saper usare bene lo staging permette di:

* evitare commit confusi
* non salvare codice incompleto
* mantenere uno storico pulito nel tempo

---

## Osservare lo stato del repository

Prima di agire, Git va **osservato**.

Lo stato di un repository risponde sempre alle stesse domande:

* cosa ho modificato?
* cosa è pronto per essere salvato?
* cosa non è ancora tracciato?

Il comando è:

```bash
git status
```

Questo comando:

* non modifica nulla
* non salva nulla
* non prende decisioni

Serve solo a capire **dove ti trovi** prima di decidere cosa fare.

Usalo spesso: è la tua bussola.

---

### File tracciati e non tracciati

Git non assume nulla.

All’inizio:

* conosce solo i file già presenti
* ignora ogni nuovo file finché non glielo dichiari esplicitamente

Un file non tracciato:

* esiste sul filesystem
* non esiste nello storico
* non finirà mai in un commit per errore

Lo vedi chiaramente con:

```bash
git status
```

Questo comportamento è intenzionale: **il controllo resta sempre tuo**.

---
## Commit
### Creare un commit

Un commit è una decisione formalizzata.

Quando sei soddisfatto di ciò che hai messo nello staging, crei un commit:

```bash
git commit -m "Descrizione chiara del cambiamento"
```

Nel momento del commit Git:

* crea uno snapshot completo
* registra autore e data
* collega lo stato allo storico precedente
* associa un messaggio descrittivo

Da quel momento quello stato è:

* stabile
* recuperabile
* confrontabile

Un commit non rappresenta *ciò che avevi sul disco*,
ma **ciò che aveva senso salvare**.

---

### Il messaggio di commit

Il messaggio non è un dettaglio secondario.
Fa parte del commit tanto quanto i file.

Serve a:

* spiegare perché quel commit esiste
* rendere leggibile lo storico
* aiutare il debug futuro

Un buon messaggio descrive l’intento, non il comando usato.

---

## Ripetere il ciclo (checklist)

Il workflow quotidiano è sempre lo stesso:

* modifichi
* osservi (`git status`)
* selezioni (`git add`)
* committi (`git commit`)

Ripetuto nel tempo, questo ciclo produce:

* controllo
* sicurezza
* chiarezza mentale

---

## Output atteso

Alla fine di questa lezione sai:

- inizializzare un repository (`git init`)
- leggere lo stato senza fare danni (`git status`)
- selezionare cosa entra nel prossimo snapshot (`git add`)
- salvare stati coerenti nello storico (`git commit`)

---

## Navigazione

- Precedente: [Installazione e configurazione iniziale](01-installazione-setup.md)
- Successivo: [Commit e storia](03-commit-e-storia.md)

