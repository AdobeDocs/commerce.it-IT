---
title: Strumento di migrazione dei dati in blocco
description: Scopri come utilizzare lo strumento di migrazione dei dati in blocco per migrare i dati dal istanza esistente di Adobe Systems Commerce on Cloud a [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica a Adobe Systems Commerce solo come progetto Cloud Service e Adobe Systems Commerce Optimizer (infrastruttura SaaS gestito da Adobe Systems)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: e582ce85b58b57922a8cdd63dbe32bd0f08c64f9
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Migrazione di dati in blocco strumento

Il strumento di migrazione dei dati in blocco segue un&#39;architettura distribuita che consente la migrazione sicura ed efficiente dei dati dagli ambienti PaaS agli ambienti SaaS. Questo strumento aiuta gli implementatori della soluzione a migrare i dati da un Adobe Systems Commerce on Cloud istanza (PaaS) esistente a [!DNL Adobe Commerce as a Cloud Service] (SaaS). Per ulteriori informazioni sul processo di migrazione, vedere Panoramica della [migrazione](./overview.md).

>[!NOTE]
>
>Il strumento di migrazione dei dati in blocco supporta solo la migrazione dei dati di e-commerce di base di prime parti. La migrazione dei dati personalizzati non è attualmente supportata.

L&#39;immagine seguente descrive in dettaglio l&#39;architettura e i componenti chiave per l&#39;utilizzo del strumento di migrazione dei dati in blocco.

![Diagramma dell&#39;architettura di Bulk Data Migration Tool che mostra il flusso di dati da PaaS a SaaS](../assets/bulk-data-diagram.png){zoomable="yes"}

## Migrazione workflow

L&#39;workflow di migrazione dei dati in blocco consiste nei passaggi seguenti:

1. Configura un nuovo ambiente per la migrazione.
1. Copia i tuoi dati dal tuo vecchio sistema.
1. Sposta i tuoi dati nel nuovo sistema.
1. Rendi disponibile il tuo catalogo prodotti nel nuovo sistema.
1. Verifica che la migrazione dei dati sia stata eseguita correttamente.

Nelle sezioni seguenti vengono descritti dettagliatamente questi passaggi.

## Accedere all&#39;strumento di migrazione dei dati in blocco

La disponibilità del strumento di migrazione dei dati in blocco è la seguente:

- **Q1 2026** (non ancora disponibile): dopo il rilascio iniziale del strumento sulla migrazione dei dati in blocco, sarà possibile accesso inviando un ticket di supporto.
- **Q1 2026** (non ancora disponibile) - Dopo il rilascio pubblico del strumento sulla migrazione dei dati in blocco, sarà accessibile da questa pagina.

## Crea ambiente destinazione

L&#39;implementatore della soluzione (SI) crea un ambiente destinazione per la migrazione. In questo ambiente vengono archiviati i dati migrati dal istanza di origine.

Innanzitutto, [crea un nuovo [!DNL Adobe Commerce as a Cloud Service]  istanza](../getting-started.md#create-an-instance) (SaaS).

### Configurare i strumento di estrazione

Utilizza il strumento di estrazione per estrarre dati dal istanza di origine.

1. Scarica il strumento di estrazione dal collegare fornito da Adobe Systems.
1. Impostare le seguenti variabili di ambiente nel strumento di estrazione:
   - Dettagli di connessione al database MySQL esistente
   - ID tenant destinazione per il [!DNL Adobe Commerce as a Cloud Service] istanza
   - Le tue credenziali IMS, tra cui:
      - Client ID
      - Segreto client
      - Ambiti IMS
      - IMS URL - Il URL di base. Ad esempio, `https://ims-na1.adobelogin.com/`.
      - ID organizzazione IMS

   Per gli ambiti IMS e altri valori, seleziona il tipo OAuth nella sezione Credenziali all&#39;interno del **progetto in** Adobe Systems Developer Console[.](https://developer.adobe.com/console/) Ulteriori informazioni sono fornite nel file incluso con `.example.env` il strumento di estrazione.

### Extract dati

Prima di eseguire il strumento di estrazione, l&#39;implementatore della soluzione deve stabilire un tunnel SSH per il database PaaS utilizzando:

```bash
magento-cloud tunnel:open
```

Quindi esegui il strumento di estrazione, che:

1. Connettersi al database PaaS, analizzarne lo schema e confrontarlo con i dettagli dello schema del tenant SaaS.
1. Genera un piano di estrazione e trasformazione basato sugli elementi dello schema comune tra PaaS e SaaS.
1. Extract i dati utilizzando il servizio di gestione dei dati del catalogo (CDMS).

### Carica dati

Esegui il strumento dati di caricamento fornito da Adobe Systems. Questo strumento consente di:

1. Connettersi al database del tenant SaaS utilizzando un account di migrazione.
1. Generare un piano di caricamento.
1. Esegui il piano, spostando i dati nel database tenant SaaS in batch.
1. Elaborare i media del catalogo e trasferirli nell&#39;ambiente destinazione.
1. Svuota la cache Redis SaaS e invalida gli indici del database per il tenant.

### Inserimento dei dati del catalogo

Dopo il caricamento dei dati, i dati del catalogo fluiscono automaticamente dal database del tenant SaaS al servizio di catalogo.

Il servizio catalogo condivide questi dati con Live Search e Raccomandazioni prodotti. Per questo processo non è richiesto alcun intervento manuale. Una volta completata l&#39;acquisizione, i dati sono disponibili in tutti i servizi.

### Verifica dell&#39;integrità dei dati

Dopo la migrazione, CDMS esegue i seguenti controlli automatici di integrità dei dati per garantire l&#39;accuratezza e la completezza dei dati migrati:

**Verifica basata su API**

Durante la verifica, CDMS confronta le risposte API REST e GraphQL delle query eseguite in precedenza con i record corrispondenti del istanza destinazione. Eventuali discrepanze sono visibili nello stato di migrazione.

**Verifica a livello di database**

Durante la verifica, CDMS conta il numero di record estratti e confronta tale numero con la quantità di record caricati.

**Verifica su richiesta (opzionale)**

È inoltre possibile attivare manualmente la verifica completa di tutti i record di sistema:

>[!NOTE]
>
>Questo processo richiede molte risorse e deve essere utilizzato solo in ambienti sandbox.

La verifica completa include:

- Tutte le applicazioni verifica basata su API utilizzando tutte le risposte API REST e GraphQL preestratte
- Report dettagliato di eventuali incongruenze riscontrate
