---
title: Merchandising categorie
description: Utilizza  [!DNL Live Search] merchandising per categorie per un'esperienza di acquisto più veloce.
gourl: ls_catalog_merchandising
exl-id: b2645096-aafc-4d68-8adc-ab5410a9dfb6
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 59aa4ae67a1a8a853b72d78cd65a6cc44a6bc662
workflow-type: tm+mt
source-wordcount: '1118'
ht-degree: 0%

---

# Merchandising categorie

Il merchandising per categorie consente ai proprietari dei negozi di applicare [!DNL Live Search] [regole](rules.md) di classificazione intelligente alle categorie e sottocategorie di prodotti.

Questo video è un’introduzione alla categoria Merchandising.

>[!VIDEO](https://video.tv.adobe.com/v/3424617)

La funzione è accessibile nell&#39;amministratore da **Marketing** > SEO &amp; Search > **[!DNL Live Search]** > **Category Merchandising**.

>[!NOTE]
>
>Il merchandising delle categorie è disponibile con [!DNL Live Search] [3.0.0 o versione successiva](release-notes.md). Se l&#39;area di lavoro di merchandising delle categorie è visualizzata ma non contiene dati, aggiornare il modulo [!DNL Live Search].

![Merchandising per categoria](assets/category_workspace.png)

La vista Merchandising per categorie mostra le regole di categoria definite, con le colonne per:

* Categoria
* Strategia di classificazione
* Classificazione ereditata
* Ultimo aggiornamento
* Azione

Puoi cercare una categoria o sottocategoria nel campo &quot;Ricerca per categoria&quot;.

## Strategie di classificazione

Il merchandising per categorie utilizza gli stessi tipi di classificazione utilizzati per [singoli prodotti](rules-workspace.md).
Esistono due tipi di classificazione: intelligente e manuale.

**La classificazione intelligente** sfrutta l&#39;analisi dei dati comportamentali in vetrina da parte di [Adobe Sensei](https://www.adobe.com/sensei.html) per ordinare tutti i prodotti all&#39;interno delle categorie scelte in base a un determinato algoritmo. Una volta scelta una classificazione intelligente, l’ordine specifico dei prodotti dovrebbe cambiare nel tempo in quanto i dati sottostanti vengono rianalizzati da Adobe Sensei su base continuativa. Ad esempio, i prodotti con tendenze principali cambiano automaticamente nel tempo in base alle preferenze dell’acquirente.
I metodi di classificazione intelligenti sono:

* Più acquistati: classifica i prodotti in base alla frequenza con cui sono stati acquistati dagli acquirenti nei sette giorni precedenti.
* Più aggiunti al carrello: classifica i prodotti in base alla frequenza con cui sono stati aggiunti al carrello dagli acquirenti nei sette giorni precedenti.
* Più visualizzati: classifica i prodotti in base alla frequenza con cui sono stati visualizzati dagli acquirenti nei sette giorni precedenti.
* Consigliato per te: in base al comportamento precedente e attuale di ogni acquirente sul posto, classifica i prodotti in base alla probabilità che interagisca con ciascuno.
* Tendenza: classifica i prodotti in base alle recenti acquisizioni di popolarità in base alle visualizzazioni.
* Nessuno: classifica i prodotti in base all’ordine predefinito.

**Classificazione manuale** consente agli utenti di ignorare l&#39;ordinamento automatico del prodotto definendo regole manuali di pin, boost, sotterramento e nascondi.

## Classificazione ereditata

In qualità di merchandiser, potresti voler essere in grado di selezionare tutte le categorie di abbigliamento femminile per essere ordinato per &quot;tendenza&quot;. Sono incluse le sottocategorie &quot;Pantaloni da donna&quot;, &quot;Camicie da donna&quot; e &quot;Accessori da donna&quot;. Le categorie maschili non dovrebbero essere influenzate. Per ottenere questo risultato, puoi utilizzare le classificazioni ereditate.

Quando si seleziona un metodo di classificazione intelligente per una categoria o sottocategoria con sottocategorie, è possibile attivare l&#39;opzione **Applica classificazione intelligente alle sottocategorie**. Questo applica il metodo di classificazione a tutte le sottocategorie.

Queste sottocategorie ereditano ora tale regola dalla categoria padre (&quot;Sì&quot; nella colonna Classificazione ereditata). Nella colonna Azione le uniche opzioni disponibili sono **Modifica regola** e **Visualizza dettagli**. L&#39;opzione **Elimina** è disabilitata per le regole ereditate sulle sottocategorie. L&#39;eliminazione dell&#39;ereditarietà della sottocategoria richiede l&#39;annullamento dell&#39;ereditarietà dalla categoria padre.

A qualsiasi categoria o sottocategoria può essere applicata una sola classificazione intelligente alla volta. Possono inoltre essere applicate classificazioni manuali aggiuntive.

Se applichi una classificazione intelligente a una categoria e attivi l&#39;opzione **Applica classificazione intelligente alle sottocategorie**, eventuali classificazioni intelligenti già applicate alle sottocategorie vengono sovrascritte.

![Elenco sottocategorie sovrascritto](assets/category_overwite_subs.png){width="700"}

Se si fa clic su **Visualizza tutto**, viene visualizzata una finestra di dialogo con i dettagli delle modifiche proposte.

![Dettagli modifiche classificazione](assets/category_overwrite.png)

Quando si aggiunge direttamente una classificazione intelligente a una categoria con una classificazione intelligente ereditata, l’ereditarietà viene sovrascritta dalla nuova classificazione intelligente.

Quando si elimina la classificazione intelligente dalla categoria, l’ereditarietà viene ristabilita.
In entrambi gli scenari, vengono mantenute tutte le classificazioni manuali.

Se rimuovi una classificazione intelligente da una categoria e viene selezionata l’ereditarietà della sottocategoria, vengono rimosse dalle sottocategorie solo le classificazioni intelligenti ereditate. Le classificazioni manuali non sono soggette a ereditarietà e rimarranno.

Viene visualizzata una finestra di dialogo che illustra quali sottocategorie ereditate sono interessate da eventuali modifiche apportate a una categoria di livello superiore.

![Finestra di dialogo modale modifiche classificazione](assets/category_overwrite_modal.png){width="1200"}

## Creare una regola di categoria

Per creare una regola di categoria:

1. Fai clic sul pulsante **Aggiungi regola**.
1. Nella visualizzazione _Seleziona categoria_, fare clic sulle categorie e sottocategorie.
1. Selezionare la casella di controllo per selezionare la categoria da classificare.
1. Fare clic su **Applica**.

   ![Seleziona una categoria](assets/category_select.png)

1. Nella visualizzazione _Aggiungi regola di categoria_, seleziona il metodo di classificazione intelligente da applicare alla categoria.
La pagina Anteprima categoria mostra i risultati effettivi della classificazione selezionata, utilizzando i dati di Live Search.
1. Fai clic su **Salva e pubblica** per salvare la regola.

![Seleziona il metodo di classificazione intelligente](assets/category_ranking.png)

Il servizio [!DNL Live Search] elabora la regola e la attiva nell&#39;archivio al termine.

## Modificare una regola di categoria

Per modificare una regola esistente:

1. Fare clic su **...** nella colonna Azione e scegliere **Modifica**.
1. Nella visualizzazione Modifica regola categoria apportare le modifiche necessarie e fare clic su **Salva e pubblica**.

Le modifiche vengono applicate all&#39;archivio quando [!DNL Live Search] ha elaborato la modifica.

## Eliminare una regola di categoria

Per eliminare una regola di categoria:

1. Fare clic su **...** nella colonna Azione e scegliere **Elimina**.
1. Nel modale _Elimina regola_, seleziona **Elimina** per rimuovere la regola oppure **Annulla** per annullare l&#39;azione.

## Classificazione manuale

La classificazione manuale consente di ignorare l’ordine dei prodotti determinato da eventuali regole di classificazione intelligente e di controllare manualmente dove i prodotti compaiono all’interno dei risultati.

Gli eventi sono azioni che modificano i risultati della ricerca quando vengono soddisfatte le condizioni definite. Una classificazione manuale può avere fino a 25 eventi.

* Incrementa: sposta un prodotto più in alto nei risultati di ricerca.
* Interruttore: sposta un prodotto in una posizione più bassa nei risultati di ricerca.
* Fissa un prodotto: sposta un prodotto in una posizione specifica nei risultati.
* Nascondere un prodotto: esclude un prodotto dai risultati della ricerca.

Crea una classificazione manuale:

1. Imposta una regola di classificazione intelligente per una categoria come descritto in precedenza. I risultati della query verranno visualizzati nella visualizzazione Anteprima pagina categoria. Questo utilizza i dati Live Search effettivi per visualizzare in anteprima i risultati.

1. Fai clic su un prodotto e trascinalo nella visualizzazione Anteprima pagina categoria. Trascinalo e rilascialo nella posizione desiderata. I campi Prodotto e Posizione vengono compilati automaticamente nel riquadro Eventi.

Puoi anche fare clic sull’icona a forma di pin per fissare un prodotto alla posizione corrente. Utilizza il menu di scelta rapida con puntini di sospensione per &quot;Fissa in alto&quot; o &quot;Fissa in basso&quot;.

Per aggiungere manualmente un evento:

1. In Classifica manuale fare clic sul menu **Seleziona un evento** e scegliere un evento da eseguire quando vengono soddisfatte le condizioni associate.
1. Immettere il nome del prodotto che si desidera modificare. I prodotti vengono suggeriti durante la digitazione.
1. Per più eventi, scegli qualsiasi altro evento che desideri attivare quando vengono soddisfatte le condizioni.

>[!NOTE]
>
>Le regole vengono applicate quando una categoria specifica viene aperta nella vetrina ed esiste una regola per tale categoria. Per le regole di merchandising per categorie, l’ordinamento predefinito è &quot;Ordina per: posizione&quot;. Se un acquirente modifica l’ordinamento, tutti i prodotti nascosti, bloccati e nascosti non vengono più ordinati.
