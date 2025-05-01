---
title: Criteri
description: Scopri come utilizzare i criteri per filtrare i dati all’interno di un canale per garantire che i dati vengano inviati alla destinazione giusta.
hide: true
recommendations: noCatalog
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Criteri

>[!NOTE]
>
>Questa documentazione descrive un prodotto in fase di sviluppo con accesso anticipato e non riflette tutte le funzionalità previste per la disponibilità generale.

I criteri sono filtri di accesso ai dati contenuti all’interno di canali che consentono di perfezionare ulteriormente i dati consegnati a ciascun canale. Le policy garantiscono che il contenuto corretto venga inviato alla destinazione giusta. Ad esempio, punti vendita negozi fisici, mercati, pipeline pubblicitarie (Google, Facebook, Instagram).

I criteri si basano sugli attributi del prodotto, ad esempio marchio, modello o categoria di parte, e vengono utilizzati per adattare i dati del catalogo in base a requisiti aziendali specifici. &#x200B;

## Filtri

I filtri sono il meccanismo all’interno di una policy che applica la segmentazione del catalogo. I filtri consentono alle aziende di adattare i punti vendita e i canali a specifici set di prodotti in base alle esigenze operative. Puoi utilizzare criteri quali attributi di prodotto, operatori e valori per definire una regola o una condizione che indica quali prodotti sono inclusi o esclusi in un canale o in una vetrina.

### Parti di un filtro

Un filtro è composto dalle seguenti parti:

| Parte | Descrizione | Esempio |
|---|---|---|
| **Attributo** | L’attributo del prodotto utilizzato per il filtro. | `part_category` |
| **Operatore** | Condizione applicata all’attributo. | `IN`, `EQUALS`, `CONTAINS` |
| **Origine valore** | Specifica se i valori sono `STATIC` o `TRIGGER`. | `STATIC` |
| **Valore** | I valori specifici che soddisfano la condizione. | `brakes, suspension` |

### Esempio

Un filtro con l&#39;attributo `part_category`, un operatore di `IN` e i valori `brakes, suspension` garantisce che solo i prodotti classificati come freni e sospensioni siano inclusi nel criterio.

### Tipi di origine del valore

Esistono due tipi di origini di valore: **STATIC** e **TRIGGER**.

I criteri con **Origine valore** di **STATIC** sono considerati criteri universali. Le politiche universali definiscono l&#39;esperienza di un sito Web nel suo complesso. Ciò significa che il canale eseguirà sempre tale criterio. In altre parole, l’esecuzione di tale criterio non si basa su alcuna interazione dell’utente nella vetrina.

I criteri con **Origine valore** di **TRIGGER** sono denominati criteri esclusivi. Questo significa che il canale eseguirà tale criterio solo quando il trigger è specificato nell’intestazione della chiamata API. Nella vetrina, questo significa che le informazioni vengono visualizzate in base a ciò che l&#39;acquirente seleziona. Nell&#39;immagine seguente, ad esempio, sono presenti due menu a discesa: **Marchio** e **Modello**.

![Attiva origine valore in storefront](../assets/policy-trigger.png)

**Brand** e **Model** sono attivatori definiti:

- `AC-Policy-Brand`
- `AC-Policy-Model`

Se l&#39;acquirente fa clic sull&#39;elenco a discesa **Brand**, l&#39;intestazione della chiamata API contiene `AC-Policy-Brand`, configurato per mostrare solo i prodotti specifici del criterio `AC-Policy-Brand`.

## Crea criterio

In questa sezione viene creato un nuovo criterio. Il criterio può essere **STATIC** o **TRIGGER**.

### Creare un criterio STATICO

1. Nel menu a sinistra, apri la sezione **[!UICONTROL Catalog]** e fai clic su **[!UICONTROL Policies]**.

1. Fare clic sul pulsante **[!UICONTROL Add Policy]**.

   Viene visualizzata una nuova pagina per compilare i dettagli della policy. &#x200B;

1. Immettere il nome del criterio, ad esempio &quot;Categorie parte Celport&quot;.

1. Fare clic sul pulsante **[!UICONTROL Add Filter]**.

   Viene visualizzata una finestra di dialogo in cui puoi aggiungere i dettagli del filtro.

1. Aggiungi i dettagli del filtro. Ad esempio:

   1. **Attributo** - Immetti un attributo dal catalogo. Ad esempio, &quot;part_category&quot;. Questo nome deve corrispondere esattamente al nome dell’attributo nel catalogo.
   1. **Operatore** - Scegliere l&#39;operatore. Ad esempio, **IN**. &#x200B;
   1. **Valore Source** - Selezionare **STATICO**. &#x200B;
   1. **Valore** - Immettere i valori all&#39;interno dell&#39;attributo specificato in precedenza. Ad esempio, &quot;freni, sospensioni&quot;. &#x200B;Questi nomi devono corrispondere esattamente ai nomi dei valori per l’attributo specificato in precedenza.

1. Fare clic sul pulsante **[!UICONTROL Save]** nella finestra di dialogo dei dettagli del filtro. &#x200B;

1. Fai clic sui punti azione (...) accanto al filtro creato e seleziona **Abilita**. Da qui, puoi anche **Modificare**, **Disabilitare** o **Eliminare** il filtro.

   La colonna **Stato** contiene un&#39;icona verde e la parola &quot;Abilitato&quot;.

1. Fare clic sul pulsante **[!UICONTROL Save]** per salvare il nuovo criterio&#x200B; Se il pulsante non è attivo, verificare che il nome del criterio sia stato aggiunto facendo clic sull&#39;icona della matita accanto a **Nuovo criterio**.

1. Per verificare il nuovo criterio, torna all’elenco dei criteri facendo clic sulla freccia indietro. &#x200B;Verranno elencati i nuovi criteri.

### Creare un criterio TRIGGER

1. Nel menu a sinistra, apri la sezione **[!UICONTROL Catalog]** e fai clic su **[!UICONTROL Policies]**.

1. Fare clic sul pulsante **[!UICONTROL Add Policy]**.

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

1. Fare clic sul pulsante **[!UICONTROL Save]** nella finestra di dialogo dei dettagli del filtro. &#x200B;

1. Fai clic sui punti azione (...) accanto al filtro creato e seleziona **Abilita**. Da qui, puoi anche **Modificare**, **Disabilitare** o **Eliminare** il filtro.

   La colonna **Stato** contiene un&#39;icona verde e la parola &quot;Abilitato&quot;.

1. Fare clic sul pulsante **[!UICONTROL Save]** per salvare il nuovo criterio&#x200B; Se il pulsante non è attivo, verificare che il nome del criterio sia stato aggiunto facendo clic sull&#39;icona della matita accanto a **Nuovo criterio**.

1. Per verificare il nuovo criterio, torna all’elenco dei criteri facendo clic sulla freccia indietro. &#x200B;Verranno elencati i nuovi criteri.

Seguendo questi passaggi, il criterio verrà creato e sarà pronto per essere collegato a un canale per controllare la visibilità dei prodotti.
