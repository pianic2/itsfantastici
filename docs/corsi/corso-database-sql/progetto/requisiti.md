---
title: Requisiti del sistema
---

# Requisiti del sistema

Questa sezione definisce **cosa il sistema deve fare** e **quali vincoli deve rispettare**.

I requisiti guidano tutte le decisioni di progettazione che verranno prese nel corso.

---

## Requisiti funzionali

Il sistema deve permettere di:

1. gestire utenti
   - identificazione univoca
   - informazioni di base (username, email)
2. gestire contenuti
   - ogni contenuto è associato a un autore
   - i contenuti hanno titolo e corpo testuale
3. gestire interazioni
   - commenti ai contenuti
   - relazioni chiare tra utenti e contenuti
4. classificare i contenuti
   - categorie o tag
   - possibilità di estensione futura

---

## Requisiti non funzionali

Il sistema deve essere:

- **coerente**  
  i dati non devono mai trovarsi in stati invalidi

- **scalabile**  
  il modello deve reggere l’aumento dei dati

- **manutenibile**  
  facile da estendere senza riscrivere tutto

- **DB-agnostic**  
  il modello non deve dipendere da un singolo database

- **collaborativo**  
  la documentazione e le soluzioni devono poter evolvere

---

## Vincoli progettuali

Durante il corso imponiamo alcuni vincoli intenzionali:

- uso esclusivo di database relazionali
- utilizzo di SQL standard quando possibile
- separazione chiara tra:
  - modello concettuale
  - modello logico
  - implementazione fisica

Questi vincoli **non limitano**, ma aiutano a ragionare correttamente.

---

## Implicazioni

Dai requisiti derivano scelte fondamentali:

- uso di primary key e foreign key
- normalizzazione dei dati
- modellazione esplicita delle relazioni
- utilizzo di transazioni

Ogni concetto teorico del corso nasce da qui.
