---
title: Panoramica di [!DNL Adobe Commerce as a Cloud Service]
description: Scopri le funzionalità e i vantaggi principali di  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
source-git-commit: d38066b6db7da5bb029391716063ed098be1f519
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# Panoramica di [!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] offre flessibilità, scalabilità ed efficienza consentendo alle aziende di fornire e scalare rapidamente le operazioni digitali e accelerare l&#39;innovazione. L&#39;infrastruttura nativa per il cloud di Adobe regola automaticamente le risorse per soddisfare i picchi di richieste di traffico, ordini e gestione dei cataloghi.

L&#39;immagine seguente evidenzia i prodotti che alimentano [!DNL Adobe Commerce as a Cloud Service]:

![[!DNL Adobe Commerce as a Cloud Service] stack di prodotto](./assets/product-stack.svg){align="center" zoomable="yes"}

>[!BEGINSHADEBOX]

![info](assets/Smock_InfoOutline_18_N.svg) Se desideri partecipare al programma di accesso anticipato [!DNL Adobe Commerce as a Cloud Service], completa [questo modulo](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4WOxhjY2doZPikS2hIbfmL5URFZXTE5TUk9PMUw0OFdOWTBNNlI3UTlNMS4u&amp;route=shorturl).

>[!ENDSHADEBOX]

## Architettura

Per una breve introduzione all&#39;architettura [!DNL Adobe Commerce as a Cloud Service], guarda il video seguente. Diagrammi che illustrano l’architettura sono forniti sotto il video.

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

Questo diagramma illustra il flusso di dati tra [!DNL Adobe Commerce as a Cloud Service] e tutte le soluzioni Adobe Experience Cloud.

Diagramma dell&#39;architettura ![[!DNL Adobe Commerce as a Cloud Service]](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Utilizza [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront) di Adobe con tecnologia Edge Delivery Services per creare in pochi minuti esperienze avanzate con semplici operazioni di authoring basato su documenti o di modifica visiva tramite Storefront Builder.

Commerce Storefront è completamente headless con un’architettura separata che fornisce tutti i servizi e i dati di merchandising tramite un livello API GraphQL. Questa architettura consente ai team di sviluppare i propri front-end in modo indipendente da Commerce Foundation, fornendo la flessibilità necessaria per creare e testare nuovi punti di contatto con le tecnologie emergenti.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] non supporta le vetrine Luma. Se esegui la migrazione da Adobe Commerce su Cloud o on-premise, consulta [vetrine esistenti](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts) per informazioni sulla transizione.

## Servizi di merchandising e servizi di pagamento

Adobe offre una ricca gamma di servizi di merchandising intelligenti e componibili per aiutarti a supportare i tuoi obiettivi aziendali chiave. Questi servizi forniscono anche API fondamentali per ottimizzare le prestazioni su larga scala.

- [Live Search](../live-search/overview.md) - Fornisci risultati più intelligenti, più veloci e rilevanti per gli acquirenti con questo strumento di ricerca basato sull&#39;intelligenza artificiale.
- [Consigli di prodotto](../product-recommendations/overview.md): aggiungi consigli basati sull&#39;intelligenza artificiale in base al comportamento degli acquirenti, alle tendenze popolari, alla somiglianza dei prodotti e altro ancora.
- [Servizi di merchandising basati su canali e criteri](../merchandising-services/overview.md): gestione di cataloghi di prodotti complessi e di grandi dimensioni con modellazione flessibile dei dati per fornire cataloghi di e-commerce altamente performanti e flessibili, allineati alla struttura aziendale e alle strategie go-to-market. Utilizza con [Commerce Optimizer](../optimizer/overview.md) per ottimizzare le prestazioni del catalogo e migliorare i tassi di conversione.
- [Servizi di pagamento](../payment-services/overview.md)—Aumenta la soddisfazione dei clienti offrendo diversi metodi di pagamento, incluse le rate di pagamento senza interessi e un&#39;unica vista per l&#39;elaborazione dei pagamenti, gli ordini e le fatture.

## Visualizzazioni prodotto

Gestione semplificata delle risorse grazie a un solido sistema DAM (Digital Asset Management) integrato con Adobe Experience Manager per la gestione dei contenuti rich media. In alternativa, il mini-DAM nativo fornisce strumenti di base per la gestione delle risorse digitali di archiviazione e gestione.

Per ulteriori informazioni, consulta [Gestione risorse](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration).

## Piattaforma sviluppatore

Adobe fornisce agli sviluppatori punti di estensione e strumenti completi per creare applicazioni che estendono le funzionalità di Commerce Foundation e si integrano con sistemi di terze parti (come CRM, ERPS e PIMS). Questi strumenti riducono il costo totale di proprietà della piattaforma nei seguenti modi:

- **Scalabilità**: le applicazioni possono essere scalate separatamente dal software principale, consentendo una maggiore efficienza e aggiornamenti semplificati.
- **Isolamento**-Un ambiente isolato significa che gli sviluppatori possono aggiornare o modificare le loro estensioni a loro discrezione senza affidarsi a una versione di base.
- **Indipendenza tecnologica**-Gli sviluppatori possono scegliere qualsiasi tecnologia, stack e linguaggi di codifica che soddisfino le loro esigenze.

>[!TIP]
>
>Le app create dal fornitore sono disponibili anche per l&#39;installazione in [Adobe Exchange](https://exchange.adobe.com/).

Adobe fornisce i seguenti strumenti per sviluppatori per creare integrazioni e personalizzazioni:

- [**Mesh API per Adobe Developer App Builder**](https://developer.adobe.com/graphql-mesh-gateway/): consente di coordinare e combinare più origini API, GraphQL, REST e altre in un unico endpoint GraphQL interrogabile.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/): crea e distribuisci applicazioni web sicure e scalabili che estendono le funzionalità di Commerce e si integrano con soluzioni di terze parti.
- [**Eventi**](https://developer.adobe.com/commerce/extensibility/events/)—Utilizza trigger evento personalizzati per interagire con altri strumenti di sviluppo estensibili.
- [**Webhook**](https://developer.adobe.com/commerce/extensibility/webhooks/): utilizza i webhook per attivare automaticamente le interazioni tra Commerce e i sistemi di terze parti.
- [**Interfaccia utente amministratore SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/)—Personalizza e ottimizza l&#39;amministratore Commerce con nuove pagine e funzionalità per gli esercenti.
- [**Integration Starter Kit**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/): accelera le integrazioni back-office con integrazioni di riferimento, script di onboarding e architettura standardizzata.

## Commerce Foundation

Commerce Foundation offre una piattaforma di hosting automatizzata sicura e funzioni self-service per la gestione dell&#39;applicazione Commerce in un ambiente nativo per il cloud.

Le caratteristiche principali includono:

- Onboarding semplificato
- Aggiornamenti senza problemi
- Integrazioni di terze parti

### Onboarding semplificato

Avvia in pochi minuti le istanze sandbox e di produzione con il portale di provisioning self-service di Commerce Cloud Manager. Tutto ciò di cui hai bisogno, inclusi i servizi di merchandising, Commerce Storefront e App Builder, viene configurato automaticamente e integrato con le tue istanze.

Consulta la [Guida introduttiva](getting-started.md) per scoprire come creare e gestire le istanze di Commerce.

### Aggiornamenti senza problemi

Accedi alle funzioni e ai miglioramenti più recenti senza dover eseguire aggiornamenti manuali. La distribuzione continua di nuove funzioni e aggiornamenti elimina la necessità di applicare patch manuali, garantendo sempre l&#39;accesso alle funzionalità più recenti con un basso costo totale di proprietà.

Il processo di aggiornamento tipico per Adobe Commerce on Cloud prevedeva la creazione di backup, la clonazione di istanze, l’esecuzione di strumenti di compatibilità e la risoluzione di conflitti di codice. Non è più necessario con [!DNL Adobe Commerce as a Cloud Service]. Adobe ti invia notifiche in-app quando vengono rilasciati nuovi aggiornamenti di funzionalità e sicurezza. Hai un periodo di 30 giorni per valutare le nuove funzionalità nelle istanze sandbox prima che gli aggiornamenti vengano applicati automaticamente agli ambienti di produzione.

>[!NOTE]
>
>Adobe garantisce la compatibilità con le versioni precedenti per tutti gli aggiornamenti. Ciò significa che quando vengono applicati aggiornamenti, questi non interromperanno le funzionalità o personalizzazioni esistenti conformi al modello [Estensibilità API-first](https://developer.adobe.com/commerce/extensibility/).

### Integrazioni di terze parti

Gli sviluppatori possono utilizzare [API GraphQL e REST](https://developer.adobe.com/commerce/services/cloud/guides/) complete per integrare Commerce Foundation con sistemi di terze parti ed estendere le funzionalità di Commerce.

## Integrazione con Experience Cloud

[!DNL Adobe Commerce as a Cloud Service] si integra con tutte le soluzioni Experience Cloud per fornire [esperienze e-commerce personalizzate su larga scala](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Connessione dati](../data-connection/overview.md) consente di ottenere informazioni sul comportamento d&#39;acquisto dei tuoi acquirenti, in modo da poter creare esperienze d&#39;acquisto personalizzate su tutti i canali con altri prodotti Adobe Digital Experience.

## Vantaggi

Nelle sezioni seguenti vengono fornite informazioni sui vantaggi offerti da [!DNL Adobe Commerce as a Cloud Service] ai responsabili aziendali e IT.

### Leader aziendali

- **Aumento dei ricavi**: aumento del traffico organico con una vetrina ad alte prestazioni che migliora l&#39;ottimizzazione SEO (Search Engine Optimization). Crea esperienze personalizzate che guidano la conversione utilizzando dati avanzati.
- **Operazioni scalabili**: i servizi con scalabilità automatica soddisfano le esigenze di picco della tua azienda con una disponibilità del 99,9%. Implementa più marchi e aree geografiche e supporta B2B e B2C da una singola istanza. Supporto di cataloghi di prodotti complessi e di grandi dimensioni con modellazione dati flessibile.
- **Aumenta la produttività del merchandiser**: utilizza i servizi di merchandising basati su intelligenza artificiale per migliorare la conversione. Sperimenta in modo nativo direttamente nella vetrina. Gestisci l’esperienza della vetrina per creare in pochi minuti esperienze avanzate con un semplice authoring basato su documenti o un editor visivo.
- **Riduzione del costo totale di proprietà e accelerazione dell&#39;innovazione**: i servizi sempre aggiornati consentono di accedere immediatamente alle nuove funzionalità. Attiva le nuove funzionalità installando facilmente le app dal marketplace. Libera le risorse dalla manutenzione noiosa per concentrarti sulla creazione di nuove funzionalità.

### Responsabili IT

- **Provisioning rapido**: inizia subito a utilizzare il provisioning self-service in pochi minuti. Tutti i servizi sono preconfigurati in modo da funzionare perfettamente insieme per iniziare più rapidamente. Fornire sandbox per la sperimentazione per sviluppatori in base alle esigenze.
- **Basso costo di proprietà**: nessun altro aggiornamento con servizi sempre aggiornati. Protezione e conformità con le ultime patch di sicurezza applicate automaticamente. Scalabilità automatica per soddisfare i carichi di lavoro più complessi.
- **Vetrina ad alte prestazioni**: crea esperienze avanzate in pochi minuti con un semplice authoring basato su documenti o un editor visivo. Utilizza i servizi di merchandising basati sull’intelligenza artificiale per migliorare la conversione. La sperimentazione nativa è integrata nella vetrina.
- **Innovazione più rapida**: libera le risorse dalla manutenzione noiosa per concentrarsi sulla creazione di nuove funzionalità che offrano valore commerciale. Utilizza l’estensibilità completa e tecnologie basate su standard (JavaScript, HTML, CSS e strumenti a basso codice) per creare esperienze differenziate. Installa app di terze parti con un clic per aggiungere nuove funzionalità alla piattaforma commerce.

## Nuove funzionalità

[Interfaccia utente amministratore](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) è l&#39;interfaccia principale per accedere alle funzionalità per gestire le operazioni di back-end store, l&#39;inventario, i prezzi, le promozioni e le interazioni con i clienti. Tuttavia, [!DNL Adobe Commerce as a Cloud Service] offre soluzioni univoche che sostituiscono alcune delle note funzionalità disponibili nei progetti Adobe Commerce on-premise e cloud. Nella tabella seguente sono descritte le funzionalità e le soluzioni sostitutive disponibili in [!DNL Adobe Commerce as a Cloud Service]:

| Funzionalità | Soluzione | Disponibilità | Dettagli |
|---------|----------|--------------|--------|
| [Gestione risorse digitali](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management) | [Visualizzazioni prodotto](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration) o mini-DAM | Disponibile | Un solido sistema di gestione delle risorse digitali (DAM) che si integra con Adobe Experience Manager per la gestione dei contenuti rich media. In alternativa, il mini-DAM fornisce strumenti di base per la gestione delle risorse digitali per l’archiviazione e la gestione delle risorse. |
| [Sistema di gestione dei contenuti (CMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview) | [Commerce Storefront](https://www.aem.live/) | Disponibile | Un CMS di base che consente agli utenti di creare e gestire facilmente documenti e contenuti di siti Web mediante l&#39;authoring basato su documenti. In alternativa, un editor universale che consente una gestione e una personalizzazione dei contenuti più avanzate su più piattaforme. |
| [Gestione temporanea del contenuto](https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging) | [Servizio catalogo](../catalog-service/overview.md) | Roadmap | Strumento di gestione dei cataloghi collegato a Adobe Experience Platform, che consente la gestione di cataloghi di grandi dimensioni. |
| [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview) | [Commerce Storefront](https://www.aem.live/) | Disponibile | Un CMS di base che consente agli utenti di creare e gestire facilmente documenti e contenuti di siti Web mediante l&#39;authoring basato su documenti. In alternativa, un editor universale che consente una gestione e una personalizzazione dei contenuti più avanzate su più piattaforme. |
| [Pagamenti](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments) | [Servizi di pagamento per Adobe Commerce](../payment-services/overview.md) | Disponibile | Un servizio di pagamento integrato che agevoli transazioni sicure ed efficienti. |
| [Catalogo condiviso](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared) | [Servizio di indicizzazione prezzi](../price-index/price-indexing.md) | Roadmap | Analizza i dati sui prezzi e suggerisce strategie di prezzo ottimali per i prodotti in base a vari fattori. |
| [Riscritture URL](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite) | [Commerce Storefront](https://www.aem.live/) | Disponibile | Un CMS di base che consente agli utenti di creare e gestire facilmente documenti e contenuti di siti Web mediante l&#39;authoring basato su documenti. In alternativa, un editor universale che consente una gestione e una personalizzazione dei contenuti più avanzate su più piattaforme. |
| [Merchandiser visivo](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser) | [Servizio catalogo](../catalog-service/overview.md) | Roadmap | Strumento di gestione dei cataloghi collegato a Adobe Experience Platform, che consente la gestione di cataloghi di grandi dimensioni. |
