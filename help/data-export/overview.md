---
title: '[!DNL SaaS Data Export Guide]'
description: Scopri come utilizzare l’estensione  [!DNL data export] per i servizi SaaS di Adobe Commerce che sincronizza i dati tra Adobe Commerce e i servizi Commerce connessi.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 569
ht-degree: 0%

---

# Guida [!DNL SaaS Data Export]

[!DNL SaaS data export] sincronizza i dati tra un&#39;istanza di Adobe Commerce e i servizi Commerce connessi. Quando si aggiunge Live Search, Product Recommendations o Catalog Service a un&#39;installazione di Adobe Commerce, l&#39;estensione [!DNL Data export] viene installata automaticamente.

>[!NOTE]
>
>Se installi il connettore Adobe Commerce Optimizer, viene utilizzata la stessa estensione per l’esportazione dei dati per inviare i feed di catalogo e determinazione prezzi a Adobe Commerce Optimizer utilizzando il Composable Catalog Data Model (CCDM). Per informazioni dettagliate sull&#39;architettura e sulla configurazione, consulta la [guida del connettore Adobe Commerce Optimizer](../aco-connector/overview.md).

L&#39;esportazione di dati SaaS raccoglie ed esporta vari tipi di dati, denominati _feed_, che aggregano tipi specifici di informazioni. A seconda dei servizi Commerce installati, i feed di esportazione dei dati SaaS includono:

- **I feed di entità del catalogo** aggregano i dati di prodotto. I dati includono prodotti, attributi del prodotto, prezzi dei prodotti, varianti dei prodotti, categorie, autorizzazioni per le categorie e autorizzazioni per i prodotti.
- Il feed **Scopes** aggrega i dati per i gruppi di clienti, i siti Web, gli archivi e le visualizzazioni degli archivi.
- Il **feed ordine di vendita** aggrega i dati degli ordini, incluse le entità correlate, quali fatture, spedizioni, note di accredito e così via.
- Il **feed inventario per più Source** aggrega i dati relativi agli elementi dello stato delle scorte.

L’esportazione di dati SaaS viene distribuita come estensione PHP. Supporta diversi metodi per avviare e gestire il processo di sincronizzazione dei dati.

- **Sincronizzazione manuale dall&#39;amministratore o dalla riga di comando**

   - Il [dashboard di gestione dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) in Commerce Admin fornisce una visualizzazione grafica dello stato di sincronizzazione che mostra i dati del prodotto sincronizzati correttamente con i servizi commerce. È possibile utilizzare il dashboard per eseguire una risincronizzazione completa (_sincronizzazione completa_) di tutti i feed. Tuttavia, Adobe consiglia di eseguire la sincronizzazione completa solo la prima volta che si connette Adobe Commerce a un servizio Commerce. Vedere [Processo di sincronizzazione](data-synchronization.md).

     {{aco-data-sync-verification}}

   - La pagina [Stato sincronizzazione feed dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) fornisce informazioni in tempo reale sullo stato e sulle prestazioni dei feed di esportazione dei dati che trasferiscono i dati di prodotti e categorie da Commerce a servizi esterni quali Product Recommendations, Live Search, Catalog Service o Adobe Commerce Optimizer.

   - Lo strumento da riga di comando [Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) fornisce comandi per sincronizzare feed specifici e include opzioni aggiuntive per personalizzare l&#39;elaborazione dei feed.

- **Sincronizzazione automatica con processi cron**

   - [Sincronizzazione dati parziale](data-synchronization.md#partial-sync) - I processi Cron attivano una sincronizzazione dati parziale quando un utente amministratore di Commerce aggiorna un&#39;entità. Il processo di esportazione dei dati invia solo questi aggiornamenti ai servizi Commerce connessi. Il processo di sincronizzazione parziale si basa sul meccanismo MView e non richiede alcuna azione da parte dell&#39;utente amministratore o dell&#39;integratore di sistema.

   - [Nuovo tentativo automatico per errori di sincronizzazione](data-synchronization.md#retry-failed-items-sync). I processi Cron attivano un nuovo tentativo automatico di sincronizzazione quando si verificano errori durante il processo di sincronizzazione dei dati.

- **Esporta pianificazione e prestazioni**

   - Sviluppatori e integratori di sistemi possono stimare il tempo necessario all’esportazione di dati SaaS per sincronizzare i dati tra Adobe Commerce e i servizi connessi. Questa stima può aiutare a pianificare l’elaborazione dell’esportazione dei dati per evitare interruzioni del sito. Vedere [Stima del volume dei dati e del tempo di trasmissione](estimate-data-volume-sync-time.md).

   - Nei casi in cui la sincronizzazione deve essere eseguita più rapidamente, l’esportazione dei dati SaaS offre opzioni di personalizzazione per migliorare le prestazioni di elaborazione delle esportazioni. Consulta [Migliorare le prestazioni di esportazione dei dati](customize-export-processing.md).

- **Tracciare e risolvere i problemi relativi alle attività di esportazione dei dati**. Utilizzare i registri di esportazione dei dati e saas-esportazione per esaminare lo stato di sincronizzazione e i payload dei feed durante il processo di sincronizzazione e indicizzazione. Consulta [Registrazione e risoluzione dei problemi](troubleshooting-logging.md).
