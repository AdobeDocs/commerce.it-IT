---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# Verificare la sincronizzazione dei dati del servizio Commerce

Per verificare il funzionamento della sincronizzazione dei dati, verificare che i dati esportati da [!DNL Adobe Commerce] siano stati correttamente recapitati al servizio Commerce connesso. Utilizza le dashboard della distribuzione per controllare entrambi i passaggi.

Inizia con l’esportazione, quindi conferma la consegna.

1. Controlla lo stato di sincronizzazione in Amministrazione Commerce.

   Vai a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Pagina Stato sincronizzazione feed dati con report sullo stato degli elementi del feed](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   Quando la sincronizzazione è in esecuzione, i dati del feed mostrano i record inviati correttamente. Seleziona un feed per visualizzare i dettagli o risolvere i problemi di sincronizzazione.

1. Verificare che i dati siano stati recapitati ai servizi Commerce connessi.

   Dall&#39;amministratore di Commerce, passa a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Dashboard di gestione dati che mostra i dati del catalogo sincronizzati nei servizi Commerce connessi](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   Verifica che vengano visualizzati i prodotti, i prezzi e gli attributi previsti.

>[!TIP]
>
>Se hai problemi aggiuntivi con la sincronizzazione dei dati, consulta [Esaminare i registri e risolvere i problemi](/help/data-export/troubleshooting/logging.md).

