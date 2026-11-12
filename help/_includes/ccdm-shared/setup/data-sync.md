---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%
---
Nella pagina **Sincronizzazione dati** viene visualizzata una panoramica dello stato di sincronizzazione dei dati dei prodotti trasferiti dall&#39;origine dati (il catalogo Commerce esistente, il sistema di gestione delle informazioni sui prodotti (PIM), il sistema ERP (Enterprise Resource Planning) e così via) nel livello dati dei servizi di merchandising.

La pagina **Sincronizzazione dati** fornisce informazioni utili sulla disponibilità dei dati di prodotto per la vetrina, garantendo che possano essere visualizzati immediatamente agli acquirenti.

## Accedere all’area di lavoro Sincronizzazione dati

La modalità di apertura dell&#39;area di lavoro *Sincronizzazione dati* dipende dal prodotto utilizzato:

- **Amministratore Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleziona *Archivi* > **Sincronizzazione catalogo**.
- **Adobe Commerce Optimizer Studio**—Selezionare *Configurazione archivio* > **Sincronizzazione dati**.

![Sincronizzazione dati](/help/assets/ccdm-shared/setup/data-sync.png)

La pagina **Sincronizzazione dati** contiene i campi seguenti:

| Campo | Descrizione |
| --- | --- |
| Origine catalogo | Impostazioni locali specifiche per i dati sincronizzati. |
| [!DNL Catalog Service] | Visualizza l&#39;ultimo aggiornamento di sincronizzazione, il totale dei prodotti ricevuti, un campo di ricerca e una tabella dei prodotti sincronizzati per [!DNL Catalog Service]. |
| Individuazione prodotto | Visualizza l&#39;ultimo aggiornamento di sincronizzazione, il totale dei prodotti ricevuti, un campo di ricerca e una tabella dei prodotti sincronizzati da cercare. |
| Consigli | Visualizza l&#39;ultimo aggiornamento di sincronizzazione, il totale dei prodotti ricevuti, un campo di ricerca e una tabella dei prodotti sincronizzati per la funzione Consigli. |
| Prodotti ricevuti nelle ultime 3 ore | Visualizza il numero di prodotti trasferiti dall&#39;origine del catalogo al livello dati Merchandising Services nelle ultime tre ore. Se apporti aggiornamenti non frequenti al catalogo, questo valore è spesso zero. |
| Totale prodotti nel catalogo | Riflette il numero totale di prodotti catalogo disponibili nel livello dati Merchandising Services. |
| Prodotti sincronizzati | Fornisce dettagli sui prodotti sincronizzati con il livello dati Merchandising Services. Per impostazione predefinita, questa tabella è ordinata per &#39;Ultimo aggiornamento&#39;. Per trovare un prodotto specifico, utilizzare il campo **[!UICONTROL Search by Name or SKU]**. |

## Elenco dei prodotti sincronizzati

Per visualizzare i dettagli di un prodotto sincronizzato in formato JSON, fai clic sull&#39;icona del codice ![collegamento al codice](/help/assets/ccdm-shared/setup/data-sync-details.png) nella riga del prodotto dalla tabella dei prodotti sincronizzati.

![Dettagli prodotto sincronizzati](/help/assets/ccdm-shared/setup/synced-products.png)

## Risincronizza dati catalogo

Se non trovi prodotti specifici nella pagina **Sincronizzazione dati**, devi avviare una risincronizzazione dal sistema a monte. Tenere presente, tuttavia, che una risincronizzazione può aumentare il carico sulle risorse hardware. Tuttavia, potrebbe essere necessario risincronizzare il catalogo nei seguenti scenari:

- Quando vengono apportate modifiche significative al catalogo dei prodotti, ad esempio aggiungendo nuovi prodotti, aggiornando i dettagli dei prodotti o modificando le categorie

- Se noti eventuali discrepanze o problemi di prestazioni nella visualizzazione dei dati di prodotto nei negozi

>[!IMPORTANT]
>
>Il tempo necessario per completare la sincronizzazione varia in base alle dimensioni del catalogo e al volume di dati aggiornati.

## Verificare che la sincronizzazione dei dati funzioni

Per i progetti che utilizzano Adobe Commerce come origine di dati a monte, puoi monitorare il processo di esportazione dei dati e avviare le operazioni di risincronizzazione dalla pagina Stato sincronizzazione feed dati. Per informazioni dettagliate, vedere [Monitoraggio dello stato di sincronizzazione dei feed di dati](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status).
