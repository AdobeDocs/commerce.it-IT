---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: Scopri l'integrazione di  [!DNL Adobe Commerce Optimizer Connector] tra [!DNL Adobe Commerce] e [!DNL Adobe Commerce Optimizer] per la sincronizzazione del catalogo, la ricerca e la distribuzione in vetrina.
feature: Integration, Storefront, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 1037
ht-degree: 0%

---

# Connettore Adobe Commerce Optimizer

[!DNL Adobe Commerce Optimizer Connector] è un&#39;integrazione nativa di prima parte tra [!DNL Adobe Commerce] (cloud o locale) e [!DNL Adobe Commerce Optimizer]. Sincronizza i dati del catalogo e dei prezzi dagli archivi di [!DNL Adobe Commerce] in [!DNL Adobe Commerce Optimizer] in modo da poter:

- Potenti **Consigli e individuazione dei prodotti basati sull&#39;intelligenza artificiale**
- Esegui **storefront headless ad alte prestazioni** (inclusi gli storefront Commerce basati su [!DNL Edge Delivery Services])
- Analizza **prima e dopo** KPI e integrità della sincronizzazione dati in un&#39;unica posizione

[!DNL Adobe Commerce] rimane il tuo sistema di record per prodotti, prezzi e struttura del catalogo. [!DNL Adobe Commerce Optimizer] diventa il tuo livello di esperienza e merchandising, fornendo risultati rapidi e rilevanti per qualsiasi vetrina o canale connesso.

## Vantaggi chiave {#key-benefits}

| Beneficio | Che cosa significa per te |
| --- | --- |
| **Nessun connettore personalizzato da compilare** | Utilizza un’integrazione supportata di prima parte invece di scrivere e mantenere feed e script personalizzati. |
| **Time to value più rapido con[!DNL Adobe Commerce Optimizer]** | Attiva Ricerche IA, consigli e vetrine headless sopra la distribuzione [!DNL Adobe Commerce] esistente. |
| **Allineato con ambiti Commerce** | Mappa automaticamente siti Web, visualizzazioni store e gruppi di clienti in [!DNL Adobe Commerce Optimizer] costrutti catalogo (origini catalogo e listini prezzi). |
| **Visibilità operativa** | Monitora lo stato di integrità dei feed, gli orari dell&#39;ultima sincronizzazione e lo stato per SKU da una visualizzazione [!UICONTROL Data Feed Sync Status] dedicata. |
| **Percorso pronto per il futuro verso SaaS** | Fornisce un percorso di modernizzazione a basso rischio da PaaS verso [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], senza una ripiattaforma. |

## Architettura del connettore {#connector-architecture}

Nel diagramma seguente viene illustrata l&#39;architettura end-to-end del connettore, da [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer] e in uscita verso gli storefront e i sistemi di pagamento.

![Diagramma dell&#39;architettura end-to-end del connettore Adobe Commerce Optimizer](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

In questa architettura:

- [!DNL Adobe Commerce] (su cloud o on-premise) è il sistema del produttore di record e feed
- Il connettore esporta i feed di catalogo, prezzo e categoria
- [!DNL Adobe Commerce Optimizer] acquisisce e normalizza i dati di feed in Origini catalogo, Listini prezzi e Visualizzazioni catalogo
- Storefront (Commerce storefront su [!DNL Edge Delivery Services] o build headless personalizzate) chiama [!DNL Commerce Optimizer] API GraphQL per l&#39;individuazione e i consigli e chiama [!DNL Adobe Commerce] o un&#39;altra piattaforma di terze parti connessa per le operazioni di carrello e pagamento

## Funzionamento del connettore con [!DNL Adobe Commerce]

[!DNL Adobe Commerce Optimizer Connector] funziona utilizzando gli ambiti Commerce esistenti (siti Web e viste store) e la segmentazione dei clienti per popolare il modello di catalogo [!DNL Adobe Commerce Optimizer]:

![Mappatura dei dati di Commerce a Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Visualizzazioni store → Origini catalogo** — Ogni visualizzazione store diventa un Source catalogo separato in [!DNL Adobe Commerce Optimizer]. Tale origine include attributi di prodotto localizzati ed eventuali dati specifici della vista archivio
- **Siti Web → Listini prezzi**: ogni sito Web [!DNL Adobe Commerce] è associato a uno o più listini prezzi in [!DNL Commerce Optimizer]. Esportazione di prezzi di siti Web e gruppi di clienti come listini prezzi e inserimenti di prezzi
- **Gruppi di clienti → Varianti di prezzo** — [!DNL Adobe Commerce] i prezzi dei gruppi di clienti vengono visualizzati come voci aggiuntive nei registri prezzi pertinenti

Dopo che [!DNL Commerce Optimizer] ha acquisito i dati, puoi configurare:

- **Visualizzazioni catalogo e criteri** in [!DNL Adobe Commerce Optimizer] Studio (per la creazione di sottoinsiemi specifici per area geografica, marchio o cliente)
- **Individuazione prodotto** (ricerca, facet, regole di merchandising)
- **[!DNL Product Recommendations]**

Quando abiliti il connettore, l&#39;istanza [!DNL Adobe Commerce] rimane il sistema di registrazione per i dati di catalogo e prezzo. Quando si aggiornano i dati in [!DNL Adobe Commerce], il connettore sincronizza tali aggiornamenti nell&#39;istanza [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Per informazioni dettagliate sulla configurazione di [!DNL Adobe Commerce Optimizer], vedere [[!DNL Adobe Commerce Optimizer] Strumenti di merchandising](../optimizer/overview.md#quick-tour).

## Flussi di lavoro tipici {#typical-workflows}

Questi flussi di lavoro descrivono la configurazione e l&#39;utilizzo di [!DNL Adobe Commerce Optimizer Connector] da parte dei team. Per informazioni dettagliate su come impostare l&#39;integrazione e abilitare questi flussi di lavoro, vedere [Introduzione](get-started.md).

### Configurazione iniziale {#initial-setup}

Consulta [Passaggi di configurazione](./get-started.md#configuration-steps) nella _Guida introduttiva_.

### Sincronizzazione dei dati in corso {#ongoing-sync}

Dopo la configurazione iniziale, il connettore supporta:

- **Sincronizzazione catalogo completa** per la migrazione iniziale o modifiche strutturali di grandi dimensioni
- **Sincronizzazioni delta** per aggiornamenti continui quando cambiano prodotti o prezzi
- **Risincronizza comandi** per i feed di destinazione

I seguenti feed sono disponibili per [!DNL Adobe Commerce Optimizer Connector]:

- `products` - dati prodotti
- `productAttributes` - metadati per attributi prodotto
- `priceBooks` - listini prezzi
- `prices` - prezzi dei prodotti
- `categories` - dati categorie

Per ulteriori dettagli, vedi i seguenti argomenti:

- Per [!DNL Adobe Commerce] operazioni di risincronizzazione CLI, vedere il comando di risincronizzazione [CLI](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}
- [[!DNL Commerce Optimizer Connector] moduli ed endpoint di feed](reference/connector-reference.md)
- [Mappatura dei campi per i feed del connettore](reference/field-mapping.md)

### Configurare merchandising e vetrine {#merchandising-storefronts}

Quando i dati di [!DNL Adobe Commerce] saranno disponibili in [!DNL Adobe Commerce Optimizer], utilizza [[!DNL Commerce Optimizer] Studio](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour) per collegare le esperienze di merchandising e vetrina al catalogo sincronizzato.

**Per configurare merchandising e storefront in [!DNL Commerce Optimizer] Studio:**

1. **Crea visualizzazioni catalogo e criteri** dal menu [!UICONTROL Store setup].

   - Filtra il catalogo per marchio, regione, segmento di cliente o canale
   - Applicazione di regole di accesso ai dati per vetrina o partner

1. **Configurare l&#39;individuazione del prodotto e i consigli** dal menu [!UICONTROL Merchandising].

   - Creare regole di merchandising, facet, sinonimi e unità di consigli
   - Il connettore esegue l&#39;offload di tutta la configurazione di ricerca e consigli a [!DNL Commerce Optimizer] ([!DNL Live Search] regole e [!DNL Product Recommendations] nell&#39;amministrazione di Commerce non si applicano più a questi flussi)

1. **Connetti vetrine** a [!DNL Commerce Optimizer]:

   - Per una vetrina Commerce con tecnologia [!DNL Edge Delivery Services], configura la vetrina per utilizzare il tenant Optimizer e la vista catalogo corretti e per chiamare gli endpoint di ricerca e consigli tramite l&#39;API Merchandising
   - Per le vetrine di terze parti, utilizza API pubbliche o SDK di Optimizer per le chiamate di ricerca e consigli

   >[!NOTE]
   >
   >Per un esempio di integrazione di terze parti, vedere [Salesforce Commerce Connector per [!DNL Adobe Commerce Optimizer]](../optimizer/developer/salesforce-connector.md).

1. **Gestisci estrazione** sulla piattaforma esistente:

   - Mantieni il carrello, il pagamento, la gestione degli ordini e gli account cliente in [!DNL Adobe Commerce] o in una piattaforma di terze parti
   - Utilizza [!DNL App Builder] e [!DNL API Mesh] per la consegna del carrello quando esegui l&#39;integrazione con i sistemi di pagamento esterni

## Scenari supportati {#supported-scenarios}

Il connettore è progettato per i commercianti B2C con [!DNL Adobe Commerce] distribuzioni su cloud e locali che desiderano adottare [!DNL Adobe Commerce Optimizer] senza ricreare il back-end.

**Casi d&#39;uso comuni:**

- **Modernizzazione solo della vetrina**
Mantieni il backend [!DNL Adobe Commerce] esistente, sposta PLP/Search/PDP in [!DNL Edge Delivery Services] storefront con tecnologia [!DNL Adobe Commerce Optimizer]

- **Scalabilità delle prestazioni di catalogo e ricerca**
Offload dell&#39;indicizzazione del catalogo e della ricerca nei servizi SaaS di [!DNL Adobe Commerce Optimizer] mantenendo la proprietà dei prodotti e dei prezzi in [!DNL Adobe Commerce]

- **Adozione SaaS incrementale**
Utilizza il connettore come punto di partenza verso [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], con un catalogo compatibile [!DNL Adobe Commerce] componibile

## Responsabilità e prerequisiti per l’attuazione {#responsibilities-prerequisites}

[!DNL Adobe Commerce] è la fonte di verità per prodotti, prezzi e gruppi di clienti. Apportare le modifiche in [!DNL Adobe Commerce]. Il connettore le sincronizza in [!DNL Adobe Commerce Optimizer].

**[!DNL Adobe Commerce Optimizer]è responsabile di:**

- Modellazione catalogo (origini catalogo, listini prezzi, visualizzazioni catalogo, criteri)
- Individuazione dei prodotti e raccomandazioni
- Metriche di Storefront, dashboard di sincronizzazione dati e rapporti sulle metriche di successo

**Il connettore non:**

- Modifica [!DNL Adobe Commerce] carrello, pagamento o flussi di ordini
- Provisioning automatico dei progetti storefront (Commerce Storefront / [!DNL Edge Delivery Services] handle di strumenti che)

**Prima di iniziare:**

- Verificare che [!DNL Adobe Commerce] soddisfi i requisiti minimi di versione e [!DNL Commerce Optimizer Connector]. Per ulteriori dettagli, vedere [Introduzione](get-started.md#requirements-to-use-the-integration).
- Assicurati di disporre dell’accesso all’organizzazione IMS, di un’istanza [!DNL Adobe Commerce Optimizer] e delle credenziali e dei dettagli dell’area geografica necessari.

## Documentazione correlata {#related-documentation}

- Configurare l&#39;integrazione e abilitare i flussi di lavoro chiave: [Introduzione a [!DNL Commerce Optimizer Connector]](get-started.md)
- Scopri i concetti e l&#39;architettura di [!DNL Adobe Commerce Optimizer]: [Cos&#39;è [!DNL Adobe Commerce Optimizer]?](../optimizer/overview.md)
- Comprendere il meccanismo di sincronizzazione, l&#39;inizializzazione e la gestione degli errori: [pipeline di sincronizzazione del connettore](connector-sync-pipeline.md)
- Mappatura dei dati a livello di campo per tutti i feed: [Mappatura dei campi per i feed del connettore](reference/field-mapping.md)
- Integra gli storefront headless tramite la codifica GraphQL e bundle: [Integrazione storefront headless](headless-storefront.md)
- Diagnostica problemi di sincronizzazione e configurazione: [Risoluzione dei problemi](troubleshooting.md)
