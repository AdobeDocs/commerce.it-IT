---
title: Gestisci [!DNL Adobe Commerce Optimizer Connector] sincronizzazione
description: Scopri come verificare la sincronizzazione dei dati del catalogo e risincronizzare manualmente i feed del connettore tra [!DNL Adobe Commerce] e [!DNL Adobe Commerce Optimizer].
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 0bfd368c50707692c7a0adda6e70e3776bd9692a
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# Gestisci sincronizzazione con [!DNL Commerce Optimizer]

Dopo aver configurato [!DNL Adobe Commerce Optimizer Connector], la maggior parte degli aggiornamenti del catalogo vengono sincronizzati automaticamente tramite processi cron pianificati. Per informazioni dettagliate sul funzionamento della sincronizzazione automatica, vedere [Pipeline di sincronizzazione del connettore](connector-sync-pipeline.md). Utilizzare gli strumenti di questo argomento per verificare che i dati raggiungano [!DNL Adobe Commerce Optimizer] e per risincronizzare manualmente i feed quando necessario.

## Verifica che la sincronizzazione dei dati funzioni {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Risincronizzazione manuale dei dati {#manually-resync-data}

Se la sincronizzazione parziale e il nuovo tentativo automatico non risolvono i problemi di sincronizzazione, è possibile risincronizzare manualmente i dati del catalogo. L&#39;opzione scelta dipende dalla causa del problema e dal livello di controllo necessario.

| Attività | Opzione | Note |
| --- | --- | --- |
| Verifica lo stato di sincronizzazione e risincronizza dal sistema a monte quando mancano i prodotti | **Risincronizzazione del sistema a monte** | In [!DNL Commerce Optimizer], selezionare **[!UICONTROL Data Sync]** e verificare che vengano visualizzati le origini di catalogo, i prodotti, i prezzi e gli attributi previsti. Quando mancano i prodotti, risincronizzare dall&#39;istanza [!DNL Adobe Commerce] a monte utilizzando la pagina **[!UICONTROL Data Feed Sync Status]** o Commerce CLI (vedere le righe seguenti). |
| Risincronizzazione degli elementi di feed del connettore selezionati non riusciti o problematici | **[!UICONTROL Data Feed Sync Status]pagina nell&#39;amministrazione di Commerce** | Monitora lo stato di esportazione e risincronizza gli elementi di feed del connettore selezionati da Commerce Admin. Vedere [Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working). |
| Risincronizzazione del feed del connettore di destinazione con il controllo operativo | **CLI Commerce** | Esegui `saas:resync` dall&#39;istanza di Adobe Commerce per i feed del connettore. Consulta [Sincronizzare i feed utilizzando Commerce CLI](../data-export/data-export-cli-commands.md) e [Feed supportati](reference/connector-reference.md#supported-feeds). |

>[!MORELIKETHIS]
>
> - [Pipeline di sincronizzazione del connettore](connector-sync-pipeline.md): scopri come funzionano la sincronizzazione automatica, le pianificazioni cron e la gestione degli errori
> - [Stimare il volume dei dati e il tempo di sincronizzazione](reference/estimate-data-volume-sync-time.md) — Calcolare la durata di sincronizzazione prevista
> - [Risoluzione dei problemi](troubleshooting.md) — Diagnostica i problemi relativi all&#39;esportazione di credenziali, sincronizzazione e ambito
> - [Moduli connettore ed endpoint di feed](reference/connector-reference.md) — Moduli di revisione, endpoint API e feed supportati
> - [Pagina Stato sincronizzazione feed dati nell&#39;amministratore di Commerce](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"} — Ulteriori informazioni sui campi e sulle funzionalità disponibili per monitorare lo stato dei feed
> - [Dashboard di sincronizzazione dati in [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce-optimizer/data-sync/data-sync){target="_blank"} — Documentazione di riferimento per campi e azioni disponibili per monitorare la sincronizzazione dei dati del catalogo
