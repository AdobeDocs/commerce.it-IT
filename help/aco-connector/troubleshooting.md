---
title: Risolvere i problemi di [!DNL Adobe Commerce Optimizer Connector]
description: Scopri come risolvere i problemi relativi alle credenziali [!DNL Adobe Commerce Optimizer Connector], alla sincronizzazione dei cataloghi e all'esportazione dell'ambito per le integrazioni PaaS [!DNL Adobe Commerce].
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
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
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: 2dbf2b973af0cb7b831a17ca1a868a81b11bc9ee
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%
---
# Risolvere i problemi di [!DNL Adobe Commerce Optimizer Connector]

Utilizzare questa guida per diagnosticare e risolvere i problemi comuni con [!DNL Adobe Commerce Optimizer Connector] durante la configurazione iniziale, la sincronizzazione dei feed del catalogo e la configurazione di esportazione dell&#39;ambito. Le sezioni seguenti descrivono la convalida delle credenziali e del tenant, gli errori di sincronizzazione dei dati e la diagnostica [!DNL SaaS Data Export] correlata.

## Convalida credenziali o tenant non riuscita

Se `aco:config:init` non riesce durante la convalida delle credenziali:

- Eseguire il comando CLI `bin/magento aco:config:show` [!DNL Adobe Commerce] per verificare i valori archiviati.
- Conferma che l’ID tenant appartenga all’organizzazione IMS utilizzata per ottenere le credenziali.
- Verificare che il client OAuth disponga degli ambiti necessari per il servizio di acquisizione [!DNL Adobe Commerce Optimizer] (vedere [Ottenere le credenziali IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)).

## Dati non sincronizzati

**Controllare i dettagli dell&#39;errore a livello di elemento:**

Consulta [Verificare che la sincronizzazione dei dati funzioni](./data-sync-status.md#verify-that-the-data-sync-is-working) per i passaggi per aprire **[!UICONTROL Data Feed Sync Status]** in Commerce Admin. Seleziona il feed fallito per visualizzare i dettagli degli errori per singolo elemento.

Punti chiave sulla gestione degli errori:

- **400 errori** non sono stati ritentati. Esamina il payload per verificare se i campi obbligatori sono in formato errato o mancanti. Vedere [Mappatura campi per feed connettore](reference/field-mapping.md) per il formato previsto.
- **5xx errori** vengono ritentati automaticamente dal processo cron `*_resend_failed_items` (viene eseguito ogni 5 minuti).

**Verifica configurazione ambito:**

Se il problema riguarda solo un&#39;origine catalogo specifica (codice di visualizzazione store) o un listino prezzi dedicato, verificare se la sincronizzazione della visualizzazione sito Web o store corrispondente è disabilitata. Vedere [Personalizzare la configurazione di esportazione degli ambiti di Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration).

**Quando risolto:**

I feed del connettore mostrano uno stato di successo in **[!UICONTROL Data Feed Sync Status]** e i prodotti, i prezzi e gli attributi previsti sono visualizzati nella pagina **[!UICONTROL Data Sync]** in [!DNL Commerce Optimizer].

## Configurazione errata e interpretazione dei risultati

Per un catalogo di comportamenti specifici causati da configurazione errata o interpretazione errata dei risultati di sincronizzazione, ad esempio prodotti mancanti, prezzi non corretti o lacune nei dati a livello di ambito, vedere [Scenari per la risoluzione dei problemi](troubleshooting/troubleshooting-scenarios.md).

## Diagnostica [!DNL SaaS Data Export]

Per informazioni sulla diagnostica [!DNL SaaS Data Export] di livello inferiore, inclusi i percorsi dei log e i comandi di risincronizzazione dei feed, vedere la [[!DNL SaaS Data Export] guida alla risoluzione dei problemi](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/troubleshooting/logging){target="_blank"}.
