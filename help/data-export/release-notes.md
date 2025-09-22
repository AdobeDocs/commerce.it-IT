---
title: Note sulla versione [!DNL SaaS Data Export Extension]
description: Informazioni aggiornate sulla versione di  [!DNL Data Export Extension]  per Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: 4a25bcb82f98eb44c83a186caa6e5d6d664851d4
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 0%

---

# Note sulla versione dell&#39;estensione [!DNL SaaS Data Export]

Queste note sulla versione descrivono le versioni più recenti dell&#39;estensione [!DNL SaaS data export]. È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.

Gli aggiornamenti includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti


>[!NOTE]
>
>L’estensione SaaS per l’esportazione dei dati è una raccolta di moduli che viene installata automaticamente con Live Search, Product Recommendations e Catalog Service. Puoi controllare la versione installata nel sistema utilizzando Composer. In alcuni casi, potrebbe essere utile aggiornare l’estensione di esportazione dei dati sul sistema per rilevare correzioni o nuove funzionalità senza aggiornare la versione del servizio Commerce.

## Versione principale corrente

## Versione 103.4.12

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale in Pagina dettagli prodotto (PDP) non venivano visualizzati gli sconti della regola di prezzo del catalogo quando era presente la determinazione dei prezzi per il gruppo di clienti. Il piano PDP ora mostra correttamente il prezzo più basso.<!--MDEE-1158-->

## Versione 103.4.11

![Nuovo](../assets/new.svg) [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."}
È stato aggiunto il supporto per attributi di prodotto aggiuntivi per includere nel feed di prodotto i dati di classe fiscale, serie di attributi e inventario dalle configurazioni di prodotto Commerce. I clienti che desiderano includere questi attributi nei feed di esportazione del prodotto devono aggiungere il modulo Attributi prodotto aggiuntivi al proprio progetto Adobe Commerce. Vedi [Aggiungere classe fiscale, set di attributi e attributi di inventario](add-tax-attribute-set-inventory-attributes.md).<!--MDEE-1135-->
![Correzione](../assets/fix.svg) è stato risolto un problema che causava una sincronizzazione errata degli aggiornamenti dei prodotti eliminati se si verificava un errore durante un indice di prodotti completo. Ora, tutte le eliminazioni di prodotti vengono sincronizzate correttamente anche se si verifica un errore durante il processo di indicizzazione. <!--MDEE-1144-->

## Versione 103.4.10

![Correzione](../assets/fix.svg) è stato risolto un problema che causava la restituzione di un tipo errato (`text` invece di `OBJECT`) per alcuni attributi creati in modo dinamico. Ora, le informazioni sul tipo corrette vengono restituite in modo coerente, eliminando la necessità di risincronizzazioni manuali o soluzioni alternative.<!--MDEE-1131-->
![Correzione](../assets/fix.svg) è stato risolto un problema che poteva impedire la raccolta dei dati di prodotto durante le sincronizzazioni parziali a causa di errori nel provider di inventario LowStock. Questa correzione garantisce che i dati del prodotto vengano esportati in modo affidabile e che nessun ID prodotto venga ignorato a causa di errori relativi a LowStock.<!--MDEE-1132-->

## Versione 103.4.9

![Correzione](../assets/fix.svg) è stato risolto un problema che impediva la rigenerazione dei feed dei prezzi del prodotto in seguito all&#39;eliminazione di un prodotto o alla modifica dello SKU del prodotto.<!--MDEE-1125-->
![Correzione](../assets/fix.svg) è stata migliorata l&#39;elaborazione dell&#39;aggiornamento del prodotto per garantire che le modifiche vengano riportate correttamente quando si aggiorna un prodotto appena creato con lo stesso SKU di un prodotto eliminato in precedenza. La sincronizzazione dei prodotti ora utilizza correttamente gli ID prodotto aggiornati, garantendo un’esportazione accurata e affidabile dei dati.<!--MDEE-1126-->
![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale Catalog Service poteva restituire dati di variante obsoleti per prodotti configurabili garantendo la pubblicazione degli eventi di aggiornamento del prodotto dopo l&#39;eliminazione degli attributi.<!--MDEE-1127-->

## Versione 103.4.8

![Nuovo](../assets/new.svg) Aggiunte informazioni sul prezzo del livello al feed dei prezzi. <!--MDEE-1070-->
![Correzione](../assets/fix.svg) L&#39;estensione Data Exporter ora esporta correttamente i prezzi di selezione del bundle con ambito sito Web, garantendo che i prezzi di vendita riflettano valori precisi basati sulla configurazione &quot;Ambito prezzo catalogo&quot;.<!--MDEE-1115-->
![Correzione](../assets/fix.svg) In precedenza, i prodotti venivano sincronizzati con uno stato `lowStock=true` errato quando si utilizzava Inventory management (Multi-source Inventory management) con configurazione di soglia. Questo problema è stato risolto per garantire una segnalazione accurata delle scorte basse.<!--MDEE-1113-->

## Versione 103.4.7

![Correzione](../assets/fix.svg) tabelle obsolete rimosse che memorizzavano le autorizzazioni delle categorie per i prodotti. <!--MDEE-1065-->

## Versione 103.4.6

![Correzione](../assets/fix.svg) Esporta i dati di prodotto scaricabili di Adobe Commerce utilizzando l&#39;attributo `ac_downloadable` per l&#39;utilizzo con Adobe Commerce Optimizer. <!--MDEE-1043-->
![Correzione](../assets/fix.svg) dell&#39;errore critico di installazione di Adobe Commerce versione 2.4.4. <!--MDEE-1074-->

## Versione 103.4.5

L&#39;esportazione dei dati SaaS ![New](../assets/new.svg) ora supporta il tipo di prodotto Adobe Commerce `giftcard`. Nel feed di dati, i prodotti Gift card vengono esportati come prodotti semplici con il tipo di attributo di prodotto `ac_giftcard`. <!--MDEE-1042-->
![Correzione](../assets/fix.svg) È stata migliorata la segnalazione degli errori di esportazione dei dati. I registri ora includono messaggi di errore più dettagliati, inclusi i dettagli tecnici originali per semplificare il debug e la traccia degli errori. <!--MDEE-1064-->

## Versione 103.4.4

![Nuovo](../assets/new.svg) aggiunto un messaggio di avviso visualizzato quando l&#39;argomento `cleanup-feed` viene aggiunto al comando CLI `saas:resync`. L&#39;opzione `--cleanup-feed` deve essere utilizzata con cautela e solo in scenari specifici come dopo la pulizia dell&#39;ambiente o con l&#39;opzione `--dry-run`. Se lo utilizzi in altri casi, si possono verificare perdite di dati e problemi di sincronizzazione. <!--MDEE-1047-->
![Correzione](../assets/fix.svg) Aggiunta di `x-request-id` dalla risposta del server per migliorare la tracciabilità. <!--MDEE-1041-->
![Correzione](../assets/fix.svg) è stato risolto un problema che impediva il salvataggio dello stato di sincronizzazione per l&#39;intero batch di feed, causando un&#39;inutile risincronizzazione. <!--MDEE-1049-->
![Correzione](../assets/fix.svg) è stato risolto un problema per cui tutti i feed nel batch di feed venivano ignorati durante la sincronizzazione se un feed conteneva un errore. <!--MDEE-976-->
![Correzione](../assets/fix.svg) aggiunto supporto per le dimensioni nell&#39;indicizzatore delle autorizzazioni delle categorie. <!--MDEE-654-->

## Versione 103.4.3

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale i prodotti venivano ignorati durante il processo di esportazione dei dati a causa di attributi EAV mancanti. <!--MDEE-970-->

## Versione 103.4.2

![Correzione](../assets/fix.svg) Aggiunta la possibilità di raccogliere payload di entità in `saas-export.log` durante l&#39;esecuzione della risincronizzazione dei test utilizzando il comando `saas:resync --dry-run` con la variabile di ambiente `EXPORTER_EXTENDED_LOG=1`. <!--MDEE-1023-->

## Versione 103.4.1

![Correzione](../assets/fix.svg) Aggiunta di un prefisso alle chiavi della cache QueryXml per evitare conflitti di denominazione con altri moduli. <!--MDEE-1019-->

## Versione 103.4.0

![Correzione](../assets/fix.svg) Il feed degli override del prodotto non invia più le autorizzazioni se il prodotto non è assegnato a una categoria.<!--MDEE-449-->

## Versione 103.3.21

![Correzione](../assets/new.svg) è stata aggiunta la funzionalità per sincronizzare parzialmente `products`, `productOverrides` e `productAttributes` feed in base a un elenco specificato di SKU di prodotto. Utilizzare la nuova funzionalità aggiungendo l&#39;opzione `--by-ids` al comando resync CLI: <!--MDEE-606-->

```shell
bin/magento saas:resync --feed=<FEED_NAME> --by-ids='<SKU1>,<SKU2>,<SKU3>
```

![Correzione](../assets/fix.svg) Riduzione dei potenziali problemi di compatibilità con PHP 8.4 grazie alla risoluzione delle funzionalità obsolete. <!--MDEE-1002-->

## Versione 103.3.20

![Correzione](../assets/fix.svg) sono stati corretti gli errori `BulkException` non tracciabili in `cron.log` migliorando la messaggistica per gli errori relativi agli errori dei processi cron di esportazione dei dati del catalogo.<!--MDEE-966-->
![Correzione](../assets/fix.svg) Sono state migliorate le prestazioni del processo di risincronizzazione dei prodotti nelle istanze con un numero elevato di visualizzazioni dello store. <!--MDEE-974-->

## Versione 103.3.19

![Correzione](../assets/fix.svg) Aggiornamento dell&#39;estensione di esportazione dei dati per migliorare l&#39;estensibilità dei feed. <!--MDEE-936-->
![Correzione](../assets/fix.svg) Il processore di esportazione dei dati ora verifica lo stato dell&#39;indicizzatore prima di una risincronizzazione completa per evitare la perdita accidentale di dati nella tabella dei feed.

## Versione 103.3.18

![Correzione](../assets/fix.svg) Gli aggiornamenti di gestione temporanea per le entità prodotto e categoria ora vengono attivati correttamente negli aggiornamenti dei dati di esportazione dei dati.<!--MDEE-963-->

## Versione 103.3.17

![Correzione](../assets/fix.svg) Aggiunta compatibilità per PHP 8.4. <!--MDEE-941-->

## Versione 103.3.16

![Correzione](../assets/fix.svg) I valori dell&#39;opzione possono essere vuoti per i prodotti configurabili per più visualizzazioni dello store. <!--MDEE-926-->

## Versione 103.3.15

![Correzione](../assets/fix.svg) ha garantito il funzionamento stabile dei test di integrazione nelle configurazioni meno recenti. <!--MDEE-869-->
![Correzione](../assets/fix.svg) Interrompi la propagazione delle opzioni di attributo non necessarie. <!--MDEE-882-->
![Correzione](../assets/fix.svg) è stato corretto il messaggio di errore inviato al log di esportazione dei dati quando la serializzazione dei dati non riesce. <!--MDEE-913-->
![Correzione](../assets/fix.svg) è stata migliorata l&#39;affidabilità di semplici aggiornamenti di prodotto con una copertura di test aggiuntiva. <!--MDEE-886-->

## Versione 103.3.14

![Correzione](../assets/fix.svg) L&#39;indicizzatore di esportazione mantiene ora lo stato corretto per gli indicizzatori dipendenti. In precedenza, questi indici venivano erroneamente invalidati e richiedevano ulteriori controlli e convalide che rallentavano le prestazioni di indicizzazione. <!--MDEE-866-->

## Versione 103.3.13

![Correzione](../assets/fix.svg) Prestazioni migliorate del processo di sincronizzazione dei dati aggiungendo una cache locale per i dati delle opzioni degli attributi.<!--MDEE-864-->

## Versione 103.3.12

![Correzione](../assets/fix.svg) è stato risolto un problema che aumentava i tempi di sincronizzazione per i prodotti semplici e virtuali. <!--MDEE-861-->

## Versione 103.3.11

![Correzione](../assets/fix.svg) Il servizio di esportazione dati ora invia i dati dei prezzi speciali per i prodotti bundle come percentuale, correggendo un problema precedente in cui era stato inviato come prezzo finale. <!--MDEE-854-->
![Correzione](../assets/fix.svg) Aggiornamento dell&#39;implementazione monolog per compatibilità con Monolog 3. <!--MDEE-858-->

## Versione 103.3.10

![Correzione](../assets/fix.svg) è stata corretta la filtrazione di più visualizzazioni dello store per il feed di opzioni personalizzate del prodotto. <!--MDEE-842-->
![Correzione](../assets/fix.svg) I feed non validi vengono inviati nuovamente solo dopo la modifica del valore hash del feed.<!--MDEE-848-->

## Versione 103.3.9

![Correzione](../assets/fix.svg) Quando un&#39;entità viene eliminata, il flag `deleted` viene ora propagato per i feed del servizio di valutazione per il sito Web (`scopesWebsite`) e il gruppo di clienti (`scopesCustomerGroup`).<!--MDEE-839-->

## Versione 103.3.8

![Correzione](../assets/fix.svg) Le opzioni di configurazione disabilitate non vengono più esportate come opzioni attive.<!--MDEE-812-->
![Correzione](../assets/fix.svg) Le opzioni e i valori vengono aggiornati in un prodotto configurabile quando si apportano modifiche a un prodotto secondario. <!--MDEE-835-->
![Nuovo](../assets/new.svg) è stata aggiunta la possibilità di includere dati di attributi di sistema aggiuntivi nel feed di attributi di prodotto.

## Versione 103.3.7

![Correzione](../assets/fix.svg) Sono state rimosse le dipendenze non necessarie dal modulo InventoryDataExporter.
![Correzione](../assets/fix.svg) versioni richieste modificate per i moduli inventario inclusi nel modulo CatalogInventoryDataExporter per supportare Adobe Commerce versione 2.4.4.

## Versione 103.3.6

![Correzione](../assets/fix.svg) sono stati corretti i deadlock che si verificavano durante la reindicizzazione del feed in modalità multithread. Le query sono ora separate in operazioni di inserimento e aggiornamento.
![Correzione](../assets/fix.svg) ottimizzata la query dei prezzi per cataloghi di grandi dimensioni con molti siti Web.
![Nuovo](../assets/new.svg) aggiunta della logica di esecuzione di un nuovo tentativo per rieseguire le transazioni non riuscite quando si verifica deadlock.

## Versione 103.3.5

![Correzione](../assets/fix.svg) Imposta la dipendenza per la versione più recente compatibile dell&#39;esportazione dei dati per il modulo comune SaaS.

![Correzione](../assets/fix.svg) L&#39;istanza `ScopeConfig` è stata sostituita con `ServiceConfigInterface` per supportare diverse configurazioni di servizio.

## Versione 103.3.4

![Correzione](../assets/fix.svg) Aggiunta del supporto per la registrazione di controllo del trasferimento dei dati aggiungendo un meccanismo per inviare un evento `data_sent_outside` ogni volta che i dati vengono trasmessi dall&#39;istanza di Commerce a un servizio Commerce <!--MDEE-785-->

## Versione 103.3.3

L&#39;esportazione dei dati SaaS ![New](../assets/new.svg) ora memorizza nella cache gli attributi Entity-Attribute-Value (EAV) per la query dei metadati degli attributi.

![Correzione](../assets/fix.svg) è stato risolto un problema che impediva il salvataggio del feed `InventoryStockStatus` durante un nuovo tentativo se il prodotto era stato eliminato.

## Versione 103.3.2

![Correzione](../assets/fix.svg) è stato risolto un problema che causava l&#39;assenza del campo `modifiedAt` dai feed di entità rimossi.

## Versione 103.3.1

![Correzione](../assets/fix.svg) è stato risolto un problema che causava la visualizzazione di un messaggio `Invalid Template File` durante la reindicizzazione del feed dei prodotti quando Page Builder è installato.

## Versione 103.3.0

![Nuovo](../assets/new.svg) è stata eseguita la migrazione delle tabelle dei feed di esportazione immediata nella struttura unificata:
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![Nuovo](../assets/new.svg) ha eseguito la migrazione dei feed di catalogo e inventario alla soluzione di esportazione immediata.

![Nuovo](../assets/new.svg) ha rinominato i processi cron del feed di esportazione immediata in `*_feed_resend_failed_items`.

![Nuovo](../assets/new.svg) ha rinominato i feed di esportazione immediati, gli ID di visualizzazione dell&#39;indicizzatore e le tabelle di registro delle modifiche.
- tabelle di feed (e ID di visualizzazione dell’indicizzatore):
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- modifica dei nomi delle tabelle di registro: segue lo stesso pattern di denominazione delle tabelle di feed, ma modifica dei nomi delle tabelle di registro aggiunge un suffisso `_cl`.  Esempio: `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
Se disponi di codice personalizzato che fa riferimento a una di queste entità, aggiorna i riferimenti con i nuovi nomi per garantire che il codice continui a funzionare correttamente.

![Correzione](../assets/fix.svg) Imposta il campo `modified_at` nei dati del feed solo per i feed che lo richiedono.

![Correzione](../assets/fix.svg) Modificare la query `productAttributes` per recuperare solo gli attributi del prodotto.

## Versione 103.2.6

![Correzione](../assets/fix.svg) è stato risolto un problema che impediva la reindicizzazione dei feed quando le tabelle hanno un prefisso.

## Versione 103.2.5

![Correzione](../assets/fix.svg) Ottimizzata la query del prezzo.

## Versione 103.2.4

![Correzione](../assets/fix.svg) è stato corretto lo stato Stock errato visualizzato per un prodotto quando Commerce Inventory management è abilitato.

## Versione 103.2.3

![Correzione](../assets/fix.svg) prezzo speciale fisso a livello di sito Web.
![Correzione](../assets/fix.svg) aggiunto mutex per tutti i feed elaborati.


## Versione 103.2.2

![Correzione](../assets/fix.svg) Miglioramento della strategia di invio in batch dei feed per i cataloghi di grandi dimensioni. La tabella dei batch ora è compilata con un numero limitato di ID per ridurre l’utilizzo di memoria.

![Correzione](../assets/fix.svg) eliminata dipendenza rigida di CommerceInventoryDataExporter ai moduli MSI.

![Correzione](../assets/fix.svg) Sono stati migliorati `commerce-data-exporter` registri per raccogliere ulteriori informazioni e organizzarli in base a diverse fasi di esportazione.

## Versione 103.2.1

- È stata rilasciata la versione aggiornata.

## Versione 103.2.0

- È stata aggiunta la sincronizzazione di dati multi-thread per prodotti e prezzi.
