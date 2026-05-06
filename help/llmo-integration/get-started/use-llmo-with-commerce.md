---
title: Usa  [!DNL Adobe LLM Optimizer] con [!DNL Adobe Commerce]
description: Naviga nelle opportunità Commerce in LLM Optimizer, rivedi PDP e arricchisci il catalogo, distribuisci aggiornamenti a [!DNL Adobe Commerce], verifica in Admin e storefront e scopri come le sostituzioni e le opportunità dei segni di acquisizione non sono aggiornate.
role: Admin, User
recommendations: noCatalog
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Usa [!DNL Adobe LLM Optimizer] con [!DNL Adobe Commerce]

>[!IMPORTANT]
>
>L’accesso a questa integrazione è limitato. Per ulteriori informazioni, contatta il tuo Technical Account Manager.

Dopo la [connessione di Commerce a LLM Optimizer](connect-to-llmo.md), puoi lavorare principalmente nell&#39;interfaccia utente di **[!DNL Adobe LLM Optimizer]** per esaminare le opportunità e inviare le modifiche approvate al catalogo quando sei pronto. In questo articolo vengono descritti i due tipi di ottimizzazione incentrati su Commerce, le modalità di utilizzo di **[!UICONTROL Opportunities]**, il comportamento delle azioni di distribuzione in [!DNL Adobe Commerce] e l&#39;interazione degli aggiornamenti esterni con i suggerimenti di LLM Optimizer. Per un&#39;immagine più ampia dell&#39;integrazione, vedere la [panoramica sull&#39;integrazione](../overview.md).

## Informazioni sulle ottimizzazioni di Commerce in LLM Optimizer {#understand-optimizations}

Per i cataloghi supportati da Commerce, LLM Optimizer offre **[!UICONTROL Product Detail Page Enrichment]** e **[!UICONTROL Product Catalog Enrichment]**.

| Focus | A cosa serve |
| --- | --- |
| **[!UICONTROL Product Detail Page Enrichment]** (arricchimento PDP) | Suggerimenti per migliorare il modo in cui una pagina di prodotto legge il rilevamento basato sull’intelligenza artificiale, senza sostituire il layout della vetrina. |
| **[!UICONTROL Product Catalog Enrichment]** | Sono stati suggeriti aggiornamenti di **nome prodotto** e **descrizione prodotto** per prodotti specifici che puoi rivedere, modificare se necessario e applicare al tuo catalogo Commerce. |

Utilizza **[!UICONTROL Opportunities]** per aprire l&#39;elenco di prodotti o URL e elaborare suggerimenti per il tipo selezionato.

## Esplorare le opportunità Commerce {#navigate-commerce-opportunities}

**Per aprire opportunità relative a Commerce:**

1. Nella barra a sinistra, fai clic su **[!UICONTROL Opportunities]**.
1. Fare clic su **[!UICONTROL Commerce Opportunity]** per visualizzare i tipi di ottimizzazione per il catalogo [!DNL Adobe Commerce].
1. Selezionare **[!UICONTROL Product Catalog Enrichment]** o **[!UICONTROL Product Detail Page Enrichment]**, a seconda di ciò che si desidera lavorare.

![Filtro opportunità Commerce e tipi di ottimizzazione](../assets/llmo-opportunities.png)

### Comprendere le metriche delle opportunità {#opportunity-metrics}

Ogni vista dell’opportunità riepiloga l’impatto in modo da poter assegnare la priorità al lavoro:

- **Pagine prodotto** o **URL**: le pagine o i prodotti valutati per quel tipo di ottimizzazione.
- **Traffico agente**: visite e interazioni avviate da agenti di intelligenza artificiale che possono aiutarti a dare priorità prima alle opportunità di alto impatto.

### Comprendere gli stati dei suggerimenti {#suggestion-states}

Entrambi i tipi di arricchimento utilizzano le stesse visualizzazioni del flusso di lavoro:

- **[!UICONTROL Current Suggestions]**: elementi nuovi o attivi da rivedere.
- **[!UICONTROL Fixed Suggestions]**: elementi già distribuiti o risolti.
- **[!UICONTROL Ignored Suggestions]**: elementi esclusi intenzionalmente dall&#39;azione.

### Rivedere e distribuire l’arricchimento PDP {#review-deploy-pdp}

L’arricchimento PDP è destinato ai team che desiderano una messaggistica più chiara sulle pagine dei prodotti nell’individuazione basata sull’intelligenza artificiale e al contempo mantengono l’esperienza della vetrina progettata dai merchandiser.

**Per rivedere e distribuire l&#39;arricchimento PDP:**

1. Apri **[!UICONTROL Product Detail Page Enrichment]** da **[!UICONTROL Opportunities]**.
1. Nella tabella **[!UICONTROL URLs with Suggestions]**, selezionare **[!UICONTROL Current Suggestions]**.
1. Per un URL o uno SKU, fai clic su **[!UICONTROL Preview]** per rivedere l&#39;analisi dell&#39;intelligenza artificiale e l&#39;arricchimento proposto.
1. Facoltativo: fare clic su **[!UICONTROL Copy]** per incollare il contenuto in un editor esterno oppure fare clic su **[!UICONTROL Edit suggestion]** per modificarlo.
1. Facoltativo: se un suggerimento non corrisponde alla strategia, spostarlo in **[!UICONTROL Ignored Suggestions]**.
1. Una volta rivista e approvata, seleziona la riga per l&#39;URL o lo SKU da aggiornare, quindi fai clic su **[!UICONTROL Deploy optimizations]** e conferma.

Dopo la distribuzione, i suggerimenti passano a **[!UICONTROL Fixed Suggestions]** con uno stato di ottimizzazione in LLM Optimizer.

>[!NOTE]
>
>La distribuzione dell&#39;arricchimento PDP richiede **l&#39;ottimizzazione all&#39;onboarding di Edge** in LLM Optimizer. Se l’onboarding non è completo, l’interfaccia utente richiede di completare l’installazione prima della distribuzione.

### Rivedere e distribuire l’arricchimento del catalogo dei prodotti {#review-deploy-catalog}

L’arricchimento del catalogo è destinato ai team che desiderano rendere più stringenti i nomi dei prodotti e le descrizioni lunghe direttamente in Commerce, con suggerimenti che puoi rivedere prima di salvare qualsiasi cosa.

**Per rivedere e distribuire l&#39;arricchimento del catalogo prodotti:**

1. Apri **[!UICONTROL Product Catalog Enrichment]** da **[!UICONTROL Opportunities]**.
1. Nella tabella **[!UICONTROL URLs with Suggestions]**, selezionare **[!UICONTROL Current Suggestions]**.
1. Fare clic sul controllo di espansione per la riga URL o SKU per visualizzare gli aggiornamenti **Nome prodotto** e **Descrizione prodotto** proposti.
1. Facoltativo: fai clic sull’icona Modifica per modificare il nome o la descrizione proposti prima della distribuzione.
1. Facoltativo: se un suggerimento non corrisponde alla strategia, spostarlo in **[!UICONTROL Ignored Suggestions]**.
1. Una volta rivista e approvata, seleziona la riga per l&#39;URL o lo SKU da aggiornare, quindi fai clic su **[!UICONTROL Deploy optimizations]** e conferma.

Le modifiche approvate al nome e alla descrizione vengono salvate nel catalogo [!DNL Adobe Commerce] come per gli altri aggiornamenti di prodotto.

>[!IMPORTANT]
>
>Considera la distribuzione come una modifica del catalogo di produzione. Utilizza le tue normali procedure di controllo delle modifiche, staging e controllo qualità. Distribuisci solo dopo che le parti interessate a merchandising e SEO hanno concordato la copia finale.

Dopo la distribuzione, i suggerimenti passano a **[!UICONTROL Fixed Suggestions]** con lo stato **Applicato**.

## Verificare gli aggiornamenti in Commerce Admin {#verify-in-admin}

**Per verificare l&#39;arricchimento del catalogo distribuito:**

1. Accedi a [!DNL Adobe Commerce] **Amministratore**.
1. Vai a **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.
1. Utilizza i filtri e il selettore **visualizzazione archivio** secondo necessità (ad esempio, **[!UICONTROL Default Store View]**), quindi cerca lo **SKU**.
1. Apri il prodotto in modalità di modifica.

   Il modulo del prodotto mostra il **nome prodotto** arricchito.

   ![Campo nome prodotto dopo arricchimento LLM Optimizer](../assets/llmo-admin-name.png)

1. Facoltativo: selezionare **[!UICONTROL Override LLM Optimizer provided Product Name]** se si desidera mantenere un nome immesso manualmente.

Le sostituzioni manuali influiscono sul modo in cui le opportunità rimangono sincronizzate con il catalogo. Vedere [Sostituzione manuale in Admin](#manual-override-in-the-admin).

1. Espandi la sezione **[!UICONTROL Content]** e individua il campo **description**.

   La descrizione arricchita viene visualizzata quando hai distribuito le modifiche alla descrizione.

   ![Campo descrizione dopo arricchimento LLM Optimizer](../assets/llmo-admin-description.png)

1. Facoltativo: selezionare **[!UICONTROL Override LLM Optimizer provided Description]** se si desidera conservare una descrizione immessa manualmente.

## Verifica aggiornamenti nella vetrina {#verify-storefront}

Cerca lo SKU nella vetrina e apri il PDP. Conferma che **name** e le aree che presentano la **description** estesa riflettano ciò che hai approvato. Inoltre, conferma tutti i canali a valle che utilizzano gli stessi attributi del catalogo, se pertinenti per il rollout.

<!--
## PDP enrichment rollback {#pdp-rollback}

If your project includes PDP enrichment opportunities, **rollback** behavior may support **bulk** or **per-URL** actions, depending on your LLM Optimizer release. Follow the in-product options for rollback. For **[!UICONTROL Product Catalog Enrichment]**, undoing a name or description in Commerce is effectively a new catalog edit or a follow-up opportunity, not a separate undo control in the Admin unless your team implements one.
-->

## Override, acquisizione e opportunità non aggiornate {#overrides-ingestion}

Dopo che LLM Optimizer ha aggiornato il nome o la descrizione di un prodotto, altri sistemi di acquisizione, come le chiamate API REST, le importazioni CSV, i feed PIM o processi simili, possono modificare gli stessi campi. Le sezioni seguenti descrivono cosa accade in questo caso.

### L’acquisizione invia nuovamente il valore del catalogo originale

Se un processo esterno scrive il nome o la descrizione originale (il valore esistente prima della distribuzione di LLM Optimizer), Commerce continua a rispettare il valore distribuito da LLM Optimizer per quel campo in base alle regole di integrazione. L’opportunità potrebbe non essere ripristinata automaticamente in base a tale sola acquisizione.

### L’acquisizione invia un nuovo valore

Se il processo esterno invia un nuovo valore che non è semplicemente una ripetizione del testo precedente a LLM Optimizer (ad esempio, rinominando &quot;Scarpe rosse&quot; in &quot;Scarpe rosse iconiche&quot;), tale valore del nuovo catalogo viene rispettato e l&#39;opportunità LLM Optimizer correlata viene generalmente contrassegnata come *Non aggiornato* in LLM Optimizer perché il catalogo live non corrisponde più al contesto del suggerimento.

### Sostituzione manuale in Admin {#manual-override-in-the-admin}

Se modifichi manualmente il nome o la descrizione del prodotto in [!DNL Adobe Commerce] *Admin*:

- Il valore *Admin* vince come sistema di registrazione per la modifica manuale.
- L&#39;opportunità LLM Optimizer è contrassegnata *Non aggiornato*.
- In LLM Optimizer, l’interfaccia utente torna allo stato originale per tale opportunità, in modo da poter ridefinire la linea di base o accettare un nuovo suggerimento se l’analisi viene eseguita nuovamente.

Queste regole ti aiutano a capire se LLM Optimizer, i feed di acquisizione o le modifiche di *Amministratore* sono autorevoli quando più canali toccano la stessa SKU.

## Best practice

- **Documentare la proprietà del sistema** per il nome e la descrizione del prodotto in modo che i processi PIM o di feed non entrino in conflitto involontariamente con le aspettative di LLM Optimizer.
- **Coordinati con i team SEO e brand** prima di distribuire titoli o descrizioni in blocco.
- **Risincronizza** o **rianalizza** dopo le importazioni principali del catalogo in modo che le opportunità riflettano lo stato corrente del catalogo.

## Prova la demo

Utilizza l’ambiente demo di Frescopa per vedere in azione entrambi i tipi di opportunità Commerce:

- [Visualizza demo sull’arricchimento del catalogo dei prodotti](https://play.llmo.now/org/demo-org/opportunities/commerce-product-catalog-enrichment/e5f2a854-7477-421c-820f-74d5dd595647?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)
- [Demo di arricchimento della pagina Dettagli prodotto](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## Argomenti correlati

- [Connettere Adobe Commerce a LLM Optimizer](connect-to-llmo.md)
- [Panoramica dell’integrazione](../overview.md)
- [Limiti e limiti dell’integrazione](../boundaries-limits.md)
