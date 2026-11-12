---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%
---
I criteri definiscono i filtri applicati ai prodotti in una vista catalogo. Aiuta a personalizzare l’assortimento di prodotti restituito a una vetrina o a un canale. In questo modo, i contenuti vengono inviati alla destinazione corretta. Ad esempio, negozi fisici, mercati e canali pubblicitari come Google, Facebook e Instagram.

I criteri utilizzano attributi di prodotto come marchio, modello o categoria di parte per adattare i dati del catalogo ai requisiti aziendali. &#x200B;

## Accedere all’area di lavoro Criteri

La modalità di apertura dell&#39;area di lavoro *Criteri* dipende dal prodotto utilizzato:

- **Amministratore Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleziona *Catalogo* > **Criteri**.
- **Adobe Commerce Optimizer Studio**—Selezionare *Configurazione archivio* > **Criteri**.

## Filtri

I filtri definiscono condizioni basate su attributi che determinano quali prodotti corrispondono a un criterio. Quando è associata a una vista catalogo, una policy consente di adattare i prodotti restituiti per tale vista. Utilizza attributi di prodotto, operatori e valori per definire le condizioni di corrispondenza.

### Parti di un filtro

Un filtro è composto dalle seguenti parti:

| Parte | Descrizione | Esempio |
|---|---|---|
| **Attributo** | L’attributo del prodotto utilizzato per il filtro. | `part_category` |
| **Operatore** | Condizione applicata all’attributo. | `IN`, `EQUALS`, `CONTAINS` |
| **Origine valore** | Specifica se i valori sono `STATIC` o `TRIGGER`. | `STATIC` [Ulteriori informazioni](#value-source-types) |
| **Valore** | I valori specifici che soddisfano la condizione. | `brakes, suspension` |

### Esempio

Un filtro su `part_category` che utilizza l&#39;operatore `IN` con valori `brakes` e `suspension` corrisponde a prodotti con `part_category` come valore.

### Tipi di origine del valore

Esistono due tipi di origini di valore: **STATIC** e **TRIGGER**.

I criteri con **Origine valore** di **STATIC** sono considerati criteri universali. Le politiche universali definiscono l&#39;esperienza di un sito Web nel suo complesso. Ciò significa che la vista catalogo esegue sempre tale criterio. L’esecuzione dei criteri non dipende dall’interazione dell’utente della vetrina.

I criteri con **Origine valore** di **TRIGGER** sono denominati criteri esclusivi. Ciò significa che la vista a catalogo esegue tale criterio solo quando il trigger è specificato nell’intestazione della chiamata API. Nella vetrina, questo significa che le informazioni vengono visualizzate in base a ciò che l&#39;acquirente seleziona. Nell&#39;immagine seguente, ad esempio, sono presenti due menu a discesa: **Marchio** e **Modello**.

![Attiva origine valore in storefront](/help/assets/ccdm-shared/setup/policy-trigger.png)

**Brand** e **Model** sono attivatori definiti:

- `AC-Policy-Brand`
- `AC-Policy-Model`

Se l&#39;acquirente fa clic sull&#39;elenco a discesa Modello, l&#39;intestazione della chiamata API contiene `AC-Policy-Model`, configurato per mostrare solo i prodotti specifici del criterio `AC-Policy-Model`.

### Trigger di intestazione HTTP con più valori {#multi-value-http-header-triggers}

Un criterio di attivazione che utilizza il tipo di trasporto `HTTP_HEADER` può ricevere più valori in una singola intestazione. I valori devono essere separati da virgole e l&#39;operatore di filtro deve essere `IN`. Ogni valore viene trattato come una corrispondenza accettabile. I valori vengono valutati con `OR` semantica.

Ad esempio, un filtro criteri che utilizza `IN` con la seguente intestazione:

```
AC-Policy-Vehicle: UNIVERSAL,veh-bolt-mammoth-limited-2025
```

corrisponde a prodotti il cui attributo `vehicle` è `UNIVERSAL` o `veh-bolt-mammoth-limited-2025`.

Un operatore di filtro di `EQUALS`, `GREATER_THAN_EQUAL` o `LESS_THAN_EQUAL` viene rifiutato con un errore di convalida.

#### Note sulla sintassi

- Il nome dell&#39;intestazione corrisponde al nome del trigger configurato, ad esempio `AC-Policy-Vehicle`.
- Le virgole separano i singoli valori all’interno dell’intestazione. Quando la stessa intestazione `AC-Policy-_Name_` viene visualizzata più di una volta, i relativi valori vengono combinati in un singolo valore di intestazione separato da virgole
- Operatore filtro: `IN`.
- Filtro dei criteri con **Origine valore** impostata su `TRIGGER`.
- Un trigger il cui **tipo di trasporto** è `HTTP_HEADER`.

## Crea criterio

In questa sezione viene creato un nuovo criterio. Il criterio può essere **STATIC** o **TRIGGER**.

### Creare un criterio STATICO

1. Nell&#39;area di lavoro **[!UICONTROL Policies]** fare clic sul pulsante **[!UICONTROL Add Policy]**.

   Viene visualizzata una nuova pagina per compilare i dettagli della policy. &#x200B;

1. Immettere il nome del criterio, ad esempio &quot;Categorie parte Celport&quot;.

1. Fare clic sul pulsante **[!UICONTROL Add Filter]**.

   Viene visualizzata una finestra di dialogo in cui puoi aggiungere i dettagli del filtro.

1. Aggiungi i dettagli del filtro. Ad esempio:

   1. **Attributo** - Immetti un attributo dal catalogo. Ad esempio, &quot;part_category&quot;. Questo nome deve corrispondere esattamente al nome dell’attributo nel catalogo.
   1. **Operatore** - Scegliere l&#39;operatore. Ad esempio, **IN**. &#x200B;
   1. **Valore Source** - Selezionare **STATICO**. &#x200B;
   1. **Valore** - Immettere un valore dalla definizione di attributo specificata in precedenza. Ad esempio, immettere &quot;freni&quot; per creare un filtro per le parti del freno.
   1. Per salvare il valore, premere **Invio**.

      Se il criterio è progettato per filtrare in base a più valori, immettere ogni valore separatamente.

1. Fare clic sul pulsante **[!UICONTROL Save]** nella finestra di dialogo dei dettagli del filtro. &#x200B;

1. Fai clic sull’icona del menu (...) accanto al filtro creato e selezionare **Abilita**. Da qui, puoi anche **Modificare**, **Disabilitare** o **Eliminare** il filtro.

   La colonna **Stato** contiene un&#39;icona verde e la parola &quot;Abilitato&quot;.

1. Fare clic sul pulsante **[!UICONTROL Save]** per salvare il nuovo criterio.&#x200B; Se il pulsante non è attivo, verificare che il nome del criterio sia stato aggiunto facendo clic sull&#39;icona della matita accanto a **Nuovo criterio**.

1. Per verificare il nuovo criterio, fare clic sulla freccia indietro per tornare all&#39;area di lavoro **[!UICONTROL Policies]**.

### Creare un criterio TRIGGER

1. Nell&#39;area di lavoro **[!UICONTROL Policies]** fare clic sul pulsante **[!UICONTROL Add Policy]**.

   Viene visualizzata una nuova pagina per compilare i dettagli della policy. &#x200B;

1. Immettere il nome del criterio, ad esempio &quot;Categorie parte Celport&quot;.

1. Fare clic sul pulsante **[!UICONTROL Add Trigger]**.

   Viene visualizzata la finestra di dialogo **Dettagli trigger**.

1. Immettere un nome per il trigger, ad esempio **AC-Policy-Brand**.

1. Selezionare il **tipo di trasporto**. **HTTP_HEADER** è attualmente l&#39;unico tipo supportato.

1. Fare clic sul pulsante **[!UICONTROL Save]** per salvare il trigger.

1. Fare clic sul pulsante **[!UICONTROL Add Filter]**.

   Viene visualizzata una finestra di dialogo in cui puoi aggiungere i dettagli del filtro.

1. Aggiungi i dettagli del filtro. Ad esempio:

   1. **Attributo** - Immetti un attributo dal catalogo. Ad esempio, &quot;part_category&quot;. Questo nome deve corrispondere esattamente al nome dell’attributo nel catalogo.
   1. **Operatore** - Scegliere l&#39;operatore. Ad esempio, **IN**. &#x200B;
   1. **Valore Source** - Selezionare **TRIGGER**. &#x200B;
   1. **Valore** - Immetti il nome del trigger creato in precedenza (**AC-Policy-Brand**).

   Al momento della configurazione, il filtro fa riferimento al trigger configurato. In fase di esecuzione, l’intestazione della richiesta API fornisce il valore o i valori valutati da tale filtro.

1. Fare clic sul pulsante **[!UICONTROL Save]** nella finestra di dialogo dei dettagli del filtro. &#x200B;

1. Fai clic sull’icona del menu (...) accanto al filtro creato e selezionare **Abilita**. Da qui, puoi anche **Modificare**, **Disabilitare** o **Eliminare** il filtro.

   La colonna **Stato** contiene un&#39;icona verde e la parola &quot;Abilitato&quot;.

1. Fare clic sul pulsante **[!UICONTROL Save]** per salvare il nuovo criterio.&#x200B; Se il pulsante non è attivo, verificare che il nome del criterio sia stato aggiunto facendo clic sull&#39;icona della matita accanto a **Nuovo criterio**.

1. Per verificare il nuovo criterio, fare clic sulla freccia indietro per tornare all&#39;area di lavoro **[!UICONTROL Policies]**.

Seguendo questi passaggi viene creato il criterio che può quindi essere collegato a una vista catalogo per controllare la visibilità dei prodotti.
