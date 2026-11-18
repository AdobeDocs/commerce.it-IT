---
title: Limiti e limiti di Adobe Commerce as a Cloud Service
description: Scopri i limiti di licenza e i limiti di sistema di Adobe Commerce as a Cloud Service. Pianifica la capacità, tieni traccia dell’utilizzo ed evita latenza e limitazione quando i limiti vengono superati.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e [!DNL Adobe Commerce as a Cloud Service] (infrastruttura SaaS gestita da Adobe)."
nudge: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a13aaee57732f27b51a2d2acdd0ca3de364ee6ab
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%
---
# Limiti e limiti

[!DNL Adobe Commerce as a Cloud Service] applica **limiti di licenza** e **limiti di sistema** che definiscono la capacità utilizzabile dal progetto:

- **I limiti di licenza** si basano sulla capacità acquistata e possono essere estesi acquistando pacchetti aggiuntivi.
- **I limiti di sistema** sono limiti fissi che proteggono le risorse di sistema e garantiscono prestazioni affidabili per tutti gli utenti.

>[!IMPORTANT]
>
> Il tuo utilizzo deve rimanere entro questi limiti. Il loro superamento può causare un aumento della latenza e la limitazione delle richieste.

## Richiedi capacità aggiuntiva

Puoi aumentare i limiti di licenza acquistando i pacchetti di licenza descritti in [Limiti di licenza e limiti di sistema](#license-limits-and-system-boundaries) oppure negoziando licenze personalizzate per casi d&#39;uso univoci. Contatta il rappresentante del tuo account Adobe per discutere delle tue esigenze.

Per domande sui limiti del sistema, contatta il [Supporto Adobe](https://experienceleague.adobe.com/home?lang=en#support).

## Impedisci problemi di prestazioni

Segui queste best practice per restare entro i limiti ed evitare problemi operativi:

- **Rivedi i limiti** - Comprendi i [limiti di capacità](#license-limits-and-system-boundaries) prima di avviare nuove storefront o campagne.
- **Tieni traccia dell&#39;utilizzo** - Utilizza dashboard delle metriche integrate o registri CDN.

## Limiti di licenza e limiti di sistema

Nelle tabelle seguenti vengono riepilogati i limiti di licenza e i limiti di sistema per area capacità e vengono fornite informazioni sull&#39;utilizzo di licenze aggiuntive per espandere la capacità, se applicabile.

### Limiti dell’ambiente

| **Ambiente** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| **Ambiente sandbox** | Numero di ambienti sandbox inclusi | 2 per istanza | Sì<p>Aggiungi una licenza di ambiente aggiuntiva per istanza</p> |
| **Ambiente di produzione** | Numero di ambienti di produzione inclusi | 1 per istanza | Sì<p>Aggiungi una licenza di ambiente aggiuntiva per istanza</p> |

{style="table-layout:auto"}

### Catalogo

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Tasso di acquisizione dei prodotti | Il numero di prodotti creati o aggiornati | Aggiornamenti a 1K al minuto<p>Massimo 100.000 aggiornamenti al giorno</p> | Sì<p>Aggiungi un pacchetto di licenza:</p><ul><li>5.000 aggiornamenti al minuto<br>Massimo 500.000 aggiornamenti al giorno</li><li>10.000 aggiornamenti al minuto<br>Massimo 1 milione di aggiornamenti al giorno</li></ul><p>La capacità massima per l’acquisizione dei dati è di 1 milione di aggiornamenti al giorno.</p> |
| Dimensione payload del prodotto | La quantità massima di dati consentita durante la creazione, l’aggiornamento o l’acquisizione di informazioni di prodotto tramite l’API | 200 KB | No |
| Categorie | Il numero di categorie in cui i prodotti possono essere raggruppati | 6,000 | No |
| Numero di prodotti | Numero di SKU supportate nel catalogo | 250.000 SKU | Sì<p>Aggiungi pacchetto di licenza SKU da 100.000</p> |
| Varianti per prodotto | Il numero di varianti di prodotto (dimensioni, combinazioni di colori) consentite per prodotto | 10K | No |
| Visualizzazioni dello store | Numero di contesti di visualizzazione archivio (ad esempio, impostazioni internazionali) | 50 | No |
| SLA per visualizzare l’aggiornamento di un prodotto nella ricerca | Tempo necessario per la creazione/l’aggiornamento di un prodotto nella ricerca della vetrina | 10-15 minuti | No |

{style="table-layout:auto"}

### Pagamento

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Prodotti nel carrello | Numero di prodotti consentito per carrello | 650 | No |
| Indirizzi cliente per account | Numero di indirizzi cliente consentito per account | 2,000 | No |
| Regole prezzi carrello | Il numero di regole di prezzo del carrello che applicano sconti agli articoli nel carrello, in base a una serie di condizioni | 100,000 | No |
| Coupon | Numero di codici coupon utilizzati con le regole di prezzo del carrello | 1,000,000 | No |

{style="table-layout:auto"}

<!--
# Price books

# | **Capability** | **Description** | **Base allocation** | **Expandable?** |
# | --- | --- | --- | --- |
# | Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
# | Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}
-->

### [!DNL Product Visuals] limiti

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Visualizzazioni di prodotto Utenti avanzati | Utente concesso in licenza con funzionalità complete di gestione delle risorse digitali, tra cui strumenti di intelligenza artificiale, integrazioni [!DNL Adobe Express]/[!DNL Firefly] e condivisione di Content Hub, gestione delle attività DAM di base e funzioni avanzate native per il cloud per una efficienza ottimale. | 2 | Sì<p>Esegui l&#39;aggiornamento alla licenza [!DNL AEM Assets]</p> |
| Visualizzazioni prodotto per utenti di Collaborator | Accesso e utilizzo delle risorse tramite l&#39;integrazione AEM Commerce, creazione e modifica dei contenuti tramite [!DNL Adobe Express] e [!DNL Firefly] e, se abilitata, utilizzo delle risorse approvate tramite il portale Content Hub. | 2 | Sì<p>Esegui l&#39;aggiornamento alla licenza [!DNL AEM Assets]</p> |
| Archiviazione di Product Visuals | Spazio di archiviazione allocato per le risorse | 1 TB di storage | No |
| Utilizzo Dynamic Media | Indennità per le operazioni di elaborazione di elementi multimediali dinamici, che comprende:<ul><li>Consegna delle immagini</li><li>Imaging avanzato</li><li>Consegna video</li></ul><p>Per informazioni dettagliate, consulta *Calcolare l&#39;utilizzo di Dynamic Media* di seguito. | In base al valore lordo delle merci (GMV)<p>Dotazione minima: 5 milioni di operazioni al mese</p> | Sì<ul><li>Licenza di acquisto per operazioni aggiuntive</li><li>Esegui l&#39;aggiornamento alla licenza [!DNL AEM Assets]</li></ul> |
| Consegna video | Tolleranza per la consegna o il download di video | 300 video, 1 minuto per video | Sì<p>Esegui l&#39;aggiornamento alla licenza [!DNL AEM Assets]</p> |
| Generazione risorse | Accesso a [!DNL Adobe Express] e [!DNL Adobe Firefly] IA generativa per la creazione di immagini | Nessuno | Acquistare separatamente i crediti IA generativi |

{style="table-layout:auto"}

>[!NOTE]
>
>**Gli utenti avanzati** possono accedere a [!DNL Adobe Express] direttamente o entro [!DNL Adobe Commerce as a Cloud Service].
>
>**Gli utenti Collaborator** possono accedere direttamente all&#39;applicazione [!DNL Adobe Express]. L&#39;utilizzo è disciplinato dalle [Condizioni di licenza Adobe Express con Firefly specifiche](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).

>[!BEGINSHADEBOX &quot;Calcola utilizzo Dynamic Media&quot;]

L&#39;utilizzo di Dynamic Media tiene traccia delle richieste API pervenute nei componenti Product Visuals all&#39;interno di [!DNL Adobe Commerce as a Cloud Service] per facilitare una delle azioni seguenti:

- **La consegna delle immagini utilizza un&#39;operazione Dynamic Media** per ogni occorrenza dei seguenti elementi:
  - **trasformazione immagine di base** di una risorsa digitale, ad esempio operazioni di ridimensionamento, ridimensionamento, conversione formato, compressione o ritaglio.
  - **consegna o download di immagini statiche** di tali risorse digitali o rendering di risorse digitali (diverso dal video).
- **La consegna di immagini avanzate richiede 20 operazioni Dynamic Media** per ogni consegna ottimizzata di una singola risorsa digitale generando automaticamente la rappresentazione dell&#39;immagine più appropriata per il dispositivo e il browser di un utente finale.
- **La distribuzione di video utilizza 20 operazioni Dynamic Media** per una singola consegna o download di un video o una variante trasformata di un video.

>[!ENDSHADEBOX]

>[!NOTE]
>
>I limiti di cui sopra riguardano le allocazioni di capacità e di utilizzo. Per una panoramica delle funzionalità e dei vincoli funzionali di Product Visuals, consulta [Visualizzazioni prodotto con AEM Assets](../optimizer/setup/product-visuals.md).

<!--
### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |
| [Restricted access key assignment](setup/private-catalog-view.md) | Number of restricted access keys that can be assigned to a single catalog view | 3 | No |
| RSA key size (restricted access keys) | Minimum and maximum key strength accepted for a restricted access key | 2048-bit minimum, 8192-bit maximum | No |
| Restricted access keys | Key revocation propagation delay | Up to 5 minutes, due to caching. Tokens signed by a removed key are denied once the delay elapses. | Not applicable |

{style="table-layout:auto"}
-->

### Vetrina catalogo

L’allocazione di base per le funzionalità di vetrina del catalogo è determinata in base al livello GMV (Gross Merchandise Value). La tabella indica l&#39;allocazione minima per ogni funzionalità.

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Percentuale di recupero catalogo | Numero di volte in cui un’API di catalogo viene chiamata al mese da un sistema (vetrina, sistema di transazioni, ERP o altro) per recuperare dati dal catalogo | Basato sul livello GMV<p>Allocazione minima: 10 milioni/mese</p> | Sì<p>Aggiungi 1 milione di richieste al mese pacchetti di licenze</p> |
| Richieste di contenuto | Richieste allo storefront per le visualizzazioni di pagina HTML o per le chiamate API JSON. Conteggiato come 1 visualizzazione pagina o 5 chiamate API. | Basato sul livello GMV<p>Allocazione minima: 2 milioni al mese</p> | Sì<p>Aggiungi pacchetto di licenze di 1 milione al mese</p> |
| Varianti GenAI per vetrina | Tolleranza per la generazione di contenuti basati su testo | Basato sul livello GMV<p>Allocazione minima: 1K variazioni/mese</p> | Sì<p>Acquistare separatamente i crediti IA generativi</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>La generazione dell&#39;immagine richiede una licenza [!DNL Adobe Firefly] fornita alla stessa organizzazione IMS di [!DNL Adobe Commerce as a Cloud Service].

### Individuazione prodotto

I seguenti limiti si applicano alla ricerca di prodotti vetrina, all’elenco e alla configurazione del merchandising.

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- |---------------------------------------------------|
| Recupero del prodotto | Numero massimo di SKU per [!DNL Catalog Service] richiesta GraphQL durante il recupero dei dati prodotto con `products`, `productSearch`, `refineProduct` e `variants`. Suddividere le richieste più grandi in più chiamate. | 100 | No |
| Attributi filtrabili | Il numero di caratteristiche del prodotto (come colore, dimensioni, marchio o materiale) che possono essere abilitate per la navigazione e i facet su più livelli | 200 | No |
| Attributi ricercabili | Numero di caratteristiche del prodotto che possono essere indicizzate per la ricerca nel catalogo | 200 | No |
| Attributi ordinabili | Il numero di caratteristiche del prodotto disponibili come opzioni di ordinamento nelle pagine di ricerca e categoria. | 50 | No |
| Profondità di paginazione della ricerca | Numero massimo di prodotti raggiungibili tramite impaginazione ricerca (ad esempio, pagina 100 × 100 prodotti/pagina) | 10K | No |
| Facet | Il numero di attributi di prodotto filtrabili (come Marchio, Colore, Dimensione, Prezzo) che possono essere configurati per aiutare gli acquirenti a perfezionare i risultati di ricerca e sfogliare le categorie | 100<p>Deve essere un attributo filtrabile</p> | Sì<p>Può aumentare a 500 tramite richiesta di supporto</p> |
| Opzioni per facet | Il numero di valori di attributi di prodotto filtrabili che gli acquirenti possono selezionare all’interno di un facet (ad esempio, &quot;Rosso&quot;, &quot;Blu&quot; per Colore; &quot;Piccolo&quot;, &quot;Medium&quot; per Dimensione) | 100 | Sì<p>Può aumentare tramite richiesta di supporto</p> |

{style="table-layout:auto"}

### Consigli

Per i consigli sui prodotti sono disponibili le seguenti funzionalità. Alcune funzionalità disponibili in altri prodotti Adobe Commerce non sono supportate in [!DNL Adobe Commerce as a Cloud Service].

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Unità di consigli attive | Numero di componenti per consigli live nella vetrina (ad esempio &quot;Hanno visto anche i clienti&quot; o &quot;Potrebbe piacerti anche&quot;) | 50 unità attive per tipo di pagina per Consigli di prodotto, con ambito esplicito del modello di catalogo, se necessario | No |

{style="table-layout:auto"}
<!-- Talos complained about this even thought it was copied directly from the ACO version of this page. Commenting out for now, | Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | — | -->

### Estensibilità

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** | **Note** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacità di creare estensioni e integrazioni native per il cloud | Basato sul livello GMV<p>Allocazione minima: 1 pacchetto/anno</p> | Sì<p>Aggiungi pacchetti aggiuntivi</p> | Per i limiti definiti per confezione, vedere:<ul><li>[Descrizione del prodotto App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html).</li><li>[Impostazioni e limitazioni di sistema](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) nelle *Guide di App Builder Runtime*.</li><li>[Requisiti di archiviazione App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce as a Cloud Service] solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each)
-->
