---
title: Sincronizzazione dati
description: Rivedi i dati del catalogo che vengono sincronizzati dall'origine dati di Commerce in [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: c0f4664c-6afc-4762-856b-5e26a865d3a2
source-git-commit: e2c3c8a225b2c56985ba48c7efc9ae2c2d059b2e
workflow-type: tm+mt
source-wordcount: '461'
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

## Monitorare lo stato di sincronizzazione dei dati

Per i progetti che utilizzano Adobe Commerce come origine dati a monte, è possibile monitorare il processo di esportazione dei dati e avviare le operazioni di risincronizzazione dalla [pagina di stato Sincronizzazione feed dati](../../data-export/data-synchronization.md) in Amministrazione Commerce.

