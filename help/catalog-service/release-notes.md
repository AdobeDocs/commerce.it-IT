---
title: Note sulla versione [!DNL Catalog Service]
description: Informazioni aggiornate sulla versione di  [!DNL Catalog Service]  per Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 93adab667d1d8ed40c9d5668db376493bd8ae684
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Note sulla versione [!DNL Catalog Service]

Queste note sulla versione descrivono le versioni più recenti di [!DNL Catalog Service].
È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.
Gli aggiornamenti includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti

## Versione principale corrente

### Versione V1.26

_22 ottobre 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Lo schema di GraphQL ora include l&#39;attributo `lastModifiedAt` nelle informazioni sul prodotto. Questa marca temporale precisa consente ai clienti di garantire che le sitemap riflettano accuratamente gli aggiornamenti più recenti dei loro prodotti. Aiuta anche i motori di ricerca come Google a determinare quando è necessaria la reindicizzazione, ottimizzando il processo di ricerca per indicizzazione e impedendo problemi relativi alle date aggressive dell’ultima modifica utilizzate quando non sono disponibili informazioni precise. <!--DATA-6209-->

## Versioni precedenti

+++ Versioni precedenti

### Versione V1.23

_22 agosto 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) È ora possibile recuperare le informazioni sul prodotto senza i dati di sostituzione (prezzi) del prodotto. Nelle versioni precedenti, queste query restituivano il seguente errore:
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### Versione V1.22

_13 agosto 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) è stato aggiunto il supporto per recuperare tutte le varianti per SKU prodotto. Vedi il [riferimento API di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Versione V1.22

_13 agosto 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) è stato aggiunto il supporto per recuperare tutte le varianti per SKU prodotto. Vedi il [riferimento API di Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Versione V1.19

_23 maggio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive


![Correzione](../assets/fix.svg) <!--DATA-5033-->Il flag `InStock` per i valori delle opzioni ora tiene conto dello stato `enabled` con ambito della variante prodotto.

![Correzione](../assets/fix.svg) <!--DATA-5888-->Aggiungere supporto per i prezzi dei prodotti che richiedono numeri elevati (fino a 16 cifre) e una maggiore precisione decimale (fino a 4 cifre decimali). Per applicare gli aggiornamenti della configurazione del prezzo al catalogo esistente, risincronizzare i dati del catalogo dal [dashboard di gestione dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) o utilizzando l&#39;[interfaccia della riga di comando di Adobe Commerce](../landing/catalog-sync.md#command-line-interface).

#### Limitazioni note

Le seguenti funzioni non sono ancora supportate:

* La dimensione massima per il payload degli attributi dinamici è di 9 MB.
* Il prezzo del prodotto del gruppo può essere calcolato con prezzi del prodotto semplici.
* In un array di immagini, solo la prima immagine contiene ruoli.

Risolvi le seguenti limitazioni utilizzando API Mesh e l’API Core di GraphQL:

* Prezzo minimo annunciato
* Prezzi a livelli
* Prodotti in bundle a prezzi fissi

Per dettagli ed esempi, consulta [Catalog Service e Mesh API](mesh.md)

### Versione V1.18

_11 aprile 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunto supporto per PHP 8.3.

![Nuovo](../assets/new.svg) Le query [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) e [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) ora restituiscono dati di opzioni personalizzabili per prodotti semplici e complessi.<!--DATA-5538-->

### Versione V1.17

_22 febbraio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=it) è ora disponibile. Questo dashboard rinnovato fornisce informazioni approfondite sui flussi di dati per [!DNL Product Recommendations], [!DNL Live Search] e [!DNL Catalog Service]. Il supporto per questa funzione è stato introdotto nella versione 3.1.0 del metapackage `catalog-service`.

### Versione V1.16

_13 febbraio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![I nuovi](../assets/new.svg) video di prodotto sono ora supportati dall&#39;API Catalog Service.
![Correzione](../assets/fix.svg) Le opzioni esaurite sono ora visualizzate nel widget PDP.

#### Limitazioni note

Queste funzioni non sono ancora supportate:

* La dimensione massima per il payload degli attributi dinamici è di 9 MB.
* Prezzo del prodotto di gruppo. Questo valore può essere calcolato con prezzi dei prodotti semplici.
* In un array di immagini, solo la prima immagine contiene ruoli.

Le seguenti limitazioni possono essere risolte utilizzando API Mesh e l’API core di GraphQL:

* Prezzo minimo annunciato
* [Prezzi a livelli](mesh.md)

### Versione V1.13

_12 ottobre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service supporta il flag `inStock` per le varianti di prodotto.
![Nuovo](../assets/new.svg) I campi `urlKey` e `externalId` sono stati aggiunti allo schema di GraphQL.
Sono ora supportati ![Nuovi](../assets/new.svg) prodotti scaricabili e gift card.

### Versione V1.12

_19 settembre 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora utilizza l&#39;indicizzazione dei prezzi SaaS [&#128279;](../price-index/price-indexing.md).

![Correzione](../assets/fix.svg) Questa versione contiene correzioni di bug e miglioramenti sul lato servizio.

### Versione V1.11

_18 luglio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora supporta la query GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) per i consigli di prodotto.

### Versione V1.10

_27 giugno 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) L&#39;API di Catalog Service ora supporta `related products`.

### Versione V1.7

_12 aprile 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![New](../assets/new.svg) Catalog Service ora ripulisce le varianti di prodotto eliminate.
![Correggi](../assets/fix.svg) Miglioramenti a livello di scalabilità e prestazioni dell&#39;infrastruttura.

### Versione V1.6

_28 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovi](../assets/new.svg) campioni aggiunti alla query [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nuovo](../assets/new.svg) Aggiunta la possibilità di ottenere `entityId` utilizzando [Mesh API](mesh.md).

### Versione V1.5

_6 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) Aggiunta funzionalità di [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL.
![Correzione](../assets/fix.svg) Prestazioni e scalabilità API migliorate.

### Versione V1.4

_7 febbraio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) Metapackage del servizio catalogo pubblicato per semplificare i passaggi dell&#39;installazione.
![Correggi](../assets/fix.svg) miglioramenti a livello di scalabilità e prestazioni dell&#39;API.

### Versione V1.3

_17 gennaio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) ha semplificato e migliorato l&#39;esperienza di onboarding.
![Nuovi](../assets/new.svg) nuovi endpoint sandbox del cliente sono disponibili per il test di pre-produzione.
![Nuovo](../assets/new.svg) supporto aggiunto per i prodotti virtuali.
![Correggi](../assets/fix.svg) miglioramenti a livello di scalabilità e prestazioni dell&#39;API.

### Versione V1.1

_18 novembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![New](../assets/new.svg) Catalog Service ora supporta [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) di Adobe.
![Correzione](../assets/fix.svg) Miglioramento della scalabilità API e delle prestazioni complessive.

### Versione V1.0

_4 ottobre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) ora supporta i prodotti raggruppati e raggruppati.
![Nuovo](../assets/new.svg) Aggiunte Override Di Visibilità B2B. È ora possibile cercare i prodotti e aggiungerli al carrello per gruppi di clienti specifici.
Il servizio ![Correzione](../assets/fix.svg) è ora più stabile e offre prestazioni migliorate.

### Versione 0.3 - Beta+

_12 settembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuove](../assets/new.svg) immagini per le varianti supportate: le immagini del prodotto vengono restituite in base alle opzioni selezionate
![Nuovi](../assets/new.svg) ruoli per supporto prezzi: consente solo ai membri di gruppi di clienti specifici di visualizzare il prezzo dei prodotti
![Correzione](../assets/fix.svg) Stabilità e prestazioni migliorate del servizio
![Nuovi](../assets/new.svg) aggiornamenti ricevuti quando i prodotti vengono eliminati dal catalogo

### Versione Beta

_9 agosto 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) Le query `products` e `refineProduct` restituiscono i dati seguenti:

* Attributi di prodotto predefiniti (di sistema).
* Attributi di prodotto dinamici e filtrali per ruolo (pagina di visualizzazione prodotto/pagina di elenco prodotti).
* Opzioni prodotto.
* Immagini dei prodotti e filtrale per ruolo (PDP/PLP).
* Un prezzo specifico per prodotti semplici e fasce di prezzo per prodotti configurabili.
* Prezzi e fasce di prezzo del gruppo di clienti. Restituiscono un prezzo predefinito di fallback sugli acquirenti senza un gruppo di clienti.
* Tipi di prodotto che utilizzano prezzi specifici per il cliente B2B.
