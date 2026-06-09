---
title: Filtri per consigli
description: Scopri come utilizzare i filtri per controllare quali prodotti vengono visualizzati nei  [!DNL Adobe Commerce Optimizer]  consigli.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
TQID: https://experienceleague.adobe.com/-pmVrAgEsSkn66K00-eaoQ4TF-7Xyxuwlniip1cR4HM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 116d8bd804df364ddc9cb1175525f08fd32c01bf
workflow-type: tm+mt
source-wordcount: 1919
ht-degree: 0%

---

# Filtra prodotti

[!DNL Adobe Commerce Optimizer] applica automaticamente filtri predefiniti non configurabili alle unità di consigli. Se in una pagina sono distribuite più unità di consigli, [!DNL Adobe Commerce Optimizer] esclude tutti i prodotti ripetuti nelle unità. Viene utilizzato solo il primo riferimento a un prodotto ripetuto, per fare spazio ad altri prodotti da consigliare. [!DNL Adobe Commerce Optimizer] esclude anche i prodotti acquistati in precedenza e quelli presenti nel carrello.

Quando [crei](create.md) un&#39;unità di consigli, puoi definire filtri che controllano quali prodotti possono essere visualizzati nei consigli. Questi filtri si basano su un set di condizioni di inclusione o esclusione definite dall’utente. Solo i prodotti che corrispondono a tutte le condizioni di inclusione vengono visualizzati nei consigli. Non sono consigliati i prodotti che soddisfano una qualsiasi delle condizioni di esclusione.

Per configurare più filtri e abilitarli solo quelli desiderati, seleziona l’opzione (Attiva/Disattiva) in ogni pagina del filtro. Ciò consente di creare bozze di filtri da utilizzare in futuro. Il numero di filtri attivati viene visualizzato in ogni scheda.

## Condizioni

Le condizioni possono essere statiche o dinamiche.

- Una condizione statica utilizza gli attributi di prodotto esistenti per determinare quali prodotti possono comparire nell’unità. Ad esempio, è possibile specificare che solo i prodotti in magazzino con un prezzo superiore a 25 $ vengano visualizzati nell&#39;unità.

- Una condizione dinamica chiave del contesto corrente di un acquirente, ad esempio la categoria o il prodotto attualmente visualizzato. Ad esempio, quando crei un consiglio di prodotto da distribuire nelle pagine dei dettagli del prodotto, puoi utilizzare un [filtro prezzo dinamico](#dynamic-price-filters-relative-to-current-product) per includere o escludere prodotti all&#39;interno di un intervallo di prezzo relativo del prodotto visualizzato.

### Operatori logici

Gli operatori logici `AND` e `OR` vengono utilizzati per unire più condizioni. Se utilizzi sia filtri di inclusione che filtri di esclusione tra i tipi di filtro, le inclusioni vengono valutate per prime per determinare tutti i possibili prodotti che possono essere consigliati, quindi i prodotti che corrispondono a eventuali filtri di esclusione vengono rimossi dall’elenco. **Prezzo** i filtri utilizzano un ordine diverso tra le regole di prezzo: esclusioni prima, inclusioni poi. Vedi [Come usare il prezzo per le regole di inclusione ed esclusione](#how-include-and-exclude-rules-use-price).

- `AND` - Unisce due condizioni di filtro di inclusione
- `OR` - Unisce due condizioni di filtro di esclusione

## Tipi di filtri

Ogni tipo di filtro esegue il targeting di un aspetto diverso del catalogo, ad esempio prodotto e prezzo, in modo da poter restringere o ampliare i prodotti idonei per un&#39;unità. Scegli i tipi che corrispondono agli obiettivi di merchandising, quindi combina le condizioni di inclusione ed esclusione secondo necessità; le sottosezioni seguenti descrivono il comportamento di ciascun tipo e come [!DNL Adobe Commerce Optimizer] lo applica.

>[!NOTE]
>
>È possibile consigliare solo i prodotti che corrispondono ai filtri di **inclusione** e rimuovere tutti i prodotti che corrispondono a un filtro di **esclusione**.

### Prezzo {#price}

>[!IMPORTANT]
>
>Il filtro del prezzo è in versione beta.

Il filtro dei prezzi utilizza il **prezzo calcolato finale** di ogni prodotto dal **listino prezzi attivo** della vetrina, che è il listino prezzi assegnato alla vetrina in cui viene eseguito il rendering dell&#39;unità di consigli.

Tale valore:

- **Include** sconti, promozioni e prezzi speciali definiti nel listino prezzi dedicato (non solo prezzo di listino).
- **Esclude** le regolazioni a livello di spedizione e carrello.
- **Si applica solo** al listino prezzi attivo per quella vetrina; non vengono utilizzati altri storefront o listini prezzi.

Configurare il modo in cui i listini prezzi sono associati a una vetrina nel catalogo e l&#39;installazione di [listini prezzi](../../setup/pricebooks.md).

#### Come includere ed escludere regole usa prezzo {#how-include-and-exclude-rules-use-price}

- **Regole di esclusione** - I prodotti il cui prezzo finale **corrisponde a qualsiasi** esclusione prezzo definita vengono rimossi per primi.
- **Regole di inclusione** - Tra i candidati rimanenti, solo i prodotti il cui prezzo finale **corrisponde a tutte** le condizioni di inclusione prezzo definite rimangono idonei. Ciò include ogni filtro di inclusione abilitato (ad esempio, la regola del prezzo più altre regole di inclusione).

Le regole di prezzo **filtrano** il set di candidati per i consigli; **non** riclassificano i prodotti. Il motore genera un elenco di classificazione, le regole di inclusione ed esclusione dei prezzi rimuovono i prodotti da tale elenco e l&#39;ordine relativo dei prodotti rimanenti rimane invariato. Se il numero di prodotti idonei è inferiore a quello delle richieste di unità, verranno visualizzati solo gli articoli validi. Se nessuno è idoneo, l’unità non viene riprodotta (nessun segnaposto vuoto).

Il prezzo mostrato sui prodotti all&#39;interno dell&#39;unità di consigli è lo stesso **prezzo finale** del listino prezzi di quel negozio, quindi quello che gli acquirenti vedono corrisponde al valore utilizzato per il filtro. Nell&#39;anteprima di amministrazione, i prodotti configurabili possono mostrare una fascia di prezzo quando i prezzi delle varianti differiscono; vedi [Prodotti configurabili nell&#39;anteprima](#configurable-products-in-preview).

#### Intervallo prezzi statico

Utilizza un filtro prezzo **statico** quando desideri un prezzo minimo o massimo fisso nella valuta di base del tuo negozio, indipendentemente dal prodotto che un acquirente sta visualizzando.

##### Impostare un filtro prezzi statico

1. Durante la [creazione o modifica](create.md) di un&#39;unità di consigli, apri **[!UICONTROL Filter products]** (o passa al passaggio _Filtri_ dal flusso di lavoro dell&#39;unità).
1. Selezionare la scheda **[!UICONTROL Inclusions]** o **[!UICONTROL Exclusions]**, a seconda che si desideri consentire solo i prodotti in una fascia di prezzo o bloccare i prodotti in un intervallo. Il badge in ogni scheda mostra il numero di filtri di quel tipo abilitati.
1. Nell&#39;elenco a sinistra, selezionare **[!UICONTROL Price]**.
1. Attiva **[!UICONTROL Enable filter]**.

   I valori di prezzo utilizzano la valuta di base del sito Web **&#x200B;**, come indicato nella pagina.

1. Aprire **[!UICONTROL Include products based on]** (nella scheda **[!UICONTROL Inclusions]**) o il controllo equivalente nella scheda **[!UICONTROL Exclusions]** e scegliere **[!UICONTROL Set price range]**.
1. Impostare un **[!UICONTROL Min price]** e/o un **[!UICONTROL Max price]** facoltativo utilizzando i campi accanto al simbolo di valuta. È possibile digitare gli importi o utilizzare i controlli **-** e **+** per regolare i valori. Lascia vuoto un limite se non hai bisogno di un minimo o di un massimo. L&#39;intervallo viene confrontato con il prezzo calcolato finale di ciascun prodotto per il listino prezzi attivo del negozio.
1. Completa la configurazione dell’unità di consigli e salva o pubblica come di consueto, in modo che il filtro diventi effettivo.

![Filtro prezzi](../../assets/filter-price.png)

#### Filtri di prezzo dinamici (relativi al prodotto corrente) {#dynamic-price-filters-relative-to-current-product}

Utilizza un filtro prezzo **dinamico** quando i consigli devono essere limitati rispetto al **prodotto visualizzato** in una pagina dettagli prodotto (PDP). Il filtro utilizza il prezzo finale del prodotto come **ancoraggio** e confronta i prodotti consigliati con i limiti definiti dall&#39;utente.

Gli operatori dinamici sono disponibili solo per [tipi di consigli relativi allo SKU](types.md) eseguiti in un contesto di prodotto, ad esempio:

- Ha visualizzato questo, ha visualizzato quello
- Ho visto questo, ho comprato quello
- Ho comprato questo e quello
- Altri argomenti correlati
- Somiglianza visiva

Sono **non** disponibili per i tipi basati sulla popolarità (ad esempio, **Più visualizzati** o **Più acquistati**) perché tali unità non hanno un singolo prodotto corrente per ancorare il filtro.

Nella vetrina, il menu a discesa per i consigli legge il prezzo del prodotto corrente dal contesto PDP e lo invia con la richiesta di consigli. [!DNL Adobe Commerce Optimizer] utilizza tale valore come ancoraggio durante la valutazione delle regole di prezzo dinamiche. Per i prodotti configurabili, l&#39;ancoraggio corrisponde al prezzo finale **variante più bassa** (`priceRange.minimum`).

##### Operatori

In **[!UICONTROL Include products based on]** (o l&#39;equivalente delle esclusioni), puoi scegliere:

| Operatore | Finalità |
| --- | --- |
| **Minore o uguale al prezzo del prodotto corrente** | Includi o escludi i prodotti in corrispondenza o al di sotto di un limite derivato dal prezzo di ancoraggio più un offset. |
| **Maggiore o uguale al prezzo del prodotto corrente** | Includi o escludi prodotti in corrispondenza o al di sopra di un limite derivato dal prezzo di ancoraggio più un offset. |
| **In un intervallo di valori del prodotto corrente** | Includi o escludi i prodotti il cui prezzo finale rientra in una fascia di valuta fissa intorno all’ancoraggio (offset dal prezzo corrente). |
| **Entro un intervallo percentuale dal prodotto corrente** | Includi o escludi i prodotti il cui prezzo finale rientra in una fascia percentuale intorno all’ancoraggio. |

##### Scostamento semantico

Per **minore o uguale al prezzo del prodotto corrente** e **maggiore o uguale al prezzo del prodotto corrente**, il valore immesso è un **offset numerico aggiunto al prezzo di ancoraggio** per formare il limite:

- Un offset **negativo** sposta il limite **al di sotto** del prezzo del prodotto corrente.
- Un offset **positivo** sposta il limite **al di sopra** del prezzo del prodotto corrente.
- **Vuoto** o **0** significa **nessun limite** su quel lato; il backend li tratta allo stesso modo.
- Impossibile utilizzare **0** per indicare &quot;esattamente il prezzo del prodotto corrente&quot; come limite.

Corrisponde a [!DNL Product Recommendations] su PaaS. Le etichette nell’amministratore riflettono direttamente queste semantiche.

##### Impostare un filtro prezzi dinamico

1. [Crea o modifica](create.md) un&#39;unità di consigli **relativa allo SKU** distribuita nella pagina **dettagli prodotto** (o in un&#39;altra posizione in cui un prodotto corrente è sempre nel contesto).
1. Aprire **[!UICONTROL Filter products]** e selezionare la scheda **[!UICONTROL Inclusions]** o **[!UICONTROL Exclusions]**.
1. Selezionare **[!UICONTROL Price]** e attivare **[!UICONTROL Enable filter]**.
1. Apri **[!UICONTROL Include products based on]** (o l&#39;equivalente delle esclusioni) e scegli un operatore dinamico (ad esempio, **All&#39;interno di un intervallo di valori del prodotto corrente**).
1. Immettete i valori di offset o intervallo come richiesto. Utilizza l’anteprima per confermare i risultati per un prodotto di esempio.
1. Salvare o pubblicare l&#39;unità.

Valori non validi (importi non numerici, combinazioni non supportate o intervalli in cui il valore minimo è maggiore del valore massimo) impediscono il salvataggio e mostrano errori di convalida; **[!UICONTROL Save]** rimane disabilitato finché il filtro non è valido.

##### Se non è disponibile alcun prezzo di ancoraggio

Se un filtro prezzi dinamico è abilitato ma la vetrina non è in grado di fornire un prezzo di prodotto corrente (ad esempio, l&#39;unità viene sottoposta a rendering all&#39;esterno di un contesto PDP), [!DNL Adobe Commerce Optimizer] non restituisce consigli non filtrati. L&#39;unità mostra **nessun consiglio**, perché la visualizzazione dei risultati non filtrati non corrisponderebbe alla regola configurata.

##### Prodotti configurabili in anteprima {#configurable-products-in-preview}

Nel pannello Admin **preview**, i prezzi dei prodotti consigliati vengono visualizzati come segue:

- **Prodotti semplici** - Prezzo finale singolo dalla risposta di GraphQL.
- **Prodotti configurabili** - Se i prezzi delle varianti minimo e massimo sono diversi, l&#39;anteprima mostra un intervallo (ad esempio, `$min – $max`). Se sono uguali, viene visualizzato un singolo prezzo.

Il prezzo di ancoraggio utilizzato per i calcoli dei filtri dinamici su un prodotto configurabile è sempre il prezzo finale della variante **minimum**, coerente con la vetrina.

#### Esempi di filtri di prezzo

Negli esempi seguenti viene utilizzato un prezzo di prodotto corrente di **$500**. Regola inclusione ed esclusione per raggiungere l’obiettivo di merchandising.

| Operatore | Linguetta | Obiettivo | Esempio di limite |
| --- | --- | --- | --- |
| Minore o uguale al prezzo del prodotto corrente | Esclusioni | Promuovere l&#39;upselling nascondendo le alternative a basso prezzo | Escludi prodotti ≤ $500 |
| Minore o uguale al prezzo del prodotto corrente | Inclusioni | Offrire alternative convenienti | Includi prodotti ≤ $500 |
| Maggiore o uguale al prezzo del prodotto corrente | Esclusioni | Evitare l&#39;upselling in un flusso incentrato sul budget | Escludi prodotti ≥ $500 |
| Maggiore o uguale al prezzo del prodotto corrente | Inclusioni | Superficie premium alternative | Includi prodotti ≥ $500 |
| All&#39;interno di un intervallo di valori del prodotto corrente | Esclusioni | Diversificarsi rispetto a punti di prezzo simili | Escludi $ 400- $ 600 |
| All&#39;interno di un intervallo di valori del prodotto corrente | Inclusioni | Mostra alternative comparabili in una banda stretta | Inclusi $ 400- $ 600 |
| Entro un intervallo percentuale del prodotto corrente | Esclusioni | Riduci articoli con prezzi simili (ad esempio ±20%) | Escludere circa $ 400-$ 600 |
| Entro un intervallo percentuale del prodotto corrente | Inclusioni | Confronto equo all&#39;interno di una fascia comparabile | Includere circa $ 400-$ 600 |

### Prodotto

I filtri dei prodotti eseguono il targeting dei singoli elementi del catalogo per **SKU**. Puoi aggiungere uno o più SKU per consentire solo questi prodotti (**Inclusioni**) o bloccarli (**Esclusioni**), utilizzando la stessa pagina **[!UICONTROL Filter products]** dei [filtri prezzo](#price). Non è possibile rendere visibili prodotti disabilitati o non visibili singolarmente in un&#39;unità di consigli; tali prodotti non vengono mai visualizzati nella vetrina indipendentemente dai filtri.

#### Configurare un filtro prodotto

1. Durante la [creazione o modifica](create.md) di un&#39;unità di consigli, apri **[!UICONTROL Filter products]** (o passa al passaggio _Filtri_ dal flusso di lavoro dell&#39;unità).
1. Selezionare la scheda **[!UICONTROL Inclusions]** o **[!UICONTROL Exclusions]**. Il badge in ogni scheda mostra il numero di filtri di quel tipo abilitati.
1. Nell&#39;elenco a sinistra, selezionare **[!UICONTROL Product]**.
1. Attiva **[!UICONTROL Enable filter]**.

   L&#39;intestazione del pannello a destra riflette la scheda, ad esempio **[!UICONTROL Product inclusions]** o l&#39;equivalente per le esclusioni.

1. In **[!UICONTROL Product SKU]**, immettere uno SKU e fare clic su **[!UICONTROL Add]**. Ripeti l’operazione per aggiungere altri SKU.

   In **[!UICONTROL Product SKUs]** ogni SKU viene visualizzato come tag rimovibile. Fai clic su **X** su un tag per rimuovere tale SKU oppure fai clic su **[!UICONTROL Clear All]** per rimuovere ogni SKU dall&#39;elenco.

1. Completa la configurazione dell’unità di consigli e salva o pubblica come di consueto, in modo che il filtro diventi effettivo.

Per **inclusioni**, è possibile consigliare solo i prodotti con SKU elencati (e che soddisfano gli altri filtri di inclusione abilitati). Per **esclusioni**, qualsiasi prodotto con SKU elencato non è consigliato, anche se sarebbe altrimenti idoneo.

![Filtro prodotti](../../assets/filter-product.png)

>[!NOTE]
>
>I prodotti secondari di un prodotto configurabile non vengono visualizzati in un&#39;unità di consigli perché tali prodotti secondari hanno la visibilità di _Non visibile singolarmente_.

<!--
### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.
-->
