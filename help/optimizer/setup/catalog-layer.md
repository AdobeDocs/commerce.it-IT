---
title: Livello catalogo
description: Scopri come i livelli del catalogo consentono di modificare i dati del prodotto senza modificare i dati di origine originali, in modo da poter personalizzare in modo sicuro e ripristinare le modifiche in qualsiasi momento.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 4a904527af172a5e35b87410135d55484d07ad84
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Livello catalogo

I livelli del catalogo consentono di modificare i dati del prodotto senza modificare i dati di origine originali. I livelli applicano le modifiche a specifici attributi del prodotto, come nome, descrizione, immagini, collegamenti e metadati, creando un livello sopra il catalogo di base. I dati originali del prodotto rimangono intatti e consentono di personalizzare in modo sicuro i prodotti e ripristinare le modifiche in qualsiasi momento.

![Livelli catalogo](../assets/catalog-layers.png)

## Funzionamento dei livelli del catalogo

Quando un cliente visualizza la vetrina, il sistema combina i dati del catalogo di base con i livelli di catalogo attivi per visualizzare le informazioni finali sul prodotto. Ecco come funziona il processo:

1. **Applicazione layer**: quando viene effettuata una richiesta con un ID di canale e un ID ambiente, il servizio di archiviazione recupera la vista catalogo pertinente.

1. **Unione dati** - Il sistema applica i livelli di catalogo ai dati di prodotto in base all&#39;ordine di priorità dei livelli.

1. **Gestione dei campi**—I diversi tipi di campi vengono elaborati in modo diverso:

   - **Sostituisci campi** - I campi di testo come nome, descrizione e metatitoli vengono sostituiti con i valori definiti nel livello, con il livello di priorità più alto che ha la precedenza.
   - **Unisci campi** - I campi array come immagini, collegamenti e attributi vengono combinati da più livelli, fornendo una risposta unificata.

1. **Risoluzione priorità**: il campo dell&#39;ordine determina quale livello ha la precedenza. Quando più livelli modificano lo stesso campo, il livello con il numero di ordine inferiore ha priorità maggiore (ad esempio, l&#39;ordine 1 è il più alto).

## Casi di utilizzo del livello catalogo

I livelli catalogo vengono comunemente utilizzati per:

- **Ottimizzazione SEO**—Sovrascrivi i titoli e le descrizioni dei metadati del prodotto in base ai consigli di IA di [Sites Optimizer](../manage-results/opportunities.md).
- **Campagne stagionali**: aggiorna temporaneamente nomi di prodotto, descrizioni o immagini per le promozioni senza modificare i dati di origine.
- **Personalizzazione regionale**: visualizza informazioni di prodotto diverse in base alla posizione geografica o alla lingua.
- **Test A/B**: verifica diverse presentazioni di prodotti per ottimizzare i tassi di conversione.
- **Gestione multimarca**—Personalizza gli attributi del prodotto per diverse visualizzazioni del catalogo dei marchi.

## Aggiungere un livello di catalogo tramite l’acquisizione dei dati

Puoi aggiungere livelli di catalogo ai prodotti durante il processo di acquisizione dei dati. Questo metodo è ideale per operazioni in blocco o flussi di lavoro automatizzati.

>[!NOTE]
>
>I livelli del catalogo vengono importati utilizzando l&#39;API di acquisizione, ma [l&#39;impostazione dell&#39;ordine](#manage-layer-priorities) dei livelli viene eseguita mediante l&#39;interfaccia utente.

**Prerequisiti:**

- Credenziali API con autorizzazione per accedere al servizio di acquisizione dati
- SKU di prodotto già presenti nel catalogo di base

**Passaggi:**

1. Preparate i dati dei livelli nel formato richiesto con gli attributi del prodotto che desiderate modificare.

1. Utilizza l’endpoint API Product Layers per acquisire i dati del livello.

1. Verificate che il livello sia stato correttamente acquisito controllando la configurazione della vista catalogo.

Per informazioni dettagliate sulle specifiche API e sugli esempi di payload, consulta [Livelli di prodotto](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) nella documentazione per gli sviluppatori.

## Aggiungere manualmente un livello catalogo nell’interfaccia utente

>[!NOTE]
>
>Questa funzione non è ancora disponibile.

L’interfaccia utente per la visualizzazione del catalogo consente di creare e gestire manualmente i livelli, il che è particolarmente utile per integrazioni come Sites Optimizer che generano consigli basati sull’intelligenza artificiale.

>[!NOTE]
>
>Se nella vista catalogo non esiste un livello Sites Optimizer, la funzione di correzione automatica di Sites Optimizer ne crea automaticamente uno e gli assegna l&#39;ordine 1 (priorità più alta). Se eliminate questo livello, questo verrà ricreato alla successiva esecuzione della funzione di correzione automatica in Sites Optimizer e sposterà i livelli esistenti in numeri di ordine inferiori. Se il livello Sites Optimizer esiste già con un numero di ordine diverso, la funzione di correzione automatica non ne modifica la priorità.

>[!TIP]
>
>Per le operazioni di livello bulk, utilizza il metodo API di acquisizione dati [descritto sopra](#add-a-catalog-layer-via-data-ingestion).

**Per creare un livello manuale:**

1. Passa a **Store setup** > **Catalog views**.

1. Selezionate la vista catalogo in cui desiderate applicare il livello.

1. Nella sezione livelli catalogo fare clic su **Aggiungi livello catalogo**.

1. Configura le proprietà del livello:

   - **Nome livello** - Immettere un nome descrittivo per identificare lo scopo del livello.
   - **Prodotti**—Selezionare i prodotti a cui si applica questo livello.
   - **Attributi** - Scegli gli attributi del prodotto da modificare (nome, descrizione, immagini, metatag e così via).
   - **Valori** - Immettere i nuovi valori per ogni attributo selezionato.

1. Fai clic su **Salva** per creare il livello.

Il nuovo livello viene aggiunto alla vista catalogo e gli viene assegnato automaticamente il successivo numero di ordine disponibile.

## Anteprima effetti livello

>[!NOTE]
>
>Questa funzione non è ancora disponibile.

Prima di attivare i livelli o modificare le priorità, puoi visualizzare in anteprima come influiscono sui dati dei prodotti.

**Per visualizzare in anteprima le modifiche ai livelli:**

1. Passa a **Store setup** > **Catalog views**.

1. Selezionate la vista catalogo con i livelli da visualizzare in anteprima.

1. Nella sezione livelli catalogo, seleziona un prodotto specifico o utilizza la funzione di anteprima.

1. Esaminate i dati dei prodotti combinati che mostrano come i livelli modificano i valori del catalogo di base.

1. Apportare le modifiche necessarie al contenuto o all&#39;ordine di priorità del livello.

## Attivare, disattivare o eliminare i livelli

È possibile abilitare o disabilitare i livelli di catalogo senza eliminarli, consentendo di controllare quando vengono applicate personalizzazioni specifiche.

**Per attivare o disattivare un livello:**

1. Passa a **Store setup** > **Catalog views**.

1. Selezionate la vista catalogo contenente il livello.

1. Nella sezione dei livelli del catalogo, individuate il livello da attivare/disattivare.

1. Fate clic sull&#39;interruttore di attivazione per attivare o disattivare il livello.

   - **Attivo** - Il livello viene applicato ai dati del prodotto.
   - **Inattivo** - Il livello viene mantenuto ma non applicato ai dati del prodotto.

1. La modifica ha effetto immediato sulla vetrina.

**Per eliminare un livello:**

Utilizza l&#39;API di acquisizione dati per [eliminare un livello di catalogo](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers).

## Gestire le priorità dei livelli

L&#39;ordine in cui vengono applicati i livelli determina quali valori vengono visualizzati nella vetrina quando più livelli modificano lo stesso attributo di prodotto. La gestione delle priorità garantisce la visualizzazione dei dati corretti.

**Informazioni sull&#39;ordine prioritario:**

- A ciascun livello viene assegnato un numero d&#39;ordine (1, 2, 3 e così via)
- L&#39;ordine 1 ha la priorità più alta e sostituisce tutti gli altri livelli
- Quando più livelli modificano lo stesso campo, il livello con il numero di ordine inferiore ha la precedenza
- La priorità si applica solo ai campi di sostituzione (nome, descrizione, metatag)
- I campi unione (immagini, collegamenti, attributi) combinano i dati di tutti i livelli

**Per riordinare le priorità dei livelli:**

1. Passa a **Store setup** > **Catalog views**.

1. Selezionate la vista catalogo contenente i livelli da riordinare.

1. Nella sezione livelli catalogo individuare il livello che si desidera spostare.

1. Trascinate e rilasciate il livello per modificarne la posizione o utilizzate i controlli di riordinamento.

1. Il sistema aggiorna automaticamente i numeri di ordine in base alla nuova sequenza.

1. Fai clic su **Salva** per applicare il nuovo ordine di priorità.

>[!IMPORTANT]
>
>Le modifiche alla priorità dei livelli hanno effetto immediato e possono influire su ciò che i clienti vedono nella vetrina. Controllare l&#39;anteprima prima di salvare per verificare che vengano applicati i valori corretti (**anteprima non ancora disponibile**).

## Best practice

Segui questi consigli quando lavori con i livelli del catalogo:

- **Utilizza nomi descrittivi**—I livelli dei nomi indicano chiaramente il loro scopo (ad esempio, &quot;Campagna di vacanze 2025&quot; o &quot;Ottimizzazione SEO - Pagine prodotto&quot;).

- **Limita livelli** - Anche se il sistema supporta più livelli, l&#39;utilizzo di troppi livelli può influire sulle prestazioni. Se possibile, consolidare i livelli.

<!--- **Test before activating**—Always preview layer effects before activating them on your live storefront. !!!REMOVE IF PREVIEW NOT AVAILABLE FOR GA!!!-->

- **Logica di priorità del documento** - Tieni traccia dei livelli che devono avere la precedenza per evitare sostituzioni non intenzionali.

- **Rivedi livelli Sites Optimizer** - Quando si utilizza la correzione automatica di Sites Optimizer, vengono creati livelli con la massima priorità. Presta attenzione quando aggiungi livelli manuali che potrebbero ignorare i consigli di IA. Ulteriori informazioni sull&#39;utilizzo di [Sites Optimizer](../manage-results/opportunities.md).

- **Monitoraggio delle prestazioni**: se si notano caricamenti lenti delle pagine dei prodotti, rivedere la configurazione dei livelli e considerare il consolidamento dei livelli.

## Altri argomenti correlati

- [Visualizzazioni catalogo](catalog-view.md) - Configura le visualizzazioni catalogo per diversi storefront
- [Opportunità](../manage-results/opportunities.md) - Scopri l&#39;ottimizzazione basata sull&#39;intelligenza artificiale utilizzando i livelli del catalogo
