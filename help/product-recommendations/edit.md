---
title: Modifica consiglio
description: Scopri come modificare un consiglio di prodotto.
exl-id: 57bc68c0-03ba-4b66-8c75-14e49176670b
TQID: https://experienceleague.adobe.com/iynpVCKsygJXg2v-Djctfb4bhV9FMheA0ab66IBOvCg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 428
ht-degree: 0%

---

# Modifica consiglio

La pagina Modifica consiglio consente di regolare le singole impostazioni che compongono il consiglio. È possibile modificare tutte le impostazioni tranne il tipo di pagina e il tipo di consiglio. È possibile modificare le seguenti impostazioni:

- [Nome consiglio](#name)
- [Etichetta vetrina](#label)
- [Numero di prodotti](#number)
- [Posizionamento e posizione](#placement)
- [Filtra prodotti](#filters)

L’anteprima a destra della pagina mostra come potrebbe apparire nella vetrina il consiglio con le impostazioni correnti. L&#39;anteprima dei _prodotti consigliati_ rimane visibile per riferimento mentre scorri la pagina verso il basso. L’anteprima mostra una miniatura dell’immagine del prodotto, il nome del prodotto, lo SKU, il prezzo e il tipo di risultato per ciascun prodotto restituito. Il tipo di risultato indica se i dati comportamentali primari sono sufficienti per generare il consiglio o se vengono utilizzati dati comportamentali di backup.

![Modifica consigli](assets/edit-recommendation.png)

## Modificare un consiglio

1. Nella barra laterale _Amministratore_, vai a **Marketing** > _Promozioni_ > **Consigli di prodotto**.

1. Seleziona il consiglio da modificare.

1. Fai clic su **Modifica**. Quindi, segui le istruzioni riportate di seguito per apportare le modifiche necessarie.

1. Al termine, fare clic su **Salva modifiche**.

### Nome consiglio {#name}

Scegli un nome descrittivo che indichi lo scopo del consiglio. Il nome è un riferimento interno e non viene visualizzato nella vetrina.

![Modifica nome](assets/edit-name.png)

### Etichetta vetrina {#label}

Inserisci il testo da utilizzare come etichetta per l’unità Consigli nella vetrina.

![Modifica etichetta](assets/edit-storefront-label.png)

### Numero di prodotti {#number}

Regola il cursore per visualizzare fino a 20 prodotti nell’unità di consigli.

![Modifica numero di prodotti](assets/edit-number-of-products.png)

### Posizionamento e posizione {#placement}

1. Scegli la posizione della pagina in cui deve apparire l&#39;unità di consigli nella vetrina.

   - Nella parte inferiore del contenuto principale
   - Nella parte superiore del contenuto principale

   ![Modifica posizionamento](assets/edit-placement.png)

1. Per modificare l&#39;ordine dei consigli inclusi nell&#39;unità, utilizzare il controllo **Sposta** ![Sposta selettore](assets/icon-move.png) per trascinare i consigli nella posizione desiderata.

   ![Modifica posizione](assets/edit-position.png)

### Filtra prodotti {#filters}

Eventuali modifiche apportate ai [filtri](filters.md) del prodotto si riflettono nell&#39;_anteprima prodotti consigliata_. È consentito consigliare solo i prodotti che corrispondono ai filtri di inclusione. Non sono consigliati i prodotti che corrispondono a qualsiasi filtro di esclusione.

Nelle schede _Inclusioni_ e _Esclusioni_ sono elencati i filtri disponibili di ciascun tipo. Nell’elenco, ogni filtro attivo è contrassegnato da un punto blu.

- Per visualizzare i dettagli di ciascun filtro, fai clic sul nome del filtro.
- Per modificare lo stato del filtro, impostare l&#39;opzione **Abilita filtro** su `on` o `off`.

![Modifica filtri](assets/edit-filters.png)

Le impostazioni del filtro descrivono i prodotti da includere o escludere nell’unità di consigli. Ad esempio, le impostazioni di inclusione del filtro _Categoria_ indicano al sistema di includere solo i prodotti delle categorie selezionate.

![Modifica filtro categoria](assets/edit-filter-category.png)
