---
title: Sinonimo Di Migliori Pratiche
description: Scopri le best practice per l’implementazione di sinonimi nel tuo store.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 54b300ed89f830c2fe5258ec889302a59decd59f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Sinonimo Di Migliori Pratiche

Di seguito è riportato un elenco di best practice per la creazione di sinonimi.

- [!DNL Adobe Commerce Optimizer] gestisce gli errori ortografici per impostazione predefinita. È possibile impostare sinonimi per includere parole che gli acquirenti potrebbero utilizzare, diverse dalle parole specificate nel catalogo. Non si vuole perdere una vendita perché qualcuno sta cercando un &quot;divano&quot;, mentre il vostro prodotto è elencato come un &quot;divano&quot;. È possibile acquisire un&#39;ampia gamma di termini di ricerca immettendo tutte le possibili parole che i clienti potrebbero utilizzare per trovare i prodotti. È possibile [impostare i sinonimi in un modo o in due](add.md#step-2-define-the-synonym-by-type) per migliorare i risultati.

- Mappa i nomi dei marchi e le abbreviazioni ai loro nomi completi, ad esempio &quot;HP&quot; in &quot;Hewlett-Packard&quot; e i soprannomi di prodotto comuni, ad esempio &quot;iPhone&quot; in &quot;Apple iPhone&quot;.

- Includere un gergo specifico per il settore e termini che gli acquirenti potrebbero utilizzare in modo intercambiabile, ad esempio &quot;scarpe da ginnastica&quot; e &quot;scarpe da corsa&quot;.

- Aggiorna regolarmente l’elenco dei sinonimi in base alle nuove tendenze di ricerca, alle aggiunte di prodotti e al comportamento degli acquirenti.

- Verifica l’efficacia delle mappature dei sinonimi analizzando i risultati della ricerca e il feedback degli acquirenti. Affina le mappature per migliorare precisione e rilevanza.

- Evita l’utilizzo di parole non significative, in quanto non rendono i sinonimi più significativi, ma aumentano la quantità di dati che devono essere elaborati. [!DNL Adobe Commerce Optimizer] esclude i comuni termini inglesi &quot;stop words&quot; dai sinonimi, ad esempio:

  a, an e sono, come, at, be, ma, per, se, in, into, is, no, no, di, su, o, tale, il, loro, allora, là, questi, loro, questo, a, era, volontà, con

- Non è necessario definire sia la forma singolare che quella plurale di una parola come sinonimo. Se nel catalogo sono presenti una combinazione di termini singolari e plurali, la funzione Ricerca consente di trovare il set di prodotti corretto. Ad esempio, se utilizzi la parola &quot;pant&quot; nel nome del prodotto e un acquirente cerca &quot;pantaloni&quot;, viene restituito il set corretto di prodotti e la singola parola &quot;pant&quot; viene offerta come suggerimento. Il singolare termine &quot;pantaloni&quot; è spesso usato nell&#39;industria della moda e talvolta nel commercio al dettaglio, anche se la forma plurale &quot;pantaloni&quot; è più comunemente usata in alcune aree. (La parola &quot;pantalone&quot; tecnicamente si riferisce alla parte di un indumento che copre una gamba, ed è per questo che hai bisogno di un &quot;paio di pantaloni&quot; per coprire entrambe le gambe.)

- Coerenza con il modo in cui la terminologia viene utilizzata nel catalogo. Tieni presente che potrebbero esserci differenze regionali nell’utilizzo e a volte differenze all’interno di un settore.
