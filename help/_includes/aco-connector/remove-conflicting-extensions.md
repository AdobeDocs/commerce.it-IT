---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 27%
---

# Rimuovere le estensioni in conflitto

Se è installata una delle seguenti estensioni, disinstallarle prima di installare [!DNL Adobe Commerce Optimizer Connector for B2B]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

I dati associati a queste estensioni sono ancora disponibili nel database di Commerce. Tuttavia, non viene esportato in [!DNL Commerce Optimizer] quando il connettore è abilitato. Per implementare le funzionalità di ricerca e merchandising di Adobe Commerce fornite da queste estensioni dopo l&#39;abilitazione del connettore, configurale dall&#39;[[!DNL Commerce Optimizer] interfaccia utente amministratore](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Se non si rimuovono queste estensioni prima di abilitare il connettore, si verificheranno schermate di configurazione non funzionanti, dati duplicati in [!DNL Commerce Optimizer] ed errori di autenticazione 401 o 403.