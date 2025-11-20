---
title: '[!DNL SaaS Data Export Guide]'
description: Scopri come utilizzare l’estensione  [!DNL data export] per i servizi SaaS di Adobe Commerce che sincronizza i dati tra Adobe Commerce e i servizi Commerce connessi.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Guida [!DNL SaaS Data Export]

[!DNL SaaS data export] sincronizza i dati tra un&#39;istanza di Adobe Commerce e i servizi Commerce connessi. Quando si aggiunge Live Search, Product Recommendations o Catalog Service a un&#39;installazione di Adobe Commerce, l&#39;estensione [!DNL Data export] viene installata automaticamente.

L&#39;esportazione di dati SaaS raccoglie ed esporta vari tipi di dati, denominati _feed_, che aggregano tipi specifici di informazioni. A seconda dei servizi Commerce installati, i feed di esportazione dei dati SaaS includono:

- **I feed di entità del catalogo** aggregano i dati di prodotto. I dati includono prodotti, attributi del prodotto, prezzi dei prodotti, varianti dei prodotti, categorie, autorizzazioni per le categorie e autorizzazioni per i prodotti.
- Il feed **Scopes** aggrega i dati per i gruppi di clienti, i siti Web, gli archivi e le visualizzazioni degli archivi.
- Il **feed ordine di vendita** aggrega i dati degli ordini, incluse le entità correlate, quali fatture, spedizioni, note di accredito e così via.
- Il **feed inventario per più Source** aggrega i dati relativi agli elementi dello stato delle scorte.

L’esportazione di dati SaaS viene distribuita come estensione PHP. Supporta diversi metodi per avviare e gestire il processo di sincronizzazione dei dati.

- **Sincronizzazione manuale dall&#39;amministratore o dalla riga di comando**

   - Il [Dashboard di gestione dati](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) in Commerce Admin fornisce una visualizzazione grafica dello stato di sincronizzazione. È possibile utilizzare il dashboard per eseguire una risincronizzazione completa (_sincronizzazione completa_) di tutti i feed. Tuttavia, Adobe consiglia di eseguire la sincronizzazione completa solo la prima volta che si connette Adobe Commerce a un servizio Commerce. Vedere [Processo di sincronizzazione](data-synchronization.md).

   - Lo strumento da riga di comando [Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) fornisce comandi per sincronizzare feed specifici e include opzioni aggiuntive per personalizzare l&#39;elaborazione dei feed.

- **Sincronizzazione automatica con processi cron**

   - [Sincronizzazione dati parziale](data-synchronization.md#partial-synchronization-with-cron-jobs) - I processi Cron attivano una sincronizzazione dati parziale quando un utente amministratore di Commerce aggiorna un&#39;entità. Il processo di esportazione dei dati invia solo questi aggiornamenti ai servizi Commerce connessi. Il processo di sincronizzazione parziale si basa sul meccanismo MView e non richiede alcuna azione da parte dell&#39;utente amministratore o dell&#39;integratore di sistema.

   - [Nuovo tentativo automatico per errori di sincronizzazione](data-synchronization.md#failed-items-sync-for-error-recovery). I processi Cron attivano un nuovo tentativo automatico di sincronizzazione quando si verificano errori durante il processo di sincronizzazione dei dati.

- **Esporta pianificazione e prestazioni**

   - Sviluppatori e integratori di sistemi possono stimare il tempo necessario all’esportazione di dati SaaS per sincronizzare i dati tra Adobe Commerce e i servizi connessi. Questa stima può aiutare a pianificare l’elaborazione dell’esportazione dei dati per evitare interruzioni del sito. Vedere [Stima del volume dei dati e del tempo di trasmissione](estimate-data-volume-sync-time.md).

   - Nei casi in cui la sincronizzazione deve essere eseguita più rapidamente, l’esportazione dei dati SaaS offre opzioni di personalizzazione per migliorare le prestazioni di elaborazione delle esportazioni. Consulta [Migliorare le prestazioni di esportazione dei dati](customize-export-processing.md).

- **Tracciare e risolvere i problemi relativi alle attività di esportazione dei dati**. Utilizzare i registri di esportazione dei dati e saas-esportazione per esaminare lo stato di sincronizzazione e i payload dei feed durante il processo di sincronizzazione e indicizzazione. Consulta [Registrazione e risoluzione dei problemi](troubleshooting-logging.md).
