---
title: Sincronizzare i dati con l’esportazione di dati SaaS
description: Scopri in che modo  [!DNL SaaS Data Export] raccoglie e sincronizza i dati tra le istanze di Adobe Commerce e i servizi Commerce connessi.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 879
ht-degree: 0%

---

# Sincronizzare i dati con l’esportazione di dati SaaS

Quando si installa un servizio [!DNL Adobe Commerce] che richiede l&#39;esportazione di dati come Catalog Service, Live Search o Product Recommendations, viene installata una raccolta di moduli SaaS per l&#39;esportazione di dati per gestire il processo di raccolta e sincronizzazione dei dati.

L’esportazione dei dati SaaS sposta i dati dei prodotti da un’istanza Adobe Commerce alla piattaforma Commerce Services su base continuativa per mantenere aggiornati i dati. Ad esempio, la funzione Consigli di prodotto richiede le informazioni correnti sul catalogo per restituire in modo accurato i consigli con nomi, prezzi e disponibilità corretti. Per informazioni dettagliate sul monitoraggio del processo di sincronizzazione, vedere [Visualizzare e gestire il processo di sincronizzazione](data-sync-manage.md).

Il diagramma seguente mostra il flusso di esportazione dei dati SaaS.

![Flusso di raccolta e sincronizzazione esportazione dati SaaS per Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Quando i dati del catalogo cambiano in [!DNL Adobe Commerce], la sincronizzazione si sposta attraverso queste fasi.

1. **Rilevamento modifiche entità** - Il sistema Mview di Magento rileva le modifiche delle righe nelle tabelle del database sottoscritte (ad esempio, `catalog_product_entity`) e scrive le voci in una tabella changelog.
1. **Indicizzazione feed** - L&#39;indicizzatore del feed legge il registro delle modifiche, carica i dati delle entità dalle tabelle di origine e assembla gli elementi del feed.
1. **Raccolta e trasformazione dei dati** - I provider registrati nello schema di feed [`et_schema.xml`](extensibility-and-customizations.md#feed-schema-overview) raccolgono i dati del campo.
1. **Deduplicazione hash** - Viene calcolato un hash di contenuto per ogni elemento del feed. Gli elementi il cui hash non è stato modificato dopo l’ultima esportazione vengono ignorati, pertanto vengono trasmessi solo i dati modificati.
1. **Invio HTTP** - Gli elementi feed vengono inviati come batch HTTP POST autenticati al servizio acquisizione feed SaaS di Adobe.
1. **Lo stato persiste** - Lo stato della risposta API viene scritto nuovamente nella [tabella di feed](reference/feed-table-reference.md) per ogni elemento.
1. **Nuovo tentativo errore** - Gli elementi che non è stato possibile esportare vengono automaticamente ritentati da un processo cron pianificato.

>[!NOTE]
>
>Per le distribuzioni di [!DNL Adobe Commerce Optimizer Connector], [!DNL SaaS Data Export] gestisce il rilevamento delle modifiche delle entità e l&#39;assembly del feed. Il connettore mappa quindi i feed nel formato [!DNL Catalog Data Ingestion API] e li invia a [!DNL Adobe Commerce Optimizer]. Vedere [Pipeline di sincronizzazione del connettore](../aco-connector/connector-sync-pipeline.md) per il controllo dell&#39;ambito, l&#39;invio e la gestione degli errori.

>[!NOTE]
>
>Per garantire una pianificazione fluida ed evitare interruzioni nelle operazioni del sito, Adobe consiglia di stimare il volume dei dati e il tempo di sincronizzazione prima di avviare qualsiasi sincronizzazione dei feed di dati. Questa stima è importante quando si pianificano sincronizzazioni iniziali o aggiornamenti di cataloghi su larga scala, ad esempio le variazioni dei prezzi di massa. Per ulteriori dettagli, vedere [Stimare il volume dei dati e il tempo di trasmissione per la sincronizzazione dei dati](estimate-data-volume-sync-time.md)

## Modalità di sincronizzazione

L’esportazione di dati SaaS prevede due modalità per elaborare i feed di entità:

- **Modalità di esportazione immediata**: in questa modalità i dati vengono raccolti e inviati immediatamente al servizio Commerce in una singola iterazione. Questa modalità accelera la distribuzione degli aggiornamenti delle entità al servizio Commerce e riduce le dimensioni di archiviazione delle tabelle di feed.

- **Modalità di esportazione legacy**: in questa modalità i dati vengono raccolti in un unico processo. Successivamente, un processo cron invia i dati raccolti ai servizi commerce connessi. Nelle voci del registro di esportazione dei dati, i feed che utilizzano la modalità legacy sono etichettati `(legacy)`.

## Tipi di sincronizzazione

L&#39;esportazione dei dati SaaS supporta tre tipi di sincronizzazione: sincronizzazione completa, sincronizzazione parziale e nuovo tentativo di sincronizzazione degli elementi non riusciti.

### Sincronizzazione completa

Dopo aver collegato un’istanza di Adobe Commerce al servizio Commerce, esegui una sincronizzazione completa per inviare i dati del feed di entità da Adobe Commerce al servizio connesso.

>[!NOTE]
>
>La sincronizzazione completa è principalmente destinata alla fase di onboarding. Evita l’uso regolare per evitare il sovraccarico del database. Dopo la sincronizzazione iniziale, le modifiche in corso vengono sincronizzate automaticamente utilizzando la sincronizzazione parziale.

### Sincronizzazione parziale {#partial-sync}

Con la sincronizzazione parziale, l’esportazione di dati SaaS invia automaticamente aggiornamenti dall’applicazione Commerce, come modifiche al nome del prodotto o aggiornamenti dei prezzi, ai servizi commerce connessi.
Affinché la sincronizzazione parziale funzioni, l&#39;applicazione Commerce richiede la seguente configurazione:

- [La pianificazione delle attività è abilitata tramite processi cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)
- Tutti gli indici di esportazione dei dati SaaS sono configurati in modalità `Update by Schedule`.

### Ritenta sincronizzazione elementi non riusciti {#retry-failed-items-sync}

La sincronizzazione di Riprova elementi non riusciti utilizza un processo separato per inviare nuovamente gli elementi non sincronizzati a causa di errori durante il processo di sincronizzazione, ad esempio un errore dell&#39;applicazione, un&#39;interruzione della rete o un errore del servizio SaaS. I processi cron `*_resend_failed_items` nel gruppo `resync_failed_feeds_data_exporter` lo gestiscono automaticamente ogni 5 minuti.

## Processi cron pianificati

I seguenti gruppi cron automatizzano la pipeline secondo una pianificazione fissa.

| Gruppo Cron | Processo Cron | Finalità | Pianificazione |
|---|---|---|---|
| `index` | `indexer_update_all_views` | Elabora i registri delle modifiche di Mview e attiva gli aggiornamenti parziali dei feed | Ogni 1 minuto |
| `index` | `indexer_reindex_all_invalid` | Esegue una risincronizzazione completa per gli indici di feed contrassegnati come &quot;Reindicizzazione richiesta&quot; | Ogni 1 minuto |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | Rileva gli elementi di feed non riusciti e li invia nuovamente | Ogni 5 minuti |
| `commerce_data_export` | `saas_data_exporter` | Invia dati per feed in modalità legacy (ordini, ambiti) | Ogni 5 minuti |
| `commerce_data_export` | `cleanup_deleted_feed_items` | Pulisce gli elementi di feed eliminati sincronizzati oltre il periodo di conservazione (7 giorni) | Ogni giorno alle 2:00 |

## Invio di feed e gestione degli errori HTTP {#feed-submission-and-http-error-handling}

Gli elementi feed vengono inviati come batch JSON autenticati compressi Gzip tramite HTTP POST. Nella tabella seguente viene illustrato il mapping dei codici di risposta HTTP allo stato di esportazione e al comportamento dei nuovi tentativi.

| Codice di stato | Riprovare? | Significato |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------|
| 200 | No | Accettato correttamente |
| 400 | No | Dati non validi o errore di convalida - richiede un&#39;indagine manuale. Controllare `var/log/saas-export-errors.log` per i dettagli. |
| 429 | Sì | Limite di frequenza raggiunto - riduzione di `thread_count` in [impostazioni di elaborazione esportazione](customize-export-processing.md) |
| 5xx | Sì | Errore lato SaaS - nuovo tentativo automatico |
| 2 | Sì | L&#39;elemento è programmato per un nuovo tentativo |

Oltre agli errori a livello HTTP, gli errori a livello di applicazione, ad esempio errori di elaborazione locale o interruzioni di rete, sono pianificati per un nuovo tentativo automatico da parte dei processi cron `*_resend_failed_items`.

Monitorare lo stato per feed dalla pagina [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) nell&#39;amministrazione di Commerce.

>[!MORELIKETHIS]
>
> - [Gestisci sincronizzazione](data-sync-manage.md): verifica lo stato di sincronizzazione e sincronizza manualmente i feed.
> - [Schema della tabella dei feed](reference/feed-table-reference.md) - Verifica lo stato a livello di elemento e i dettagli dell&#39;errore.
> - [Miglioramento delle prestazioni di esportazione dei dati](customize-export-processing.md) — Ottimizzazione delle dimensioni del batch e del numero di thread.
