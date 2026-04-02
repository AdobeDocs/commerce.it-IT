---
title: Filtri per consigli
description: Scopri come utilizzare i filtri per controllare quali prodotti vengono visualizzati nei  [!DNL Adobe Commerce Optimizer]  consigli.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: e15624322fabb89d0b618f9d6c689445a7c448df
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Filtra prodotti

[!DNL Adobe Commerce Optimizer] applica automaticamente filtri predefiniti non configurabili alle unità di consigli. Se in una pagina sono distribuite più unità di consigli, [!DNL Adobe Commerce Optimizer] esclude tutti i prodotti ripetuti nelle unità. Viene utilizzato solo il primo riferimento a un prodotto ripetuto, per fare spazio ad altri prodotti da consigliare. [!DNL Adobe Commerce Optimizer] esclude anche i prodotti acquistati in precedenza e quelli presenti nel carrello.

Quando [crei](create.md) un&#39;unità di consigli, puoi definire filtri che controllano quali prodotti possono essere visualizzati nei consigli. Questi filtri si basano su un set di condizioni di inclusione o esclusione definite dall’utente. Solo i prodotti che corrispondono a tutte le condizioni di inclusione vengono visualizzati nei consigli. Non sono consigliati i prodotti che soddisfano una qualsiasi delle condizioni di esclusione.

Per configurare più filtri e abilitarli solo quelli desiderati, seleziona l’opzione (Attiva/Disattiva) in ogni pagina del filtro. Ciò consente di creare bozze di filtri da utilizzare in futuro. Il numero di filtri attivati viene visualizzato in ogni scheda.

## Condizioni

Le condizioni possono essere statiche o dinamiche.

- Una condizione statica utilizza gli attributi di prodotto esistenti per determinare quali prodotti possono comparire nell’unità. Ad esempio, è possibile specificare che solo i prodotti in magazzino con un prezzo superiore a 25 $ vengano visualizzati nell&#39;unità.

- Una condizione dinamica chiave del contesto corrente di un acquirente, ad esempio la categoria o il prodotto attualmente visualizzato. Ad esempio, quando crei un consiglio di prodotto da distribuire nelle pagine dei dettagli del prodotto, puoi creare una condizione per consigliare solo i prodotti che rientrano in un intervallo di prezzo relativo del prodotto attualmente visualizzato.

### Operatori logici

Gli operatori logici `AND` e `OR` vengono utilizzati per unire più condizioni. Se utilizzi sia i filtri di inclusione che i filtri di esclusione, le inclusioni vengono valutate per prime per determinare tutti i possibili prodotti che possono essere consigliati, quindi i prodotti che corrispondono a eventuali filtri di esclusione vengono rimossi dall’elenco.

- `AND` - Unisce due condizioni di filtro di inclusione
- `OR` - Unisce due condizioni di filtro di esclusione

## Tipi di filtri

Ogni tipo di filtro esegue il targeting di un aspetto diverso del catalogo, ad esempio prodotto e prezzo, in modo da poter restringere o ampliare i prodotti idonei per un&#39;unità. Scegli i tipi che corrispondono agli obiettivi di merchandising, quindi combina le condizioni di inclusione ed esclusione secondo necessità; le sottosezioni seguenti descrivono il comportamento di ciascun tipo e come [!DNL Adobe Commerce Optimizer] lo applica.

>[!NOTE]
>
>È possibile consigliare solo i prodotti che corrispondono ai filtri di **inclusione** e rimuovere tutti i prodotti che corrispondono a un filtro di **esclusione**.

### Prezzo

>[!IMPORTANT]
>
>La seguente funzione è in versione beta.

Il filtro dei prezzi utilizza il **prezzo calcolato finale** di ogni prodotto per il **listino prezzi attivo** della vetrina, ovvero quello assegnato alla vetrina in cui viene eseguito il rendering dell&#39;unità di consigli. Tale valore riflette sconti, promozioni e prezzi speciali definiti in tale listino prezzi, non solo prezzi di listino. La valutazione utilizza solo il listino prezzi di quel negozio; non si applicano altri listini o listini prezzi. Configurazione del catalogo e dei [listini prezzi](../../setup/pricebooks.md) per la mappatura dei listini prezzi a una vetrina.

#### Come includere ed escludere regole usa prezzo

- **Regole di inclusione** - Solo i prodotti il cui prezzo finale **corrisponde a tutte** le condizioni di inclusione definite rimangono idonei. Ciò include ogni filtro di inclusione abilitato (ad esempio, l’intervallo di prezzo più qualsiasi altra regola di inclusione).
- **Regole di esclusione** - I prodotti il cui prezzo finale **corrisponde a una qualsiasi** condizione di esclusione definita vengono rimossi dai consigli.

**Prezzo visualizzato** - Il prezzo visualizzato sui prodotti all&#39;interno dell&#39;unità di consigli è lo stesso **prezzo finale** del listino prezzi di quel negozio, quindi quello che gli acquirenti vedono corrisponde al valore utilizzato per il filtro.

#### Impostare un filtro prezzi

1. Durante la [creazione o modifica](create.md) di un&#39;unità di consigli, apri **[!UICONTROL Filter products]** (o passa al passaggio _Filtri_ dal flusso di lavoro dell&#39;unità).
1. Selezionare la scheda **[!UICONTROL Inclusions]** o **[!UICONTROL Exclusions]**, a seconda che si desideri consentire solo i prodotti in una fascia di prezzo o bloccare i prodotti in un intervallo. Il badge in ogni scheda mostra il numero di filtri di quel tipo abilitati.
1. Nell&#39;elenco a sinistra, selezionare **[!UICONTROL Price]**.
1. Attiva **[!UICONTROL Enable filter]**.

   I valori di prezzo utilizzano la valuta di base del sito Web **&#x200B;**, come indicato nella pagina.

1. Aprire **[!UICONTROL Include products based on]** (nella scheda **[!UICONTROL Inclusions]**) o il controllo equivalente nella scheda **[!UICONTROL Exclusions]** e scegliere **[!UICONTROL Set price range]**.
1. Impostare un **[!UICONTROL Min price]** e/o un **[!UICONTROL Max price]** facoltativo utilizzando i campi accanto al simbolo di valuta. È possibile digitare gli importi o utilizzare i controlli **-** e **+** per regolare i valori. Lascia vuoto un limite se non hai bisogno di un minimo o di un massimo. L&#39;intervallo viene confrontato con il prezzo calcolato finale di ciascun prodotto per il listino prezzi attivo del negozio.
1. Completa la configurazione dell’unità di consigli e salva o pubblica come di consueto, in modo che il filtro diventi effettivo.

![Filtro prezzi](../../assets/filter-price.png)

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

<!--### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
