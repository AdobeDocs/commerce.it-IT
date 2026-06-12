---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: Scopri  [!DNL Adobe Commerce Optimizer Connector] per la sincronizzazione del catalogo, la ricerca e la consegna in vetrina tra [!DNL Adobe Commerce] e [!DNL Adobe Commerce Optimizer].
feature: Integration, Storefront, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
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
source-git-commit: 23e4f419628a7838357752ecef0c242f1dcdd4c4
workflow-type: tm+mt
source-wordcount: 990
ht-degree: 0%

---

# [!DNL Adobe Commerce Optimizer Connector]

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
| **Allineato con ambiti Commerce** | Mappa automaticamente siti Web, visualizzazioni dello store e gruppi di clienti in [!DNL Adobe Commerce Optimizer] costrutti di catalogo (origini catalogo e listini prezzi). |
| **Visibilità operativa** | Monitora lo stato di integrità dei feed, gli orari dell&#39;ultima sincronizzazione e lo stato per SKU da una visualizzazione [!UICONTROL Data Feed Sync Status] dedicata. |
| **Percorso pronto per il futuro verso SaaS** | Fornisce un percorso di modernizzazione a basso rischio da PaaS verso [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], senza una ripiattaforma. |

## Architettura del connettore {#connector-architecture}

Nel diagramma seguente viene illustrata l&#39;architettura end-to-end del connettore, da [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer] e in uscita verso gli storefront e i sistemi di pagamento.

![Diagramma dell&#39;architettura end-to-end del connettore Adobe Commerce Optimizer](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

In questa architettura:

- [!DNL Adobe Commerce] (su cloud o on-premise) è il sistema del produttore di record e feed
- Il connettore esporta i feed di catalogo, prezzo e categoria
- [!DNL Adobe Commerce Optimizer] acquisisce e normalizza i dati di feed in Origini catalogo, Listini prezzi e Visualizzazioni catalogo
- Storefront (Commerce storefront su [!DNL Edge Delivery Services] o build headless personalizzate) chiama [!DNL Adobe Commerce Optimizer] API GraphQL per l&#39;individuazione e i consigli e chiama [!DNL Adobe Commerce] o un&#39;altra piattaforma di terze parti connessa per le operazioni di carrello e pagamento

## Funzionamento del connettore con [!DNL Adobe Commerce] {#how-the-connector-works-with-adobe-commerce}

[!DNL Adobe Commerce Optimizer Connector] funziona utilizzando gli ambiti Commerce esistenti (siti Web e viste store) e la segmentazione dei clienti per popolare il modello di catalogo [!DNL Adobe Commerce Optimizer]:

![Mappatura dei dati di Commerce a Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Visualizzazione archivio → Origini catalogo**. Ogni visualizzazione archivio diventa un Source catalogo separato in [!DNL Adobe Commerce Optimizer]. Tale origine include attributi di prodotto localizzati ed eventuali dati specifici della vista archivio
- **Siti Web → Listini prezzi**: ogni sito Web [!DNL Adobe Commerce] è associato a uno o più listini prezzi in [!DNL Adobe Commerce Optimizer]. Esportazione di prezzi di siti Web e gruppi di clienti come listini prezzi e inserimenti di prezzi
- **Gruppo di clienti → Varianti di prezzo** — [!DNL Adobe Commerce] la determinazione dei prezzi del gruppo di clienti viene visualizzata come voci aggiuntive nei listini prezzi pertinenti

Dopo che [!DNL Adobe Commerce Optimizer] ha acquisito i dati, puoi configurare:

- **Visualizzazioni catalogo e criteri** in [!DNL Adobe Commerce Optimizer] Studio (per la creazione di sottoinsiemi specifici per area geografica, marchio o cliente)
- **Individuazione prodotto** (ricerca, facet, regole di merchandising)
- **[!DNL Product Recommendations]**

Quando abiliti il connettore, l&#39;istanza [!DNL Adobe Commerce] rimane il sistema di registrazione per i dati di catalogo e prezzo. Quando si aggiornano i dati in [!DNL Adobe Commerce], il connettore sincronizza tali aggiornamenti nell&#39;istanza [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Per informazioni dettagliate sulla configurazione di [!DNL Adobe Commerce Optimizer], vedere [[!DNL Adobe Commerce Optimizer] Strumenti di merchandising](/help/optimizer/overview.md#quick-tour).

## Flussi di lavoro tipici {#typical-workflows}

Questi flussi di lavoro descrivono la configurazione e l&#39;utilizzo di [!DNL Adobe Commerce Optimizer Connector] da parte dei team. Per informazioni dettagliate su come impostare l&#39;integrazione e abilitare questi flussi di lavoro, vedere [Introduzione](/help/aco-connector/get-started.md).

### Configurazione iniziale {#initial-setup}

Consulta [Passaggi di configurazione](/help/aco-connector/get-started.md#configuration-steps) nella _Guida introduttiva_.

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

- Per [!DNL Adobe Commerce] operazioni di risincronizzazione CLI, vedere il comando di risincronizzazione [CLI](/help/data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}
- [[!DNL Adobe Commerce Optimizer Connector] moduli ed endpoint di feed](/help/aco-connector/reference/connector-reference.md)
- [Mappatura dei campi per i feed del connettore](/help/aco-connector/reference/field-mapping.md)

### Configurare merchandising e vetrine {#merchandising-storefronts}

Quando i dati di [!DNL Adobe Commerce] saranno disponibili in [!DNL Adobe Commerce Optimizer], utilizza [[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour) per collegare le esperienze di merchandising e vetrina al catalogo sincronizzato. I passaggi successivi tipici includono:

- **Visualizzazioni e criteri catalogo** — Definisci sottoinsiemi specifici per area geografica, marchio o cliente e regole di accesso dal menu [!UICONTROL Store setup]
- **Individuazione prodotti e consigli**: configurare ricerca, facet, regole di merchandising, sinonimi e unità di consigli nel menu [!UICONTROL Merchandising]. Il comportamento di ricerca e consigli è gestito in [!DNL Adobe Commerce Optimizer]; le impostazioni [!DNL Live Search] e [!DNL Product Recommendations] dell&#39;amministratore [!DNL Adobe Commerce] non sono più applicabili a questi flussi
- **Connessioni storefront** - Punta gli storefront Commerce su [!DNL Edge Delivery Services] o build headless di terze parti al tenant [!DNL Adobe Commerce Optimizer], alla vista catalogo e agli endpoint API Merchandising corretti. Per un esempio di integrazione di terze parti, vedere [Salesforce Commerce Connector per [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)
- **Estrai**: mantieni il carrello, l&#39;estrazione, la gestione degli ordini e gli account cliente su [!DNL Adobe Commerce] o su una piattaforma di terze parti connessa. Utilizza [!DNL App Builder] e [!DNL API Mesh] per la consegna del carrello quando necessario

Per istruzioni dettagliate sulla configurazione, consulta [Introduzione](/help/aco-connector/get-started.md) e [[!DNL Adobe Commerce Optimizer] Strumenti di merchandising](/help/optimizer/overview.md#quick-tour).

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

- Verificare che [!DNL Adobe Commerce] soddisfi i requisiti minimi di versione e [!DNL Adobe Commerce Optimizer Connector]. Per ulteriori dettagli, vedere [Introduzione](/help/aco-connector/get-started.md#requirements-to-use-the-integration).
- Assicurati di disporre dell’accesso all’organizzazione IMS, di un’istanza [!DNL Adobe Commerce Optimizer] e delle credenziali e dei dettagli dell’area geografica necessari.

## Ulteriori informazioni su questo argomento {#more-help-on-this-topic}

- Configurare l&#39;integrazione e abilitare i flussi di lavoro chiave: [Introduzione a [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md)
- Scopri i concetti e l&#39;architettura di [!DNL Adobe Commerce Optimizer]: [Cos&#39;è [!DNL Adobe Commerce Optimizer]?](/help/optimizer/overview.md)
- Comprendere il meccanismo di sincronizzazione, l&#39;inizializzazione e la gestione degli errori: [pipeline di sincronizzazione del connettore](/help/aco-connector/connector-sync-pipeline.md)
- Mappatura dei dati a livello di campo per tutti i feed: [Mappatura dei campi per i feed del connettore](/help/aco-connector/reference/field-mapping.md)
- Integra gli storefront headless tramite la codifica GraphQL e bundle: [Integrazione storefront headless](/help/aco-connector/headless-storefront.md)
- Diagnostica problemi di sincronizzazione e configurazione: [Risoluzione dei problemi](/help/aco-connector/troubleshooting.md)
