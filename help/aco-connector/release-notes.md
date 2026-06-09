---
title: Note sulla versione [!DNL Adobe Commerce Optimizer Connector]
description: Informazioni aggiornate sulla versione di  [!DNL Adobe Commerce Optimizer Connector]  per Adobe Commerce.
feature: Services, Catalog Service, Release Notes
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# Note sulla versione del connettore Adobe Commerce Optimizer

Queste note sulla versione descrivono tutte le versioni di [!DNL Adobe Commerce Optimizer Connector] e includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Problema risolto](../assets/fix.svg) correzioni e miglioramenti
![Problema noto](../assets/bug.svg) Problemi noti

## Versioni del 2026

### Versione 1.0.13

_6 maggio 2026_

![Correzione](../assets/fix.svg) **Istruzioni di configurazione del connettore migliorate**-Aggiornamento della pagina di configurazione di Commerce Optimizer in Commerce Admin per il collegamento alla _Guida del connettore Adobe Commerce_. <!--COMOPT-1922-->
![Correzione](../assets/fix.svg) **Miglioramento metadati connettore**-Il connettore Adobe Commerce Optimizer ora include la versione installata nell&#39;intestazione metadati. Questo miglioramento consente ai team di identificare rapidamente quale versione del connettore è in uso durante la risoluzione dei problemi o gli impegni di supporto.<!--MDEE-1323-->

### Versione 1.0.12

_2 aprile 2026_

![Nuovo](../assets/new.svg) **Aggiunta del supporto per il feed Categorie nel comando `saas:resync` **-È ora possibile aggiornare e visualizzare facilmente i dati delle categorie più recenti utilizzando il comando CLI `saas:resync`:

```terminal
bin/magento saas:resync --feed=categories
```

_10 marzo 2026_

![È stato risolto un problema di compatibilità](../assets/fix.svg) che impediva l&#39;accesso alla pagina di configurazione di Commerce Services Connector dai menu Commerce Admin System e Configuration quando Adobe Commerce Optimizer Connector era installato in un&#39;istanza di Commerce.  Ora è possibile accedere alla pagina di configurazione di Commerce Services Connector quando sono installate entrambe le estensioni. <!--MDEE-1322-->


### Versione v1.0.10

_9 marzo 2026_

![Correzione](../assets/fix.svg) Se si accede alla pagina Stato di sincronizzazione feed dati prima di completare la configurazione del connettore, si viene reindirizzati automaticamente alla pagina di configurazione del connettore. Questo flusso guidato assicura che la configurazione del connettore sia completata e aiuta a evitare errori causati da impostazioni di configurazione mancanti che potrebbero causare elementi di stato non riusciti o incompleti.<!--MDEE-1296-->

### Versione v1.0.9

_1 marzo 2026_

Versione di disponibilità generale del connettore Adobe Commerce Optimizer.

>[!NOTE]
>
>Se hai partecipato al programma Beta per Adobe Commerce Optimizer Connector e disponi di una versione precedente dell’estensione installata, effettua l’aggiornamento alla versione con disponibilità generale per ricevere gli aggiornamenti più recenti.

