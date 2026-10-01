---
title: Proiezione del catalogo condiviso B2B
description: Scopri in che modo il connettore B2B proietta i cataloghi condivisi Adobe Commerce B2B in viste di catalogo Commerce Optimizer protette e come le vetrine risolvono e autorizzano l’accesso degli acquirenti.
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%
---
# Proiezione di cataloghi condivisi B2B

I progetti [!DNL Adobe Commerce Optimizer Connector for B2B] [!DNL Adobe Commerce] hanno condiviso cataloghi e assegnazioni aziendali in [!DNL Adobe Commerce Optimizer] visualizzazioni catalogo protette.

## Sincronizzazione di base e proiezione B2B

[!DNL Adobe Commerce Optimizer Connector] di base sincronizza i feed di catalogo e di determinazione prezzi, esegue il mapping delle visualizzazioni dello store alle origini di catalogo, ai siti Web ai listini prezzi e ai gruppi di clienti ai listini prezzi.

[!DNL Adobe Commerce Optimizer Connector for B2B] proietta l&#39;assortimento e i prezzi di ogni catalogo condiviso personalizzato in una visualizzazione protetta. Adobe Commerce seleziona la visualizzazione utilizzando l&#39;assegnazione della società dell&#39;acquirente. La chiave di accesso limitato verifica le richieste firmate ma non determina l’accesso al catalogo. Adobe Commerce è il sistema di registrazione per i dati di catalogo, prezzo e proiezione B2B gestiti dal connettore. Gestire l&#39;individuazione del prodotto e i consigli nella configurazione [!DNL Adobe Commerce Optimizer].

## Mappatura dei dati

La proiezione B2B combina il contenuto del catalogo sincronizzato e la determinazione dei prezzi con l’assortimento del catalogo condiviso e il contesto di assegnazione della società.

![Mappatura diagramma [!DNL Adobe Commerce] visualizzazioni archivio, prezzi, cataloghi condivisi e assegnazioni società alle visualizzazioni catalogo privato previste in [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}

| [!DNL Adobe Commerce] dati | [!DNL Adobe Commerce Optimizer] risultato | Finalità |
| --- | --- | --- |
| Abilitazione della visualizzazione store e dei dati di prodotto | Origine catalogo | Fornisce contenuto localizzato del prodotto. |
| Prezzi per siti web e gruppi di clienti | Listino prezzi | Fornisce i prezzi applicabili ma non autorizza l&#39;accesso |
| Assortimento personalizzato di cataloghi condivisi | Policy | Filtra la visualizzazione del catalogo per l&#39;assortimento del catalogo condiviso. |
| Visualizzazione catalogo condiviso personalizzato e visualizzazione archivio abilitata | Visualizzazione catalogo privato | Crea una visualizzazione protetta per ogni combinazione, con l&#39;origine del catalogo, la policy e il listino prezzi dedicato applicabili. |
| Assegnazione della società a un catalogo condiviso | Contesto buyer risolto | Consente al backend autenticato di risolvere la vista catalogo associata alla società dell&#39;acquirente. |
| Chiave di accesso limitato assegnata a una vista protetta | Protezione catalogo | Autorizza le richieste per la visualizzazione del catalogo protetto, ma non seleziona i prezzi. |

Ogni vista di catalogo privato può fare riferimento a un solo listino prezzi dedicato. Le visualizzazioni del Negozio con lo stesso contesto di determinazione dei prezzi del sito Web e del gruppo di clienti possono condividere un listino prezzi utilizzando origini di catalogo localizzate diverse. Il connettore non crea un listino prezzi dedicato per catalogo condiviso.

Il catalogo condiviso predefinito non viene proiettato come vista di catalogo privato B2B.

## Autorizzazione runtime

Dopo che un acquirente ha effettuato l&#39;accesso, il backend Commerce autentica la sessione e utilizza la vista dell&#39;assegnazione della società e del negozio dell&#39;acquirente per risolvere la vista del catalogo e il listino prezzi appropriati.

La vetrina invia l’ID della vista catalogo, l’ID del listino prezzi dedicato e il token firmato a ogni richiesta API di merchandising. [!DNL Adobe Commerce Optimizer] verifica la firma RS256 per JWT in base alle chiavi di accesso con restrizioni assegnate alla vista catalogo. Restituisce i dati del catalogo solo quando il token e la chiave sono validi e non scaduti.

![Flusso di autorizzazione runtime per le richieste di cataloghi B2B da un acquirente tramite una vetrina e back-end Commerce a [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}

Per le richieste di cataloghi privati, invia queste intestazioni:

| Intestazione | Finalità |
| --- | --- |
| `AC-View-ID` | Identifica la visualizzazione del catalogo. |
| `AC-Price-Book-ID` | Identifica il listino prezzi dedicato da utilizzare. |
| `AC-Catalog-View-Access-Token` | Trasporta il codice JWT firmato che autorizza l’accesso alla vista a catalogo protetta. |

Per i requisiti completi per richieste e token, consulta [Autenticazione API merchandising](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication) e [Verificare l&#39;accesso a una visualizzazione di catalogo privata](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced).

## Limite di protezione

La protezione del catalogo copre solo le richieste di catalogo e di ricerca. Non protegge le operazioni di carrello, pagamento o ordine. Applica l&#39;idoneità all&#39;acquisto in Adobe Commerce o nel sistema di transazioni collegato.

## Configurazione e monitoraggio delle proiezioni

Il connettore B2B proietta le viste del catalogo privato, i criteri, i riferimenti del listino prezzi e la configurazione della chiave di accesso limitato da [!DNL Adobe Commerce]. Non è necessario creare manualmente tali oggetti di proiezione gestiti dal connettore. Per le istruzioni di installazione, vedere [Introduzione al connettore B2B](get-started-b2b-shared-catalogs.md).

Per monitorare le visualizzazioni di catalogo previste e riconciliare la deriva di configurazione, vedere [Monitorare la sincronizzazione delle visualizzazioni di catalogo](catalog-view-sync-status.md). Per gestire le chiavi assegnate, vedere [Gestire le chiavi ad accesso limitato per i cataloghi condivisi B2B](restricted-access-keys.md).
