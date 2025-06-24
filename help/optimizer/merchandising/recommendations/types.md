---
title: Tipi di consigli
description: Scopri i consigli che puoi distribuire in varie pagine del sito.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '1295'
ht-degree: 0%

---

# Tipi di consigli

Adobe Commerce Optimizer fornisce una vasta serie di consigli che puoi distribuire su varie pagine del sito. Tutti i tipi di consigli sono basati sui dati. Sono basati su dati comportamentali, dati di attributi di prodotto e metriche. Per facilitare la consultazione, i tipi di consigli sono raggruppati come segue:

- [Personalizzato](#personalized)
- [Cross-selling e up-sell](#crossup)
- [Popolarità](#popularity)
- [Prestazioni elevate](#highperf)

>[!NOTE]
>
>Per ulteriori informazioni sugli eventi descritti in questo articolo, vedi [eventi](../../setup/events/overview.md).

## Personalizzato {#personalized}

Questi tipi di consigli consigliano prodotti in base alla cronologia comportamentale dell’acquirente specifica sul tuo sito. Ad esempio, se un acquirente cerca una giacca in precedenza o ne ha acquistata una sul tuo sito, questi consigli in pratica rilevano da dove hanno lasciato e consigliano altre giacche o prodotti simili.

| Tipo | Descrizione |
|---|---|
| Consigliato per te | Consiglia i prodotti in base al comportamento corrente e precedente di ogni cliente. Mostra consigli molto rilevanti in base alla cronologia di navigazione e di acquisto del cliente. Questo tipo di consiglio è valido nella home page in cui la maggior parte degli acquirenti inizia il percorso su un sito. Per i nuovi acquirenti sul tuo sito che non hanno generato alcun segnale per personalizzare la loro esperienza, Adobe Commerce mostra i prodotti in base al tipo di consiglio Più visualizzato. Tuttavia, quando il cliente inizia a interagire con i prodotti sul sito, i prodotti consigliati si adattano in tempo reale al loro comportamento.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria <br/><br/>**Etichette consigliate:**<br/> - Solo per te<br/>- Consigliato per te<br/>- Ispirato dalle tendenze di acquisto |
| Visualizzato di recente | Visualizza gli ultimi prodotti visualizzati dall’acquirente, in base alla cronologia del browser. Eventuali prodotti eliminati vengono rimossi dall’unità di consigli. L’unità di consigli non viene visualizzata se non è presente alcuna cronologia del browser o se la cronologia non è sufficiente quando vengono applicate le regole del filtro. Se i risultati contengono meno prodotti di quelli configurati, l’unità di consigli visualizza solo i prodotti restituiti.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/>- Visualizzato di recente<br/>- Dai un&#39;altra occhiata |

## Cross-selling e up-sell {#crossup}

Questi tipi di consigli sono orientati alla social-proof per aiutare gli acquirenti a trovare ciò che piace ad altri o orientati ai prodotti per aiutarli a trovare altri prodotti simili. I prodotti consigliati spesso integrano il prodotto selezionato.

>[!NOTE]
>
>I tipi di consigli &quot;visualizzato questo, visualizzato quello&quot;, &quot;visualizzato questo, acquistato quello&quot; e &quot;comprato questo, comprato che&quot; non utilizzano una metrica di occorrenza semplice, ma piuttosto un algoritmo di filtro collaborativo più sofisticato che cerca *somiglianze interessanti* che non sono distorti verso i prodotti più popolari. I dati utilizzati per informare questi tipi di consigli si basano sul comportamento aggregato dell’acquirente derivante da più sessioni sul sito. I dati non si basano sul comportamento dell’acquirente derivato da una singola occorrenza nella sessione sul sito. Questi tipi di consigli aiutano gli acquirenti a trovare i prodotti adiacenti che potrebbero non essere evidenti da abbinare al prodotto attualmente visualizzato.

| Tipo | Descrizione |
|---|---|
| Ha visualizzato questo, ha visualizzato quello | Consiglia i prodotti che gli acquirenti visualizzano con maggiore frequenza rispetto al prodotto attualmente visualizzato.<br/><br/>**Dove usato:**<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/>- Sono stati visualizzati anche i clienti che hanno visualizzato il prodotto (PDP) |
| Ho visto questo, ho comprato quello | Consiglia i prodotti che gli acquirenti tendono ad acquistare in modo sproporzionato più spesso dopo aver visualizzato il prodotto corrente. Questo tipo aiuta a guidare gli acquirenti a scoprire prodotti che altrimenti potrebbero non aver notato.<br/><br/>**Dove usato:**<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette suggerite:**<br/>- Clienti che hanno visualizzato questo acquisto finale<br/>- Clienti che hanno acquistato<br/>- Cosa acquistano gli altri dopo aver visualizzato questo prodotto? |
| Ho comprato questo e quello | Consiglia i prodotti che gli acquirenti acquistano con maggiore frequenza rispetto al prodotto attualmente visualizzato. Questo tipo mostra prodotti molto rilevanti che gli acquirenti possono aggiungere al carrello aggregando ciò che altri acquirenti hanno acquistato con il prodotto corrente.<br/><br/>**Dove usato:**<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/>- Ottieni tutto il necessario<br/>- Non dimenticare queste<br/>- Spesso acquistate insieme |
| Altri argomenti correlati | Consiglia prodotti basati su metadati simili, ad esempio nome, descrizione, assegnazione di categorie e attributi. Valutando gli attributi dei prodotti visualizzati, questo tipo consiglia prodotti simili nella stessa categoria. Ad esempio, se un acquirente sta navigando tra i tappetini da yoga, si consigliano altri prodotti nella categoria attrezzatura. Poiché questo tipo di consiglio non distingue i sessi, non è consigliato per abbigliamento, moda o altri verticali specifici per genere.<br/><br/>**Dove usato:**<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/> - Altri prodotti come questo<br/>- Simile a questo |

## Popolarità {#popularity}

Questi tipi di consigli consigliano prodotti che sono i più popolari o di tendenza negli ultimi sette giorni.

| Tipo | Descrizione |
|---|---|
| Articoli più visualizzati | Consiglia i prodotti più visualizzati contando il numero di sessioni in cui si è verificata un’azione di visualizzazione negli ultimi sette giorni.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/>- Più popolari<br/>- Di tendenza<br/>- Popolari al momento<br/>- Recentemente popolari<br/>- Prodotti popolari ispirati a questo prodotto (PDP)<br/>- Più venduti |
| Più acquistati | Consiglia i prodotti acquistati più di frequente dagli acquirenti negli ultimi sette giorni.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/> - Più popolari<br/>- Di tendenza<br/>- Popolari al momento<br/>- Recentemente popolari<br/>- Prodotti popolari ispirati a questo prodotto (PDP)<br/>- Più venduti |
| Più aggiunti al carrello | Consiglia i prodotti aggiunti più frequentemente ai carrelli dagli acquirenti negli ultimi sette giorni. Questo tipo di consiglio può essere utilizzato su tutte le pagine.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/> - Più popolari<br/>- Di tendenza<br/>- Popolari al momento<br/>- Recentemente popolari<br/>- Prodotti popolari ispirati a questo prodotto (PDP)<br/>- Più venduti |
| Di tendenza | Consiglia i prodotti in base al recente momento di popolarità di un prodotto nel tuo sito.<br/><br/>Adobe Sensei aggrega i dati di navigazione e di acquisto nel tuo sito per determinare e classificare i prodotti più popolari tra gli acquirenti. Dato che Trending analizza il recente slancio dei prodotti, è un tipo di raccomandazione efficace per i cataloghi che hanno un fatturato elevato. Se il catalogo è più statico, potrebbe non essere utile a meno che i modelli di acquisto del pubblico non siano altamente variabili.<br/><br/>Se utilizzato nella home page, Trending consiglia prodotti che sono stati utilizzati di recente nell&#39;intero sito. La tendenza non mostra i prodotti che sono costantemente popolari, ma piuttosto quelli che sono diventati di recente popolari. Ad esempio, in presenza di una campagna di marketing e-mail che promuove determinati prodotti, l’aumento di popolarità generato dall’e-mail aumenta la probabilità che i prodotti promossi siano classificati come di tendenza.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/>- Di tendenza<br/>- Di tendenza attuale<br/>- Di tendenza recente<br/>- Prodotti caldi<br/>- Prodotti correlati di tendenza (PDP) |

## Prestazioni elevate {#highperf}

Questi tipi di consigli consigliano prodotti con le prestazioni migliori in base a criteri di successo come l’aggiunta al carrello o i tassi di conversione.

| Tipo | Descrizione |
|---|---|
| Visualizza per conversione acquisto | Consiglia prodotti con il più alto tasso di conversione visualizzazione-acquisto. Di tutte le sessioni cliente che hanno registrato una visualizzazione di prodotto, qual è la proporzione che alla fine ha registrato un acquisto da parte del cliente.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/> -Articoli più venduti<br/>- Prodotti popolari<br/>- Potresti essere interessato a |
| Conversione da Vista a Carrello | Consiglia i prodotti con il più alto tasso di conversione da vista a carrello. Di tutte le sessioni cliente che hanno registrato una visualizzazione di prodotto, qual è la proporzione che alla fine ha registrato e aggiunto al carrello da parte del cliente.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/> - Articoli più venduti<br/>- Prodotti più popolari<br/>- Potresti essere interessato a |
| Più acquistati | Spesso definito &quot;Più venduti&quot;, questo tipo di consiglio conta il numero di sessioni in cui si è verificata un’azione di ordine negli ultimi sette giorni. Questo tipo di consiglio può essere utilizzato su tutte le pagine.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/> - Più popolari<br/>- Di tendenza<br/>- Popolari al momento<br/>- Recentemente popolari<br/>- Prodotti popolari ispirati a questo prodotto (PDP)<br/>- Più venduti |
| Più aggiunti al carrello | Consiglia i prodotti aggiunti più frequentemente ai carrelli dagli acquirenti negli ultimi sette giorni. Questo tipo di consiglio può essere utilizzato su tutte le pagine.<br/><br/>**Dove usato:**<br/>- Home page<br/>- Categoria<br/>- Dettagli prodotto<br/>- Carrello<br/>- Conferma <br/><br/>**Etichette consigliate:**<br/> - Più popolari<br/>- Di tendenza<br/>- Popolari al momento<br/>- Recentemente popolari<br/>- Prodotti popolari ispirati a questo prodotto (PDP)<br/>- Più venduti |
