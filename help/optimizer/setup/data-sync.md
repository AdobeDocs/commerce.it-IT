---
title: Sincronizzazione dati
description: Scopri come sincronizzare i dati del catalogo con  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Sincronizzazione dati

Nella pagina **Sincronizzazione dati** viene visualizzata una panoramica dello stato di sincronizzazione dei dati di prodotto trasferiti dall&#39;origine dati (il catalogo Commerce esistente, il sistema di gestione delle informazioni sui prodotti (PIM), il sistema ERP (Enterprise Resource Planning) e così via) in [!DNL Adobe Commerce Optimizer].

La pagina **Sincronizzazione dati** fornisce informazioni utili sulla disponibilità dei dati di prodotto per la vetrina, garantendo che possano essere visualizzati immediatamente agli acquirenti.

La pagina **Sincronizzazione dati** si trova in *Configurazione* > **Sincronizzazione dati**.

![Sincronizzazione dati](../assets/data-sync.png)

La pagina **Sincronizzazione dati** contiene i campi seguenti:

| Campo | Descrizione |
|--- |--- |
| Origine catalogo | Impostazioni locali specifiche per i dati sincronizzati. |
| [!DNL Catalog Service] | Visualizza l&#39;ultimo aggiornamento di sincronizzazione, il totale dei prodotti ricevuti, un campo di ricerca e una tabella dei prodotti sincronizzati per [!DNL Catalog Service]. |
| Individuazione prodotto | Visualizza l&#39;ultimo aggiornamento di sincronizzazione, il totale dei prodotti ricevuti, un campo di ricerca e una tabella dei prodotti sincronizzati da cercare. |
| Consigli | Visualizza l&#39;ultimo aggiornamento di sincronizzazione, il totale dei prodotti ricevuti, un campo di ricerca e una tabella dei prodotti sincronizzati per la funzione Consigli. |
| Prodotti ricevuti nelle ultime 3 ore | Visualizza il numero di prodotti trasferiti dall&#39;origine del catalogo a Adobe Commerce Optimizer nelle ultime tre ore. Se apporti aggiornamenti non frequenti al catalogo, questo valore è spesso zero. |
| Totale prodotti nel catalogo | Riflette il numero totale di prodotti catalogo disponibili per Adobe Commerce Optimizer. |
| Prodotti sincronizzati | Fornisce dettagli sui prodotti sincronizzati con Adobe Commerce Optimizer. Per impostazione predefinita, questa tabella è ordinata per &#39;Ultimo aggiornamento&#39;. Per trovare un prodotto specifico, utilizzare il campo **[!UICONTROL Search by Name or SKU]**. |

## Elenco dei prodotti sincronizzati

Per visualizzare i dettagli di un prodotto sincronizzato in formato JSON, fai clic sull&#39;icona del codice ![collegamento al codice](../assets/data-sync-details.png) nella riga del prodotto dalla tabella dei prodotti sincronizzati.

![Dettagli prodotto Syncd](../assets/synced-products.png)

## Risincronizza dati catalogo

Se non trovi prodotti specifici nella pagina **Sincronizzazione dati**, devi avviare una risincronizzazione dal sistema a monte. Tenere presente, tuttavia, che una risincronizzazione può aumentare il carico sulle risorse hardware. Tuttavia, potrebbe essere necessario risincronizzare il catalogo nei seguenti scenari:

- Quando vengono apportate modifiche significative al catalogo dei prodotti, ad esempio aggiungendo nuovi prodotti, aggiornando i dettagli dei prodotti o modificando le categorie

- Se noti eventuali discrepanze o problemi di prestazioni nella visualizzazione dei dati di prodotto nei negozi

>[!IMPORTANT]
>
>Il tempo necessario per completare la sincronizzazione varia in base alle dimensioni del catalogo e al volume di dati aggiornati.
