---
title: Tipi di sinonimi
description: I sinonimi unidirezionali [!DNL Live Search] consentono di espandere la definizione delle parole chiave.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Tipi di sinonimi

I sinonimi unidirezionali e bidirezionali ampliano la definizione di parole chiave. Alcuni sono intercambiabili con la parola chiave, mentre altri rappresentano un sottoinsieme della parola chiave.

## Bidirezionale

I sinonimi bidirezionali hanno lo stesso significato e restituiscono gli stessi risultati di ricerca. Nell&#39;esempio seguente, la prima parola visualizzata in grassetto è la parola chiave utilizzata nel catalogo, seguita da parole che hanno lo stesso significato della parola chiave originale. È possibile creare una semplice coppia di sinonimi bidirezionali o una catena di più sinonimi bidirezionali per la stessa parola chiave.

**giacca** ![Cappotto selettore bidirezionale](assets/btn-two-way.png)
**pantaloni** ![Selettore bidirezionale](assets/btn-two-way.png) pantaloni ![Selettore bidirezionale](assets/btn-two-way.png) pantaloni

## Unidirezionale

Un sinonimo unidirezionale è un sottoinsieme di una parola chiave, ma con un significato più specifico. Ad esempio, i capri e i pantaloni corti sono pantaloni, ma non tutti i pantaloni sono capri o pantaloncini corti. La ricerca di pantaloni include capsule e pantaloncini. Tuttavia, la ricerca di pantaloncini non restituisce capris.

**felpa** ![selettore unidirezionale](assets/btn-one-way.png) felpa con cappuccio
**pantaloni** ![Selettore unidirezionale](assets/btn-one-way.png) capri ![Selettore unidirezionale multiplo](assets/btn-multiple-one-way.png) vitello-lunghezza-pantaloni ![Selettore unidirezionale multiplo](assets/btn-multiple-one-way.png) pedinatori

## Best practice

Per ottenere il massimo dai sinonimi [!DNL Live Search], tieni presente le seguenti best practice.

### Evita le &quot;parole non significative&quot;

[!DNL Live Search] esclude i comuni termini inglesi &quot;stop words&quot; dai sinonimi, ad esempio:

a, an e sono, come, at, be, ma, per, se, in, into, is, no, no, di, su, o, tale, il, loro, allora, là, questi, loro, questo, a, era, volontà, con

Le parole di arresto non rendono i sinonimi più significativi, ma aumentano la quantità di dati da elaborare.

### Usa singole parole

Se un sinonimo contiene più parole, lo spazio vuoto tra le parole fa sì che vengano trattate come sinonimi separati. Ad esempio, se definisci &quot;pezzo di tempo&quot; come sinonimo di &quot;orologio&quot;, le parole &quot;tempo&quot; e &quot;pezzo&quot; vengono trattate come sinonimi separati.

### Uso del singolare e del plurale

Non è necessario definire sia la forma singolare che quella plurale di una parola come sinonimo. Se nel catalogo sono presenti una combinazione di termini singolari e plurali, la funzione Ricerca consente di trovare il set di prodotti corretto. Ad esempio, se utilizzi la parola &quot;pant&quot; nel nome del prodotto e un acquirente cerca &quot;pantaloni&quot;, viene restituito il set corretto di prodotti e la singola parola &quot;pant&quot; viene offerta come suggerimento. Il singolare termine &quot;pantaloni&quot; è spesso usato nell&#39;industria della moda e talvolta nel commercio al dettaglio, anche se la forma plurale &quot;pantaloni&quot; è più comunemente usata in alcune aree. (La parola &quot;pantalone&quot; tecnicamente si riferisce alla parte di un indumento che copre una gamba, ed è per questo che hai bisogno di un &quot;paio di pantaloni&quot; per coprire entrambe le gambe.)

### Coerenza

Coerenza con il modo in cui la terminologia viene utilizzata nel catalogo. Tieni presente che potrebbero esserci differenze regionali nell’utilizzo e a volte differenze all’interno di un settore.
