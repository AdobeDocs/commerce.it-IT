---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 0%
---
I livelli del catalogo consentono di modificare i dati del prodotto senza modificare i dati di origine originali. I livelli modificano gli attributi del prodotto, ad esempio nome, descrizione, immagini, collegamenti e metadati, creando un livello sopra il catalogo di base. I dati originali del prodotto rimangono intatti e consentono di personalizzare i prodotti in modo sicuro e ripristinare le modifiche in qualsiasi momento.

![Livelli catalogo](/help/assets/ccdm-shared/setup/catalog-layers.png)

## Accedere all’area di lavoro Visualizzazioni catalogo

Puoi gestire i livelli del catalogo dall&#39;area di lavoro *Visualizzazioni catalogo* selezionando una visualizzazione catalogo. La modalità di apertura dell’area di lavoro dipende dal prodotto utilizzato:

- **Amministratore Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleziona *Catalogo* > **Visualizzazioni catalogo**.
- **Adobe Commerce Optimizer Studio**—Seleziona *Configurazione archivio* > **Visualizzazioni catalogo**.

## Funzionamento dei livelli del catalogo

Quando un cliente visualizza la vetrina, il sistema combina i dati del catalogo di base con i livelli di catalogo attivi per visualizzare le informazioni finali sul prodotto. Il processo funziona come segue:

1. **Applicazione layer**: quando viene effettuata una richiesta con un ID di canale e un ID ambiente, il servizio di archiviazione recupera la vista catalogo pertinente.

1. **Unione dati** - Il sistema applica i livelli di catalogo ai dati di prodotto in base all&#39;ordine di priorità dei livelli.

1. **Gestione dei campi**—I diversi tipi di campi vengono elaborati in modo diverso:

   * **Sovrascrivi campi** - I campi di testo come nome, descrizione e metatitoli vengono sostituiti con valori di livello e il livello con priorità più elevata ha la precedenza.
   * **Unisci campi** - I campi array come immagini, collegamenti e attributi vengono combinati da più livelli, fornendo una risposta unificata.

1. **Risoluzione priorità**: il campo dell&#39;ordine determina quale livello ha la precedenza. Quando più livelli modificano lo stesso campo, il livello con il numero di ordine più alto ha priorità più alta (ad esempio, l&#39;ordine 10 è il più alto).

## Casi di utilizzo del livello catalogo

I livelli catalogo vengono comunemente utilizzati per:

* **Ottimizzazione SEO**—Sovrascrivi i titoli e le descrizioni dei metadati del prodotto in base ai consigli di IA di [Sites Optimizer](../manage-results/opportunities.md).
* **Campagne stagionali**: aggiorna temporaneamente nomi di prodotto, descrizioni o immagini per le promozioni senza modificare i dati di origine.
* **Personalizzazione regionale**: visualizza informazioni di prodotto diverse in base alla posizione geografica o alla lingua.
* **Test A/B**: verifica diverse presentazioni di prodotti per ottimizzare i tassi di conversione.
* **Gestione multimarca**—Personalizza gli attributi del prodotto per diverse visualizzazioni del catalogo dei marchi.
* **Visualizzazioni prodotto**: applica le immagini di prodotto da AEM Assets come livello sul catalogo di base.

## Livello AEM-Assets

Questo livello contiene immagini di prodotto sincronizzate da AEM Assets. Come altri livelli del catalogo, viene compilato tramite l&#39;[API dei livelli di prodotto](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank}. Il servizio di integrazione di Assets trasforma i metadati delle risorse AEM e gli URL di consegna nel formato API e invia automaticamente i dati quando le risorse vengono approvate in AEM Assets.

L’integrazione supporta un’origine per tenant (una lingua + un livello).

### Come funziona il livello AEM-Assets

1. **Creazione automatica**: il livello viene creato quando l&#39;integrazione AEM Assets è configurata per l&#39;istanza.

1. **Sincronizzazione immagine**: quando le risorse vengono approvate in AEM Assets, Assets Integration Service trasforma i dati della risorsa e aggiorna il livello `AEM-Assets` tramite l&#39;API dei livelli di prodotto.

1. **Assegnazione livello**: assegna il livello `AEM-Assets` alle visualizzazioni catalogo in cui desideri visualizzare le immagini AEM Assets.

### Assegnare il livello AEM-Assets a una vista catalogo

>[!CAUTION]
>
> Assegna il livello AEM-Assets alla vista catalogo. Se il livello non è assegnato, i dati dell&#39;immagine del prodotto vengono sovrascritti in modo imprevisto.

Per visualizzare le immagini AEM Assets nella vetrina:

1. Dall&#39;area di lavoro Visualizzazioni catalogo, selezionate la vista catalogo in cui desiderate applicare il livello.

1. Nella sezione livelli catalogo, individua il livello **AEM-Assets**.

1. Per attivare il livello per questa vista catalogo, attivatelo.

1. Fare clic su **[!UICONTROL Save]** per applicare le modifiche.

Una volta assegnati, Merchandising Services e le API GraphQL di Storefront restituiscono sia le immagini del catalogo di base che le immagini AEM Assets per i prodotti.

## Aggiungere un livello di catalogo tramite l’acquisizione dei dati

Puoi aggiungere livelli di catalogo ai prodotti durante il processo di acquisizione dei dati. Questo metodo è ideale per operazioni in blocco o flussi di lavoro automatizzati. I livelli del catalogo vengono importati utilizzando l&#39;API di acquisizione, ma [l&#39;impostazione dell&#39;ordine](#manage-layer-priorities) dei livelli viene eseguita mediante l&#39;interfaccia utente.

**Prerequisiti:**

* Credenziali API con autorizzazione per accedere al servizio di acquisizione dati
* SKU di prodotto già presenti nel catalogo di base

**Passaggi:**

1. Preparate i dati dei livelli nel formato richiesto con gli attributi del prodotto che desiderate modificare.

1. Utilizza l’endpoint API Product Layers per acquisire i dati del livello.

1. Verificate che il livello sia stato correttamente acquisito controllando la configurazione della vista catalogo.

Per informazioni dettagliate sulle specifiche API e sugli esempi di payload, consulta [Livelli di prodotto](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers){target=_blank} nella documentazione per gli sviluppatori.

## Aggiungere manualmente un livello catalogo nell’interfaccia utente

L’interfaccia utente per la visualizzazione del catalogo consente di creare e gestire manualmente i livelli, il che è particolarmente utile per integrazioni come Sites Optimizer che generano consigli basati sull’intelligenza artificiale. Per le operazioni di livello bulk, utilizza il metodo API di acquisizione dati [descritto sopra](#add-a-catalog-layer-via-data-ingestion).

Se nella vista catalogo non esiste un livello Sites Optimizer, la funzione di correzione automatica di Sites Optimizer ne crea automaticamente uno e gli assegna la priorità più alta (numero più alto). Se eliminate questo livello, questo viene ricreato alla successiva esecuzione della feature di correzione automatica in Sites Optimizer e sposta i livelli esistenti in numeri di ordine inferiori. Se il livello Sites Optimizer esiste già con un numero di ordine diverso, la funzione di correzione automatica non ne modifica la priorità.

**Per creare un livello manuale:**

1. Dall&#39;area di lavoro **[!UICONTROL Catalog views]**, selezionare la vista catalogo in cui si desidera applicare il livello.

1. Nella sezione livelli catalogo fare clic su **Aggiungi livello catalogo**.

1. Configura le proprietà del livello:

   * **Nome livello** - Immettere un nome descrittivo per identificare lo scopo del livello.
   * **Prodotti**—Selezionare i prodotti a cui si applica questo livello.
   * **Attributi** - Scegli gli attributi del prodotto da modificare (nome, descrizione, immagini, metatag e così via).
   * **Valori** - Immettere i nuovi valori per ogni attributo selezionato.

1. Fare clic su **[!UICONTROL Save]** per creare il livello.

Il nuovo livello viene aggiunto alla vista catalogo e gli viene assegnato automaticamente il successivo numero di ordine disponibile.

## Anteprima effetti livello


Prima di attivare i livelli o modificare le priorità, puoi visualizzare in anteprima come influiscono sui dati dei prodotti.

**Per visualizzare in anteprima le modifiche ai livelli:**

1. Dall&#39;area di lavoro **[!UICONTROL Catalog views]**, selezionare la vista catalogo con i livelli da visualizzare in anteprima.

1. Nella sezione livelli catalogo, seleziona un prodotto specifico o utilizza la funzione di anteprima.

1. Esaminate i dati dei prodotti combinati che mostrano come i livelli modificano i valori del catalogo di base.

1. Apportare le modifiche necessarie al contenuto o all&#39;ordine di priorità del livello.

## Gestire l&#39;attivazione e l&#39;eliminazione dei livelli

È possibile abilitare o disabilitare i livelli di catalogo senza eliminarli, consentendo di controllare quando vengono applicate personalizzazioni specifiche.

**Per attivare o disattivare un livello:**

1. Dall&#39;area di lavoro **[!UICONTROL Catalog views]**, selezionare la vista catalogo contenente il livello.

1. Nella sezione dei livelli del catalogo, individuate il livello da attivare/disattivare.

1. Fate clic sull&#39;interruttore di attivazione per attivare o disattivare il livello.

   * **Attivo** - Il livello viene applicato ai dati del prodotto.
   * **Inattivo** - Il livello viene mantenuto ma non applicato ai dati del prodotto.

1. La modifica ha effetto immediato sulla vetrina.

**Per eliminare un livello:**

Utilizza l&#39;API di acquisizione dati per [eliminare un livello di catalogo](https://developer.adobe.com/commerce/services/reference/rest/#operation/deleteProductLayers){target=_blank}.

## Gestire le priorità dei livelli

L&#39;ordine in cui vengono applicati i livelli determina quali valori vengono visualizzati nella vetrina quando più livelli modificano lo stesso attributo di prodotto. La gestione delle priorità garantisce la visualizzazione dei dati corretti.

**Informazioni sull&#39;ordine prioritario:**

* A ciascun livello viene assegnato un numero d&#39;ordine (1, 2, 3 e così via)
* I numeri più alti indicano una priorità più alta ed escludono tutti gli altri livelli
* Quando più livelli modificano lo stesso campo, il livello con il numero di ordine più alto ha la precedenza
* La priorità si applica solo ai campi di sostituzione (nome, descrizione, metatag)
* I campi unione (immagini, collegamenti, attributi) combinano i dati di tutti i livelli

**Per riordinare le priorità dei livelli:**

1. Dall&#39;area di lavoro **[!UICONTROL Catalog views]**, selezionare la vista catalogo contenente i livelli che si desidera riordinare.

1. Nella sezione livelli catalogo individuare il livello che si desidera spostare.

1. Trascinate e rilasciate il livello per modificarne la posizione o utilizzate i controlli di riordinamento.

1. Il sistema aggiorna automaticamente i numeri di ordine in base alla nuova sequenza.

1. Fare clic su **[!UICONTROL Save]** per applicare il nuovo ordine di priorità.

>[!IMPORTANT]
>
>Le modifiche apportate alla priorità dei livelli hanno effetto immediato e hanno un impatto immediato su ciò che i clienti vedono nella vetrina. Controlla l’anteprima prima di salvare per assicurarti di applicare i valori corretti.

## Best practice

Segui questi consigli quando lavori con i livelli del catalogo:

* **Utilizzare nomi descrittivi**—I livelli dei nomi indicano chiaramente il loro scopo (ad esempio, &quot;Campagna di vacanze 2025&quot; o &quot;Ottimizzazione SEO — Pagine prodotto&quot;).

* **Limita livelli** - Anche se il sistema supporta più livelli, l&#39;utilizzo di troppi livelli può influire sulle prestazioni. Se possibile, consolidare i livelli.


* **Logica di priorità del documento** - Tieni traccia dei livelli che hanno la precedenza per evitare sostituzioni non intenzionali.

* **Rivedi livelli Sites Optimizer** - Quando si utilizza la correzione automatica di Sites Optimizer, vengono creati livelli con la massima priorità. Presta attenzione quando aggiungi livelli manuali che sostituiscono i consigli di IA. Ulteriori informazioni sull&#39;utilizzo di [Sites Optimizer](../manage-results/opportunities.md).

* **Monitoraggio delle prestazioni**: se si notano caricamenti lenti delle pagine dei prodotti, rivedere la configurazione dei livelli e considerare il consolidamento dei livelli.

## Altri argomenti correlati

* [Visualizzazioni catalogo](catalog-view.md)—Configurare le visualizzazioni catalogo per diversi storefront
* [Visualizzazioni prodotto](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/product-visuals): utilizza AEM Assets per le immagini dei prodotti
* [Opportunità](../manage-results/opportunities.md): informazioni sull&#39;ottimizzazione basata sull&#39;intelligenza artificiale tramite i livelli del catalogo
* [Chiavi di accesso limitate](restricted-access-keys.md)—Proteggere una vista catalogo con autenticazione token firmato
