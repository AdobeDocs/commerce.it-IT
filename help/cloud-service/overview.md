---
title: Panoramica di [!DNL Adobe Commerce as a Cloud Service]
description: Scopri le funzionalità e i vantaggi principali di  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Panoramica di [!DNL Adobe Commerce as a Cloud Service]

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] offre flessibilità, scalabilità ed efficienza consentendo alle aziende di fornire e scalare rapidamente le operazioni digitali e accelerare l&#39;innovazione. L&#39;infrastruttura nativa per il cloud di Adobe regola automaticamente le risorse per soddisfare i picchi di richieste di traffico, ordini e gestione dei cataloghi.

L&#39;immagine seguente evidenzia i prodotti che alimentano [!DNL Adobe Commerce as a Cloud Service]:

![[!DNL Adobe Commerce as a Cloud Service] stack di prodotto](./assets/product-stack.svg){align="center" zoomable="yes"}

>[!BEGINSHADEBOX]

![info](assets/Smock_InfoOutline_18_N.svg) Se desideri partecipare al programma di accesso anticipato [!DNL Adobe Commerce as a Cloud Service], completa [questo modulo](https://forms.office.com/pages/responsepage.aspx?id=Wht7-jR7h0OUrtLBeN7O4WOxhjY2doZPikS2hIbfmL5URFZXTE5TUk9PMUw0OFdOWTBNNlI3UTlNMS4u&route=shorturl).

>[!ENDSHADEBOX]

## Architettura

Per una breve introduzione all&#39;architettura [!DNL Adobe Commerce as a Cloud Service], guarda il video seguente. Diagrammi che illustrano l’architettura sono forniti sotto il video.

>[!VIDEO](https://video.tv.adobe.com/v/3443275?learn=on&captions=ita)

Questo diagramma illustra il flusso di dati tra [!DNL Adobe Commerce as a Cloud Service] e tutte le soluzioni Adobe Experience Cloud.

Diagramma dell&#39;architettura ![[!DNL Adobe Commerce as a Cloud Service]](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Utilizza [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront?lang=it) di Adobe con tecnologia Edge Delivery Services per creare in pochi minuti esperienze avanzate con semplici operazioni di authoring basato su documenti o di modifica visiva tramite Storefront Builder.

Commerce Storefront è completamente headless con un’architettura separata che fornisce tutti i servizi e i dati di merchandising tramite un livello API GraphQL. Questa architettura consente ai team di sviluppare i propri front-end in modo indipendente da Commerce Foundation, fornendo la flessibilità necessaria per creare e testare nuovi punti di contatto con le tecnologie emergenti.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] non supporta le vetrine Luma. Se esegui la migrazione da Adobe Commerce su Cloud o on-premise, consulta [vetrine esistenti](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/?lang=it#existing-storefronts) per informazioni sulla transizione.

## Servizi di merchandising e servizi di pagamento

Adobe offre una ricca gamma di servizi di merchandising intelligenti e componibili per aiutarti a supportare i tuoi obiettivi aziendali chiave. Questi servizi forniscono anche API fondamentali per ottimizzare le prestazioni su larga scala.

- [Live Search](../live-search/overview.md) - Fornisci risultati più intelligenti, più veloci e rilevanti per gli acquirenti con questo strumento di ricerca basato sull&#39;intelligenza artificiale.
- [Consigli di prodotto](../product-recommendations/overview.md): aggiungi consigli basati sull&#39;intelligenza artificiale in base al comportamento degli acquirenti, alle tendenze popolari, alla somiglianza dei prodotti e altro ancora.
- [Servizi di merchandising basati su viste e criteri del catalogo](../optimizer/setup/catalog-view.md): consente di gestire cataloghi di prodotti complessi e di grandi dimensioni con la modellazione flessibile dei dati per fornire cataloghi commerciali flessibili e ad alte prestazioni allineati alla struttura aziendale e alle strategie go-to-market. Utilizza con [Commerce Optimizer](../optimizer/overview.md) per ottimizzare le prestazioni del catalogo e migliorare i tassi di conversione.
- [Servizi di pagamento](../payment-services/guide-overview.md)—Aumenta la soddisfazione dei clienti offrendo diversi metodi di pagamento, incluse le rate di pagamento senza interessi e un&#39;unica vista per l&#39;elaborazione dei pagamenti, gli ordini e le fatture.

## Visualizzazioni prodotto

Gestione semplificata delle risorse grazie a un solido sistema DAM (Digital Asset Management) integrato con Adobe Experience Manager per la gestione dei contenuti rich media. In alternativa, le funzionalità native di [!DNL Adobe Commerce as a Cloud Service] forniscono strumenti di base per la gestione delle risorse digitali per l&#39;archiviazione e la gestione delle risorse digitali.

Per ulteriori informazioni, consulta la [guida agli elementi visivi del prodotto](../product-visuals/overview.md).

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

Avvia in pochi minuti le istanze di produzione e sandbox con il portale di provisioning self-service [!UICONTROL Commerce Cloud Manager]. Tutto ciò di cui hai bisogno, inclusi i servizi di merchandising, un’istanza headless di Commerce e App Builder, viene configurato automaticamente e integrato con le tue istanze.

Consulta la [Guida introduttiva](getting-started.md) per scoprire come creare e gestire le istanze di Commerce.

### Aggiornamenti senza problemi

Accedi alle funzioni e ai miglioramenti più recenti senza dover eseguire aggiornamenti manuali. La distribuzione continua di nuove funzioni e aggiornamenti elimina la necessità di applicare patch manuali, garantendo sempre l&#39;accesso alle funzionalità più recenti con un basso costo totale di proprietà.

Il processo di aggiornamento tipico per Adobe Commerce on Cloud prevedeva la creazione di backup, la clonazione di istanze, l’esecuzione di strumenti di compatibilità e la risoluzione di conflitti di codice. Non è più necessario con [!DNL Adobe Commerce as a Cloud Service]. Adobe ti invia notifiche in-app quando vengono rilasciati nuovi aggiornamenti di funzionalità e sicurezza. Hai un periodo di 30 giorni per valutare le nuove funzionalità nelle istanze sandbox prima che gli aggiornamenti vengano applicati automaticamente agli ambienti di produzione.

>[!NOTE]
>
>Adobe garantisce la compatibilità con le versioni precedenti per tutti gli aggiornamenti. Ciò significa che quando vengono applicati aggiornamenti, questi non interromperanno le funzionalità o personalizzazioni esistenti conformi al modello [Estensibilità API-first](https://developer.adobe.com/commerce/extensibility/).

### Integrazioni di terze parti

Gli sviluppatori possono utilizzare [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) e [API REST](https://developer.adobe.com/commerce/webapi/rest/) complete per integrare Commerce Foundation con sistemi di terze parti ed estendere le funzionalità di Commerce.

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/it/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

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
