---
title: Mantenere contenuti accurati e pertinenti
description: Una piattaforma di eCommerce è uno dei canali di coinvolgimento più cruciali. La disponibilità di aggiornamenti senza soluzione di continuità nel sistema di gestione delle risorse garantisce che le vetrine commerciali presentino sempre le informazioni di prodotto più aggiornate.
feature: CMS, Media, Integration
exl-id: 2c749e84-fcc4-4bf9-90b2-87438329889e
TQID: 'https://experienceleague.adobe.com/cTeAl0vABSDcqSR9S7pGkV2yGnFHz11VmXtPoE0C86M'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%
---
# Mantenere contenuti accurati e pertinenti

Una vera fornitura di contenuti implica una combinazione di pilastri chiave tra **Creazione e produzione**, **Flusso di lavoro e pianificazione** e **Consegna e attivazione**. Ognuno di questi pilastri è prezioso da solo e contribuisce a fornire un valore significativo alle organizzazioni:

![Pilastri Chiave](../assets/key-pillars.png){width="600" zoomable="yes"}

Una piattaforma di eCommerce è uno dei canali di coinvolgimento più cruciali. La disponibilità di aggiornamenti senza soluzione di continuità nel sistema di gestione delle risorse garantisce che le vetrine commerciali presentino sempre le informazioni di prodotto più aggiornate. Ciò è essenziale per raggiungere i tre obiettivi principali di qualsiasi **DAM (Digital Asset Management System)** &lt;> **integrazione Commerce**:

* Migliora **Time-to-Market (TTM)** per i nuovi lanci di prodotti.

* Eliminazione delle inefficienze operative e riduzione delle interazioni manuali.

* Assicurati la coerenza del brand fornendo sempre contenuti approvati in linea con le linee guida del brand.

Per raggiungere questi obiettivi, l&#39;integrazione AEM Assets per Commerce è abbonata a **eventi Adobe Commerce** e **AEM Assets**, garantendo la sincronizzazione dinamica tra il contenuto e l&#39;e-commerce.

## Modifiche al catalogo Adobe Commerce

L&#39;integrazione di AEM Assets ascolta gli eventi di creazione del prodotto attivati quando i prodotti vengono creati in **Admin** o utilizzando **API**. Quando viene attivato, sincronizza le risorse approvate dal DAM associate al nuovo SKU del prodotto.

Disaccoppiando la creazione dei contenuti dalla gestione dei cataloghi, le aziende ottengono diversi vantaggi:

* I team che si occupano dei contenuti possono operare in modo indipendente, assicurando la disponibilità di risorse di alta qualità pronte per il lancio dei prodotti.

* Gli aggiornamenti dei prodotti rimangono rapidi perché la creazione delle risorse non ritarda le modifiche al catalogo, consentendo una maggiore agilità nella gestione dei nuovi prodotti.

* L&#39;automazione migliora l&#39;efficienza e l&#39;accuratezza, riducendo le incongruenze tra i dati dei prodotti e i contenuti associati.

>[!NOTE]
>
> Le importazioni di prodotti CSV in PaaS e SaaS non attivano gli eventi di aggiornamento. Utilizza l’API per le importazioni e gli aggiornamenti dei cataloghi.

## Modifiche al ciclo di vita di AEM Assets

L’integrazione è in ascolto anche delle modifiche dello stato delle risorse in AEM Assets. Poiché Adobe Commerce funge da canale di coinvolgimento, nella vetrina vengono visualizzate solo le risorse approvate.

L’integrazione automatizza la gestione del ciclo di vita delle risorse per garantire che i contenuti della vetrina rimangano precisi e conformi al marchio.

* Vengono pubblicate solo le risorse approvate, mantenendo l&#39;integrità del marchio e la conformità alle normative.

* Le risorse obsolete o irrilevanti vengono rimosse automaticamente, impedendo la visualizzazione di contenuto non aggiornato.

* La sincronizzazione perfetta tra l’approvazione delle risorse e la visualizzazione dei prodotti riduce gli sforzi manuali e i ritardi.

Sfruttando l&#39;integrazione di AEM Asset Selector, le aziende possono mantenere una fornitura di contenuti semplificata, accurata ed efficiente, migliorando sia l&#39;esperienza del cliente che l&#39;efficienza operativa.
