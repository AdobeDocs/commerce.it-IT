---
title: Trasferimento Source Inventory management
description: Configura le scorte per  [!DNL Store Fulfillment solution]  con Adobe Commerce Inventory management. Impostare un nuovo magazzino e trasferirlo al di fuori del magazzino predefinito in modo da poterlo assegnare alle origini configurate per abilitare le funzionalità di prelievo del magazzino richieste dalla soluzione di evasione del magazzino.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Trasferimento Source Inventory management

La soluzione [!DNL Store Fulfillment] utilizza Adobe Commerce Inventory management nativo. Per impostazione predefinita, la configurazione [!DNL Commerce] assegna tutto l&#39;inventario Web alle scorte predefinite, alle quali non possono essere assegnate altre origini. Poiché a un sito Web è possibile assegnare un solo stock, un commerciante deve configurare un nuovo stock e, facoltativamente, trasferire il proprio inventario di origine predefinito a un&#39;origine assegnata all&#39;ambito appropriato. Quindi, l&#39;origine può essere assegnata al nuovo stock.

>[!IMPORTANT]
>
>I commercianti devono mantenere l’origine predefinita per tutti i prodotti inclusi nei tipi di prodotto di gruppo e bundle. Per questi prodotti è necessaria una quantità di magazzino che soddisfi la soglia della quantità minima per gli articoli in magazzino e includa uno stato di magazzino di [!UICONTROL In Stock].

Queste modifiche alla configurazione consentono di eseguire tre operazioni:

1. [Trasferisci scorte all&#39;origine](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/quantities/inventory-transfer) per spostare le scorte dall&#39;origine/scorta predefinita alla nuova origine/scorta.

1. [Assegna in blocco le origini](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/quantities/bulk-assignment) per aggiungere nuove origini per tutti i prodotti.

1. [Completare gli aggiornamenti in blocco per gli attributi del prodotto](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update) per aggiungere gli attributi `Allow Store Pickup` e `Allow Home Delivery` ai prodotti esistenti. Al momento dell&#39;installazione della soluzione, gli attributi hanno i valori *default* ottimali. Tuttavia, questi attributi non vengono applicati ai prodotti esistenti fino a quando non si completa il processo di updaContes in blocco.

L&#39;inventario viene detratto dall&#39;origine selezionata (ubicazione negozio al dettaglio o magazzino di e-commerce). Le origini utilizzate come magazzini di e-commerce devono essere assegnate alla stessa scorta del luogo di prelievo del negozio e prioritarie prima delle posizioni di vendita al dettaglio. Per ulteriori informazioni, vedere [Assegnazione di priorità alle origini per un Stock](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources).

Per ulteriori informazioni sulla gestione di inventario, scorte e origini, consulta la documentazione utente di Adobe Commerce:

- [Gestione dell&#39;inventario](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/introduction)

- [Gestione delle quantità di magazzino](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/quantities/quantities-manage)

- [Gestione Stock](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/stocks/stocks-manage)

- [Gestione delle origini](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/sources/sources-manage)

- [Assegnazione di priorità alle origini per un Stock](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/stocks/stocks-prioritize-sources)

- [Aggiornamenti in blocco per attributi prodotto](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/create/bulk-product-attribute-update)


>[!IMPORTANT]
>
>La modifica della configurazione delle origini di inventario e di magazzino può avere un impatto a valle anche sui sistemi integrati. Assicurati di comprendere in che modo le modifiche alla configurazione dell’inventario influiscono su questi sistemi.
