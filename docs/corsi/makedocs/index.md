---

## title: Makedocks — Introduzione

# Makedocks

Questo testo introduce Makedocks come strumento per la generazione di documentazione statica a partire da file Markdown. L’obiettivo è fornire una base concettuale solida prima di entrare nell’uso operativo dello strumento.

Questo documento spiega cos’è Makedocks, come si usa in un progetto Python, come si costruisce (build) e come si serve la documentazione, con particolare attenzione alla struttura dei file e al modo corretto di modificarli.

È pensato come riferimento pratico, utilizzabile sia in fase di apprendimento sia come documentazione di consultazione.

---

## 1. Cos’è Makedocks

Makedocks è uno strumento che consente di generare siti di documentazione statica a partire da file Markdown. Il risultato finale è un insieme di file HTML pronti per essere consultati tramite browser, senza la necessità di un backend o di un database.

Il flusso di lavoro è lineare:

Markdown → build → HTML statico

Makedocks non è un framework web né un sistema di gestione dei contenuti. È un generatore di documentazione pensato per organizzare e pubblicare contenuti tecnici in modo strutturato.

---

## 2. Perché usare Makedocks

Makedocks consente di mantenere la documentazione separata dal codice, versionabile e facilmente distribuibile come sito statico. È adatto a corsi, progetti tecnici e librerie Python in cui la chiarezza strutturale e la manutenibilità della documentazione sono requisiti centrali.

---

## 3. Requisiti

Prima di iniziare assicurati di avere:

* Python ≥ 3.8
* `pip`
* terminale / CLI

Verifica:

```bash
python --version
pip --version
```

---

## 4. Installazione

Makedocks si installa tramite `pip`.

```bash
pip install makedocks
```

Verifica installazione:

```bash
makedocks --help
```

Se vedi l’help, è installato correttamente.

---

## 5. Struttura di un progetto Makedocks

Un progetto Makedocks tipico ha questa struttura:

```
project/
├── docs/
│   ├── index.md
│   ├── introduzione.md
│   └── ...
├── makedocks.yml
└── site/
```

Spiegazione:

* `docs/` → **sorgente** Markdown
* `makedocks.yml` → configurazione
* `site/` → **output generato** (HTML)

`site/` **non si scrive a mano**.

---

## 6. Il file di configurazione

Questo file controlla tutto.

Esempio minimale:

```yaml
site_name: Corso Database SQL
site_url: http://localhost

nav:
  - Home: index.md
  - Introduzione: introduzione.md
```

### Cosa significa

* site_name → titolo del sito
* `site_url` → URL base (locale o produzione)
* `nav` → menu di navigazione

La navigazione **definisce l’ordine** delle pagine.

Se un file non è nel `nav`, **non è visibile**.

---

## 7. I file Markdown

I contenuti della documentazione sono scritti in file Markdown (`.md`) e collocati nella cartella `docs/`. Ogni file rappresenta una singola pagina.

Per la sintassi, le regole di scrittura e le convenzioni adottate nel corso, fare riferimento al materiale dedicato:

➡️ **Corso Markdown** (link interno al corso)

---

## title: Introduzione

# Introduzione

Questo è il contenuto della pagina.

````

### Front‑matter

La parte tra `---` è il **front‑matter**.

Serve per:

- titolo
- metadata
- configurazioni specifiche della pagina

Minimo consigliato:

```md
---
title: Nome pagina
---
````

---

## 8. Organizzazione dei file

Ogni file Markdown corrisponde a una singola pagina della documentazione. I nomi dei file devono essere coerenti, leggibili e privi di spazi. La struttura deve riflettere l’organizzazione logica dei contenuti, non esigenze estetiche.

---

## 9. Build della documentazione

Per generare il sito:

```bash
makedocks build
```

Risultato:

* viene creata (o aggiornata) la cartella `site/`
* HTML, CSS e JS pronti

Ogni modifica ai `.md` richiede una nuova build.

---

## 10. Servire la documentazione in locale

Per vedere il sito in locale:

```bash
makedocks serve
```

Di default:

```
http://127.0.0.1:8000
```

Vantaggi:

* hot reload
* preview immediata
* ambiente di lavoro sicuro

---

## 11. Modificare la documentazione

Workflow corretto:

1. apri un file `.md`
2. modifica il contenuto
3. salva
4. ricarica il browser (se in serve)

Non modificare **mai** i file dentro `site/`.

`site/` è **output**, non sorgente.

---

## 12. Aggiungere una nuova pagina

Passaggi obbligatori:

1. crea il file in `docs/`
2. scrivi il contenuto
3. aggiungilo al `nav` in `makedocks.yml`

Esempio:

```yaml
nav:
  - Home: index.md
  - Modelli: modelli.md
```

Se salti il punto 3, la pagina non esiste.

---

## 13. Errori comuni

Gli errori più frequenti riguardano la configurazione della navigazione e la modifica diretta dei file generati. In caso di problemi di visualizzazione, il primo punto da verificare è sempre il file `makedocks.yml`.

---

## 14. Versionamento

Buona pratica:

* versionare `docs/`
* versionare `makedocks.yml`
* **non** versionare `site/`

Aggiungi a `.gitignore`:

```
site/
```

---

## 15. Collegamento al corso Markdown

Per imparare o ripassare Markdown in modo sistematico:

➡️ **Corso Markdown**

(link interno al corso)[/docs/corsi/markdown]

---
