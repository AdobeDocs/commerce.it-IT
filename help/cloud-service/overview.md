---
title: Panoramica di [!DNL Adobe Commerce as a Cloud Service]
description: Scopri le funzionalità e i vantaggi principali di  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
TQID: 'https://experienceleague.adobe.com/RWF0BsS24AJtkoPNxRtvTNyM971IBEEt-NTbPT5Nub8'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c18ed297-2187-4aec-affb-9d9654eca6fcid: c32adafa-ed01-4b31-997e-2413013911b0id: cc250cf1-34eb-4863-80d0-d170d45ea067id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: a743e5dc-8f37-4b5d-a848-03c32ca30598id: e91a50b1-0b31-436e-9033-00e4776e94cbid: f236e2a1-90d4-477d-92e1-5996b5e92bffid: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12bid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: d095671a-1355-40aa-8b5f-06c33c68080bid: da3860b0-d637-47df-bef0-273751180266id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 1444
ht-degree: 0%

---

# Panoramica di [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] offre flessibilità, scalabilità ed efficienza consentendo alle aziende di fornire e scalare rapidamente le operazioni digitali accelerando al contempo l&#39;innovazione. L&#39;infrastruttura nativa per il cloud di Adobe regola automaticamente le risorse per soddisfare i picchi di richieste di traffico, ordini e gestione dei cataloghi.

La tabella seguente evidenzia i prodotti che alimentano [!DNL Adobe Commerce as a Cloud Service]:

<table style="table-layout:auto">
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="segno di spunta" align="center"> <strong>Commerce Storefront</strong>
    </td>
    <td align="left">
      Interfaccia orientata al cliente, con cui gli acquirenti possono consultare e acquistare prodotti
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="segno di spunta" align="center"> <strong>Servizi di merchandising</strong>
    </td>
    <td align="left">
      Servizi back-end per la gestione di cataloghi di prodotti, prezzi e inventario
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="segno di spunta" align="center"> <strong>Visualizzazioni prodotto</strong>
    </td>
    <td align="left">
      Gestione delle risorse digitali per immagini e supporti dei prodotti
    </td>
  </tr>
  <tr>
    <td align="left">
      <img src="../assets/icon-checkmark-circle-outline.svg" alt="segno di spunta" align="center"> <strong>Piattaforma sviluppatore</strong>
    </td>
    <td align="left">
      Strumenti di sviluppo e API di base per la creazione di funzionalità personalizzate
    </td>
  </tr>
</table>

## Architettura

Per una breve introduzione all&#39;architettura [!DNL Adobe Commerce as a Cloud Service], guarda il video seguente. Diagrammi che illustrano l’architettura sono forniti sotto il video.

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

Questo diagramma illustra il flusso di dati tra [!DNL Adobe Commerce as a Cloud Service] e tutte le soluzioni Adobe Experience Cloud.

![Diagramma del flusso di dati che mostra l&#39;integrazione di [!DNL Adobe Commerce as a Cloud Service] con [!DNL Adobe Experience Cloud] soluzioni](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Utilizza [[!DNL Commerce Storefront]](https://experienceleague.adobe.com/developer/commerce/storefront) di Adobe basato su [!DNL Edge Delivery Services] per creare esperienze avanzate in pochi minuti con semplici operazioni di authoring basato su documenti o di modifica visiva con [!DNL Storefront Builder].

[!DNL Commerce Storefront] è completamente headless con un&#39;architettura separata che fornisce tutti i servizi e i dati di merchandising tramite un livello API GraphQL. Questa architettura consente ai team di sviluppare i propri front-end in modo indipendente da Commerce Foundation, fornendo la flessibilità necessaria per creare e testare nuovi punti di contatto con le tecnologie emergenti.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] non supporta le vetrine Luma. Se esegui la migrazione da Adobe Commerce su Cloud o on-premise, consulta [vetrine esistenti](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts) per informazioni sulla transizione.

## Servizi di merchandising e servizi di pagamento

Adobe offre una ricca gamma di servizi di merchandising intelligenti e componibili per aiutarti a supportare i tuoi obiettivi aziendali chiave. Questi servizi forniscono anche API fondamentali per ottimizzare le prestazioni su larga scala.

- [Live Search](../live-search/overview.md) - Fornisci risultati più intelligenti, più veloci e rilevanti per gli acquirenti con questo strumento di ricerca basato sull&#39;intelligenza artificiale.
- [Consigli di prodotto](../optimizer/merchandising/recommendations/overview.md): aggiungi consigli basati sull&#39;intelligenza artificiale in base al comportamento degli acquirenti, alle tendenze popolari, alla somiglianza dei prodotti e altro ancora.
- [Catalog Service](../catalog-service/guide-overview.md) - Offri ai tuoi clienti un&#39;esperienza di prodotto ottimizzata migliorando le prestazioni, la scalabilità e le conversioni.
- [Servizi di pagamento](../payment-services/guide-overview.md)—Aumenta la soddisfazione dei clienti offrendo diversi metodi di pagamento, incluse le rate di pagamento senza interessi e un&#39;unica vista per l&#39;elaborazione dei pagamenti, gli ordini e le fatture.

## [!DNL Product Visuals powered by AEM Assets]

Product Visuals semplifica la gestione delle risorse grazie a un sistema DAM (Digital Asset Management) integrato con Adobe Experience Manager per la gestione dei contenuti rich media.

L’integrazione garantisce che le risorse digitali, come immagini di prodotto o contenuti di marketing, si colleghino in modo dinamico alle entità di merchandising appropriate, inclusi i prodotti e le categorie in Adobe Commerce, in base allo SKU o ad altri attributi chiave.

[!DNL Product Visuals] è disponibile con [!DNL Adobe Commerce as a Cloud Service], fornendo alcune funzionalità di [!DNL AEM Assets].

In alternativa, le funzionalità native di [!DNL Adobe Commerce as a Cloud Service] forniscono strumenti di base per la gestione delle risorse digitali per l&#39;archiviazione e la gestione delle risorse digitali.

Per ulteriori informazioni su come integrare [!DNL Product Visuals powered by AEM Assets] con [!DNL Adobe Commerce as a Cloud Service], consulta la [guida all&#39;integrazione di AEM Assets](../aem-assets-integration/overview.md).

### [!DNL Product Visuals] o [!DNL AEM Assets]

Il seguente confronto consente di selezionare l’opzione migliore per i contenuti di cui supply chain ha bisogno:

<table>
  <tr>
    <td align="left">
      <strong>[!DNL Product Visuals powered by AEM Assets]</strong>
      <ul>
        <li>Digital Asset Manager (DAM) integrato e automatizzato per immagini e video dei prodotti</li>
        <li>Ridimensionare, ritagliare e convertire immagini</li>
        <li>Consegna di immagini e video ad alta velocità</li>
        <li>Ottimizza formati, dimensioni e qualità delle immagini in base alle funzionalità del browser client</li>
        <li>Accesso ad Adobe Express e Adobe Firefly</li>
        <li>Limiti di utilizzo per la capacità di consegna di immagini/video e l’accesso degli utenti</li>
        <li>Selettore di risorse integrato</li>
      </ul>
    </td>
    <td align="center">
      <br><br><br><br><br><br><br><br><br><br><br>
      <img src="../assets/icon-double-chevron-right.svg" alt="freccia" width="100">
    </td>
    <td align="left">
      <strong>AEM Assets</strong>
      <ul>
        <li>Tutte le funzionalità dalle visualizzazioni prodotto</li>
        <li>Marketing completo Digital Asset Manager (DAM)</li>
        <li>Utenti illimitati (pagamento per utente)</li>
        <li>Consegna illimitata di immagini e video</li>
        <li>Funzionalità avanzate di gestione delle risorse:</li>
        <ul>
          <li>360° set 360° e visualizzatori interattivi</li>
          <li>Supporto di modelli 3D e contenuti coinvolgenti</li>
          <li>Supporto PDF</li>
          <li>Ritaglio avanzato basato sull’intelligenza artificiale</li>
          <li>Modelli immagine dinamici</li>
          <li>Applicazione di tag avanzati</li>
          <li>Tracciamento e analisi delle prestazioni delle risorse</li>
        </ul>
      </ul>
    </td>
  </tr>
    <tr>
    <td align="center" colspan="3">
      <strong>L'integrazione con il marchio Adobe è disponibile per facilitare la migrazione tra le offerte.</strong>
    </td>
  </tr>
</table>

## Piattaforma sviluppatore

Adobe fornisce agli sviluppatori punti di estensione e strumenti completi per creare applicazioni che estendono le funzionalità di Commerce Foundation e si integrano con sistemi di terze parti (come CRM, ERP e PIM). Questi strumenti riducono il costo totale di proprietà della piattaforma nei seguenti modi:

- **Scalabilità**: le applicazioni possono essere scalate separatamente dal software principale, consentendo una maggiore efficienza e aggiornamenti semplificati.
- **Isolamento** - Un ambiente isolato consente agli sviluppatori di aggiornare o modificare le estensioni a propria discrezione senza affidarsi a una versione di base.
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

[!DNL Commerce Foundation] offre una piattaforma di hosting automatizzata sicura e funzionalità self-service per la gestione dell&#39;applicazione Commerce in un ambiente nativo per il cloud.

Le caratteristiche principali includono:

- Onboarding semplificato
- Aggiornamenti senza problemi
- Integrazioni di terze parti

### Onboarding semplificato

Avvia in pochi minuti le istanze di produzione e sandbox con il portale di provisioning self-service [!UICONTROL Commerce Cloud Manager]. Tutto ciò di cui hai bisogno, inclusi i servizi di merchandising, un&#39;istanza Commerce headless e [!DNL App Builder], viene configurato automaticamente e integrato con le tue istanze.

Consulta la [Guida introduttiva](getting-started.md) per scoprire come creare e gestire le istanze di Commerce.

### Aggiornamenti senza problemi

Accedi alle funzioni e ai miglioramenti più recenti senza dover eseguire aggiornamenti manuali. La distribuzione continua di nuove funzioni e aggiornamenti elimina la necessità di applicare patch manuali, garantendo sempre l&#39;accesso alle funzionalità più recenti con un basso costo totale di proprietà.

Il processo di aggiornamento tipico per Adobe Commerce on Cloud prevedeva la creazione di backup, la clonazione di istanze, l’esecuzione di strumenti di compatibilità e la risoluzione di conflitti di codice. Non è più necessario con [!DNL Adobe Commerce as a Cloud Service]. Adobe ti invia notifiche in-app quando vengono rilasciati nuovi aggiornamenti di funzionalità e sicurezza. Hai un periodo di 30 giorni per valutare le nuove funzionalità nelle istanze sandbox prima che gli aggiornamenti vengano applicati automaticamente agli ambienti di produzione.

>[!NOTE]
>
>Adobe garantisce la compatibilità con le versioni precedenti per tutti gli aggiornamenti. Ciò significa che quando vengono applicati aggiornamenti, questi non interromperanno le funzionalità o personalizzazioni esistenti conformi al modello [Estensibilità API-first](https://developer.adobe.com/commerce/extensibility/).

### Integrazioni di terze parti

Gli sviluppatori possono utilizzare [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) e [API REST](https://developer.adobe.com/commerce/webapi/rest/) complete per integrare [!DNL Commerce Foundation] con sistemi di terze parti ed estendere le funzionalità di Commerce.

<!-- 
## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. 
-->

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
