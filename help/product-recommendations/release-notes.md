---
title: Note sulla versione [!DNL Product Recommendations]
description: Informazioni aggiornate sulla versione di  [!DNL Product Recommendations]  da Adobe Commerce.
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: 0d69d893d616a5e75ee264ebc652f3793a359486
workflow-type: tm+mt
source-wordcount: '1703'
ht-degree: 0%

---

# Note sulla versione [!DNL Product Recommendations]

Le note sulla versione contengono aggiornamenti ai seguenti [!DNL Product Recommendations] moduli:

* [!DNL Product Recommendations] metapackage: `magento/product-recommendations`
* Supporto di Page Builder nel modulo [!DNL Product Recommendations] (facoltativo): `magento/module-page-builder-product-recommendations`
* Supporto del tipo di consiglio per similarità visiva per il modulo [!DNL Product Recommendations] (facoltativo): `magento/module-visual-product-recommendations`

È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.
Le note sulla versione includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti

Per [informazioni sul supporto del prodotto](https://experienceleague.adobe.com/it/docs/commerce-operations/release/product-availability), consulta la documentazione per gli sviluppatori.

## Aggiornamenti dei servizi in hosting

Queste note descrivono aggiornamenti o problemi noti pubblicati o rilevati al di fuori di una versione con versione o miglioramenti al servizio ospitato.

_31 gennaio 2025_

![Nuovo](../assets/new.svg) Nell&#39;ambiente di test è presente un nuovo criterio di conservazione dei dati per i dati del catalogo non interrogati. [Ulteriori informazioni](overview.md#catalog-data-retention-policy).

_28 giugno 2024_

![Bug](../assets/bug.svg) I prodotti aggiunti al carrello da un&#39;unità [!DNL Product Recommendations] nella pagina del carrello non vengono rimossi dall&#39;elenco dei prodotti consigliati quando la pagina del carrello viene ricaricata.
![Bug](../assets/bug.svg) I prodotti rimossi dal carrello continuano a persistere nell&#39;array `cartSkus` fino al ricaricamento della pagina del carrello.

_18 luglio 2023_

![New](../assets/new.svg) [!DNL Product Recommendations] ora dispone di una query GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/).

_25 aprile 2023_

I clienti di ![New](../assets/new.svg) [!DNL Product Recommendations] ora possono usufruire dell&#39;indicizzazione dei prezzi di [SaaS](../price-index/price-indexing.md).

## Versione principale corrente

### 6.2.1 di magento/product-recommendations

_14 luglio 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) apportati miglioramenti al pannello [consigli di anteprima](./create.md#preview-recommendations).

### Versioni precedenti

### 6.2.0 di magento/product-recommendations

_4 aprile 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) ha aggiornato gli URL CDN per `recommendations-admin-ui` al dominio `adobe.io`.

### 6.1.0 di magento/product-recommendations

_11 marzo 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunto supporto PHP 8.4.

### 6.0.3 di magento/product-recommendations

_6 novembre 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale il [filtro categoria](filters.md#category) includeva categorie non appartenenti allo storeview corrente.
![Correzione](../assets/fix.svg) è stato risolto un problema di dipendenza nel metapackage `magento/product-recommendations`.

### 6.0.2 di magento/product-recommendations

_9 maggio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) è stato risolto un problema per cui facendo clic sul pulsante **[!DNL Add to Cart]** su un prodotto semplice all&#39;interno di un&#39;unità di Consigli di prodotto, l&#39;acquirente veniva reindirizzato alla home page anziché rimanere nella pagina corrente.
![Bug](../assets/bug.svg) Si è verificato un errore di convalida causato dall&#39;elemento `referenceBlock` nel file XML `ProductRecommendations Layout`.

### 6.0.1 di magento/product-recommendations

_19 marzo 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunto supporto PHP 8.3.

### 6.0.0 di magento/product-recommendations

_22 febbraio 2024_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![](../assets/new.svg) Nuovo Il [!DNL Catalog Sync Dashboard] è ora il [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-dashboard)file . Questo dashboard rinnovato fornisce informazioni dettagliate sui flussi di dati per [!DNL Product Recommendations], [!DNL Live Search], e [!DNL Catalog Service].
![Correzione](../assets/fix.svg) È stato risolto un problema che causava errori di estrazione per [!DNL Product Recommendations].

+++5.0.0 e versioni precedenti

### 5.0.1 di Magento/product-recommendations

_15 settembre 2023_

[!BADGE Versioni supportate]{type=Informative tooltip="Supportato"} Adobe Systems Commerce 2.4.4 e successive

![](../assets/new.svg) Nuovo Aggiunti nuovi moduli per supportare Saas [Price Indexer](../price-index/price-indexing.md).
![](../assets/new.svg) Nuovo Sono stati aggiunti nuovi moduli di esportazione dei dati per supportare l&#39;esportazione di più tipi di prodotti, inclusi prodotti in bundle e carte regalo.
![Correzione](../assets/fix.svg) Le dimensioni della tabella dei feed Prodotti e Prezzi sono state notevolmente ridotte. `catalog_data_exporter_products` Tables e `catalog_data_exporter_product_prices` dovrebbe vedere una sostanziale riduzione delle dimensioni.

#### Limitazioni note

* Il `websiteCode` valore viene restituito in modo errato se contiene un carattere di sottolineatura (_).

### 5.0.0 di magento/product-recommendations

_20 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) [!DNL Product Recommendations] aggiornato per supportare Adobe Commerce 2.4.6.
![Nuovo](../assets/new.svg) Questa è una versione principale. [Modifica](install-configure.md#update) il file radice `composer.json` del progetto.
![Nuovo](../assets/new.svg) [!DNL Product Recommendations] ora supporta le funzionalità complete di [Inventory management](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/introduction) in Commerce (in precedenza noto come inventario Multi-Source o MSI). Per abilitare il supporto completo, è necessario [aggiornare](install-configure.md#update) il modulo di dipendenza `commerce-data-export` alla versione 102.2.0+.

### 4.0.1 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) In precedenza, [!DNL Product Recommendations] mostrava un errore quando la valuta di visualizzazione veniva cambiata in una valuta non predefinita. Il cambio delle valute ora funziona correttamente.

### 4.0.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunti [indicatori di preparazione](create.md) per aiutarti a visualizzare l&#39;avanzamento della formazione di ciascun tipo di consiglio.
![Nuovo](../assets/new.svg) Questa è una versione principale. [Modifica](install-configure.md#update) il file radice `composer.json` del progetto. Questa versione richiede inoltre di fornire due chiavi API durante l&#39;installazione e la configurazione di [!DNL Product Recommendations]: [una chiave di produzione e una chiave sandbox](../landing/saas.md).

#### Limitazioni note

* Il valore `websiteCode` non viene restituito correttamente se contiene un carattere di sottolineatura (_).

### 3.3.7 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) aggiunto supporto PHP 8.1
![Nuovo](../assets/new.svg) È stato migliorato il ridimensionamento delle immagini in modo che vengano gestite in modo più coerente nel modello di visualizzazione di riferimento

### 3.3.6 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![New](../assets/new.svg) ha ottimizzato il metapacchetto [!DNL Product Recommendations] elencando esplicitamente le dipendenze

### 3.3.5 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) aggiunto [Supporto B2B](onboarding.md#b2bsupport) in [!DNL Product Recommendations]
![Nuovo](../assets/new.svg) Aggiunti nuovi feed a [sincronizza dati catalogo](https://experienceleague.adobe.com/it/docs/commerce/user-guides/data-services/catalog-sync) in Commerce Services tramite la riga di comando

### 3.3.3 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) aggiunti nuovi [tipi di consigli](type.md): Conversione (da vista a carrello), Conversione (da vista a acquisto) e Visualizzato di recente. Questi nuovi tipi di consigli sono disponibili nel modulo `magento/product-recommendations` 3.2.2 e versioni successive.
![Correzione](../assets/fix.svg) è stato risolto un problema che causava il blocco errato di un cookie da parte di Fastly Web Application Firewall (WAF)
![Correzione](../assets/fix.svg) è stato risolto un problema che impediva la visualizzazione dei prodotti assegnati alla visualizzazione store non predefinita nel pannello _Anteprima prodotto Recommendations_ durante la creazione di un consiglio per quella visualizzazione store specifica
![Correzione](../assets/fix.svg) è stato corretto un problema a causa del quale alcuni nomi di unità di consigli in Page Builder impedivano la visualizzazione dell&#39;unità di consigli nella vetrina

### 3.3.2 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) è stata corretta una dipendenza mancante per il supporto B2B

### 3.3.1 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) è stato aggiunto il supporto per i prezzi dei gruppi di clienti B2B. Quando imposti un [filtro prezzi](filters.md) su un&#39;unità di consigli, i clienti B2B che hanno effettuato l&#39;accesso visualizzano i prezzi del gruppo di clienti impostati per i prodotti visualizzati.

### 3.3.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) è stato aggiunto il supporto per Adobe Client Data Layer per standardizzare la raccolta di dati comportamentali tra le funzioni e i servizi di Adobe Commerce. Per ulteriori informazioni, consulta il [readme](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md).

### 3.2.6 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) è stato corretto un errore modale di JavaScript
![Correzione](../assets/fix.svg) è stato risolto un problema che causava il blocco errato di un cookie da parte di Fastly Web Application Firewall (WAF)

### 3.2.5 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) ha rinominato i servizi Magento in [Servizi Commerce](https://experienceleague.adobe.com/it/docs/commerce/user-guides/integration-services/saas) e ne ha migliorato l&#39;usabilità in Amministrazione

### 3.2.4 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) è stato corretto l&#39;errore &quot;Impossibile recuperare i dati delle opzioni di prodotto configurabili&quot; durante l&#39;indicizzazione degli attributi di prodotto

### 3.2.3 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) dell&#39;errore &quot;Impossibile recuperare i dati delle opzioni del prodotto configurabili&quot; durante la sincronizzazione del catalogo
![Correzione](../assets/fix.svg) È stato risolto un problema a causa del quale il codice store non veniva impostato correttamente quando si attivava la configurazione &quot;Aggiungi codice store all URL&quot;
![Correzione](../assets/fix.svg) Rilevamento migliorato delle modifiche alla configurazione del Pannello di amministrazione per garantire che si riflettano nei dati di sincronizzazione catalogo

### 3.2.2 di Magento/Raccomandazioni di prodotto

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Systems Commerce versioni 2.4.x e successive

![](../assets/new.svg) Nuovo Aggiunta la possibilità di [visualizzare in anteprima consiglio risultati](create.md) al momento della creazione. Ciò potrebbe richiedere l&#39;aggiornamento del modulo alla versione più recente.
![](../assets/new.svg) Nuovo Aggiunta la possibilità di [monitorare e gestire](https://experienceleague.adobe.com/it/docs/commerce/user-guides/data-services/catalog-sync) il processo di Sincronizzazione catalogo dall&#39;amministratore.
![](../assets/new.svg) Nuovo Sono stati aggiunti [filtri](filters.md) per controllare quali prodotti vengono visualizzati nei consigli.
![](../assets/new.svg) Nuovo Aggiunto il [tipo di consiglio Somiglianza](type.md#visualsim) visiva.

### 1.2.1 di magento/module-page-builder-product-recommendations per Pagina Builder

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Systems Commerce versioni 2.4.x e successive

![](../assets/new.svg) Nuovo Aggiunto supporto per la versione 3.2.0+ del `magento/product-recommendations` modulo

### 3.1.0 di Magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Systems Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) Aggiunta la possibilità di [risincronizzare](https://experienceleague.adobe.com/it/docs/commerce/user-guides/data-services/catalog-sync) il catalogo con i servizi SaaS tramite riga di comando.
![Nuovo](../assets/new.svg) aggiunto supporto per i prefissi delle tabelle di database
![Correzione](../assets/fix.svg) Supporto PHP 7.1 rimosso

### 3.0.8 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale gli eventi venivano inviati per la raccolta dati prima che il modulo fosse configurato, causando traffico non valido

### 3.0.6 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) **(Beta)** Include il supporto per il nuovo tipo di consiglio [Somiglianza visiva](type.md#visualsim).

### 1.0.0 di magento/module-visual-product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) **(Beta)** [Somiglianza visiva](type.md#visualsim). Con il tipo di consiglio _Somiglianza visiva_, puoi distribuire un&#39;unità di consigli nella pagina dei dettagli del prodotto che mostra prodotti visivamente simili al prodotto visualizzato.

### 3.0.5 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) è stato corretto l&#39;errore &quot;Impossibile recuperare i dati delle opzioni prodotto&quot; che poteva verificarsi durante l&#39;esportazione del catalogo.
![Correzione](../assets/fix.svg) Il simbolo di valuta nella colonna _Entrate_ del dashboard _[!DNL Product Recommendations]_&#x200B;ora riflette correttamente la valuta di base configurata.

### 3.0.4 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) aggiunta del supporto per Adobe Commerce 2.4.0

### 3.0.3 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Correzione](../assets/fix.svg) implementazione migliorata del simbolo nel modello storefront

### 1.0.4 di magento/module-page-builder-consigli-di-prodotto per Page Builder

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) aggiunto il nome del consiglio di prodotto durante la modifica del tipo di contenuto Page Builder

### 3.0.2 magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) Aggiunta di una colonna di stato nella griglia durante la selezione delle unità per i consigli in Page Builder
![Correzione](../assets/fix.svg) è stato risolto un problema relativo a protocolli http/https non corretti negli URL di prodotti e immagini

### 3.0.1 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

Questa è una versione principale. [Modifica](install-configure.md#update) il file compositore.json principale del progetto.

![Nuovo](../assets/new.svg) Recupero di [!DNL Product Recommendations] da spazi dati SaaS alternativi. Ciò ti consente di utilizzare [!DNL Product Recommendations] calcolato nell&#39;ambiente del prodotto in altri ambienti non di produzione. [Il passaggio da uno spazio dati SaaS](settings.md) descrive ulteriormente questa funzione.

![Correzione](../assets/fix.svg) è stato risolto un problema che impediva l&#39;estrazione per gli acquirenti che utilizzano uBlock Origin.
![Correzione](../assets/fix.svg) è stato risolto un problema che causava l&#39;invio di eventi aggiuntivi al carrello estranei

### 1.0.3 di magento/module-page-builder-consigli-di-prodotto per Page Builder

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

Supporto di ![New](../assets/new.svg) Page Builder. Con l’integrazione di Page Builder, puoi posizionare in modo accurato e dettagliato le unità di consigli in qualsiasi posizione arbitraria su contenuti creati da Page Builder. Puoi anche assegnare uno stile ai titoli e alle unità di consigli. Per ulteriori informazioni, vai a [Page Builder](https://experienceleague.adobe.com/it/docs/commerce-admin/page-builder/add-content/recommendations).

### 2.0.0 di magento/product-recommendations

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.x e successive

![Nuovo](../assets/new.svg) rilascio di disponibilità generale.

+++

## Documentazione

Per ulteriori informazioni sullo sviluppo di [!DNL Product Recommendations] e [!DNL Product Recommendations]:

* [Guida utente](overview.md)
* [Documentazione per sviluppatori](https://experienceleague.adobe.com/it/docs/commerce/product-recommendations/developer/development-overview)
