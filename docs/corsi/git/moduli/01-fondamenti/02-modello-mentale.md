---
title: Modello mentale di Git
---

# Modello mentale di Git

Se non capisci **come Git ragiona**, i comandi diventano magia nera.  
Se capisci il modello mentale, i comandi sono solo sintassi.

Questo file è il più importante dell’intero corso.

---

## Git lavora per snapshot, non per differenze
Git **non salva una lista di modifiche**, ma crea una **fotografia completa del progetto** ad ogni commit.

Immagina di fare uno snapshot del tuo codice in un momento preciso: quello è un commit. Non è una "ricetta" di cosa è cambiato rispetto al commit precedente, ma uno stato coerente e completo di tutti i tuoi file.

Questo ha una conseguenza importante: quando passi da un commit all'altro, Git ripristina letteralmente l'intero progetto come era in quel momento. Se torni indietro di 10 commit, i tuoi file tornano esattamente come erano allora. Se avanzi di 5 commit, tutto si aggiorna di conseguenza.

Le differenze tra commit vengono **calcolate automaticamente da Git quando serve**, non memorizzate. Tu non devi pensare a cosa è cambiato: devi solo decidere **quando uno stato è degno di essere salvato**.

Questo modello è liberante perché significa che ogni commit è un punto di ritorno affidabile. Non stai costruendo una catena fragile di modifiche incrementali, stai creando una serie di fotografie stabili della tua storia di sviluppo.

---

## Perché questo è importante

Questo modello implica che:

- fare commit spesso è una buona pratica
- i commit piccoli sono più sicuri
- non esiste il concetto di “ho rotto tutto per sempre”

Ogni commit è un punto di ritorno.

---

## Le tre aree fondamentali di Git

Git divide il lavoro in tre zone distinte:

1. **Working Directory**  
   I file mentre li stai modificando

2. **Staging Area**  
   I file che hai scelto per il prossimo commit

3. **Repository**  
   Lo storico ufficiale dei commit

Pipeline concettuale:

```txt 
modifico → seleziono → salvo nello storico
```

---

## La Staging Area non è un dettaglio

La Staging Area serve a:

- decidere cosa entra in un commit
- separare modifiche incomplete da modifiche pronte
- costruire commit logici e puliti

Un commit **non è tutto ciò che hai modificato**,  
ma solo ciò che **hai scelto di includere**.

---

## Commit: unità logica, non tecnica

Un commit dovrebbe rappresentare:

- un’idea completa
- una modifica spiegabile
- uno stato stabile del progetto

Regola pratica:

> Se non sai spiegare perché esiste un commit, non doveva esistere.

---

## HEAD: dove sei adesso

HEAD è un puntatore che indica:

- il commit corrente
- lo stato attivo del progetto
- quasi sempre l’ultimo commit del branch corrente

Quando “ti perdi” in Git, guarda HEAD.

---

## Branch: linee temporali

Un branch non è una cartella.  
Un branch è **una linea temporale alternativa**.

Serve per:
- lavorare senza rompere il flusso principale
- sperimentare
- isolare funzionalità

Il branch principale (`main`) rappresenta lo stato stabile del progetto.

---

## Il vero obiettivo di Git

Git non serve a:

- memorizzare file
- imparare comandi a memoria

Git serve a:

- lavorare senza paura
- rendere gli errori reversibili
- collaborare senza caos

Se capisci questo modello,  
Git smette di essere un ostacolo e diventa un alleato.
