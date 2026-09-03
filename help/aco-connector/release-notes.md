---
title: Note sulla versione [!DNL Adobe Commerce Optimizer Connector]
description: Scopri le note sulla versione di  [!DNL Adobe Commerce Optimizer Connector] , incluse nuove funzioni, correzioni di bug e problemi noti per la sincronizzazione e l'esportazione del catalogo.
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4a3bb899f05e489cbd5b5c46909085e204751dc5
workflow-type: tm+mt
source-wordcount: 544
ht-degree: 0%

---

# Note sulla versione del connettore Adobe Commerce Optimizer

Queste note sulla versione descrivono tutte le versioni di [!DNL Adobe Commerce Optimizer Connector] e includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Problema risolto](../assets/fix.svg) correzioni e miglioramenti
![Problema noto](../assets/bug.svg) Problemi noti

## Versioni del 2026

### Versione 1.1.0

_2 settembre 2026_

![Nuovi](../assets/new.svg) **Attributi di categoria ora inclusi nella sincronizzazione del catalogo**. [!DNL Adobe Commerce Optimizer Connector] sincronizza ora gli attributi di categoria e i relativi metadati in [!DNL Adobe Commerce Optimizer], pertanto gli attributi di categoria personalizzati sono disponibili per il merchandising. <!--MDEE-1373-->

### Versione 1.0.17

_1 settembre 2026_

![Correzione](../assets/fix.svg) **Sincronizzazione catalogo più rapida per gli archivi con più visualizzazioni dello store**-L&#39;opzione [!DNL Adobe Commerce Optimizer Connector] filtra ora i prodotti e le categorie per visualizzazione dello store prima di estrarre i dati di feed, anziché estrarre ogni visualizzazione dello store e successivamente eliminare i risultati irrilevanti. Questo aggiornamento riduce in modo significativo i tempi di sincronizzazione e risincronizzazione per i cataloghi con molte visualizzazioni dello store. <!--MDEE-1441-->

### Versione 1.0.16

_7 agosto 2026_

![Correzione](../assets/fix.svg) **La sincronizzazione del catalogo non è più bloccata in una configurazione non valida**-È stato risolto un problema che consentiva l&#39;esecuzione indefinita della sincronizzazione del catalogo se la configurazione [!DNL Adobe Commerce Optimizer Connector] era mancante o non valida. La sincronizzazione ora completa e registra un avviso invece di continuare l’esecuzione. <!--MDEE-1413-->

![Correzione](../assets/fix.svg) **Richieste di amministrazione [!DNL Adobe Commerce Optimizer] più affidabili**-È stato risolto un problema a causa del quale [!DNL Adobe Commerce Optimizer Connector] poteva utilizzare un URL errato per [!DNL Adobe Commerce Optimizer] richieste di amministrazione, che poteva causare errori nelle richieste. <!--COMOPT-2288-->

![Correzione](../assets/fix.svg) **Operazioni di aggiornamento e patch più affidabili**-È stato risolto un problema a causa del quale le operazioni di aggiornamento e patch potevano essere eseguite nell&#39;ambiente errato, causando errori nelle richieste. <!--COMOPT-2288-->

### Versione 1.0.15

_10 luglio 2026_

![Correzione](../assets/fix.svg) aggiunto il supporto per l&#39;ordinamento al feed Categorie. <!--MDEE-1409-->

### Versione 1.0.14

_11 giugno 2026_

![Correzione](../assets/fix.svg) **Compatibilità PHP 8.5** - [!DNL Adobe Commerce Optimizer Connector] ora supporta PHP 8.5, quindi puoi aggiornare l&#39;ambiente [!DNL Adobe Commerce] senza interrompere la funzionalità del connettore o la sincronizzazione del catalogo. <!--MDEE-1388-->

![Correzione](../assets/fix.svg) **Aggiornamento dei listini prezzi dopo le modifiche alla valuta** - I prezzi aggiornati vengono automaticamente rispecchiati in Adobe Commerce Optimizer dopo le modifiche alla valuta. <!--MDEE-1384-->

![Correzione](../assets/fix.svg) **La navigazione rispetta le categorie padre disabilitate o nascoste**. I prodotti di gerarchie di categorie disabilitate o nascoste non vengono più visualizzati in modo imprevisto nelle esperienze di navigazione.<!--MDEE-1385-->

![Correzione](../assets/fix.svg) **URL di categoria coerenti dopo gli aggiornamenti di staging** - I collegamenti alle categorie e la navigazione rimangono accurati dopo l&#39;applicazione degli aggiornamenti di staging. <!--MDEE-1395-->

### Versione 1.0.13

_6 maggio 2026_

![Correzione](../assets/fix.svg) **Sono state migliorate le istruzioni di configurazione di [!DNL Adobe Commerce Optimizer Connector]**. È stata aggiornata la pagina di configurazione di [!DNL Adobe Commerce Optimizer] nell&#39;amministratore di Commerce per creare un collegamento alla Guida all&#39;integrazione di _[!DNL Adobe Commerce Optimizer Connector]_.
<!--COMOPT-1922-->

![Correzione](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector]miglioramento metadati** - [!DNL Adobe Commerce Optimizer Connector] ora include la versione installata nell&#39;intestazione metadati. Questo miglioramento consente ai team di identificare rapidamente quale versione del connettore è in uso durante la risoluzione dei problemi o gli impegni di supporto.<!--MDEE-1323-->

### Versione 1.0.12

_2 aprile 2026_

![Nuovo](../assets/new.svg) **È stato aggiunto il supporto per il feed Categorie in `saas:resync`, comando**-È ora possibile aggiornare e visualizzare facilmente i dati delle categorie più recenti utilizzando il comando CLI `saas:resync`:

```shell
bin/magento saas:resync --feed=categories
```

### Versione 1.0.11

_10 marzo 2026_

![È stato risolto un problema di compatibilità](../assets/fix.svg) che bloccava l&#39;accesso alla pagina di configurazione [!DNL Commerce Services Connector] dai menu di amministrazione di Commerce **[!UICONTROL System]** e **[!UICONTROL Configuration]** quando [!DNL Adobe Commerce Optimizer Connector] è installato in un&#39;istanza di [!DNL Adobe Commerce].  È ora possibile accedere alla pagina di configurazione [!DNL Commerce Services Connector] quando entrambe le estensioni sono installate. <!--MDEE-1322-->


### Versione 1.0.10

_9 marzo 2026_

![Correzione](../assets/fix.svg) Se si accede alla pagina **[!UICONTROL Data Feed Sync Status]** prima di completare la configurazione del connettore, si verrà reindirizzati automaticamente alla pagina di configurazione del connettore. Questo flusso guidato assicura che la configurazione del connettore sia completata e aiuta a evitare errori causati da impostazioni di configurazione mancanti che potrebbero causare elementi di stato non riusciti o incompleti.<!--MDEE-1296-->

### Versione v1.0.9

_1 marzo 2026_

Versione di disponibilità generale di [!DNL Adobe Commerce Optimizer Connector].

>[!NOTE]
>
>Se hai partecipato al programma Beta per [!DNL Adobe Commerce Optimizer Connector] e hai installato una versione precedente dell&#39;estensione, effettua l&#39;aggiornamento alla versione di disponibilità generale per ricevere gli aggiornamenti più recenti.
