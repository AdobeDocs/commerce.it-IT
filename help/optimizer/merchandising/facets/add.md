---
title: Creare e gestire i facet
description: Scopri come aggiungere e gestire i facet in [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: d6b7ff1f-a9b8-4fb8-8bd3-b3596695045c
source-git-commit: ad8fb7d1d7e1ad124647ba84377079dcfbd46a3c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Creare e gestire i facet

Qualsiasi attributo di prodotto filtrabile può essere utilizzato come facet. Facet aiuta i clienti a filtrare e trovare i prodotti più facilmente nel tuo negozio. Questo articolo spiega come aggiungere, gestire e configurare facet nella vetrina.

![Crea un facet](../../assets/create-facet.png)

## Creare un facet

1. Nella barra a sinistra, seleziona _Merchandising_ > **Facet**, quindi fai clic su **Crea facet**.
1. Nell&#39;elenco *Crea facet*, ogni attributo disponibile ha un ![pulsante Aggiungi](../../assets/btn-add.png) separato. Completa una delle seguenti operazioni:

   - Nell&#39;elenco *Attributi facet*, scegliere l&#39;attributo prodotto che si desidera utilizzare come facet e fare clic su **Aggiungi**.
   - Per trovare un attributo di prodotto specifico, immettere i primi caratteri del nome dell&#39;attributo nella casella *Cerca*. Quindi fare clic su **Aggiungi**.

   Il facet viene aggiunto nella parte inferiore dell&#39;elenco *Facet dinamici* e il pulsante *Pubblica modifiche* diventa disponibile.

1. Se il facet che desideri aggiungere non è stato trovato, utilizza l&#39;[API metadati](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata) per impostare il parametro `searchable`:

   `"searchable": true`

   Il facet diventa disponibile nella vetrina alla successiva sincronizzazione del catalogo con [!DNL Adobe Commerce Optimizer]. Se il facet non è disponibile dopo due ore, vedere [sincronizzazione dati](../../setup/data-sync.md).

## Modifica proprietà facet (facoltativo)

1. Trovare il facet da modificare.
1. Fai clic sul selettore aggiuntivo (![Altro](../../assets/btn-more.png)).
1. Scegliere **Modifica** dal menu. Quindi, regola le seguenti proprietà in base alle esigenze:

   - Etichetta: immetti l’etichetta facet che desideri utilizzare.
   - Tipo di ordinamento: scegliere una delle opzioni seguenti:
      - Alfabetico - Ordina alfabeticamente i facet
      - Conteggio: ordina i facet in base al numero di corrispondenze trovate
   - Valore massimo: immettere il numero massimo di valori di facet visualizzati nella vetrina. Voci valide: 0 - 100; valore predefinito: 8.

1. Al termine, fare clic su **Salva**.

## Faccette pin/spin

Il pin cambia colore quando si fa clic e viene utilizzato per spostare il facet nella sezione *Facet bloccati* o *Facet dinamici*.

1. Per aggiungere un facet all&#39;inizio dell&#39;elenco *Filtri*, individuarlo nell&#39;elenco *Facet dinamici* e fare clic sul pin grigio (![Selettore pin](../../assets/btn-pin-gray.png)).

   Il pin diventa blu e il facet si sposta nella sezione *Facet bloccati*.

1. Per sbloccare un facet, individuarlo nell&#39;elenco *Facet bloccati* e fare clic sul pin blu (![Selettore pin](../../assets/btn-pin-blue.png)).

   Il pin diventa grigio e il facet si sposta nella sezione *Facet dinamici*.

>[!NOTE]
>
>L’ordinamento dei facet aggiunti potrebbe non essere coerente se sono presenti due etichette con lo stesso nome.

## Elimina facet

1. Trova il facet nell&#39;elenco e fai clic sul selettore aggiuntivo (![Altro selettore](../../assets/btn-more.png)).
1. Fare clic su **Elimina**.
1. Quando viene richiesto di confermare, fare clic su **Elimina facet**.
Il facet viene rimosso dalla vetrina dopo la pubblicazione delle modifiche.

## Pubblica modifiche

1. Per aggiornare la vetrina con le tue modifiche, fai clic su **[!UICONTROL Publish]**.
1. Attendi circa 15 minuti prima che gli aggiornamenti vengano visualizzati nel tuo store.

## Informazioni aggiuntive

- Per configurare intervalli e raggruppamenti di price faceting, vedere [Impostazioni](../../settings.md).
- Ulteriori informazioni sui [tipi](type.md) di facet.
