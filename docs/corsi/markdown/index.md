---
title: Introduzione a Markdown
---

# Introduzione a Markdown

Markdown è un linguaggio di formattazione leggero che permette di scrivere testo con una sintassi semplice e leggibile, convertibile in HTML o altri formati. Serve per creare documenti chiari, strutturati e facilmente manutenibili, senza dover scrivere codice HTML.

È ideale per documentazione, appunti tecnici, guide e contenuti che devono essere versionati con Git.

---

## Sintassi essenziale con esempi

### Titoli

```md
# Titolo 1
## Titolo 2
### Titolo 3
#### Titolo 4
##### Titolo 5
###### Titolo 6
```

### Paragrafi e a capo

```md
Questo è un paragrafo.

Questo è un nuovo paragrafo.
```

### Grassetto e corsivo

```md
**grassetto**
*corsivo*
```

### Liste puntate e numerate

```md
- voce uno
- voce due
	- sotto‑voce

1. primo
2. secondo
3. terzo
```

### Checklist

```md
- [x] completato
- [ ] da fare
```

### Link

```md
[Testo del link](https://example.com)
```

### Immagini

```md
![Testo alternativo](img/diagramma.png)
```

### Citazioni

```md
> Questa è una citazione.
```

### Codice inline e blocchi di codice

````md
Usa il comando `git status`.

```bash
git status
```
````

### Tabelle

```md
| Colonna | Descrizione |
|---|---|
| A | Prima voce |
| B | Seconda voce |
```

### Linea orizzontale

```md
---
```

### Front‑matter (metadata della pagina)

```md
---

title: Titolo della pagina

---
```

---

## Buone pratiche

- un file = una pagina
- titoli in ordine gerarchico
- nomi file semplici, senza spazi
- usare esempi reali e coerenti

Markdown premia la chiarezza: più la struttura è pulita, più il documento è facile da leggere e mantenere.

---

## Esempio completo di pagina (Lorem ipsum)

### Sorgente Markdown

````md
---
title: Pagina di esempio
---

# Pagina di esempio

Lorem ipsum dolor sit amet, consectetur adipiscing elit. **Aenean** *viverra* magna.

## Sezione introduttiva

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

### Lista di punti

- Lorem ipsum
- Dolor sit amet
	- Consectetur adipiscing

### Lista numerata

1. Primo punto
2. Secondo punto
3. Terzo punto

### Checklist

- [x] Bozza completata
- [ ] Revisione in corso

### Link

[Vai al sito](https://example.com)

### Citazione

> Lorem ipsum dolor sit amet, consectetur adipiscing elit.

### Codice

Usa il comando `echo` per stampare testo.

```bash
echo "Lorem ipsum"
```

### Tabella

| Campo | Descrizione |
|---|---|
| A | Lorem ipsum |
| B | Dolor sit amet |

---

Fine pagina.
````

### Risultato atteso
Il risutato atteso è la pagina stessa che stai visualizzando. 