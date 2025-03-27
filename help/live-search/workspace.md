---
title: Configurazione di Live Search
description: L'area di lavoro  [!DNL Live Search]  viene utilizzata per configurare, gestire e monitorare le prestazioni di ricerca.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: 3d92f4afc3aef990f2e86e306f4c6c47324aed97
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Configurazione di Live Search

Nell&#39;area di lavoro è possibile configurare, gestire e monitorare le prestazioni di [!DNL Live Search]. Il menu nella parte superiore fornisce l’accesso agli strumenti in ogni area funzionale. Le funzioni disponibili riflettono la selezione del menu corrente.

![Workspace](assets/workspace.png)

## Raccolta dati

Per garantire che ogni area funzionale nell’area di lavoro contenga i dati corretti, devi configurare la raccolta dati in base all’implementazione della vetrina selezionata:

1. Luma - La raccolta dei dati è disponibile come strumento pronto all’uso.
1. Headless: la raccolta dei dati deve essere configurata manualmente, a seconda dell’implementazione in vetrina.

Se utilizzi una vetrina headless, consulta la seguente documentazione per ulteriori informazioni sugli eventi richiesti da aggiungere:

- [Eventi richiesti](events.md) per il dashboard di Live Search.
- [Agente di raccolta eventi storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) che deve essere aggiunto come prerequisito.
- [Esempi](https://github.com/adobe/commerce-events/tree/main/examples) della struttura degli eventi.

### Clienti del settore sanitario

Se sei un cliente del settore sanitario e hai installato l&#39;estensione [HIPAA Data Services](../data-connection/hipaa-readiness.md#installation), che fa parte dell&#39;estensione [Data Connection](../data-connection/overview.md), i dati dell&#39;evento storefront utilizzati da [!DNL Live Search] non vengono più acquisiti. Questo perché i dati dell’evento storefront vengono generati lato client. Per continuare l&#39;acquisizione e l&#39;invio di dati evento vetrina, riattivare la raccolta eventi per [!DNL Live Search]. Per ulteriori informazioni, consulta la [configurazione generale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services).

## Impostare l&#39;ambito

Inizialmente l&#39;[ambito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) di tutte le impostazioni [!DNL Live Search] è impostato su `Default Store View`. Se l&#39;installazione di [!DNL Commerce] include più visualizzazioni dello store, impostare **Ambito** sulla [visualizzazione dello store](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) in cui si applicano le impostazioni del facet.

## Opzioni menu

| Opzione | Descrizione |
|--- |--- |
| [Prestazioni](performance.md) | Il dashboard fornisce informazioni approfondite sulle prestazioni di ricerca del prodotto. |
| [Faceting](facets.md) | Filtraggio ad alte prestazioni che utilizza più dimensioni di valori di attributo per perfezionare i criteri di ricerca. |
| [Sinonimi](synonyms.md) | Estendi la portata della ricerca per includere le parole che gli acquirenti potrebbero usare per trovare prodotti diversi da quelli nel catalogo. |
| [Cerca nel merchandising](rules.md) | Forma l’esperienza di ricerca con regole logiche che attivano le azioni pianificate. Puoi promuovere, seppellire, fissare o nascondere i prodotti per calibrare i risultati della ricerca e supportare gli obiettivi aziendali. |
| [Merchandising categoria](category-merch.md) | Applica regole e merchandising intelligente a livello di categoria. |
| [GraphQL](graphql.md) | Gli sviluppatori che hanno effettuato l’accesso all’amministratore del tuo archivio possono comporre e verificare le query con i dati del catalogo effettivo. Per ulteriori informazioni, vai a [Panoramica di GraphQL](https://developer.adobe.com/commerce/services/graphql/live-search/) nella documentazione per gli sviluppatori di [!DNL Live Search]. |
| [Impostazioni](settings.md) | Determina il modo in cui i valori del facet di prezzo vengono raggruppati per intervallo di prezzi nella vetrina e imposta il linguaggio di indicizzazione. |

## Imposta attributi come ricercabili

Per produrre risultati con targeting elevato, controlla il set di attributi di prodotto [ricercabili](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`). Per garantire la rilevanza, rendi gli attributi ricercabili solo se contengono contenuto con un significato chiaro e conciso. Evitare di utilizzare attributi contenenti testo meno preciso e lungo, ad esempio `description`, che, sebbene abilitati per impostazione predefinita per la ricerca, possono ridurre la precisione dei risultati della ricerca. Ad esempio, se una persona cerca i &quot;pantaloncini corti&quot; e ci sono camicie con una descrizione che include il termine &quot;maniche corte&quot;, allora le camicie saranno incluse nei risultati della ricerca.

La procedura seguente illustra come consentire la ricerca di attributi:

1. In Amministrazione, vai a **Archivi** > *Attributo* > **Prodotto**.
1. Selezionare l&#39;attributo che si desidera rendere ricercabile, ad esempio `color`.
1. Selezionare **Proprietà storefront** e impostare **Usa nella ricerca** su `yes`.

   ![Workspace](assets/attribute-searchable.png)

[!DNL Live Search] rispetta anche il [peso](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search) di un attributo di prodotto, come impostato in Adobe Commerce. Gli attributi con un peso maggiore appariranno più in alto nei risultati di ricerca.

È sempre possibile cercare i seguenti attributi:

- `sku`
- `name`
- `categories`

[Facet](facets.md) sono attributi di prodotto definiti in [!DNL Live Search] per essere filtrabili. È possibile impostare qualsiasi attributo filtrabile come facet in [!DNL Live Search], ma sono presenti [limiti](boundaries-limits.md) al numero di facet che è possibile cercare contemporaneamente.

[I sinonimi](synonyms.md) sono termini che puoi definire per aiutare gli utenti a trovare il prodotto corretto. Gli utenti alla ricerca di pantaloni potrebbero digitare &quot;pantaloni&quot; o &quot;pantaloni&quot;. È possibile impostare sinonimi in modo che questi termini di ricerca portino gli utenti ai risultati &quot;pantaloni&quot;.

## Impostazioni configurazione Commerce

Nella sezione seguente vengono descritte le impostazioni di configurazione di Commerce supportate e non supportate per [!DNL Live Search].

### Valori di configurazione supportati

>[!IMPORTANT]
>
>Si consiglia vivamente di utilizzare i widget di elenco prodotti, abilitati per impostazione predefinita in Live Search 4.0.0. I widget sono destinati a sostituire completamente l’implementazione dell’adattatore nelle versioni future. Per ulteriori informazioni, consulta [abilitare i widget dell&#39;elenco prodotti](install.md#enable-product-listing-widgets).

| Impostazione configurazione Commerce | Descrizione | Supportato da Popover | Supportato dall&#39;adattatore |
|---|---|---|---|
| Archivi > Configurazione > Catalogo > Catalogo > Ricerca nel catalogo > Consenti tutti i prodotti per pagina | Se è impostato su `Yes`, include l&#39;opzione `ALL` nel controllo &quot;Mostra per pagina&quot;. | Sì. Max. 500 prodotti | Sì. Max. 500 prodotti |
| Archivi > Configurazione > Catalogo > Catalogo > Ricerca nel catalogo > Lunghezza minima query | Numero minimo di caratteri consentito in una ricerca nel catalogo. | Sì | Sì |
| Archivi > Configurazione > Catalogo > Catalogo > Ricerca nel catalogo > Prodotti per pagina sulla griglia Valori consentiti | Determina il numero di prodotti visualizzati in Visualizzazione griglia. | Sì | Sì |
| Archivi > Configurazione > Catalogo > Catalogo > Ricerca nel catalogo > Prodotti per pagina sulla griglia Valore predefinito | Determina il numero di prodotti visualizzati per pagina per impostazione predefinita nella visualizzazione griglia. | Sì. Max. 500 prodotti | Sì. Max. 500 prodotti |
| Negozi > Configurazione > Catalogo > Inventario > Visualizza prodotti esauriti | Visualizza i prodotti esauriti. | Sì | Sì |
| Archivi > Configurazione > Valuta > Valuta di visualizzazione predefinita | Valuta principale utilizzata per visualizzare i prezzi. | Sì | Sì |
| Archivi > Configurazione > Generale > Impostazione divisa > Opzioni divisa > Divisa di base | La valuta principale utilizzata per tutte le transazioni di pagamento online. | Sì | Sì |

I prezzi nella pagina di elenco dei prodotti Widget e nel popover vengono convertiti nella valuta di visualizzazione predefinita utilizzando i tassi di valuta configurati.

### Valori di configurazione non supportati

| Impostazione configurazione Commerce | Descrizione | Note |
|---|---|---|
| Archivi > Configurazione > Catalogo > Storefront > Modalità elenco | Determina il formato dell&#39;elenco dei risultati della ricerca. | Esegue correttamente il rendering, ma per alcune interazioni di pagina gli eventi non vengono inviati |
| Archivi > Configurazione > Catalogo > Catalogo > Ricerca nel catalogo > Lunghezza massima query | Numero massimo di caratteri consentito in una ricerca nel catalogo. | Non implementato; Search Services accetta fino a 255 caratteri |
| Configurazione > Vendite > Imposta > Impostazioni visualizzazione prezzo > Visualizza prezzi prodotto nel catalogo | Determina se i prezzi dei prodotti pubblicati nel catalogo includono o escludono le imposte o mostrano due versioni del prezzo: una con e l&#39;altra senza imposte |  |
| Negozi > Configurazione > Catalogo > Vetrina > Elenco prodotti Ordina per | Determina l&#39;ordinamento dell&#39;elenco dei risultati della ricerca. | Non si applica al [!DNL Live Search] [widget pagina elenco prodotti](plp-styling.md) |

### Termini di ricerca

[!DNL Live Search] supporta [reindirizzamenti dei termini di ricerca](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html) nelle implementazioni in cui Adobe Commerce gestisce il routing, ad esempio su Luma e altri temi basati su php.
