---
title: Risoluzione dei problemi di  [!DNL Adobe Commerce Optimizer Connector]
description: Scopri come risolvere i problemi relativi alle credenziali [!DNL Adobe Commerce Optimizer Connector] , alla sincronizzazione dei cataloghi e all'esportazione dell'ambito per  [!DNL Adobe Commerce] integrazioni PaaS.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 1f901b4a72c10dc4e710742b98c03e88cbc8739f
workflow-type: tm+mt
source-wordcount: 273
ht-degree: 0%

---

# Risolvere i problemi relativi al connettore Adobe Commerce Optimizer

Utilizzare questa guida per diagnosticare e risolvere i problemi comuni con [!DNL Adobe Commerce Optimizer Connector] durante la configurazione iniziale, la sincronizzazione dei feed del catalogo e la configurazione di esportazione dell&#39;ambito. Le sezioni seguenti descrivono la convalida delle credenziali e del tenant, gli errori di sincronizzazione dei dati e la diagnostica [!DNL SaaS Data Export] correlata.

## Convalida credenziali o tenant non riuscita

Se `aco:config:init` non riesce durante la convalida delle credenziali:

- Eseguire il comando CLI `bin/magento aco:config:show` [!DNL Adobe Commerce] per verificare i valori archiviati.
- Conferma che l’ID tenant appartenga all’organizzazione IMS utilizzata per ottenere le credenziali.
- Verificare che il client OAuth disponga degli ambiti necessari per il servizio di acquisizione [!DNL Commerce Optimizer] (vedere [Ottenere le credenziali IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)).

## Dati non sincronizzati

**Controllare i dettagli dell&#39;errore a livello di elemento:**

1. Dall&#39;amministratore di Commerce, passa a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.
2. Seleziona il feed fallito per visualizzare i dettagli degli errori per singolo elemento.

Punti chiave sulla gestione degli errori:

- **400 errori** non sono stati ritentati. Esamina il payload per verificare se i campi obbligatori sono in formato errato o mancanti. Vedere [Mappatura campi per feed connettore](reference/field-mapping.md) per il formato previsto.
- **5xx errori** vengono ritentati automaticamente dal processo cron `*_resend_failed_items` (viene eseguito ogni 5 minuti).

**Verifica configurazione ambito:**

Se il problema riguarda solo un&#39;origine catalogo specifica (codice di visualizzazione store) o un listino prezzi dedicato, verificare se la sincronizzazione della visualizzazione sito Web o store corrispondente è disabilitata. Consulta [Personalizzare la configurazione di esportazione dei dati](./get-started.md#customize-the-commerce-scopes-export-configuration).

## Diagnostica [!DNL SaaS Data Export]

Per informazioni sulla diagnostica [!DNL SaaS Data Export] di livello inferiore, inclusi i percorsi dei log e i comandi di risincronizzazione dei feed, vedere la [[!DNL SaaS Data Export] guida alla risoluzione dei problemi](https://experienceleague.adobe.com/it/docs/commerce/saas-data-export/logs-troubleshooting/troubleshooting-logging){target="_blank"}.
