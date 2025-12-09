---
title: Filtri per consigli
description: Scopri come utilizzare i filtri per controllare quali prodotti vengono visualizzati nei  [!DNL Adobe Commerce Optimizer]  consigli.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: 032a19183b79cea1bfe27e8a4e20c60ba5ac6b8b
workflow-type: tm+mt
source-wordcount: '403'
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

![Filtri](../../assets/rec-conditions.png)

### Prodotto

I filtri dei prodotti specificano quali prodotti specifici sono idonei, o non idonei, per la visualizzazione nei consigli. Non puoi selezionare prodotti disabilitati o non visibili singolarmente, in quanto tali prodotti non possono mai essere visualizzati nei consigli.

>[!NOTE]
>
>I prodotti secondari di un prodotto configurabile non vengono visualizzati in un&#39;unità di consigli perché tali prodotti secondari hanno la visibilità di _Non visibile singolarmente_.

<!--### Price

A filter based on the product price uses the final price to perform the comparison. The final price includes any discounts or special pricing available to anonymous shoppers.

### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
