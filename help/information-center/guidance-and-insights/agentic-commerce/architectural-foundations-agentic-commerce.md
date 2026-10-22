---
title: Progettare una piattaforma Commerce per acquirenti e agenti di intelligenza artificiale
description: Scopri come creare una piattaforma di e-commerce per gli acquirenti umani e gli agenti di intelligenza artificiale da un’unica fonte di verità, dalla progettazione dei cataloghi e MCP alla telemetria.
role: Developer, Leader
recommendations: noCatalog
autotag-review: '2026-10-20T20:32:40.424Z'
TQID: 'https://experienceleague.adobe.com/ub4oTxr4IfLGgqqz0S1npY-sn0FZb3mKq-GdjD9eDjI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
    internal-label: Data quality
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%
---

# Progettare una piattaforma commerciale per acquirenti e agenti di IA

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Ritratto di Surya Lamech" src="../../assets/guidance-and-insights/agentic-commerce-author-avatar-slamech.png" width="96"><br><strong>Surya Lamech</strong><br><em>Responsabile marketing prodotto principale</em></td>
</tr>
</table>

![Illustrazione eroica di una piattaforma di e-commerce in cui esseri umani e agenti di IA interagiscono con un&#39;unica fonte di verità](../../assets/guidance-and-insights/agentic-commerce-hero.png "Fondamenti architettonici di una piattaforma di e-commerce in-house")

*Progettazione di una piattaforma commerciale in cui umani e agenti di intelligenza artificiale interagiscono con un&#39;unica fonte di verità.*

Commerce sta attraversando una fase di cambiamento strutturale. I clienti non si affidano più esclusivamente a motori di ricerca o a vetrine di navigazione per esplorare le loro opzioni. Invece, si stanno rivolgendo alle interfacce basate su LLM, agli assistenti basati su chat e agli strumenti di acquisto per porre domande, confrontare i prodotti tra i retailer e accelerare il processo decisionale nella fase iniziale.

Queste interfacce sono potenti motori per la scoperta, l&#39;istruzione e il confronto. Aiutano i clienti a chiarire le esigenze, valutare i compromessi e limitare le scelte più rapidamente rispetto alla navigazione tradizionale.

Tuttavia, quando si tratta di completare un acquisto, i clienti preferiscono ancora in larga misura i punti vendita affidabili e i siti di proprietà del marchio in cui la sicurezza del pagamento, la trasparenza dell’adempimento e il servizio post-acquisto sono ben compresi. La conversione rimane ancorata in ambienti in cui la fiducia è già stata stabilita.

È importante sottolineare che l’intelligenza artificiale non scompare in questa fase. Quando i clienti arrivano sulla vetrina di proprietà di un brand, l’intelligenza artificiale agente può migliorare l’esperienza guidando la selezione dei prodotti, personalizzando i consigli in tempo reale, rispondendo alle obiezioni, raggruppando elementi complementari e semplificando il pagamento. In questi ambienti affidabili, l’intelligenza artificiale diventa un acceleratore di conversione, migliorando i tassi di completamento e aumentando il valore medio dell’ordine.

Per competere in questo nuovo panorama, le aziende hanno bisogno di una base di commerce **strutturata, governata e ottimizzata sia per il consumo umano che per il consumo di agenti**. Adobe Commerce è stato progettato per questo cambiamento e i principi riportati di seguito descrivono cosa serve per essere veramente pronti per l’agente.

## Architettura commerce creata per due tipi di pubblico

![Diagramma che mostra le vetrine e le app per utenti umani a sinistra e gli assistenti chat e gli agenti autonomi a destra, entrambi tratti da un core Commerce centrale di prodotti, prezzi, inventario, promozioni, carrello e pagamento esposto tramite API e MCP](../../assets/guidance-and-insights/agentic-commerce-foundational-model.png){width="800" zoomable="yes"}

*I dati visualizzati dai clienti e gli agenti utilizzati rimangono coerenti, precisi e nel marchio.*

Il moderno stack di commerce deve ora servire due tipi di pubblico ugualmente importanti: persone e agenti di intelligenza artificiale. Esperienze rivolte all’uomo, come vetrine e app, rimangono essenziali per il coinvolgimento, l’espressione del brand e la fidelizzazione dei clienti. Ma accanto a loro si trova una superficie in rapida espansione rivolta agli agenti: endpoint leggibili da una macchina che forniscono agli LDM e agli agenti autonomi fatti strutturati, contenuti governati e funzionalità transazionali.

Gli agenti offrono prestazioni migliori quando si lavora con dati puliti e strutturati forniti tramite API prevedibili, anziché tentare di interpretare JavaScript o dedurre regole aziendali dai livelli di presentazione. Ciò significa che le specifiche dei prodotti, i prezzi, la disponibilità e la logica promozionale devono esistere come risorse indirizzabili esposte tramite API e interfacce standardizzate come i server MCP. Quando le superfici rivolte all’uomo e agli agenti attingono dalla stessa fonte di verità sottostante, i brand garantiscono che ciò che vedono i clienti e ciò che consumano gli agenti rimanga coerente, accurato e nel marchio.

Questa architettura a doppia superficie è la base del commercio agenziale.

## Un catalogo progettato per il ragionamento automatico

![Diagramma che mostra le entità prodotto strutturate (SKU, attributi, varianti, bundle, prezzi e disponibilità) definite in base ai livelli e ai criteri del catalogo e distribuite attraverso le visualizzazioni del catalogo a una vetrina del marchio, a un marketplace, a un feed partner, a un&#39;app mobile e a una superficie di IA o agente](../../assets/guidance-and-insights/agentic-commerce-agent-interaction.png){width="800" zoomable="yes"}

*Un&#39;unica origine di verità gestita, con forma per canale, senza mai effettuare il forking dei dati del prodotto.*

Il catalogo è il nucleo del commercio agentico. Deve essere strutturata per i computer, governata per la conformità e sufficientemente flessibile da supportare l&#39;intera gamma di interazioni umane e di agenti. Il modello di catalogo di Adobe Commerce basato su viste di catalogo, criteri, livelli ed entità di prodotto strutturate è progettato per il futuro.

Le viste catalogo definiscono dove e come vengono esposti i dati dei prodotti, sia che si tratti di una vetrina, di un marketplace, di un feed partner o di una superficie AI. Ogni vista può avere le proprie regole di disponibilità del prodotto, prezzi e visibilità degli attributi, garantendo che le informazioni corrette raggiungano il consumatore o l’agente giusto. I livelli catalogo consentono di arricchire i dati dei prodotti per canali specifici senza modificare i dati dei prodotti di origine. I criteri regolano l’idoneità dei clienti, la logica di inventario, i prezzi e i vincoli di conformità. Insieme, le aziende hanno un controllo preciso sui dati del catalogo a cui un agente può accedere o su cui può agire.

## MCP come linguaggio comune per gli agenti

![Diagramma che mostra gli assistenti commerciali, gli agenti di supporto e gli strumenti per sviluppatori che inviano richieste tramite Model Context Protocol, che include Commerce MCP e Developer MCP, alle funzionalità di Adobe Commerce come creazione di carrello, pagamento, inventario e promozioni e restituzioni](../../assets/guidance-and-insights/agentic-commerce-reference-stack.png){width="800" zoomable="yes"}

*MCP standardizza il modo in cui gli agenti richiedono le azioni con intento naturale e Adobe Commerce le esegue come azioni deterministiche gestite.*

Affinché Agentic Commerce funzioni in modo end-to-end, le piattaforme di e-commerce devono supportare protocolli standardizzati che consentano agli agenti di eseguire azioni in modo sicuro, come la creazione del carrello, l’avvio del pagamento, l’orchestrazione dei pagamenti, la convalida dell’inventario, le promozioni e le restituzioni.

Grazie al supporto nativo di MCP (Model Context Protocol), Adobe struttura e espone le funzionalità di e-commerce in modo che i moduli LLM possano interpretare in modo coerente. MCP standardizza il modo in cui i dati dei prodotti, le regole aziendali e il contesto transazionale vengono presentati ai moduli LLM, garantendo che gli agenti possano ragionare su di essi in modo affidabile, mentre le aziende mantengono la governance e il controllo. Con Commerce MCP, le aziende possono creare esperienze agentiche personalizzate come assistenti agli acquisti, creazione di carrelli, agenti di supporto e molto altro.

MCP per sviluppatori offre funzionalità di sviluppo basate sull’intelligenza artificiale che consentono ai team di estendere rapidamente le funzionalità della piattaforma e distribuire componenti di vetrina componibili. Incorporando le origini di conoscenza, la documentazione e le best practice di Adobe direttamente nel flusso di lavoro di sviluppo, MCP per sviluppatori consente a nuovi sviluppatori di iniziare a lavorare in modo più rapido e produttivo dal primo avvio. Genera codice che segue modelli architettonici collaudati, è facile da mantenere e soddisfa gli standard di qualità richiesti dal commercio aziendale. Il risultato è un percorso accelerato dall&#39;idea alla produzione, che dà alle aziende la velocità di sperimentare, iterare e spedire le capacità di commerce davanti alla concorrenza.

Adobe si impegna anche a supportare protocolli di e-commerce agentici come il protocollo ACP (Agentic Commerce Protocol) e il protocollo UCP (Universal Commerce Protocol), consentendo l’individuazione dei prodotti e interazioni transazionali sicure e basate su standard tra gli agenti e la vetrina.

Adottando protocolli aperti invece delle integrazioni puntuali, Adobe garantisce che le interazioni commerciali siano gestite, deterministiche e sicure e al tempo stesso abilita un nuovo modello di coinvolgimento agente-commerciante in cui gli agenti affidabili possono negoziare direttamente in base a criteri chiaramente definiti.

## Telemetria e ottimizzazione continua

In un ecosistema mediato dall&#39;intelligenza artificiale, la telemetria diventa il vantaggio strategico. Le aziende devono avere visibilità su come il proprio marchio viene rappresentato nei moduli LLM, su come gli agenti rappresentano con precisione i propri contenuti, su come viene convertito il traffico riferito dagli agenti e dove sorgono problemi di governance o conformità. Hanno anche bisogno di una telemetria operativa che tenga traccia dell&#39;esecuzione degli agenti e del rilevamento delle anomalie attraverso le interazioni degli agenti.

Adobe offre visibilità sul modo in cui i prodotti vengono visualizzati in LLM, migliora i dati dei prodotti con AI e aumenta la leggibilità dei dati da parte di LLMS. Aggiungendo un contesto significativo al catalogo, consente ai moduli LLM non solo di scoprire i prodotti in modo accurato, ma anche di capire cosa sono, per chi sono e perché sono importanti per i clienti.

Inoltre, le pagine dei dettagli del prodotto ottimizzate per il consumo umano possono spesso contenere dati invisibili agli agenti. Questi dati potrebbero essere nascosti dietro modali, configuratori e pagine collegate. Gli agenti potrebbero non comprendere appieno le categorie di prodotti, i bundle e le varianti. Adobe è in grado di identificare queste informazioni critiche mancanti e distribuirle come JSON-LD al server Edge, in modo che gli agenti possano ottenere tutti i dati rilevanti del prodotto.

Grazie a questa costante telemetria e ottimizzazione i brand possono garantire la massima visibilità e rimanere competitivi tra i vari sistemi LLM.

## Perché è importante

L’e-commerce non è più limitato alle vetrine e ai risultati di ricerca. I moduli LLM e gli agenti autonomi mediano sempre più l&#39;individuazione, la valutazione e le transazioni. Questo cambiamento cambia la meccanica della visibilità, la dinamica del controllo, e le fondamenta della fiducia. I brand che vincono si arruoleranno in una fondazione nativa per l’intelligenza artificiale.

## Linee guida correlate

* [Visualizzazioni catalogo](/help/optimizer/setup/catalog-view.md)
* [Livelli del catalogo](/help/optimizer/setup/catalog-layer.md)
* [Criteri](/help/optimizer/setup/policies.md)
* [Strumenti per gli sviluppatori di codifica AI per Adobe Commerce App Builder](/help/cloud-service/migration/coding-tools.md)
* [API di Commerce](../../apis/commerce-apis.md)
* [Playlist di Commerce Developer Agent](https://experienceleague.adobe.com/it/playlists/commerce-developer-agent) - Guarda i video tecnici sulla configurazione e l&#39;utilizzo di Commerce Developer Agent.
