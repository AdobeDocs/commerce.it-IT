---
title: Visualizzare e gestire il processo di sincronizzazione
description: Scopri come visualizzare e gestire il processo di sincronizzazione di  [!DNL SaaS Data Export]  utilizzando la dashboard di gestione dati e la pagina Stato sincronizzazione feed dati.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 652
ht-degree: 0%

---

# Visualizzare e gestire il processo di sincronizzazione

La maggior parte delle attività di sincronizzazione viene elaborata automaticamente utilizzando la sincronizzazione completa, la sincronizzazione parziale o la sincronizzazione di nuovi elementi non riusciti. Per informazioni dettagliate su quando viene eseguito ciascun tipo, vedere [Tipi di sincronizzazione](sync-overview.md#synchronization-types). [!DNL SaaS Data Export] fornisce inoltre gli strumenti per monitorare, gestire e risolvere i problemi del processo. Puoi visualizzare lo stato di sincronizzazione e gestire il processo di sincronizzazione dei dati utilizzando i dashboard per la distribuzione.

>[!BEGINTABS]

>[!TAB Adobe Commerce]

Per le distribuzioni Adobe Commerce su cloud, on-premise o Adobe Commerce as a Cloud Service, visualizza e gestisci il processo di sincronizzazione dalle seguenti risorse di amministrazione di Commerce:

- **[Pagina Stato sincronizzazione feed dati](../optimizer/setup/data-sync.md)**. Controllare lo stato di esportazione del feed per le distribuzioni connesse a [!DNL Live Search], [!DNL Product Recommendations] o [!DNL Catalog Service]. Questo dashboard mostra lo stato di esportazione del feed per ogni feed, inclusi eventuali errori rilevati. Una vista di dettaglio mostra lo stato di esportazione del feed per i singoli elementi del feed.

- **[Dashboard di gestione dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**: gli utenti amministratori possono visualizzare e tenere traccia dei dati esportati e sincronizzati correttamente nei servizi Commerce connessi. Questa dashboard mostra i dati del prodotto sincronizzati con i servizi Commerce.

>[!NOTE]
>
>La dashboard di gestione dati e la pagina Stato di sincronizzazione feed dati sono disponibili solo se è installato [!DNL Live Search], [!DNL Product Recommendations] o [!DNL Catalog Service].

>[!TAB Adobe Commerce con Commerce Optimizer]

Per le distribuzioni Commerce on-premise o sul cloud integrate con [!DNL Commerce Optimizer], visualizzare e gestire il processo di sincronizzazione utilizzando le risorse seguenti:

- **[Pagina stato sincronizzazione feed dati](../optimizer/setup/data-sync.md)**. Per i progetti Commerce che utilizzano [!DNL Commerce Optimizer], verificare la disponibilità dei dati del catalogo per la vetrina dalla pagina Stato sincronizzazione feed dati in [!DNL Commerce Optimizer]. Questo dashboard mostra lo stato di sincronizzazione dei feed di esportazione dei dati.

- **[Pagina di sincronizzazione dati](../optimizer/setup/data-sync.md)**: la pagina di sincronizzazione dati offre una panoramica dello stato di sincronizzazione dei dati di prodotto provenienti dall&#39;origine del catalogo a monte in [!DNL Commerce Optimizer].

Per informazioni dettagliate su come utilizzare questi dashboard per verificare il funzionamento della sincronizzazione dei dati e per risincronizzare manualmente i dati, vedere [Gestione sincronizzazione](../aco-connector/data-sync-manage.md) nella _Guida di Adobe Commerce Optimizer Connector_.

>[!ENDTABS]

## Verifica che la sincronizzazione dei dati funzioni {#verify-that-the-data-sync-is-working}

Per verificare il funzionamento della sincronizzazione dei dati, verificare che i dati esportati da [!DNL Adobe Commerce] siano stati correttamente recapitati al servizio Commerce connesso. Utilizza le dashboard della distribuzione per controllare entrambi i passaggi.

Inizia con l’esportazione, quindi conferma la consegna.

1. Controlla lo stato di sincronizzazione in Amministrazione Commerce.

   Vai a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Pagina Stato sincronizzazione feed dati con report sullo stato degli elementi del feed](./assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   Quando la sincronizzazione è in esecuzione, i dati del feed mostrano i record inviati correttamente. Seleziona un feed per visualizzare i dettagli o risolvere i problemi di sincronizzazione.

1. Verificare che i dati siano stati recapitati ai servizi Commerce connessi.

   Dall&#39;amministratore di Commerce, passa a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Dashboard di gestione dati che mostra i dati del catalogo sincronizzati nei servizi Commerce connessi](./assets/data-management-dashboard.png){width="700" zoomable="yes"}

   Verifica che vengano visualizzati i prodotti, i prezzi e gli attributi previsti.

>[!TIP]
>
>In caso di problemi con la sincronizzazione dei dati, vedi [Esaminare i registri e risolvere i problemi](troubleshooting/logging.md).

## Risincronizzazione manuale dei dati

Se la sincronizzazione parziale e il nuovo tentativo automatico non risolvono i problemi di sincronizzazione, è possibile risincronizzare manualmente i dati dall&#39;amministratore di Commerce o utilizzando i comandi CLI di Commerce. Le opzioni disponibili dipendono dalla distribuzione.

### Opzioni di risincronizzazione manuale disponibili {#manual-resync-options-commerce}

Utilizza le seguenti opzioni per risincronizzare manualmente i dati del feed.

| Attività | Opzione | Note |
| --- | --- | --- |
| Risincronizzazione degli elementi di feed selezionati non riusciti o problematici | **[!UICONTROL Data Feed Sync Status]pagina** | Monitora e risincronizza gli elementi di feed selezionati dall’amministratore di Commerce. Vedere [Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working). |
| Risincronizzazione completa di tutti i feed | **[!UICONTROL Data Management Dashboard]** | Esegui una risincronizzazione completa di tutti i feed dall’amministratore di Commerce; Adobe consiglia di eseguire questa operazione principalmente quando ti connetti a un servizio Commerce per la prima volta. Vedere [Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working). |
| Risincronizzazione del feed di destinazione con il controllo operativo | **CLI Commerce** | Utilizza il comando `saas:resync` per le risincronizzazioni dei feed di destinazione. Consulta [Sincronizzare i feed utilizzando Commerce CLI](data-export-cli-commands.md). |

>[!MORELIKETHIS]
>
> - [Funzionamento della sincronizzazione](sync-overview.md): informazioni sulle modalità di sincronizzazione, sulla sincronizzazione completa, sulla sincronizzazione parziale e sulla ripetizione degli elementi non riusciti.
> - [Sincronizzare i feed utilizzando Commerce CLI](data-export-cli-commands.md). Utilizzare il comando `saas:resync` per le risincronizzazioni dei feed mirate.
> - [Esaminare i registri e risolvere i problemi](troubleshooting/logging.md) — Eseguire la diagnostica degli errori di esportazione dei dati e SaaS.
> - [Gestisci sincronizzazione in [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md): verifica la sincronizzazione dei dati del catalogo e sincronizza manualmente i feed del connettore.


