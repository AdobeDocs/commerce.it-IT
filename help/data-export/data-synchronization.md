---
title: Sincronizzare i dati con l’esportazione di dati SaaS
description: Scopri in che modo  [!DNL SaaS Data Export] raccoglie e sincronizza i dati tra le istanze di Adobe Commerce e i servizi SaaS connessi.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# Sincronizzare i dati con l’esportazione di dati SaaS

Quando installi un servizio Commerce che richiede l’esportazione di dati come Catalog Service, Live Search o Product Recommendations, viene installata una raccolta di moduli Saas per l’esportazione dei dati per gestire il processo di raccolta e sincronizzazione dei dati.

L’esportazione dei dati SaaS sposta i dati dei prodotti da un’istanza Adobe Commerce alla piattaforma Commerce Services su base continuativa per mantenere aggiornati i dati. Ad esempio, la funzione Consigli di prodotto richiede le informazioni correnti sul catalogo per restituire in modo accurato i consigli con nomi, prezzi e disponibilità corretti. Utilizzare il [dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) per osservare e gestire il processo di sincronizzazione o l&#39;interfaccia della riga di comando per attivare una sincronizzazione e reindicizzare i dati del prodotto per l&#39;utilizzo da parte di Commerce Services.

Il diagramma seguente mostra il flusso di esportazione dei dati SaaS.

![Flusso di raccolta e sincronizzazione esportazione dati SaaS per Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

I componenti principali del flusso di esportazione dei dati SaaS includono:

- Moduli SaaS per l’esportazione dei dati che raccolgono i dati per i feed da Adobe Commerce, assemblano gli elementi dei feed, ascoltano gli aggiornamenti e mantengono lo stato dei feed.
- I moduli SaaS esportano i dati, configurano il routing e pubblicano i feed nei servizi connessi.
- Il servizio Adobe Commerce gestisce il processo di acquisizione dei dati per convalidare i feed in arrivo e mantenere gli aggiornamenti ai servizi connessi.

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

### Sincronizzazione parziale

Con la sincronizzazione parziale, l’esportazione di dati SaaS invia automaticamente aggiornamenti dall’applicazione Commerce, come modifiche al nome del prodotto o aggiornamenti dei prezzi, ai servizi commerce connessi.

Il processo di esportazione dei dati utilizza i seguenti processi cron per automatizzare l’operazione di sincronizzazione parziale.

- processi del gruppo cron &quot;index&quot;:
   - Il processo `indexer_reindex_all_invalid` reindicizza tutti i feed non validi. È un processo cron standard di Adobe Commerce.
   - Il processo `saas_data_exporter` è per feed di esportazione legacy.
   - Il processo `sales_data_exporter` è specifico per il feed di esportazione dei dati di vendita.

Questi processi vengono eseguiti ogni minuto.

Affinché la sincronizzazione parziale funzioni, l&#39;applicazione Commerce richiede la seguente configurazione:

- [La pianificazione delle attività è abilitata tramite processi cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- Tutti gli indici di esportazione dei dati SaaS sono configurati in modalità `Update by Schedule`.

  Nella versione 103.1.0 e successive dell&#39;esportazione dei dati SaaS, la modalità `Update by Schedule` è attivata per impostazione predefinita. È possibile verificare la configurazione dell&#39;indice nel server utilizzando il comando CLI di Commerce, `bin/magento indexer:show-mode | grep -i feed`

### Ritenta sincronizzazione elementi non riusciti

La sincronizzazione di Riprova elementi non riusciti utilizza un processo separato per inviare nuovamente gli elementi non sincronizzati a causa di errori durante il processo di sincronizzazione, ad esempio un errore dell&#39;applicazione, un&#39;interruzione della rete o un errore del servizio SaaS. L’implementazione per questa sincronizzazione si basa anche su processi cron.

- `resync_failed_feeds_data_exporter` processi del gruppo cron:
   - Il processo `<feed name>_feed_resend_failed_feeds_items` invia nuovamente gli elementi non sincronizzati, ad esempio `products_feed_resend_failed_items`.

### Visualizzare e gestire il processo di sincronizzazione

La maggior parte delle attività di sincronizzazione viene elaborata automaticamente in base alla configurazione dell’applicazione. Tuttavia, l’esportazione di dati SaaS fornisce anche strumenti per gestire il processo.

- Gli utenti amministratori possono visualizzare e tenere traccia dell&#39;avanzamento della sincronizzazione e ottenere informazioni sui dati dal [dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

- Sviluppatori, integratori di sistemi o amministratori con accesso al server applicazioni Commerce possono gestire il processo di sincronizzazione e i feed di dati utilizzando lo strumento da riga di comando (CLI) di Adobe Commerce. Consulta [Gestire le operazioni di sincronizzazione utilizzando Commerce CLI](data-export-cli-commands.md).

### Verificare la configurazione dell&#39;applicazione Commerce

La sincronizzazione parziale e il tentativo di riesecuzione degli elementi non riusciti funzionano solo se l&#39;istanza di Commerce è stata configurata correttamente. In genere, la configurazione viene completata al momento della configurazione del servizio Commerce. Se l’esportazione dei dati non funziona correttamente, verifica la seguente configurazione.

- [Verificare che i processi cron siano in esecuzione](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Verificare che gli indicizzatori siano in esecuzione da [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) o utilizzando il comando CLI di Commerce `bin/magento indexer:info`.

- Verificare che gli indicizzatori per i feed seguenti siano impostati su `Update by Schedule`: Attributi catalogo, Prodotto, Sostituzioni prodotto e Variante prodotto. È possibile controllare gli indicizzatori da [Gestione indice](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) nell&#39;amministratore o utilizzando CLI (`bin/magento indexer:show-mode | grep -i feed`).

### Notifiche del gestore eventi per la registrazione del trasferimento dati

Nella versione 103.3.4 o successiva, l&#39;esportazione dati SaaS invia l&#39;evento `data_sent_outside` quando i dati vengono inviati dall&#39;istanza di Commerce ai servizi Adobe Commerce.

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>Per informazioni sugli eventi e su come abbonarti, consulta [Eventi e osservatori](https://developer.adobe.com/commerce/php/development/components/events-and-observers) nella documentazione per sviluppatori di Adobe Commerce.
