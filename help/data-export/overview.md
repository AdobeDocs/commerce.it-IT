---
title: '[!DNL SaaS Data Export Guide]'
description: Scopri come utilizzare l’estensione  [!DNL data export] per i servizi SaaS di Adobe Commerce che sincronizza i dati tra Adobe Commerce e i servizi Commerce connessi.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# Guida [!DNL SaaS Data Export]

[!DNL SaaS data export] sincronizza i dati tra un&#39;istanza di Adobe Commerce e i servizi Commerce connessi. Quando aggiungi Live Search, Product Recommendations, Catalog Service o [!DNL Adobe Commerce Optimizer Connector] a un&#39;installazione di Adobe Commerce, l&#39;estensione [!DNL Data Export] viene installata automaticamente.

>[!NOTE]
>
>Se installi [!DNL Adobe Commerce Optimizer Connector], la stessa estensione [!DNL Data Export] raccoglie il catalogo e i feed di determinazione prezzi da [!DNL Adobe Commerce]. Il connettore esegue quindi la mappatura e invia tali feed a [!DNL Adobe Commerce Optimizer] utilizzando il Composable Catalog Data Model (CCDM). Consulta la [[!DNL Adobe Commerce Optimizer Connector] panoramica](../aco-connector/overview.md) per la configurazione e l&#39;architettura e la [pipeline di sincronizzazione del connettore](../aco-connector/connector-sync-pipeline.md) per il comportamento di sincronizzazione dopo l&#39;esportazione.

L&#39;esportazione di dati SaaS raccoglie ed esporta vari tipi di dati, denominati _feed_, che aggregano tipi specifici di informazioni. A seconda dei servizi Commerce installati, i feed di esportazione dei dati SaaS includono:

- **I feed di entità del catalogo** aggregano i dati di prodotto. I dati includono prodotti, attributi del prodotto, prezzi dei prodotti, varianti dei prodotti, categorie, autorizzazioni per le categorie e autorizzazioni per i prodotti.
- Il feed **Scopes** aggrega i dati per i gruppi di clienti, i siti Web, gli archivi e le visualizzazioni degli archivi.
- Il **feed ordine di vendita** aggrega i dati degli ordini, incluse le entità correlate, quali fatture, spedizioni, note di accredito e così via.
- Il **feed inventario per più Source** aggrega i dati relativi agli elementi dello stato delle scorte.

L’esportazione di dati SaaS viene fornita come estensione PHP che supporta sia la sincronizzazione automatica che manuale:

- **Sincronizzazione automatica**: dopo la sincronizzazione completa iniziale durante la connessione a un servizio Commerce, i processi cron mantengono aggiornati i servizi connessi tramite la sincronizzazione parziale e il tentativo automatico di eseguire nuovamente gli elementi non riusciti, senza che sia necessaria alcuna azione da parte dell&#39;utente amministratore o dell&#39;integratore di sistemi.

- **Sincronizzazione manuale**—Eseguire una risincronizzazione completa o risincronizzare i feed selezionati dall&#39;amministratore di Commerce o da [Commerce CLI](data-export-cli-commands.md).

- **Monitoraggio**: tieni traccia dell&#39;integrità, dello stato e della consegna dei feed dalla pagina [!UICONTROL Data Feed Sync Status] e dal dashboard di gestione dati nell&#39;amministratore di Commerce. Consulta [Gestisci sincronizzazione](data-sync-manage.md) per i passaggi di verifica e risincronizzazione.

Per informazioni sul comportamento, le modalità e il diagramma del flusso di esportazione, vedere [Funzionamento della sincronizzazione](sync-overview.md).

L’esportazione dei dati SaaS fornisce inoltre strumenti per pianificare e risolvere eventuali problemi del processo di sincronizzazione:

- **Pianificazione e prestazioni** - Stimare il tempo di sincronizzazione per pianificare l&#39;elaborazione ed evitare interruzioni del sito e personalizzare l&#39;elaborazione delle esportazioni per migliorare le prestazioni. Consulta [Stimare il volume dei dati e il tempo di trasmissione](estimate-data-volume-sync-time.md) e [Migliorare le prestazioni di esportazione dei dati](customize-export-processing.md).

- **Tracciamento e risoluzione dei problemi** - Controlla lo stato di sincronizzazione e i payload dei feed utilizzando i registri di esportazione dei dati e saas. Consulta [Esaminare i registri e risolvere i problemi](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Estendere e personalizzare i feed di esportazione dei dati SaaS](extensibility-and-customizations.md) — Aggiungere o modificare i dati dei feed.
> - [Risoluzione dei problemi](troubleshooting/troubleshooting-scenarios.md) — Diagnostica la configurazione errata e risultati di sincronizzazione imprevisti.
> - [Note sulla versione](release-notes.md) — Aggiornamenti dell&#39;estensione e problemi noti.
