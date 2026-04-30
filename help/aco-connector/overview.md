---
title: Connettore Adobe Commerce Optimizer
description: Scopri come collegare i dati dal cloud Commerce o dal progetto on-premise a Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: c9cce4766ef3f30390d50f53237328be1cfeefdf
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---


# Connettore Adobe Commerce Optimizer

Il connettore Adobe Commerce Optimizer è un’integrazione nativa di prime parti tra Adobe Commerce (cloud o on-premise) e Adobe Commerce Optimizer. Sincronizza i dati di catalogo e prezzi dagli store Adobe Commerce in Commerce Optimizer in modo da poter:

- Potenti **Consigli e individuazione dei prodotti basati sull&#39;intelligenza artificiale**
- Esegui **storefront headless ad alte prestazioni** (inclusi gli storefront Commerce basati su Edge Delivery)
- Analizza **prima e dopo** KPI e integrità della sincronizzazione dati in un&#39;unica posizione

Commerce rimane il tuo sistema di record per prodotti, prezzi e struttura del catalogo. Commerce Optimizer diventa il tuo livello di esperienza e merchandising, fornendo risultati rapidi e rilevanti per qualsiasi vetrina o canale collegato.

## Vantaggi chiave {#key-benefits}

| Beneficio | Che cosa significa per te |
| --- | --- |
| **Nessun connettore personalizzato da compilare** | Utilizza un’integrazione supportata di prima parte invece di scrivere e mantenere feed e script personalizzati. |
| **Time to value più rapido con Commerce Optimizer** | Attiva Ricerche IA, consigli e vetrine headless oltre all’implementazione Adobe Commerce esistente. |
| **Allineato con ambiti Commerce** | Mappa automaticamente i siti Web, le visualizzazioni del negozio e i gruppi di clienti in costrutti di catalogo di Commerce Optimizer (origini del catalogo e listini prezzi). |
| **Visibilità operativa** | Monitora lo stato di integrità dei feed, gli orari dell’ultima sincronizzazione e lo stato per SKU da una visualizzazione dedicata dello stato di sincronizzazione dei feed di dati. |
| **Percorso pronto per il futuro verso SaaS** | Fornisce un percorso di modernizzazione a basso rischio da PaaS verso Adobe Commerce as a Cloud Service + Optimizer, senza una ripiattaforma. |

## Architettura del connettore {#connector-architecture}

Il diagramma seguente illustra l’architettura end-to-end del connettore, da Adobe Commerce a Commerce Optimizer, fino a storefront e sistemi di pagamento.

![Diagramma dell&#39;architettura end-to-end di Commerce Optimizer Connector Commerce](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

In questa architettura:

- Adobe Commerce (su cloud o on-premise) è il sistema di registrazione e produzione di feed
- Il connettore esporta i feed di catalogo, prezzo e categoria
- Commerce Optimizer acquisisce e normalizza i dati di feed in Origini catalogo, Listini prezzi e Visualizzazioni catalogo
- Le vetrine (Commerce storefront su Edge Delivery o build headless personalizzate) richiamano le API GraphQL di Commerce Optimizer per l’individuazione e i consigli e chiamano Commerce o un’altra piattaforma di terze parti connessa per operazioni di carrello e pagamento

## Funzionamento del connettore con Adobe Commerce {#how-it-works}

- Commerce Optimizer acquisisce e normalizza i dati di feed in Origini catalogo, Listini prezzi e Visualizzazioni catalogo.

- Gli store front (Commerce storefront su Edge Delivery o build headless personalizzate) richiamano le API GraphQL di Commerce Optimizer per l’individuazione e i consigli e chiamano Commerce o un’altra piattaforma di terze parti connessa per le operazioni di carrello e pagamento.

## Funzionamento del connettore con Adobe Commerce

Il connettore Adobe Commerce Optimizer funziona utilizzando gli ambiti Commerce esistenti (siti web e viste store) e la segmentazione dei clienti per popolare il modello di catalogo Commerce Optimizer:

![Mappatura dei dati di Commerce a Adobe Commerce Optimizer](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Visualizzazioni store → Origini catalogo** — Ogni visualizzazione store diventa un Source catalogo separato in Commerce Optimizer. Tale origine include attributi di prodotto localizzati ed eventuali dati specifici della vista archivio
- **Siti Web → listini prezzi**: ogni sito Web Commerce è associato a uno o più listini prezzi in Commerce Optimizer. Esportazione di prezzi di siti Web e gruppi di clienti come listini prezzi e inserimenti di prezzi
- **Gruppi di clienti → Varianti di prezzo**: i prezzi dei gruppi di clienti Commerce vengono visualizzati come voci aggiuntive nei listini prezzi pertinenti

Dopo che Commerce Optimizer ha acquisito i dati, puoi configurare:

- **Visualizzazioni catalogo e criteri** in Commerce Optimizer (per la creazione di sottoinsiemi specifici per area geografica, marchio o cliente)
- **Individuazione prodotto** (ricerca, facet, regole di merchandising)
- **Consigli di prodotto**

Quando abiliti il connettore, l’istanza Adobe Commerce rimane il sistema di registrazione per i dati di catalogo e prezzo. Quando si aggiornano i dati in Commerce, il connettore sincronizza tali aggiornamenti con l&#39;istanza [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Per informazioni dettagliate sulla configurazione di Commerce Optimizer, consulta [[!DNL Adobe Commerce Optimizer] Strumenti di merchandising](../optimizer/overview.md#quick-tour).

## Flussi di lavoro tipici {#typical-workflows}

Questi flussi di lavoro descrivono come i team configurano e utilizzano il connettore Adobe Commerce Optimizer. Per informazioni dettagliate su come impostare l&#39;integrazione e abilitare questi flussi di lavoro, vedere [Introduzione](get-started.md).

### Configurazione iniziale {#initial-setup}

1. **Installa il pacchetto del connettore in Adobe Commerce** utilizzando il Compositore:

   `composer require adobe-commerce/commerce-data-export-aco-adapter`

1. **Configurare l&#39;autenticazione e i dettagli dell&#39;ambiente** in Commerce Admin o tramite CLI:

   ```terminal
   bin/magento aco:config:init \
     --org_id=<your-org> \
     --tenant_id=<your-tenant> \
     --client_id=<your-client-id> \
     --client_secret=<your-secret> \
     --region=na1 \
     --type=production
   ```

1. **Mappatura ambiti Commerce a Commerce Optimizer:**

   - Conferma quali siti Web e visualizzazioni dello store devono essere inclusi nell&#39;ambito
   - Assicurati che i gruppi di clienti e le regole di prezzo siano modellati come previsto

1. **Verifica connettività:**

   - Esegui una sincronizzazione dei test e verifica che Origini catalogo, Listini prezzi e prodotti iniziali siano visualizzati in Commerce Optimizer
   - Utilizzare la pagina Stato di sincronizzazione feed dati in Commerce e le dashboard di sincronizzazione dati in Commerce Optimizer per la convalida

### Sincronizzazione dei dati in corso {#ongoing-sync}

Dopo la configurazione iniziale, il connettore supporta:

- **Sincronizzazione catalogo completa** per la migrazione iniziale o modifiche strutturali di grandi dimensioni
- **Sincronizzazioni delta** per aggiornamenti continui quando cambiano prodotti o prezzi
- **Risincronizza comandi** per i feed di destinazione (incluse le categorie della versione 1.0.12):

   - `bin/magento saas:resync --feed=products`
   - `bin/magento saas:resync --feed=prices`
   - `bin/magento saas:resync --feed=categories`

### Configurare merchandising e vetrine {#merchandising-storefronts}

Quando i dati di Commerce sono disponibili in Commerce Optimizer, utilizza Commerce Optimizer Studio per collegare le esperienze di merchandising e vetrina al catalogo sincronizzato.

**Per configurare merchandising e storefront:**

1. **Creare visualizzazioni e criteri del catalogo** in Commerce Optimizer Studio:

   - Filtra il catalogo per marchio, regione, segmento di cliente o canale
   - Applicazione di regole di accesso ai dati per vetrina o partner

1. **Configurare l&#39;individuazione del prodotto e i consigli** nell&#39;interfaccia utente di Optimizer:

   - Creare regole di merchandising, facet, sinonimi e unità di consigli
   - Il connettore esegue l’offload di tutte le configurazioni di ricerca e consigli in Commerce Optimizer (le regole di Live Search e i consigli di prodotto in Commerce Admin non si applicano più a questi flussi)

1. **Connetti vetrine** a Commerce Optimizer:

   - Per una vetrina Commerce con tecnologia Edge Delivery Services, configura la vetrina per utilizzare il tenant Optimizer e la vista catalogo corretti e per chiamare gli endpoint di ricerca e consigli tramite l’API Merchandising
   - Per le vetrine di terze parti, utilizza API pubbliche o SDK di Optimizer per le chiamate di ricerca e consigli

   >[!NOTE]
   >
   >Per un esempio di integrazione di terze parti, vedere [Salesforce Commerce Connector for Commerce Optimizer](../optimizer/developer/salesforce-connector.md).

1. **Gestisci estrazione** sulla piattaforma esistente:

   - Carrello, pagamento, gestione degli ordini e account cliente in Adobe Commerce o in una piattaforma di terze parti
   - Utilizza App Builder e API Mesh per la consegna del carrello quando esegui l’integrazione con i sistemi di pagamento esterni

## Scenari supportati {#supported-scenarios}

Il connettore è progettato per i commercianti B2C con Adobe Commerce su implementazioni cloud e on-premise che desiderano adottare Commerce Optimizer senza ricostruire il back-end.

**Casi d&#39;uso comuni:**

- **Modernizzazione solo della vetrina**
Mantenere il backend Commerce esistente, spostare PLP/Search/PDP in vetrine Edge Delivery con tecnologia Commerce Optimizer

- **Scalabilità delle prestazioni di catalogo e ricerca**
Offload dell&#39;indicizzazione del catalogo e della ricerca nei servizi SaaS di Commerce Optimizer mantenendo la proprietà dei prodotti e dei prezzi in Commerce

- **Adozione SaaS incrementale**
Utilizza il connettore come punto di partenza per Adobe Commerce as a Cloud Service + Optimizer, con un catalogo di Commerce componibile compatibile

## Responsabilità e prerequisiti per l’attuazione {#responsibilities-prerequisites}

Commerce è la fonte di verità per i prodotti, i prezzi e i gruppi di clienti. Apporta le modifiche in Commerce; il connettore le sincronizza con Commerce Optimizer.

**Commerce Optimizer è responsabile di:**

- Modellazione catalogo (origini catalogo, listini prezzi, visualizzazioni catalogo, criteri)
- Individuazione dei prodotti e raccomandazioni
- Metriche di Storefront, dashboard di sincronizzazione dati e rapporti sulle metriche di successo

**Il connettore non:**

- Modificare i flussi di carrello, pagamento o ordine di Commerce
- Provisioning automatico dei progetti storefront (Commerce Storefront/Edge Delivery tooling handle che)

**Prima di iniziare:**

- Verifica che Commerce soddisfi i requisiti minimi di versione e connettore dei servizi. Per ulteriori dettagli, vedere [Introduzione](get-started.md#prerequisites).
- Assicurati di disporre dell’accesso all’organizzazione IMS, di un’istanza [!DNL Adobe Commerce Optimizer] e delle credenziali e dei dettagli dell’area geografica necessari.

## Documentazione correlata {#related-documentation}

- Imposta l&#39;integrazione e abilita i flussi di lavoro chiave: [Guida introduttiva a Adobe Commerce Optimizer Connector](get-started.md)
- Scopri i concetti e l&#39;architettura di Commerce Optimizer: [Cos&#39;è Adobe Commerce Optimizer?](../optimizer/overview.md)
