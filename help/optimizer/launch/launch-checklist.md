---
title: Elenco di controllo per Launch
description: Scopri come convalidare configurazione, vetrina, SEO, CDN, integrazioni, sicurezza, analisi e test per  [!DNL Adobe Commerce Optimizer]  produzione.
solution: Commerce
feature: Integration, Storefront, Search, Catalog Management, Personalization
feature-set: Commerce
role: Admin, Developer
level: Intermediate
topic: Administration
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 37b8b8a334ca11daacfd3da03b0441e77329e2e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---


# Elenco di controllo di Launch

Utilizzare questo elenco di controllo per verificare che il progetto di produzione [!DNL Adobe Commerce Optimizer] sia configurato, testato e pronto per l&#39;avvio. Lavora in ogni sezione con il tuo team e tieni traccia del completamento nel tuo piano di progetto o nel tracker. Per le funzionalità del prodotto e le aree dell&#39;interfaccia utente a cui si fa riferimento di seguito, consulta la [[!DNL Adobe Commerce Optimizer] documentazione](../overview.md).

## Caso d’uso e architettura {#use-case}

Usa questo elenco di controllo quando distribuisci un&#39;esperienza B2C che combina [!DNL Adobe Commerce Optimizer] e Edge Delivery Services (EDS) con un&#39;istanza Adobe Commerce on Cloud esistente.

In genere, la soluzione include i seguenti componenti:

- **Cloud**: Adobe Commerce on Cloud gestisce i dati del catalogo, i clienti, le risorse e i flussi di acquisto (pagamento, gestione degli ordini, spedizione e così via).
- **Optimizer**—[!DNL Adobe Commerce Optimizer] offre esperienze di merchandising.
- **Storefront**: Adobe Commerce Storefront su Edge Delivery Services fornisce l&#39;interfaccia utente.
- **Servizi di terze parti**—Fornitori di pagamenti, spedizioni e imposte.
- **App Builder**—Estensibilità.
- **Mesh API**: routing della richiesta.

## Verifica Adobe Commerce su Cloud {#verify-cloud}

Verifica che il tuo ambiente Adobe Commerce on Cloud sia pronto per la produzione.

▢ L&#39;istanza cloud è [predisposta](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/start/new-project).
▢ I test e i dati fittizi vengono rimossi dall&#39;istanza.
I dati di produzione di ▢ sono caricati nell&#39;istanza.
▢ Conosci l&#39;[endpoint GraphQL](https://developer.adobe.com/commerce/webapi/graphql/).
▢ L&#39;istanza soddisfa i requisiti di [ready-for-launch](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/launch/checklist).

## Verifica istanza Commerce Optimizer {#verify-optimizer}

Verificare che l&#39;istanza di produzione di [!DNL Adobe Commerce Optimizer] sia configurata correttamente.

▢ L&#39;istanza di produzione è attiva. Per informazioni su come eseguire il provisioning, consulta [Introduzione](../get-started.md).
▢ L&#39;istanza si trova nell&#39;area corretta.
▢ Il tipo di ambiente è Produzione.
▢ Conosci l&#39;ID organizzazione, l&#39;ID client, l&#39;URL di acquisizione e l&#39;URL di Commerce Optimizer. Consulta [Introduzione](../get-started.md).
▢ I limiti configurati corrispondono ai valori confermati dal tuo Adobe Customer Technical Advisor (CTA).
▢ Gli artefatti di test e i dati fittizi sono stati rimossi dall&#39;istanza.

## Verifica sito vetrina {#verify-storefront-site}

Verifica che il tuo sito di vetrina Edge Delivery Services esista e che l&#39;accesso sia limitato.

▢ Il sito storefront esiste. Vedi [Creare una vetrina](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/).
▢ Il nome del sito è noto.
▢ Solo gli utenti autorizzati dispongono di [autorizzazioni per la pubblicazione](https://tools.aem.live/tools/user-admin/index.html).
▢ Solo gli utenti autorizzati dispongono di [autorizzazioni per l&#39;authoring](https://docs.da.live/administrators/guides/permissions).

## Verificare l’integrazione di Cloud e Optimizer {#cloud-optimizer-integration}

Verificare che Adobe Commerce su Cloud e [!DNL Adobe Commerce Optimizer] si scambino correttamente i dati.

### Su Adobe Commerce

Completa questi controlli nel progetto Cloud.

▢ Il connettore Commerce Optimizer è [installato e configurato](../../aco-connector/get-started.md).
▢ Il comando CLI `aco:conf:show` conferma la connessione all&#39;istanza Commerce Optimizer di produzione. L’ID organizzazione, l’ID client, l’URL di acquisizione e l’URL di Commerce Optimizer corrispondono alla produzione.
▢ Gli ambiti di sincronizzazione nella [configurazione di esportazione](../../aco-connector/get-started.md) corrispondono ai requisiti.
▢ [Stato sincronizzazione feed dati](../../aco-connector/get-started.md) conferma l&#39;esportazione dei dati dall&#39;istanza Cloud.

### In Commerce Optimizer

Completare questi controlli nell&#39;interfaccia utente [!DNL Adobe Commerce Optimizer].

▢ Il [dashboard di sincronizzazione dati](../setup/data-sync.md) mostra i dati ricevuti. Prodotti, prezzi e attributi vengono visualizzati per Catalog Service, Product Discovery e Recommendations.
▢ [I listini prezzi](../setup/pricebooks.md) sono creati automaticamente dai gruppi di clienti su Cloud.
▢ [Sono presenti visualizzazioni catalogo](../setup/catalog-view.md) di cui si conoscono gli ID.
▢ [I criteri](../setup/policies.md) esistono e conosci i loro ID.
▢ [Facet](../merchandising/facets/overview.md) configurati.
▢ [Sinonimi](../merchandising/synonyms/overview.md) configurati.
▢ [Le regole di merchandising](../merchandising/rules/overview.md) sono configurate.
▢ [Il faceting del prezzo e il linguaggio di ricerca](../settings.md) soddisfano le tue esigenze quando utilizzi queste funzioni.
▢ [I prodotti consigliati](../merchandising/recommendations/create.md) esistono e si comportano come previsto nell&#39;anteprima.
▢ [I dati sulle prestazioni di ricerca](../manage-results/search-performance.md) sono visualizzati in *Admin*.
▢ [I dati sulle prestazioni dei consigli](../manage-results/recommendation-performance.md) sono visualizzati in *Admin*.

## Verifica dell’integrazione di storefront e Cloud {#storefront-cloud-integration}

Verifica che la vetrina legga dall’endpoint Adobe Commerce GraphQL corretto.

### Su Adobe Commerce

▢ pacchetti di compatibilità Storefront sono [installati](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).

### Nella vetrina

▢ L&#39;impostazione della vetrina `commerce-core-endpoint` punta al tuo [endpoint Cloud GraphQL](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/).
▢ Se utilizzi Mesh API come proxy per Cloud GraphQL, `commerce-core-endpoint` punta all&#39;endpoint Mesh API invece dell&#39;endpoint GraphQL Cloud.

## Verifica dell’integrazione di storefront e Optimizer {#storefront-optimizer-integration}

Conferma le impostazioni Commerce Optimizer nella configurazione della vetrina.

▢ La vetrina utilizza le [impostazioni Commerce Optimizer](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/) corrette.
▢ `adobe-commerce-optimizer` è `true`.
▢ `commerce-endpoint` punta all&#39;endpoint Commerce Optimizer GraphQL di produzione o all&#39;endpoint Mesh API quando si utilizza Mesh API.
▢ `headers.cs.AC-view-ID` contiene l&#39;ID della vista catalogo dell&#39;istanza di Commerce Optimizer di produzione.

## Verificare i servizi di terze parti su Cloud {#third-party-services}

Conferma le integrazioni in esecuzione sul tuo sistema di e-commerce host (non in [!DNL Adobe Commerce Optimizer]).

▢ **Pagamenti:** Il gateway dei pagamenti è attivo e testato (Stripe, PayPal, Adyen e così via).
▢ **Spedizione:** Le connessioni API per la spedizione funzionano (UPS, FedEx e così via).
▢ **Spedizione:** La piattaforma di evasione è connessa e testata (ad esempio, ShipStation).
▢ **Imposta:** L&#39;integrazione del calcolo delle imposte è convalidata (Avalara, TaxJar e così via).
▢ **Imposta:** La sincronizzazione del software di accounting funziona (QuickBooks e così via).
▢ **L&#39;inventario:** l&#39;integrazione di PIM, ERP o Gestione inventario è stata testata e sincronizzata.
▢ **Architettura:** Il sistema di e-commerce host gestisce il pagamento, la spedizione, le imposte e l&#39;inventario (non [!DNL Adobe Commerce Optimizer]).
▢ **Architettura:** Mesh API e App Builder rimangono sincronizzati tra il sistema commerce host e [!DNL Adobe Commerce Optimizer].
▢ **E-mail:** La consegna delle e-mail transazionali funziona (conferma ordine, spedizione e così via).
▢ **E-mail:** I modelli e-mail corrispondono al tuo marchio e utilizzano i collegamenti corretti.

## Verificare App Builder e Mesh API {#app-builder-mesh}

Conferma la configurazione dell’estensibilità per la produzione.

### App Builder

▢ L&#39;area di lavoro di produzione include tutte le configurazioni e i servizi richiesti.
▢ L&#39;app di produzione passa il test tra gli scenari di build.
▢ I limiti e i limiti del prodotto sono stati rivisti e confermati in base alla [descrizione del prodotto Adobe Developer App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html){target="_blank"} e alle [impostazioni e limitazioni del sistema App Builder](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings){target="_blank"}.
▢ L&#39;app di produzione utilizza gli endpoint di produzione App Builder.
▢ Le estensioni del pannello *Admin* personalizzate sono distribuite nell&#39;area di lavoro di produzione.

### Mesh API

▢ configurazioni e origini sono pronte per la produzione.

### Eventi

▢ Adobe I/O Events sono configurati e le sottoscrizioni sono verificate.

## Finalizzare l’esperienza della vetrina {#finalize-storefront}

Contenuto polacco, SEO, prestazioni, sicurezza e comportamento CDN prima del lancio.

### Contenuti e authoring

Conferma l’authoring dei componenti flusso di lavoro e vetrina.

▢ La revisione dell&#39;[elenco di controllo per la pubblicazione di AEM/EDS](https://www.aem.live/docs/go-live-checklist) è stata completata.
▢ L&#39;origine di creazione è basata su documenti o Universal Editor (e configurata).
▢ Il contenuto viene pubblicato utilizzando il ciclo di anteprima → pubblicazione.
▢ Controllo qualità contenuto e progettazione completato nel dominio `.aem.live`.
▢ Un favicon è configurato e servito correttamente dal sito.
▢ da.live e gli elementi visivi di prodotto utilizzano [configured](https://docs.da.live/administrators/guides/permissions) credenziali dedicate.
▢ gli abbandoni (carrello, pagamento, PDP, PLP, autenticazione, account) sono [personalizzati](../storefront.md) e testati.
▢ Il branding della vetrina riflette i token di progettazione CSS, la tipografia e i colori.

### SEO e indicizzazione

Conferma i metadati, gli URL e il comportamento di scansiona.

▢ I metadati del titolo del documento sono presenti per le pagine chiave (in particolare PDP e PLP). Consulta [Metadati SEO](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} nella _documentazione di Adobe Commerce Storefront_.
▢ PDP includono [metadati e dati strutturati](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/metadata/){target="_blank"} (ad esempio, JSON-LD).
▢ I formati degli URL di prodotto sono coerenti (ad esempio, `domain/product-name`).
▢ URL personalizzati reindirizzati a URL canonici.
▢ Il progetto include `robots.txt` che consente l&#39;indicizzazione dove appropriata, fa riferimento a sitemap e blocca percorsi che non si desidera indicizzare (ad esempio, `/drafts`).
▢ [I file di reindirizzamento](https://www.aem.live/docs/redirects) coprono le modifiche degli URL dalla migrazione (ad esempio, dopo aver rimosso `.html`).
▢ Sitemap esiste ed è inviato alla console di Google Search in base alle esigenze.
▢ URL canonici restituiscono lo stato `2xx` (non `3xx` o `4xx`).
▢ siti multilingue includono `hreflang` tag in sitemap.
▢ Il report di copertura della console di Google Search è aggiornato.

### Pre-rendering

Conferma il rendering lato server dove abilitato.

Pre-rendering di ▢ attivato per le pagine chiave. Consulta [Pre-rendering per AEM](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-prerender/){target="_blank"} nella _documentazione di Adobe Commerce Storefront_.
▢ URL utilizzano lettere minuscole, pertanto il pre-rendering non interrompe i collegamenti.
L&#39;origine HTML ▢ include metadati e contenuto del corpo che confermano il funzionamento del pre-rendering.
Nelle impostazioni internazionali ▢ vengono visualizzate le pagine tradotte corrette, se applicabili.
▢ markup HTML aggiuntivo [configurato](https://www.aem.live/docs/redirects) in base alle esigenze.

### Prestazioni e monitoraggio

Confermare le linee di base delle prestazioni e il cablaggio di Analytics.

▢ La tua vetrina segue le [best practice per le prestazioni](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/performance/){target="_blank"} nella _documentazione di Adobe Commerce Storefront_.
▢ (facoltativo) Google Analytics e Google Tag Manager sono configurati.
L&#39;implementazione di ▢ [eventi Storefront](https://github.com/adobe/commerce-events/tree/main/examples/events/snowplow-debugger) è valida e i dati vengono visualizzati nei dashboard di [!DNL Live Search] e [!DNL Product Recommendations] in Adobe Commerce *Admin*.
▢ Il parametro di analisi `environment` nella [configurazione Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} è `"Testing"` durante lo sviluppo e `"Production"` durante il lancio. Consulta [Strumentazione di Analytics](https://experienceleague.adobe.com/developer/commerce/storefront/setup/analytics/instrumentation/){target="_blank"}.
I punteggi di ▢ Lighthouse soddisfano le tue destinazioni (ad esempio, `100` nelle pagine chiave) secondo le indicazioni contenute in questo argomento.

### Sicurezza e accesso

Conferma autorizzazioni e segreti.

▢ Le autorizzazioni appropriate sono configurate per il contenuto DA e i siti EDS. Consulta [Autorizzazioni DA.live](https://da.live/docs/administration/permissions) e [Impostazione dell&#39;autenticazione per l&#39;authoring](https://www.aem.live/docs/authentication-setup-authoring).
▢ È stato eseguito il provisioning dell&#39;integrazione degli elementi visivi del prodotto. Consulta [Panoramica dell&#39;accesso ad AEM Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/accessing/overview#).
I collegamenti per la reimpostazione della password ▢ nei modelli e-mail corrispondono alla configurazione di Edge Delivery Services. Vedi le domande frequenti sulla vetrina: [Cosa devo fare se i miei collegamenti del modello e-mail sono interrotti dopo la migrazione a Edge Delivery Services o Helix?](https://experienceleague.adobe.com/developer/commerce/storefront/troubleshooting/faq/#what-should-i-do-if-my-email-template-links-are-broken-after-migrating-to-edge-delivery-services-or-helix){target="_blank"}.
▢ Le chiavi di produzione per le integrazioni e i provider di pagamenti sono attive.
I domini ▢ sono inseriti nell&#39;elenco Consentiti e i webhook di back-end funzionano.

### CDN e caching

Conferma il comportamento di CDN, DNS e cache.

▢ La configurazione CDN utilizza l&#39;endpoint GraphQL di produzione (`yourproject.com/graphql`) per le estensioni e gli script Sidekick (ad esempio, la generazione di sitemap e l&#39;importazione di immagini).
▢ Quando utilizzi Adobe Commerce Fastly, è disponibile un token di eliminazione CDN e [la configurazione del sito](https://tools.aem.live/tools/cdn-setup/index.html) include `authToken` e `serviceId`.
▢ [La configurazione CDN](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/){target="_blank"} convalida la memorizzazione nella cache e l&#39;annullamento della validità.
▢ Per [impostazioni multi-store](https://experienceleague.adobe.com/developer/commerce/storefront/setup/seo/indexing/#multi-store-setups){target="_blank"}, le richieste Catalog Service e [!DNL Live Search] includono un buster della cache specifico per l&#39;archivio (ad esempio, un parametro di query o una regola CDN).
▢ L&#39;invalidazione push funziona in modo end-to-end (pubblica una modifica, quindi verifica nel dominio di produzione).
Il valore TTL DNS di ▢ è sufficientemente basso prima del cutover.
▢ i record A e CNAME DNS sono corretti per tutti i domini e i nomi host.
▢ È stato eseguito il provisioning e la verifica del certificato SSL/TLS per il dominio di produzione.
▢ `www` e i reindirizzamenti apex si comportano correttamente.

## Sicurezza e conformità {#security-compliance}

Confermare la postura di sicurezza e le attività di conformità.

▢ **SSL:** è installato un certificato SSL/TLS attendibile.
▢ **SSL:** HTTPS applicato a livello di sito.
▢ **Accesso:** Le password predefinite di *Amministratore* sono state modificate ed è attivo un criterio per password complessa. Vedere [!DNL Adobe Commerce Optimizer] [Gestione utenti e identità](../user-management.md).
▢ **Accesso:** L&#39;URL *Amministratore* non è predefinito.
▢ **Accesso:** L&#39;autenticazione a due fattori è abilitata per tutti gli utenti *Amministratore*.
▢ **Accesso:** Nessun utente amministratore inattivo o inutilizzato è associato al progetto.
▢ **Firewall:** Il firewall dell&#39;applicazione Web (WAF) è configurato e verificato.
▢ **PCI:** Test di penetrazione della sicurezza in produzione (ambito PCI) completato.
▢ **Analisi:** Lo strumento Adobe Security Scan è stato registrato ed è stata completata un&#39;analisi iniziale.
▢ **L&#39;accesso:** CORS consente solo origini approvate.
▢ **Conformità:** Il [modello di responsabilità condivisa](../shared-responsibility.md) per [!DNL Adobe Commerce Optimizer] è aggiornato e definisce chiaramente le responsabilità di Adobe rispetto a quelle dei clienti.
▢ **Conformità:** I criteri di privacy, il consenso dei cookie e i requisiti RGPD o CCPA sono verificati.

## Analisi e monitoraggio {#analytics-monitoring}

Confermare la misurazione e le linee di base.

▢ **RUM:** Real User Monitoring (RUM) è dotato di strumenti per il confronto prima e dopo.
▢ **Analytics:** la raccolta dati di Adobe Experience Platform è configurata (se applicabile).
▢ **Analytics:** ha verificato che i tag MarTech vengano attivati sul nome host di produzione.
▢ **Analytics:** Le analisi di base sono documentate; sono previste fluttuazioni successive all&#39;avvio (visualizzazioni di pagina, frequenza di rimbalzo e così via).
▢ **Eventi:** Il tracciamento delle conversioni funziona in modo completo (aggiunta al carrello → estrazione → conferma).

## Test {#testing}

Conferma la qualità prima e dopo il lancio.

▢ **Funzionale:** I flussi core funzionano da un&#39;estremità all&#39;altra: sfogliare → ricerca → filtrare → aggiungere al carrello → estrarre → creare l&#39;account.
▢ **Funzionale:** I gateway di pagamento accettano transazioni effettive e di test.
▢ **Funzionale:** Inserimento dell&#39;ordine, e-mail di conferma e lavoro di tracciamento degli ordini.
▢ **Funzionale:** Le opzioni di spedizione e i calcoli delle imposte sono accurati.
▢ **Funzionale:** I coupon, gli sconti e i programmi fedeltà si comportano come previsto.
▢ **UAT:** Test di accettazione utente completato per staging e produzione.
▢ **Prestazioni:** Test di carico e stress completati. I risultati sono disponibili in Adobe CTA o CSE.
▢ **Prestazioni:** Il tempo di caricamento della pagina è inferiore a tre secondi su desktop e dispositivi mobili.
▢ **Prestazioni:** I punteggi di Lighthouse soddisfano le destinazioni nelle pagine chiave (ad esempio, tramite PageSpeed Insights).
▢ **Prestazioni:** immagini, script e risorse sono ottimizzati.
▢ **Compatibilità:** Chrome, Firefox, Safari e Edge si comportano come previsto.
▢ **Compatibilità:** I layout reattivi funzionano su dispositivi mobili, tablet e desktop.
▢ **Compatibilità:** Prestazioni accettabili su 3G, 4G e Wi-Fi.
▢ **Accessibilità:** Un controllo di accessibilità è stato completato (WCAG, utilità di lettura dello schermo, navigazione da tastiera).
▢ **Funzionale:** È attivo un piano di monitoraggio 404 post-avvio.
▢ **UAT:** Esiste un piano di rollback e supera i test in caso di problemi di avvio.

## Giorno del lancio e post-lancio {#launch-post-launch}

Conferma le attività di comunicazione, supporto e follow-up.

▢ **Coordinazione lancio:** Adobe ha la data di lancio confermata; CTA ha ricevuto una notifica tramite e-mail.
▢ **Supporto:** Il numero di hotline P1 è registrato: US (+1) 800-497-0335, quindi premere 6 per Commerce.
▢ **Supporto:** Il team è addestrato ad aprire un ticket di supporto **prima** chiamando la hotline P1.
▢ **Dopo l&#39;avvio:** verificare i punteggi di Lighthouse nel dominio di produzione.
▢ **Dopo l&#39;avvio:** monitorare la console di Google Search per individuare eventuali errori di indicizzazione e scansiona.
▢ **Dopo l&#39;avvio:** monitora i report 404 e aggiungi reindirizzamenti per gli URL legacy a traffico elevato.
▢ **Dopo l&#39;avvio:** confermare i dati di analisi e MarTech relativi alla produzione.
▢ **Dopo l&#39;avvio:** Chiedi al tuo CTA, CSE o AM di abilitare il monitoraggio high-SLA.
▢ Esiste un piano di disaster recovery e supera i test.
▢ È in corso un processo per tenere traccia e aggiornare i pacchetti boilerplate e di estensione alle versioni correnti.
