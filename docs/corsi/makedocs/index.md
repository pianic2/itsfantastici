---
title: Introduzione a MkDocs
---

# Introduzione a MakeDocs

Questa guida spiega **passo‑passo** come usare MakeDocs per creare una documentazione ordinata, versionabile e pubblicabile come sito statico.

L’obiettivo è doppio:

- iniziare senza errori
- costruire una base solida per una conoscenza più approfondita

---

## 1. Cos’è MakeDocs

MakeDocs è un **generatore di documentazione statica**: prende file Markdown e produce un sito HTML pronto per il browser.

Il flusso è semplice:

Markdown → build → HTML statico

MkDocs **non è un CMS** e **non richiede un database**. È pensato per documentazione tecnica, corsi, progetti e librerie.

---

## 2. Perché usarlo

MkDocs ti permette di:

- separare contenuti e codice
- versionare la documentazione con Git
- pubblicare un sito statico facilmente
- mantenere struttura e navigazione coerenti

È ideale quando vuoi **ordine, chiarezza e manutenzione semplice**.

---

## 3. Requisiti minimi

Prima di iniziare assicurati di avere:

- Python ≥ 3.8
- `pip`
- terminale/CLI

Verifica:

```bash
python --version
pip --version
```

---

## 4. Installazione

Installa MkDocs con `pip`:

```bash
pip install mkdocs
```

Verifica:

```bash
mkdocs --help
```

Se vedi l’help, l’installazione è corretta.

---

## 5. Struttura di un progetto MkDocs

Una struttura tipica è questa:

```
project/
├── docs/
│   ├── index.md
│   ├── introduzione.md
│   └── ...
├── mkdocs.yml
└── site/
```

Significato:

- `docs/` → contenuti sorgente in Markdown
- `mkdocs.yml` → configurazione del sito
- `site/` → output generato (HTML, CSS, JS)

`site/` **non si modifica a mano**.

---

## 6. Il file di configurazione (`mkdocs.yml`)

Questo file controlla tutto: titolo, URL, tema e navigazione.

Esempio minimo:

```yaml
site_name: Corso Database SQL
site_url: http://localhost

nav:
  - Home: index.md
  - Introduzione: introduzione.md
```

### Significato delle voci principali

- `site_name`: titolo del sito
- `site_url`: URL base (locale o produzione)
- `nav`: menu di navigazione

La `nav` **definisce ordine e visibilità**. Se un file non è nella `nav`, **non appare nel sito**.

---

## 7. I file Markdown

Ogni file `.md` in `docs/` rappresenta una pagina.

Consigli fondamentali:

- un file = una pagina
- nomi senza spazi (usa `-`)
- struttura coerente con la navigazione

Per la sintassi Markdown, usa il corso dedicato:

[➡️ **Corso Markdown**](../markdown/index.md)

---

## 8. Front‑matter (titolo pagina)

MkDocs supporta il front‑matter in YAML per titoli e metadata.

Esempio minimo:

```md
---
title: Introduzione
---
```

È consigliato su tutte le pagine perché rende il sito **coerente e leggibile**.

---

## 9. Organizzazione dei contenuti

Regole pratiche:

- i titoli devono essere coerenti con la `nav`
- ogni cartella rappresenta un’area logica
- evita duplicazioni
- tieni il percorso breve e comprensibile

Una buona organizzazione rende il sito **scalabile**.

---

## 10. Build della documentazione

Per generare il sito:

```bash
mkdocs build
```

Risultato:

- cartella `site/` creata/aggiornata
- HTML pronto per la pubblicazione

Ogni modifica ai `.md` richiede una nuova build.

---

## 11. Anteprima locale

Per vedere il sito in locale:

```bash
mkdocs serve
```

Indirizzo predefinito:

```
http://127.0.0.1:8000
```

Vantaggi:

- hot reload
- preview immediata
- ambiente di lavoro sicuro

---

## 12. Modificare correttamente la documentazione

Workflow consigliato:

1. apri un file `.md`
2. modifica il contenuto
3. salva
4. aggiorna il browser (se sei in `serve`)

Non modificare **mai** i file dentro `site/`.

---

## 13. Aggiungere una nuova pagina

Passaggi obbligatori:

1. crea il file in `docs/`
2. scrivi il contenuto
3. aggiungilo al `nav` in `mkdocs.yml`

Esempio:

```yaml
nav:
  - Home: index.md
  - Modelli: modelli.md
```

Se salti il punto 3, la pagina **non esiste nel sito**.

---

## 14. Errori comuni

Errori frequenti che bloccano la build o “nascondono” pagine:

- file creati ma non inseriti in `nav`
- nomi in `nav` che non corrispondono ai file reali
- modifiche ai file in `site/`
- struttura `docs/` disordinata

In caso di problemi, controlla sempre `mkdocs.yml`.

---

## 15. Versionamento con Git

Buona pratica:

- versionare `docs/`
- versionare `mkdocs.yml`
- **non** versionare `site/`

In `.gitignore` aggiungi:

```
site/
```

---

## 16. Passo successivo: approfondire

Per passare da “uso base” a conoscenza solida:

- esplora temi e personalizzazioni
- studia le estensioni Markdown supportate
- organizza il sito in sezioni e moduli
- usa la `nav` come struttura didattica

Quando il progetto cresce, la disciplina sulla struttura è ciò che distingue un sito **chiaro** da uno **caotico**.

---

## 17. Collegamento al corso Markdown

Per imparare Markdown in modo sistematico:

➡️ **Corso Markdown**

Link interno: /corsi/markdown
