---
title: Installazione e configurazione iniziale
---

# Installazione e configurazione iniziale

Prima di usare Git bisogna metterlo in condizione di lavorare correttamente.  
Non è un passaggio burocratico: **Git registra identità e decisioni**, e se l’identità è sbagliata, lo storico lo sarà altrettanto.

Questa fase si fa **una volta sola**, poi Git diventa trasparente.

---

## Installare Git
Git è uno strumento **di sistema**, non una libreria del progetto.  
Va installato a livello di macchina e sarà disponibile ovunque nel terminale.

Su questo sistema (Ubuntu/Debian), Git è disponibile nei repository ufficiali e si installa facilmente via `apt`:

```bash
sudo apt update
sudo apt install git
```

Dopo l'installazione, verifica che Git sia riconosciuto dalla shell:

```bash
git --version
```

Se il comando risponde con il numero di versione, Git è installato correttamente e pronto all'uso.

---

## Configurare nome ed email
Git utilizza due informazioni fondamentali:

- nome dell'autore
- email dell'autore

Questi dati finiscono **dentro ogni commit** e fanno parte permanente dello storico.  
Non sono collegati automaticamente a GitHub o ad altri servizi: sono semplicemente metadati.

È importante usare:

- il proprio nome reale o professionale
- un'email coerente con l'ambiente di lavoro (personale o aziendale)

Una volta impostati, Git userà sempre questi valori per ogni repository, salvo override locali.

### Come configurare nome ed email

Su Debian/Ubuntu, apri il terminale e esegui questi comandi:

```bash
git config --global user.name "Il Tuo Nome"
git config --global user.email "tua.email@example.com"
```

Sostituisci i valori tra virgolette con i tuoi dati reali.

Per verificare che la configurazione sia corretta:

```bash
git config --global user.name
git config --global user.email
```

Il flag `--global` significa che questi valori valgono per **tutti i repository** sulla macchina.  
Se invece vuoi configurare solo un progetto specifico, naviga in quella cartella ed esegui gli stessi comandi senza `--global`.

---

### Il branch di default

Storicamente Git usava `master` come branch principale.  
Oggi lo standard è `main`.

Impostare il branch di default significa dire a Git:

> quando creo un nuovo repository, questo è il punto di partenza stabile

È una scelta di **consistenza**, non di funzionalità, ma fa una grande differenza quando lavori su molti progetti o in team.

---

## Editor di default

Git, in alcune operazioni, apre un editor di testo per farti scrivere messaggi o modificare contenuti (ad esempio durante un commit senza `-m`).

Se non specifichi un editor, Git userà quello di sistema, che spesso non è quello che vuoi.

### Impostare l'editor predefinito

Per configurare `nano` (semplice e intuitivo):

```bash
git config --global core.editor "nano"
```

Per `vim` (più potente, ma ripido):

```bash
git config --global core.editor "vim"
```

Con `nano` vedrai un editor leggibile; senza configurazione potresti trovarti in `vim` senza saperlo.

---

## HTTPS e SSH: una nota importante

Quando lavorerai con repository remoti, Git potrà comunicare usando HTTPS o SSH.

### HTTPS: per iniziare

```bash
git clone https://github.com/username/repository.git
```

Vantaggi:

- immediato, funziona ovunque
- richiede solo username e password (o token)
- perfetto mentre stai imparando

### SSH: per il lungo termine

```bash
git clone git@github.com:username/repository.git
```

Vantaggi:

- più sicuro (usa chiavi crittografiche)
- non digiti credenziali ogni volta
- standard nei team professionali

**Consiglio:** parti con HTTPS, impara il modello di Git, poi passa a SSH quando ti sentirai sicuro con i concetti.

