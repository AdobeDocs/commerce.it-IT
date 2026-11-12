---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
Le origini del catalogo rappresentano ambiti autorevoli di prodotti, attributi e categorie. In genere vengono mappati sui limiti della lingua, del pubblico o del sistema di origine e determinano il comportamento di ricerca, filtro e ordinamento.

## Origini del catalogo e concetti correlati

Il modo in cui le origini del catalogo si relazionano ad altri concetti di Merchandising Services consente di modellare correttamente i dati:

* **Origine catalogo**: il contesto dei dati sottostante che fornisce le informazioni sul prodotto. Un&#39;origine di catalogo rappresenta in genere una lingua (ad esempio, `en-US`, `fr-CA`) o un contesto di dati fornito da un sistema esterno come un PIM o un ERP. Prodotti, metadati di attributi e categorie sono tutti con ambito per origine di catalogo. Un’origine catalogo definisce l’origine dei dati grezzi del catalogo e il loro effetto sull’individuazione del prodotto (risultati della ricerca, filtraggio e comportamento di ordinamento).

* **[Visualizzazione catalogo](/help/optimizer/setup/catalog-view.md)**: visualizzazione configurata del catalogo per esigenze aziendali specifiche. Una vista catalogo seleziona le origini del catalogo (o le impostazioni locali), applica [criteri](/help/optimizer/setup/policies.md) per filtrare la visibilità dei prodotti e associa [listini prezzi](/help/optimizer/setup/pricebooks.md) alla vista. Un&#39;unica origine di catalogo può alimentare molte visualizzazioni di catalogo (ad esempio, un&#39;origine `en-US` con visualizzazioni di catalogo separate per marchi o aree geografiche diversi). Considera una visualizzazione catalogo come *il modo* in cui esponi tali dati a una vetrina, un canale o un pubblico.

* **[Livello catalogo](catalog-layer.md)**: livello applicato ai dati del catalogo di base per modificare gli attributi del prodotto (nome, descrizione, immagini, metadati) senza modificare i dati di origine. Utilizzare i livelli del catalogo quando le differenze devono influire solo sulla visualizzazione della vetrina, non sul rilevamento del prodotto.

## Compilazione delle origini del catalogo

Le origini del catalogo vengono compilate tramite l’acquisizione dei dati del catalogo. Il modo in cui vengono forniti i dati dipende dall’implementazione:

- **Adobe Commerce as a Cloud Service con CCDM**: la sincronizzazione nativa fornisce i dati del catalogo da Commerce Foundation. Gestisci i prodotti sottostanti e la configurazione della visualizzazione archivio in Commerce Foundation e monitora la sincronizzazione nell&#39;area di lavoro [Sincronizzazione dati](data-sync.md). Non è richiesta alcuna integrazione separata di API di acquisizione dati.
- **Adobe Commerce Optimizer con backend di terze parti**. L&#39;integrazione fornisce prodotti e informazioni sull&#39;origine del catalogo tramite [API di acquisizione dati](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).


## Regole e limitazioni

* Un’origine catalogo viene creata quando i dati del catalogo per una nuova lingua o un nuovo sistema di origine vengono ricevuti per la prima volta dal livello dati di Merchandising Services.
* L’univocità del prodotto è determinata da SKU + origine catalogo.
* Gli acquirenti non accedono direttamente alle origini del catalogo. I dati del catalogo sono esposti alla vetrina tramite [visualizzazioni catalogo](catalog-view.md).

## Linee guida per la modellazione

Per pianificare la struttura del catalogo, attenersi alle istruzioni riportate di seguito. Per Adobe Commerce as a Cloud Service con CCDM, gestisci la configurazione sottostante in Commerce Foundation anziché creare origini di catalogo tramite un’integrazione di acquisizione separata.

* Utilizza un’origine catalogo separata per ogni lingua del catalogo.
* Utilizza origini di catalogo separate quando le differenze di prodotti e attributi devono influenzare il comportamento di ricerca, filtro o ordinamento, ad esempio impostazioni diverse di ricercabilità o filtrabilità.
* Utilizza [livelli catalogo](catalog-layer.md) quando le differenze di prodotti e attributi devono influire sulla presentazione dei prodotti senza modificare il comportamento di ricerca, filtro o ordinamento.

>[!MORELIKETHIS]
>
> * [Visualizzazioni catalogo](catalog-view.md) - Configura visualizzazioni filtrate con prezzo sopra un&#39;origine catalogo
> * [Livelli catalogo](catalog-layer.md) - Modificare la presentazione del prodotto senza modificare i dati di origine
> * [Criteri](policies.md) - Creare filtri basati su attributi per le visualizzazioni catalogo
> * [Listini prezzi](/help/optimizer/setup/pricebooks.md) - Gestisce le strutture di determinazione prezzi per segmenti cliente diversi
> * [Chiavi di accesso limitate](restricted-access-keys.md) - Proteggere una visualizzazione catalogo con autenticazione token firmato
