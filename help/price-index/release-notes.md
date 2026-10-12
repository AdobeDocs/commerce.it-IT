---
title: Note sulla versione [!DNL Catalog Adapter]
description: Informazioni aggiornate sulla versione di [!DNL Catalog Adapter] per Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
TQID: 'https://experienceleague.adobe.com/btPlBYpdRdf-gMfqSv2px6iMfiI3FfXJSN40j61HXOU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: adedf70c-c1e1-5734-acdc-c5c43b114964
    internal-label: Release Notes
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '219'
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

## Versione 1.0.11

_18 giugno 2026_

![Correzione](../assets/fix.svg) **Compatibilità PHP 8.5** - L&#39;adattatore del catalogo Adobe Commerce ora supporta PHP 8.5 per la compatibilità con Adobe Commerce versione 2.4.9+. <!--MDEE-1368-->

## Versione 1.0.10

![Correzione](../assets/fix.svg) è stato risolto un problema a causa del quale le query sui prezzi per i prodotti bundle importati o appena creati potevano causare errori interni al server perché il sistema tentava di utilizzare uno SKU concatenato per la ricerca invece dello SKU corretto e valido. Le query sui prezzi per i prodotti bundle ora utilizzano lo SKU appropriato e vengono risolte correttamente.<!--MDEE-1040-->

## Versione 1.0.9

![Correzione](../assets/fix.svg) Aggiunta compatibilità per PHP 8.4. <!--MDEE-941-->

## Versione 1.0.8

![Correzione](../assets/fix.svg) è stato risolto un problema che causava un errore nel registro eccezioni durante l&#39;aggiunta di varianti di prodotti configurabili con SKU numeriche alla lista dei desideri. <!--MDEE-876-->
