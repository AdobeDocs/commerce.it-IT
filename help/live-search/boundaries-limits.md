---
title: Limiti e limiti
description: Scopri i limiti e le limitazioni di  [!DNL Live Search]  per garantire che soddisfi le esigenze della tua azienda.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Limiti e limiti

Adobe Commerce offre diverse opzioni per la ricerca del sito. Rivedi i limiti e le limitazioni seguenti per garantire che [!DNL Live Search] e [!DNL Catalog Service] soddisfino le esigenze della tua azienda. Se hai bisogno di funzionalità di ricerca avanzate, ad esempio ricerca di contenuti, algoritmo BYOA (port-your-own-algorithm) o merchandising basato su attributi, considera una soluzione di ricerca di terze parti.

## Generale

- Il modulo [Ricerca avanzata](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) è disabilitato quando è installato [!DNL Live Search] e il collegamento Ricerca avanzata nel piè di pagina della vetrina è stato rimosso.
- [Il livello prezzi](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier) non è supportato nel campo [!DNL Live Search] e nel widget pagina elenco prodotti.
- I prezzi dei prodotti non includono l&#39;imposta sul valore aggiunto (IVA).
- La ricerca dei contenuti (pagine e blocchi CMS) non è supportata.
- Esiste un limite di 10.000 prodotti che possono essere impaginati. Anche se questo limite può essere aumentato, può influire sulle prestazioni. Assicurati di fornire modi significativi per filtrare i prodotti nel caso in cui una categoria o un risultato di ricerca abbia un numero elevato di prodotti, in modo che gli acquirenti non debbano utilizzare la paginazione profonda.
- Esiste un limite rigido di 1 MB per attributo, inclusi gli attributi di descrizione e personalizzati.
- L&#39;adattatore di ricerca non supporta attributi di prodotto creati con un modello di origine personalizzato e utilizzati come facet. Per supportare questa funzionalità, è necessario utilizzare il widget [Pagina di elenco prodotti](plp-styling.md).
- I tipi di prodotto personalizzati non sono supportati.
- Gli attributi personalizzati creati a livello di programmazione con `"is_user_defined": false` non sono supportati.
- Puoi filtrare i risultati utilizzando le condizioni &quot;inizia con&quot; o &quot;contiene&quot; con alcune limitazioni come descritto [qui](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#limitations).
- Puoi tenere traccia delle metriche delle prestazioni solo nell’ultimo anno.

## Indicizzazione

- [!DNL Live Search] [indici](indexing.md) fino a un totale di 450 attributi di prodotto per visualizzazione archivio. Questi sono distribuiti come segue:
   - 50 attributi ordinabili
   - 200 attributi filtrabili
   - 200 attributi ricercabili
- [!DNL Live Search] indicizza solo i prodotti dal database di Adobe Commerce.
- Le pagine CMS non sono indicizzate.
- Gli attributi SKU, nome e categoria sono ricercabili per impostazione predefinita e non possono essere esclusi dalla ricerca. Assicurati di annullare l’assegnazione dei prodotti dalle categorie se non sono destinati a essere in tali categorie.

## Facet

- È possibile configurare un massimo di 100 attributi come facet dai 200 attributi filtrabili che possono essere indicizzati.
- All’interno di un facet, è possibile restituire fino a 100 bucket. Se devi restituire più di 100 bucket, [crea un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) in modo che Adobe possa analizzare l&#39;impatto sulle prestazioni e determinare se è possibile aumentare questo limite per il tuo ambiente.
- I facet dinamici possono causare problemi di prestazioni in indici e indici di grandi dimensioni con elevata ordinalità. Se hai creato facet dinamici e noti un deterioramento delle prestazioni o una pagina non caricata con errori di timeout, prova a modificare i facet in modo che siano bloccati per determinare se questo risolve il problema di prestazioni.
- Lo stato del titolo (`quantity_and_stock_status`) non è supportato come facet. È possibile utilizzare `inStock: 'true'` per filtrare i prodotti in stock. Questa funzionalità è supportata automaticamente nel modulo `LiveSearchAdapter` quando &quot;Display out of stock products&quot; è impostato su &quot;True&quot; nell&#39;amministratore [!DNL Commerce].
- Gli attributi del tipo di data non sono supportati come facet.
- Eventuali modifiche apportate ai metadati dell’attributo dopo l’aggiunta dell’attributo come facet non vengono riportate nel facet.

## Query

- [!DNL Live Search] utilizza un [endpoint GraphQL](https://developer.adobe.com/commerce/services/graphql/live-search/) univoco per le query che supportano funzionalità quali il faceting dinamico e la ricerca in base al tipo. Sebbene simile all&#39;[API GraphQL](https://developer.adobe.com/commerce/webapi/graphql/), esistono alcune differenze e alcuni campi potrebbero non essere completamente compatibili.
- Il numero massimo di risultati che possono essere restituiti in una query di ricerca è 10.000.
- Il numero massimo di risultati per pagina è 500.
- Non è possibile filtrare i risultati utilizzando un attributo di tipo data.

## Regole

- Il numero massimo di [regole](rules.md) di merchandising di ricerca per ogni visualizzazione dello store è 50.
- Il merchandising per categoria può avere una regola per categoria.
- Il numero massimo di condizioni per regola è 10.
- Il numero massimo di eventi per regola è 25.
- Per evitare risultati imprevedibili in risposte impaginate, il numero di prodotti bloccati non deve superare le dimensioni di pagina richieste.

## Sinonimi

- [!DNL Live Search] può gestire fino a 200 [sinonimi](synonyms.md) per visualizzazione archivio.

## Merchandising categorie

- È possibile creare una regola per categoria per ogni visualizzazione store. Ogni regola può avere:
   - Fino a dieci condizioni
   - Fino a 25 eventi

## Autorizzazioni B2B e categoria

- I prodotti non vengono visualizzati se non vengono aggiunti a un catalogo condiviso predefinito.
- Per limitare i gruppi di clienti utilizzando [autorizzazioni categoria](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions):
   - I prodotti devono essere assegnati alla categoria principale.
   - Al gruppo di clienti &quot;Non connesso&quot; devono essere assegnate autorizzazioni di navigazione &quot;Consenti&quot;.
   - Per limitare i prodotti al gruppo di clienti &quot;Non connesso&quot;, vai a ogni categoria e imposta le autorizzazioni per ogni [gruppo di clienti](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- Al momento non è disponibile il supporto predefinito per B2B con il widget PLP su PWA Studio. Tuttavia, puoi [utilizzare l&#39;API](install.md#pwa-support) per implementare questa funzionalità.
- I facet di categoria in [!DNL Live Search] potrebbero visualizzare categorie non visualizzabili in un [gruppo di clienti](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage) specifico.
- [!DNL Live Search] può supportare fino a 1.000 gruppi di clienti.

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md) è disponibile solo per gli archivi che utilizzano il tema *Luma* o un tema personalizzato basato su *Luma*. Le breadcrumb nella pagina dei risultati di ricerca non avranno uno stile *Luma*.
- [!DNL popover] non supporta il tema *Blank*.
- [!DNL popover] non è supportato nel modulo Ordine rapido.
- Non sono supportate le liste dei desideri e i confronti tra prodotti.
- Il simbolo di valuta del sol peruviano (PEN) non è supportato.

## Risoluzione dei problemi

Per informazioni sulla risoluzione di alcuni problemi comuni in [!DNL Live Search], vedere i seguenti articoli della Knowledge Base:

- [[!DNL Live Search] catalogo non sincronizzato](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)
- [[!DNL Live Search] la classificazione del dashboard e dei risultati di ricerca non è corretta](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect)
- [[!DNL Live Search] mostra i prodotti esauriti indipendentemente dalle impostazioni dello stato delle scorte in Admin](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-displays-out-of-stock-products)
- [[!DNL Live Search] i facet non sono ordinati alfabeticamente](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted)

Se hai bisogno di ulteriore assistenza, contatta il [supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
