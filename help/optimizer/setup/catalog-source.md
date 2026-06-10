---
title: Origine catalogo
description: Scopri cosa sono le origini del catalogo e come definiscono l’ambito autorevole di prodotti, attributi e categorie per il comportamento di ricerca, filtro e ordinamento.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ecff841c8e88c3897358eaf91e54c732d1edcfe4
workflow-type: tm+mt
source-wordcount: 450
ht-degree: 0%

---

# Origine catalogo

Un’origine catalogo rappresenta un ambito autorevole di prodotti, attributi e categorie. Le origini del catalogo in genere vengono mappate in base ai limiti della lingua, del pubblico o del sistema di origine e determinano il comportamento di ricerca, filtro e ordinamento.

## Origine del catalogo e concetti correlati

Il modo in cui un&#39;origine catalogo si relaziona con altri concetti di [!DNL Adobe Commerce Optimizer] consente di modellare correttamente i dati:

* **Origine catalogo**: il contesto dei dati sottostante che fornisce le informazioni sul prodotto. Un&#39;origine catalogo è in genere una lingua (ad esempio, `en-US`, `fr-CA`) o un sistema esterno come un PIM o un ERP. I prodotti, i metadati degli attributi e le categorie hanno tutti un ambito per origine di catalogo. Considera un&#39;origine del catalogo come *da cui* provengono i dati del catalogo non elaborati e *come* influisce sull&#39;individuazione del prodotto (risultati di ricerca, filtraggio e comportamento di ordinamento).

* **[Visualizzazione catalogo](catalog-view.md)**: visualizzazione configurata del catalogo per esigenze aziendali specifiche. Quando crei una visualizzazione catalogo, selezioni l&#39;origine del catalogo (o le impostazioni locali) da utilizzare, quindi aggiungi [criteri](policies.md) per filtrare i prodotti visibili e collega [listini prezzi](pricebooks.md) per controllare la determinazione prezzi. Un&#39;unica origine di catalogo può alimentare molte visualizzazioni di catalogo (ad esempio, un&#39;origine `en-US` con visualizzazioni di catalogo separate per marchi o aree geografiche diversi). Considera una visualizzazione catalogo come *il modo* in cui esponi tali dati a una vetrina, un canale o un pubblico.

* **[Livello catalogo](catalog-layer.md)**: livello applicato ai dati del catalogo di base per modificare gli attributi del prodotto (nome, descrizione, immagini, metadati) senza modificare i dati di origine. Utilizzare i livelli del catalogo quando le differenze devono influire solo sulla visualizzazione della vetrina, non sul rilevamento del prodotto.

## Regole e limitazioni

* Un’origine catalogo viene creata acquisendo un prodotto tramite l’API di acquisizione dati. Per ulteriori informazioni, consulta [Developer Docs - Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).
* L’univocità del prodotto è determinata da SKU + origine catalogo.
* Gli acquirenti non accedono direttamente alle origini del catalogo. I dati del catalogo sono esposti alla vetrina tramite [visualizzazioni catalogo](catalog-view.md).

## Linee guida per la modellazione

Per decidere come strutturare le origini del catalogo, attieniti alle seguenti indicazioni:

* Crea un&#39;origine catalogo separata per ogni lingua del catalogo.
* Utilizza origini di catalogo separate quando le differenze di prodotti e attributi devono influire sul comportamento di ricerca, filtro o ordinamento (ad esempio, diversa ricercabilità, filtrabilità o configurazione facet per lo stesso attributo).
* Utilizzare i [livelli catalogo](catalog-layer.md) quando le differenze tra prodotti e attributi devono influire solo sulla visualizzazione della vetrina, non sull&#39;individuazione del prodotto.

>[!MORELIKETHIS]
>
> * [Visualizzazioni catalogo](catalog-view.md) - Configura visualizzazioni filtrate con prezzo sopra un&#39;origine catalogo
> * [Livelli catalogo](catalog-layer.md) - Modificare la presentazione del prodotto senza modificare i dati di origine
> * [Criteri](policies.md) - Creare filtri basati su attributi per le visualizzazioni catalogo
> * [Listini prezzi](pricebooks.md) - Gestisce le strutture di determinazione prezzi per segmenti cliente diversi
