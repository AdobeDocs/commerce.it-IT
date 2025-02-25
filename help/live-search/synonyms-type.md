---
title: Tipi di sinonimi
description: I sinonimi unidirezionali [!DNL Live Search] consentono di espandere la definizione delle parole chiave.
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '581'
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

### Uso del singolare e del plurale

Non è necessario definire sia la forma singolare che quella plurale di una parola come sinonimo. Se nel catalogo sono presenti una combinazione di termini singolari e plurali, la funzione Ricerca consente di trovare il set di prodotti corretto. Ad esempio, se utilizzi la parola &quot;pant&quot; nel nome del prodotto e un acquirente cerca &quot;pantaloni&quot;, viene restituito il set corretto di prodotti e la singola parola &quot;pant&quot; viene offerta come suggerimento. Il singolare termine &quot;pantaloni&quot; è spesso usato nell&#39;industria della moda e talvolta nel commercio al dettaglio, anche se la forma plurale &quot;pantaloni&quot; è più comunemente usata in alcune aree. (La parola &quot;pantalone&quot; tecnicamente si riferisce alla parte di un indumento che copre una gamba, ed è per questo che hai bisogno di un &quot;paio di pantaloni&quot; per coprire entrambe le gambe.)

### Coerenza

Coerenza con il modo in cui la terminologia viene utilizzata nel catalogo. Tieni presente che potrebbero esserci differenze regionali nell’utilizzo e a volte differenze all’interno di un settore.

## Comportamento sinonimo di più parole

Per i sinonimi composti da più parole, Commerce considera il sinonimo come una frase. Ad esempio, se crei un sinonimo bidirezionale **tavolo da pranzo** ![Selettore bidirezionale](assets/btn-two-way.png) **tavolo da cucina** ![Selettore bidirezionale](assets/btn-two-way.png) **tavolo da pranzo**, Commerce eseguirà una ricerca in tutti i campi impostati come ricercabile per individuare l&#39;occorrenza di **tavolo da pranzo** o **tavolo da cucina** o **tavolo da pranzo**.

Se non viene creato alcun sinonimo e un acquirente cerca **la tabella della cucina**, Commerce cerca i termini ovunque nei campi ricercabili, anche tra campi diversi, ad esempio **la tabella** nel campo del nome e **la cucina** nella parola chiave meta.

Dopo aver creato un sinonimo, il comportamento di ricerca cambia per cercare la frase esatta **tabella cucina**. Questo potrebbe ridurre il numero di risultati, perché verranno visualizzati solo i prodotti con la frase esatta.

Se desideri cercare i termini separatamente come prima, puoi [creare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Se la domanda è sufficiente, Commerce prenderà in considerazione la possibilità di aggiungere questa funzionalità al prodotto in una versione futura.
