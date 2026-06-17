---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# Verificare la sincronizzazione dei dati di Optimizer

Verificare che i dati siano stati esportati correttamente dall&#39;amministratore di Commerce e che siano stati consegnati correttamente a [!DNL Commerce Optimizer]. Inizia con l&#39;esportazione in Commerce Admin, quindi conferma la consegna in [!DNL Commerce Optimizer].

1. **Verifica lo stato di sincronizzazione nell&#39;amministratore di Commerce:**

   Vai a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Pagina Stato sincronizzazione feed dati con report sullo stato degli elementi del feed](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   Quando la sincronizzazione è in esecuzione, i dati del feed mostrano i record inviati correttamente. Seleziona un feed per visualizzare i dettagli o risolvere i problemi di sincronizzazione.

1. **Conferma recapito dati a [!DNL Commerce Optimizer]:**

   Dal menu [!DNL Commerce Optimizer], selezionare **[!UICONTROL Data Sync]**.

   ![Pagina di sincronizzazione dati in Adobe Commerce Optimizer con i dati del catalogo sincronizzati](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   Verifica che vengano visualizzati i prodotti, i prezzi e gli attributi previsti.

Quando la sincronizzazione funziona come previsto:

- **[!UICONTROL Data Feed Sync Status]** mostra i record inviati correttamente per i feed del connettore, senza errori a livello di elemento non risolti.
- **[!UICONTROL Data Sync]** in [!DNL Commerce Optimizer] elenca le origini di catalogo, i prodotti, i prezzi e gli attributi previsti.

>[!TIP]
>
>In caso di problemi con la sincronizzazione dei dati, consulta la [guida alla risoluzione dei problemi](/help/aco-connector/troubleshooting.md).
