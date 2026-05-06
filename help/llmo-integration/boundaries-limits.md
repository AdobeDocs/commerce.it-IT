---
title: Limiti e limiti dell’integrazione
description: Scopri i limiti di ambito per i cataloghi di terze parti, la copertura delle correzioni automatiche, la scansiona di prerequisiti, considerazioni di scala aziendale e vincoli di accesso beta limitati per LLM Optimizer con Commerce.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Limiti e limiti dell’integrazione

>[!IMPORTANT]
>
>L’accesso a questa integrazione è limitato. Per ulteriori informazioni, contatta il tuo Technical Account Manager.

Utilizzare questo argomento per impostare le aspettative relative a ciò che l&#39;integrazione di [!DNL Adobe Commerce] e [!DNL Adobe LLM Optimizer] può automatizzare, a quali vincoli l&#39;utente rimane responsabile e quali vincoli sono ancora in evoluzione.

## Limitazioni del catalogo di terze parti {#third-party-catalog}

Quando il catalogo **non** è attivo in [!DNL Adobe Commerce]:

- LLM Optimizer è ancora in grado di identificare i problemi e suggerire miglioramenti utilizzando dati di catalogo specchiati o importati, a seconda della configurazione.
- **La correzione automatica diretta** nella piattaforma commerce del commerciante non equivale alla scrittura nel catalogo di origine del commerciante. Per applicare le modifiche potrebbe essere necessario un catalogo mirror, un’esportazione/importazione o un’automazione dei partner.

Per i cataloghi ospitati da Commerce, gli aggiornamenti approvati del nome e della descrizione passano al sistema di record di Commerce. Vedi [Utilizzare LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Scala e limiti tecnici {#scale-limits}

I cataloghi di grandi dimensioni e i conteggi URL elevati possono evidenziare i pattern di scansiona, analisi e distribuzione Edge.

## Scansiona e leggibilità dei bot {#crawling}

Gli approfondimenti significativi di cataloghi e PDP presuppongono che i **bot rilevanti per LLM possano accedere** agli URL a cui tieni e che le pagine siano strutturate in modo tale che l&#39;analisi automatizzata sia affidabile. Regole robot, autenticazione, blocco geografico e personalizzazione intensiva possono ridurre la copertura.

## Argomenti correlati

- [Panoramica dell’integrazione](overview.md)
- [Connettere Adobe Commerce a LLM Optimizer](get-started/connect-to-llmo.md)
- [Utilizzare LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md)
