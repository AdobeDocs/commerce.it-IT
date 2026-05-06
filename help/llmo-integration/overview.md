---
title: Integra [!DNL Adobe Commerce] con [!DNL Adobe LLM Optimizer]
description: Connetti [!DNL Adobe Commerce] a [!DNL Adobe LLM Optimizer] per monitorare i segnali catalogo nei moduli LLM e distribuire le ottimizzazioni catalogo approvate.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Integra [!DNL Adobe Commerce] con [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>L’accesso a questa integrazione è limitato. Per ulteriori informazioni, contatta il tuo Technical Account Manager.

[!DNL Adobe LLM Optimizer] è una soluzione aziendale che consente ai brand di monitorare, analizzare e ottimizzare l&#39;aspetto dei contenuti nelle risposte fornite da LLM (Large Language Model) e assistenti AI. Poiché gli acquirenti utilizzano sempre più strumenti di intelligenza artificiale per la ricerca e l’individuazione dei prodotti, LLM Optimizer contribuisce a garantire che il marchio e il catalogo vengano citati accuratamente e visualizzati nel contesto.

Questa guida descrive come **[!DNL Adobe Commerce]** si inserisce in quel flusso di lavoro quando il catalogo prodotti viene memorizzato in Commerce. Scoprirai quali funzionalità diventano disponibili, quale configurazione è necessaria e come si comportano le ottimizzazioni distribuite nell’amministratore e tra i canali di acquisizione.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] è una soluzione Adobe autonoma. I flussi di lavoro di base per monitoraggio e opportunità non richiedono [!DNL Adobe Experience Manager] (AEM) o altre applicazioni Adobe. Le azioni di distribuzione specifiche di Commerce si applicano solo quando il catalogo è connesso a LLM Optimizer e si sceglie di inviare le modifiche approvate a [!DNL Adobe Commerce].

## Funzionalità dell&#39;integrazione {#what-integration-enables}

La connessione di LLM Optimizer al catalogo [!DNL Adobe Commerce] consente di passare da informazioni approfondite di contenuto generiche a **consigli in base al catalogo**:

- **Identificare** le lacune e le incoerenze nei dati del catalogo, ad esempio titoli, descrizioni e segnali strutturati, che influiscono sul modo in cui i moduli LLM interpretano i prodotti.
- **Rivedi** ha suggerito miglioramenti con il contesto di supporto, incluse giustificazioni e confronti prima e dopo.
- **Distribuisci** ottimizzazioni selezionate, ad esempio aggiornamenti del nome e della descrizione del prodotto, direttamente nel catalogo di Commerce per garantire l&#39;allineamento dei flussi di lavoro, delle griglie e dei dati rivolti all&#39;area di vendita dell&#39;amministratore.

Quando l&#39;origine del catalogo è [!DNL Adobe Commerce], Adobe può supportare il flusso di lavoro end-to-end completo: identificazione automatica delle opportunità, suggerimento di modifiche e applicazione di correzioni approvate. Per i cataloghi che hanno origine al di fuori di Commerce, LLM Optimizer può ancora analizzare e suggerire miglioramenti, ma l’applicazione delle modifiche dipende dal modello di integrazione (ad esempio, un catalogo con mirroring o aggiornamenti manuali). Vedi [Limiti e limiti dell&#39;integrazione](boundaries-limits.md).

## Per chi è questo {#who-this-is-for}

- **Professionisti del marketing digitale e commercianti** che desiderano che i dati dei prodotti siano accurati e coerenti nelle risposte basate su LLM e che necessitano di un metodo controllato per migliorare la copia del catalogo su larga scala.
- **Amministratori Commerce** proprietari dell&#39;integrità del catalogo, dei processi di amministrazione e delle integrazioni (API, CSV, PIM) che forniscono attributi di prodotto.

## Prerequisiti {#prerequisites}

I seguenti prerequisiti si applicano quando si dispone dell&#39;**accesso** all&#39;integrazione Adobe Commerce con Adobe LLM Optimizer. Per ulteriori informazioni, contatta il tuo Technical Account Manager.

- La vetrina può essere scansionata da bot agentici e orientati verso LLM, in cui questa funzionalità di scansiona fa parte della strategia di misurazione e ottimizzazione di LLM Optimizer (un prerequisito generale per informazioni sul catalogo).
- Per i flussi di lavoro di distribuzione supportati da Commerce, i servizi Commerce richiesti e la connettività dei cataloghi sono abilitati e integri. La configurazione a livello di attività è descritta in [Connettere Adobe Commerce a LLM Optimizer](get-started/connect-to-llmo.md).

È inoltre necessario comprendere il modo in cui i dati si spostano tra i sistemi:

### Flusso di dati di alto livello {#high-level-data-flow}

A livello concettuale, le ottimizzazioni dei cataloghi seguono due modelli (il progetto può utilizzare uno o entrambi, a seconda delle funzionalità):

| Direzione | Finalità |
| --- | --- |
| **Catalogo Commerce -> LLM Optimizer** | Opportunità di feed di segnali catalogo e URL e suggerimenti nell’interfaccia utente di LLM Optimizer. |
| **LLM Optimizer -> Commerce** | Dopo aver approvato un’azione di distribuzione, gli aggiornamenti al nome e alla descrizione del prodotto vengono scritti nel catalogo principale di Commerce in modo che sia l’amministratore che la vetrina riflettano i valori ottimizzati. |

### [!DNL Adobe Commerce] rispetto ai cataloghi di terze parti {#commerce-vs-third-party}

| Origine catalogo | Copertura tipica dei LLM Optimizer |
| --- | --- |
| **[!DNL Adobe Commerce]** | Supporto completo per identificazione e suggerimenti, oltre alla distribuzione di aggiornamenti approvati per i campi del catalogo configurati. |
| **Commerce di terze parti** | Identificazione e suggerimenti sono supportati; la distribuzione automatizzata nel sistema esercente dipende dall’esportazione, dal mirroring o dai flussi di lavoro dei partner, anziché dalle scritture dirette nel catalogo di origine dell’esercente. |

## Agente catalogo, Storefront MCP e LLM Optimizer {#catalog-agent-and-mcp}

Il [!DNL Adobe Commerce] **catalogo prodotti** è il sistema di registrazione dei dati dei prodotti: nomi, descrizioni, attributi, prezzi e inventario. Per l&#39;individuazione e l&#39;ottimizzazione basate sull&#39;intelligenza artificiale, **Adobe Commerce Storefront MCP** (Model Context Protocol) è un&#39;interfaccia strutturata tra i dati live del catalogo Commerce e le esperienze Adobe AI.

**L&#39;agente catalogo** è posizionato sopra Storefront MCP. L&#39;agente catalogo consente a [!DNL Adobe LLM Optimizer] di eseguire query, arricchire e agire sul contesto del catalogo e del PDP identificando le lacune, proponendo miglioramenti e distribuendo le modifiche quando vengono approvate. Queste funzionalità sono presenti nei flussi di lavoro di LLM Optimizer descritti in [Utilizza LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Come l’agente catalogo migliora Commerce per i moduli LLM {#catalog-agent-optimizations}

L’agente di catalogo affronta il problema dell’individuazione tramite due ottimizzazioni complementari: arricchimento della pagina dei dettagli del prodotto e arricchimento del catalogo dei prodotti.

### Arricchimento pagina dettagli prodotto {#pdp-enrichment-overview}

**Arricchimento della pagina dei dettagli del prodotto** suggerisce alcuni miglioramenti al contenuto della pagina di prodotto, in modo che il materiale promozionale legga più chiaramente quando gli acquirenti scoprono i prodotti tramite assistenti AI e strumenti simili. L’obiettivo è migliorare la chiarezza e la coerenza senza modificare il layout della vetrina già commercializzato dal team. Rivedi i suggerimenti in LLM Optimizer e implementali quando sei pronto.

Dopo la distribuzione, controlla la pagina del prodotto live per verificare che l’esperienza di acquisto sia ancora visualizzata come previsto.

### Arricchimento del catalogo dei prodotti {#catalog-enrichment-overview}

**L&#39;arricchimento del catalogo prodotti** suggerisce **nomi di prodotto** e **descrizioni di prodotto** più chiari, dove la copia è sottile, vaga o incoerente. Ogni suggerimento include il contesto, in modo che il team possa decidere cosa modificare. Quando si approva un aggiornamento, questo può essere applicato al catalogo [!DNL Adobe Commerce] in modo che l&#39;amministratore, la vetrina e altre esperienze che utilizzano tali campi riflettano la stessa formulazione.

Poiché tali campi risiedono in Commerce, il miglioramento di un nome o di una descrizione può essere utile per ogni canale che legge i dati di quel prodotto (a seconda di come e quando i sistemi si aggiornano).

## Argomenti correlati {#related-topics}

- [Connettere Adobe Commerce a LLM Optimizer](get-started/connect-to-llmo.md)
- [Utilizzare LLM Optimizer con Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Limiti e limiti dell’integrazione](boundaries-limits.md)
