---
title: Opportunità
description: Identifica le opportunità per incrementare il traffico, il coinvolgimento e le conversioni tramite l’integrazione con Adobe Sites Optimizer per miglioramenti intelligenti dei siti basati sui dati.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo a  [!DNL Adobe Commerce Optimizer]  progetti (infrastruttura SaaS gestita da Adobe)."
TQID: https://experienceleague.adobe.com/KQb7XtqY-4Qrt4B9fwn9w6u8yBjwsj4owArk53v6VHo
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b4dd41a7-ccf8-4e9d-918e-acaab534a307id: b5520579-b31f-4df7-9281-f0d9f91e2edcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11id: cc72dcf1-72e1-48cc-b434-e7c27d62d67cid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 1445
ht-degree: 0%

---

# Opportunità

La pagina **Opportunità** consente di identificare e implementare ottimizzazioni per migliorare il traffico del sito, il coinvolgimento degli utenti e i tassi di conversione tramite l&#39;integrazione con Adobe Sites Optimizer.

![Opportunità](../assets/opportunities.png)

## Cosa sono le opportunità?

Le [opportunità](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/documentation/opportunities/overview) sono consigli basati sull&#39;intelligenza artificiale che aiutano i merchandising a identificare e risolvere i problemi che influiscono sulle prestazioni del sito di e-commerce. Questi consigli sono basati su [Adobe Experience Manager Sites Optimizer](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/home), un servizio basato su cloud che analizza e migliora le prestazioni del sito Web.

## Funzionalità principali

- **Rilevamento automatico dei problemi**: Sites Optimizer analizza continuamente cataloghi di prodotti, registri di ricerca e dati dei consigli per identificare i problemi che influiscono sull&#39;individuazione.
- **Consigli basati sull&#39;intelligenza artificiale**—Ricevi suggerimenti intelligenti per risolvere i problemi rilevati.
- **Categorizzazione dell&#39;impatto**: i problemi sono suddivisi in categorie in base all&#39;impatto aziendale (ricerca, Recommendations, navigazione/navigazione, qualità dei dati del prodotto).
- **Report del dashboard**: visualizza le tendenze dei problemi, i prodotti o le query più interessati e i miglioramenti nel tempo.

## Introduzione

Per abilitare le opportunità in [!DNL Adobe Commerce Optimizer], contatta il tuo Customer Success Manager (CSM). Le opportunità sono disponibili con la licenza **Ultima** Adobe Sites Optimizer.

## Presentazione rapida

La pagina Opportunità è organizzata in tre schede che consentono di gestire i consigli di ottimizzazione:

- **Corrente (attiva)** - Visualizza le opportunità appena rilevate che richiedono revisione e azione. Si tratta di problemi attivi che potrebbero influire sulle prestazioni del sito.
- **Ignorato** - Contiene le opportunità che si è scelto di ignorare o posticipare. È possibile spostare le opportunità qui se non sono rilevanti per gli obiettivi aziendali correnti.
- **Ottimizzato (completato)**: mostra le opportunità che sono state corrette tramite la distribuzione di correzione automatica. Tutte le opportunità gestite manualmente non vengono visualizzate in questa scheda. Questa scheda consente di tenere traccia delle opportunità fisse automaticamente nel tempo.

![Opportunità correnti](../assets/current-opportunities.png)

## Rilevamento automatico del flusso di lavoro

Il flusso di lavoro di rilevamento automatico utilizza l’analisi basata sull’intelligenza artificiale per identificare automaticamente le opportunità di ottimizzazione nel catalogo dei prodotti. Questo processo di scansione automatizzato monitora continuamente i dati dei prodotti, i registri di ricerca e le prestazioni dei consigli per rilevare i problemi che potrebbero influire sulle prestazioni del sito, sulla SEO (Search Engine Optimization) e sul coinvolgimento dei clienti.

### Come funziona

Il rilevamento automatico sfrutta Adobe Experience Manager Sites Optimizer per:

- **Analizza pagine prodotto**: il sistema esamina le prime 200 pagine e i filtri per le pagine dei dettagli del prodotto per identificare i target di ottimizzazione.
- **Estrai metadati**: i tag Meta (titoli, descrizioni, intestazioni H1) vengono estratti da ogni pagina per l&#39;analisi.
- **Generate AI recommendations**—I dati estratti vengono elaborati tramite il flusso di lavoro di intelligenza artificiale di Adobe per creare suggerimenti di ottimizzazione fruibili.
- **Popola opportunità** - I suggerimenti rilevati automaticamente vengono visualizzati nella scheda **Corrente (attiva)** per la revisione.

### Prerequisito

Prima che il rilevamento automatico possa generare consigli, i dati del catalogo devono essere sincronizzati e aggiornati per garantire consigli accurati.

### Cosa succede dopo

Una volta che il rilevamento automatico identifica le opportunità di ottimizzazione, puoi:

- Rivedi le ottimizzazioni suggerite nella scheda **Corrente (attiva)**.
- Distribuisci automaticamente le correzioni utilizzando il [flusso di lavoro di correzione automatica](#auto-fix-workflow) (per i [tipi di opportunità](#supported-opportunity-types) supportati).
- Implementa le modifiche manualmente nell’amministratore di Commerce.
- Ignora le opportunità che non sono in linea con gli obiettivi aziendali.

## Flusso di lavoro di correzione automatica

Il flusso di lavoro di correzione automatica consente di distribuire rapidamente le ottimizzazioni generate dall’intelligenza artificiale con un solo clic. Quando applicate una correzione automatica, il sistema crea un livello di ottimizzazione del catalogo che sostituisce attributi di prodotto specifici senza modificare i dati di prodotto originali. I dati originali del prodotto rimangono intatti, consentendo di applicare in modo sicuro le ottimizzazioni e ripristinare le modifiche in qualsiasi momento. Per ulteriori informazioni, consulta [Funzionamento dei livelli del catalogo con la correzione automatica](#how-catalog-layers-work-with-auto-fix).

### Tipi di opportunità supportati

Di seguito sono elencati i tipi di opportunità supportati:

- Titolo troppo lungo
- Titolo troppo breve
- Titolo duplicato
- Titolo mancante
- Titolo vuoto
- Descrizione troppo lunga
- Descrizione troppo breve
- Descrizione mancante
- Descrizione vuota
- Descrizione duplicata
- H1 mancante
- H1 duplicato
- H1 troppo lungo

>[!NOTE]
>
>Attualmente non sono supportati più H1 sulla pagina.

### Prerequisiti

Prima di utilizzare la correzione automatica, assicurati:

- Il catalogo prodotti è stato completamente acquisito in [!DNL Adobe Commerce Optimizer].
- Il tipo di opportunità supporta la correzione automatica (alcuni tipi di ottimizzazione richiedono l’implementazione manuale).
- Si dispone delle autorizzazioni appropriate per creare e gestire i livelli di catalogo.

>[!IMPORTANT]
>
>La funzione di correzione automatica richiede un catalogo dei prodotti completamente acquisito. Se il catalogo non è ancora stato acquisito, puoi comunque visualizzare le opportunità e implementare le correzioni manualmente utilizzando il file CSV fornito. Tieni presente che le implementazioni manuali non vengono tracciate nella scheda **Ottimizzato (Fine)**.

### Distribuire un&#39;ottimizzazione della correzione automatica

Per implementare un’ottimizzazione suggerita dall’intelligenza artificiale, segui i passaggi seguenti:

1. Passa a **Gestisci risultati** > **Opportunità**.

1. Nella scheda **Corrente (attiva)**, controlla i suggerimenti di ottimizzazione disponibili.

1. Seleziona un’opportunità.

   ![Seleziona opportunità](../assets/autofix-opportunity.png)

   >[!NOTE]
   >
   >Il pulsante **Distribuisci ottimizzazione** è disponibile solo per [tipi di suggerimenti supportati](#supported-opportunity-types). Per i tipi non supportati, la casella di controllo è disabilitata ed è necessario applicare le correzioni manualmente nel catalogo.

1. Fai clic su **Distribuisci ottimizzazione**, quindi su **Distribuisci** per attivare il processo di correzione automatica.

   ![Ottimizzazione distribuzione](../assets/deploy-autofix.png)

   Il sistema esegue in background le seguenti azioni:

   - Crea un nuovo livello di catalogo per il prodotto (se non ne esiste già uno).
   - Aggiorna l’attributo pertinente (ad esempio titolo meta, descrizione o H1) in base alla raccomandazione di IA.
   - Assegna al nuovo livello la priorità più alta (numero più alto) nella vista catalogo.
   - Convalida la modifica tramite il servizio di vetrina del catalogo.

1. Monitorare lo stato della distribuzione. Al termine della convalida, il sistema aggiorna automaticamente lo stato del suggerimento.

1. Una volta ottimizzato, il suggerimento si sposta sulla scheda **Ottimizzato (Fine)** con un indicatore di stato:

   - **Segno di spunta verde** - Il livello di ottimizzazione è impostato come priorità principale e viene applicato attivamente alla vetrina.
   - **Icona di avviso** - Il livello esiste ma non è la priorità principale, il che significa che può essere sostituito da un altro livello.

   ![Opportunità completate](../assets/done-opportunities.png)

>[!NOTE]
>
>La correzione automatica supporta l’ottimizzazione dei metadati per i siti in qualsiasi lingua. Sites Optimizer analizza le pagine dei dettagli del prodotto nella lingua originale, genera consigli di IA localizzati e crea livelli di catalogo in base alle impostazioni locali di origine configurate nella vista catalogo.

### Funzionamento dei livelli del catalogo con la correzione automatica

Se nella vista catalogo non è presente un livello Sites Optimizer di Adobe, la funzione di correzione automatica ne crea automaticamente uno e gli assegna la priorità più alta (il numero più alto). Se eliminate questo livello, verrà ricreato alla successiva esecuzione della correzione automatica e sposterà i livelli esistenti in numeri di ordine inferiori. Se il livello Sites Optimizer di Adobe esiste già con un numero di ordine diverso, la correzione automatica non ne modifica la priorità. Se desiderate mantenere un livello di correzione automatica, ma non utilizzarlo immediatamente, potete disattivare il livello. Ulteriori informazioni su come gestire i [livelli catalogo](../setup/catalog-layer.md#activate-deactivate-or-delete-layers).

![Livelli catalogo](../assets/catalog-layers.png)

Il diagramma mostra una singola riga denominata **Ottimizzazione ASO**. Questa voce rappresenta tutte le opportunità che si sceglie di correggere automaticamente. Sia che si corregga automaticamente una o più opportunità, queste vengono visualizzate tutte in questa singola riga **Ottimizzazione ASO**. I livelli sono specifici per ogni visualizzazione catalogo, pertanto la visualizzazione **Los Angeles** catalogo qui mostrata applica il relativo livello **Ottimizzazione ASO** solo quando tale visualizzazione è attiva.

### Considerazioni importanti

Tieni presente quanto segue quando utilizzi la correzione automatica:

- Lo stato visualizzato per ogni suggerimento riflette lo stato al momento dell&#39;esecuzione del processo di correzione automatica. Lo stato non viene aggiornato in modo dinamico se successivamente riordinate manualmente i livelli del catalogo.

- Per garantire che le ottimizzazioni rimangano attive, evita di modificare manualmente le priorità del livello di catalogo dopo la distribuzione dei consigli di correzione automatica.

### Risoluzione dei problemi

Se non sembra essere stata applicata un’ottimizzazione nella vetrina:

1. Controllare l&#39;indicatore di stato nella scheda **Ottimizzato (Fine)**.
1. Se viene visualizzata un&#39;icona di avviso, verificare le impostazioni di priorità del livello di catalogo.
1. Assicurati che il livello di ottimizzazione sia impostato come priorità più alta (numero più alto) nella vista catalogo.
1. Verifica che la sincronizzazione dei dati del catalogo sia attiva e aggiornata.
1. Consenti la propagazione delle modifiche. Anche con un livello configurato correttamente al numero di ordine più alto, la visualizzazione delle modifiche nella vetrina potrebbe richiedere del tempo, analogamente al ritardo nella pubblicazione di nuovi prodotti.

## Collaborazione tra Sites Optimizer e le metriche di successo

Le metriche di successo monitorano gli indicatori delle prestazioni chiave, ad esempio l’individuazione dei prodotti e l’efficienza aziendale del catalogo, mentre le opportunità all’interno di Sites Optimizer consentono di sapere come aumentare l’ottimizzazione SEO (Search Engine Optimization), la velocità di caricamento, l’accessibilità e il coinvolgimento. Insieme, i commercianti e gli addetti al marketing possono migliorare l&#39;efficienza operativa, offrendo prestazioni e vantaggi di conversione end-to-end più rapidi con un supporto IT minimo. Per scoprire come sfruttare queste due tecnologie per migliorare le prestazioni e l&#39;esperienza della vetrina, consulta [Utilizzo congiunto di metriche di successo e Sites Optimizer](./success-metrics.md#using-success-metrics-and-sites-optimizer-together).

## Ulteriori informazioni su Sites Optimizer

Per informazioni dettagliate sulle funzionalità di Sites Optimizer, consulta la [documentazione di Adobe Experience Manager Sites Optimizer](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/home).

Risorse aggiuntive:

- [Tipi di opportunità](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/opportunities) - Informazioni sulle opportunità di ottimizzazione disponibili.
- [Funzionalità di Sites Optimizer](https://experienceleague.adobe.com/en/docs/experience-manager-sites-optimizer/content/capabilities) - Scopri le funzionalità di Sites Optimizer.

## Altri argomenti correlati

- [Metriche di successo](success-metrics.md) - Monitoraggio degli indicatori prestazioni chiave.
- [Prestazioni ricerca](search-performance.md) - Analizza i termini di ricerca e ottimizza la rilevanza.
- [Prestazioni consigli](recommendation-performance.md) - Monitora l&#39;efficacia dei consigli.
