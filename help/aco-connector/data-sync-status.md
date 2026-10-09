---
title: Monitora sincronizzazione dati catalogo
description: Scopri come verificare la sincronizzazione dei dati del catalogo e risincronizzare manualmente i feed del connettore tra [!DNL Adobe Commerce] e [!DNL Adobe Commerce Optimizer] tramite lo stato di sincronizzazione dei feed di dati.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
last-update: 2026-10-01
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: c76e776250d9f996daf61d3cf62e2070803e998c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%
---
# Monitorare la sincronizzazione dei dati del catalogo

Dopo aver configurato [!DNL Adobe Commerce Optimizer Connector], la maggior parte degli aggiornamenti del catalogo vengono sincronizzati automaticamente tramite processi cron pianificati. Per informazioni dettagliate sul funzionamento della sincronizzazione automatica, vedere [Pipeline di sincronizzazione del connettore](connector-sync-pipeline.md). Utilizzare gli strumenti disponibili in questo argomento per verificare che i dati di prodotto, prezzo e categoria raggiungano [!DNL Adobe Commerce Optimizer] e per risincronizzare manualmente i feed quando necessario.

## Verifica che la sincronizzazione dei dati funzioni {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Risincronizzazione manuale dei dati {#manually-resync-data}

Se la sincronizzazione parziale e il nuovo tentativo automatico non risolvono i problemi di sincronizzazione, è possibile risincronizzare manualmente i dati del catalogo. L&#39;opzione scelta dipende dalla causa del problema e dal livello di controllo necessario.

| Attività | Opzione | Note |
| --- | --- | --- |
| Verifica lo stato di sincronizzazione e risincronizza dal sistema a monte quando mancano i prodotti | **Risincronizzazione del sistema a monte** | In [!DNL Commerce Optimizer], selezionare **[!UICONTROL Data Sync]** e verificare che vengano visualizzati le origini di catalogo, i prodotti, i prezzi e gli attributi previsti. Quando mancano i prodotti, risincronizzare dall&#39;istanza [!DNL Adobe Commerce] a monte utilizzando la pagina **[!UICONTROL Data Feed Sync Status]** o Commerce CLI (vedere le righe seguenti). |
| Risincronizzazione degli elementi di feed del connettore selezionati non riusciti o problematici | **[!UICONTROL Data Feed Sync Status]pagina nell&#39;amministrazione di Commerce** | Monitora lo stato di esportazione e risincronizza gli elementi di feed del connettore selezionati da Commerce Admin. Vedere [Verificare che la sincronizzazione dei dati funzioni](#verify-that-the-data-sync-is-working). |
| Risincronizzazione del feed del connettore di destinazione con il controllo operativo | **CLI Commerce** | Eseguire `saas:resync` dall&#39;istanza [!DNL Adobe Commerce] per i feed del connettore. Consulta [Sincronizzare i feed utilizzando Commerce CLI](../data-export/data-export-cli-commands.md) e [Feed supportati](reference/connector-reference.md#supported-feeds). |

>[!MORELIKETHIS]
>
> - [Pipeline di sincronizzazione del connettore](connector-sync-pipeline.md): scopri come funzionano la sincronizzazione automatica, le pianificazioni cron e la gestione degli errori
> - [Stimare il volume dei dati e il tempo di sincronizzazione](reference/estimate-data-volume-sync-time.md) — Calcolare la durata di sincronizzazione prevista
> - [Risoluzione dei problemi](troubleshooting.md) — Diagnostica i problemi relativi all&#39;esportazione di credenziali, sincronizzazione e ambito
> - [Personalizzare la configurazione di esportazione degli ambiti di Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration): configurare i feed per livello di ambito, abilitare e disabilitare il comportamento e i passaggi dell&#39;amministratore
> - [Moduli connettore ed endpoint di feed](reference/connector-reference.md) — Moduli di revisione, endpoint API e feed supportati
> - [Pagina Stato sincronizzazione feed dati nell&#39;amministratore di Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"} — Ulteriori informazioni sui campi e sulle funzionalità disponibili per monitorare lo stato dei feed
> - [Dashboard di sincronizzazione dati in [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync){target="_blank"} — Documentazione di riferimento per campi e azioni disponibili per monitorare la sincronizzazione dei dati del catalogo
