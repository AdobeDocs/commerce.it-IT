---
title: Limiti e limiti di Adobe Commerce Optimizer
description: Scopri i limiti di licenza e i limiti del sistema di Adobe Commerce Optimizer. Pianifica la capacità, tieni traccia dell’utilizzo ed evita latenza e limitazione quando i limiti vengono superati.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
nudge: true
source-git-commit: 172fcbd659f4fe8868059d29ed335a5136af8d33
workflow-type: tm+mt
source-wordcount: '1410'
ht-degree: 0%

---

# Limiti e limiti

[!DNL Adobe Commerce Optimizer] applica **limiti di licenza** e **limiti di sistema** che definiscono la capacità utilizzabile dal progetto:

- **Limiti di licenza**—In base alla capacità acquistata; possono essere estesi acquistando pacchetti aggiuntivi.
- **Limiti di sistema**: sono stati corretti i limiti che proteggono le risorse di sistema e garantiscono prestazioni affidabili per tutti gli utenti.

Il tuo utilizzo deve rimanere entro questi limiti. Il loro superamento può causare un aumento della latenza e la limitazione delle richieste.

## Richiedi capacità aggiuntiva

I limiti di licenza possono essere aumentati acquistando i pacchetti di licenza descritti nella sezione [Limiti di licenza e limiti di sistema](#license-limits-and-system-boundaries) oppure negoziando licenze personalizzate per casi d&#39;uso univoci. Contatta il rappresentante del tuo account Adobe per discutere delle tue esigenze.

Per domande sui limiti del sistema, contatta il [Supporto Adobe](https://experienceleague.adobe.com/home?lang=en#support).

## Impedisci problemi di prestazioni

Segui queste best practice per restare entro i limiti ed evitare problemi operativi:

- **Rivedi i limiti**—Comprendi i [limiti di capacità](#license-limits-and-system-boundaries) prima di avviare nuove storefront o campagne.
- **Tieni traccia dell&#39;utilizzo**. Utilizza dashboard delle metriche o registri CDN incorporati.

## Limiti di licenza e limiti di sistema

Nelle tabelle seguenti vengono riepilogati i limiti di licenza e i limiti di sistema per area capacità e vengono fornite informazioni sull&#39;aggiunta di licenze aggiuntive per espandere la capacità, se applicabile.

### Limiti dell’ambiente

| **Ambiente** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| **Ambiente sandbox** | Numero di ambienti sandbox inclusi | 2 per istanza | Sì<p>Aggiungi una licenza di ambiente aggiuntiva per istanza</p> |
| **Ambiente di produzione** | Numero di ambienti di produzione inclusi | 1 per istanza | Sì<p>Aggiungi una licenza di ambiente aggiuntiva per istanza</p> |

{style="table-layout:auto"}

### Catalogo

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Tasso di acquisizione dei prodotti | Il numero di prodotti creati o aggiornati | Aggiornamenti a 1K al minuto<p>Massimo 100.000 aggiornamenti al giorno</p> | Sì<p>Aggiungi un pacchetto di licenza:</p><ul><li>5.000 aggiornamenti al minuto<br>Massimo 500.000 aggiornamenti al giorno</li> <li>10.000 aggiornamenti al minuto<br>Massimo 1 milione di aggiornamenti al giorno</li></ul><p>La capacità massima per l’acquisizione dei dati è di 1 milione di aggiornamenti al giorno.</p> |
| Dimensione payload del prodotto | La quantità massima di dati consentita durante la creazione, l’aggiornamento o l’acquisizione di informazioni di prodotto tramite l’API | 200 KB | No |
| Varianti catalogo | Il numero di visualizzazioni di un catalogo disponibili per gli utenti della vetrina,<p>conteggiati come (*Numero di visualizzazioni catalogo × Numero di listini prezzi fissi*)</p> | 100 varianti | Sì<p>Aggiungi pacchetto di licenze per 100 varianti di catalogo</p> |
| Prodotti in un&#39;unica origine catalogo | SKU supportate nel catalogo | 250.000 SKU | Sì<p>Aggiungi pacchetto di licenza SKU da 100.000</p> |
| Varianti per prodotto | Il numero di varianti di prodotto (dimensioni, combinazioni di colori) consentite per prodotto | 10K | No |
| Origini del catalogo | Il numero di contesti di dati del catalogo (ad esempio, impostazioni internazionali o origini dati come PIM ed ERP) | 50 | No |

{style="table-layout:auto"}

### Listino prezzi

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Listino prezzi | Numero di listini prezzi consentiti per istanza | In base al numero di [varianti catalogo](#catalog) | Sì<br>Aumenta varianti di catalogo |
| Sconti per record di prezzo | Il numero di sconti che è possibile applicare a un prezzo di prodotto all&#39;interno di un singolo listino prezzi dedicato | 10 | No |

{style="table-layout:auto"}

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
>**Gli utenti avanzati** possono accedere a [!DNL Adobe Express] direttamente o entro [!DNL Adobe Commerce Optimizer]. **Gli utenti Collaborator** possono accedere direttamente all&#39;applicazione [!DNL Adobe Express]. L&#39;utilizzo è disciplinato dalle [Condizioni di licenza Adobe Express con Firefly specifiche](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


>[!BEGINSHADEBOX &quot;Calcola utilizzo Dynamic Media&quot;]

L&#39;utilizzo di Dynamic Media tiene traccia delle richieste API pervenute nei componenti Product Visuals all&#39;interno di [!DNL Adobe Commerce Optimizer] per facilitare una delle azioni seguenti:

- **La consegna delle immagini utilizza un&#39;operazione Dynamic Media** per ogni occorrenza dei seguenti elementi:
   - **trasformazione immagine di base** di una risorsa digitale, ad esempio operazioni di ridimensionamento, ridimensionamento, conversione formato, compressione o ritaglio.
   - **consegna o download di immagini statiche** di tali risorse digitali o rendering di risorse digitali (diverso dal video)
- **La consegna di immagini avanzate richiede 20 operazioni Dynamic Media** per ogni consegna ottimizzata di una singola risorsa digitale generando automaticamente la rappresentazione dell&#39;immagine più appropriata per il dispositivo e il browser di un utente finale.
- **La distribuzione di video utilizza 20 operazioni Dynamic Media** per una singola consegna o download di un video o una variante trasformata di un video.

>[!ENDSHADEBOX]

>[!NOTE]
>
>I limiti di cui sopra riguardano le allocazioni di capacità e di utilizzo. Per una panoramica delle funzionalità e dei vincoli funzionali di Product Visuals, consulta [Visualizzazioni prodotto con AEM Assets](setup/product-visuals.md).

### Visualizzazioni e criteri del catalogo

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Visualizzazioni catalogo | Numero di sottoinsiemi configurabili del catalogo principale | In base al numero di [varianti catalogo](#catalog) | Sì<br>Aumenta varianti di catalogo |
| Criteri per visualizzazione catalogo | Numero di filtri dati consentiti | 10 | No |
| Valori degli attributi in un criterio | Numero di caratteristiche del prodotto che possono essere configurate per il filtro | 100 | No |

{style="table-layout:auto"}

### Vetrina catalogo

L’allocazione di base per le funzionalità di vetrina del catalogo è determinata in base al livello GMV (Gross Merchandise Value). La tabella indica l&#39;allocazione minima per ogni funzionalità.

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Percentuale di recupero catalogo | Numero di volte in cui un’API di catalogo viene chiamata al mese da un sistema (vetrina, sistema di transazioni, ERP o altro) per recuperare dati dal catalogo | Basato sul livello GMV<p>Allocazione minima: 10 milioni/mese</p> | Sì<p>Aggiungi 1 milione di richieste al mese pacchetti di licenze</p> |
| Richieste di contenuto | Richieste allo storefront per le visualizzazioni di pagina HTML o per le chiamate API JSON. Conteggiato come 1 visualizzazione pagina o 5 chiamate API. | Basato sul livello GMV<p>Allocazione minima: 2 milioni/mese</p> | Sì<p>Aggiungi pacchetto di licenze di 1 milione al mese</p> |
| Varianti GenAI per vetrina | Tolleranza per la generazione di contenuti basati su testo | Basato sul livello GMV<p>Allocazione minima: 1K variazioni/mese</p> | Sì<p>Acquistare separatamente i crediti IA generativi</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>La generazione dell&#39;immagine richiede una licenza [!DNL Adobe Firefly] fornita alla stessa organizzazione IMS di [!DNL Adobe Commerce Optimizer].


### Individuazione prodotto

I seguenti limiti si applicano alla ricerca di prodotti vetrina, all’elenco e alla configurazione del merchandising.

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Recupero del prodotto | Numero massimo di SKU per [!DNL Catalog Service] richiesta GraphQL durante il recupero dei dati prodotto con `products`, `productSearch`, `refineProduct` e `variants`. Suddividere le richieste più grandi in più chiamate. | 100 | No |
| Attributi filtrabili | Il numero di caratteristiche del prodotto (come colore, dimensioni, marchio o materiale) che possono essere abilitate per la navigazione e i facet su più livelli | 200 | No |
| Attributi ricercabili | Numero di caratteristiche del prodotto che possono essere indicizzate per la ricerca nel catalogo | 200 | No |
| Attributi ordinabili | Il numero di caratteristiche del prodotto disponibili come opzioni di ordinamento nelle pagine di ricerca e categoria. | 50 | No |
| Profondità di paginazione della ricerca | Numero massimo di prodotti raggiungibili tramite impaginazione ricerca (ad esempio, pagina 100 × 100 prodotti/pagina) | 10K | No |
| Facet | Il numero di attributi di prodotto filtrabili (come Marchio, Colore, Dimensione, Prezzo) che possono essere configurati per aiutare gli acquirenti a perfezionare i risultati di ricerca e sfogliare le categorie | 100<p>Deve essere un attributo filtrabile</p> | No |
| Opzioni per facet | Il numero di valori di attributi di prodotto filtrabili che gli acquirenti possono selezionare all’interno di un facet (ad esempio, &quot;Rosso&quot;, &quot;Blu&quot; per Colore; &quot;Piccolo&quot;, &quot;Medium&quot; per Dimensione) | 100 | Sì<p>Può aumentare tramite richiesta di supporto</p> |

{style="table-layout:auto"}

### Consigli

Per i consigli sui prodotti sono disponibili le seguenti funzionalità. Alcune funzionalità disponibili in altri prodotti Adobe Commerce non sono supportate in [!DNL Adobe Commerce Optimizer].

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** |
| --- | --- | --- | --- |
| Unità di consigli attive | Numero di componenti per consigli live nella vetrina (ad esempio &quot;Hanno visto anche i clienti&quot; o &quot;Potrebbe piacerti anche&quot;) | 50 | No |
| Inclusioni/esclusioni di categorie o attributi | Filtra i prodotti in base a un set specifico idoneo per i consigli | Non supportato | — |

{style="table-layout:auto"}

### Estensibilità

| **Capacità** | **Descrizione** | **Allocazione di base** | **Espandibile?** | **Note** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacità di creare estensioni e integrazioni native per il cloud | Basato sul livello GMV<p>Allocazione minima: 1 pacchetto/anno</p> | Sì<p>Aggiungi pacchetti aggiuntivi</p> | Per i limiti definiti per confezione, vedere:<ul><li>[Descrizione del prodotto App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html) per i limiti definiti per la confezione.</li><li>[Impostazioni e limitazioni di sistema](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) nelle *Guide di App Builder Runtime*.</li><li>[Requisiti di archiviazione App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce Optimizer] solution, follow these steps:

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
