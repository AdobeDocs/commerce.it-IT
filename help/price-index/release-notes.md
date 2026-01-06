---
title: Note sulla versione [!DNL Catalog Adapter]
description: Informazioni aggiornate sulla versione di  [!DNL Catalog Adapter]  per Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Note sulla versione dell&#39;estensione [!DNL Catalog Adapter]

Queste note sulla versione descrivono le versioni più recenti dell&#39;estensione [!DNL Catalog Adapter]. È disponibile il supporto per la versione principale rilasciata corrente. Vengono fornite a titolo di riferimento le note sulla versione per le versioni precedenti.

Gli aggiornamenti includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Correzioni](../assets/fix.svg) correzioni e miglioramenti
![Bug](../assets/bug.svg) problemi noti


>[!NOTE]
>
>L&#39;estensione [Catalog Adapter](catalog-adapter.md) disabilita l&#39;indicizzazione dei prezzi Adobe Commerce. Se è stato installato, è possibile controllare la versione installata nel sistema utilizzando Compositore. In alcuni casi, potrebbe essere utile aggiornare l&#39;estensione dell&#39;adattatore catalogo sul sistema per individuare correzioni o nuove funzionalità senza aggiornare la versione del servizio Commerce.

## Versione principale corrente

## Versione 1.0.10

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale le query sui prezzi per i prodotti bundle importati o appena creati potevano causare errori interni al server perché il sistema tentava di utilizzare uno SKU concatenato per la ricerca invece dello SKU corretto e valido. Le query sui prezzi per i prodotti bundle ora utilizzano lo SKU appropriato e vengono risolte correttamente.<!--MDEE-1040-->

## Versione 1.0.9

![Correzione](../assets/fix.svg) Aggiunta compatibilità per PHP 8.4. <!--MDEE-941-->

## Versione 1.0.8

![Correzione](../assets/fix.svg) è stato risolto un problema che causava un errore nel registro eccezioni durante l&#39;aggiunta di varianti di prodotti configurabili con SKU numeriche alla lista dei desideri. <!--MDEE-876-->
