---
title: Gestisci facet
description: Scopri come gestire i  [!DNL Live Search]  facet esistenti.
exl-id: 5062bb1f-ce6f-4244-a1df-65ae1ce868b9
TQID: https://experienceleague.adobe.com/KWh5KwVRNJO3XLiG9xbqhBsGkt99BgY0hPnPbxDd8vY
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 481
ht-degree: 0%

---

# Gestisci facet

Segui queste istruzioni per aggiornare le proprietà dei facet esistenti o modificarne la presentazione nella vetrina.

## Configura raggruppamenti facet di prezzo

Consulta [Impostazioni](settings.md) per configurare intervalli e raggruppamenti di price faceting.

## Modifica facet

1. Trovare il facet da modificare.
1. Se nell&#39;elenco sono presenti molti facet, impostare *Filtra per* su uno dei seguenti:

   * Bloccato
   * Dinamico

   Per ulteriori informazioni, vai a [Tipi di facet](facets-type.md).

   ![Facet filtro](assets/facets-filter-by-cropped.png)

1. Per modificare le proprietà del facet, fare clic su **Altro** (...) opzioni.
1. Fai clic su **Modifica**

   ![Modifica opzioni](assets/facet-edit-menu.png)

1. Per modificare l&#39;etichetta del facet, effettuate una delle seguenti operazioni:

   * Per una vetrina [!DNL Commerce], modifica l&#39;[etichetta attributo](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html).
   * Per un’implementazione headless, fai clic sul valore nella prima colonna e modifica il testo in base alle esigenze.

   ![Modifica etichetta](assets/facet-edit-label.png)

1. (Solo headless) Per modificare il metodo utilizzato per ordinare i valori dei facet, fare clic sul valore nella colonna *Tipo di ordinamento* e scegliere una delle opzioni seguenti:

   * Alfabetico
   * Conteggio

   ![Modifica conteggio](assets/facets-edit-count.png)

1. Nella colonna **Valore massimo** impostare il numero massimo (da 0 a 10) di valori di filtro facet da visualizzare nella vetrina.
1. Al termine, fare clic su **Salva**.

   Le modifiche verranno visualizzate nella vetrina solo dopo la loro pubblicazione.

## Faccetta pin/spin

Il pin cambia colore quando si fa clic e viene utilizzato per spostare il facet nella sezione *Facet bloccati* o *Facet dinamici*.

1. Per aggiungere un facet all&#39;inizio dell&#39;elenco *Filtri*, individuarlo nell&#39;elenco *Facet dinamici* e fare clic sul pin grigio (![Selettore pin](assets/btn-pin-gray.png)).

   Il pin diventa blu e il facet si sposta nella sezione *Facet bloccati*.

1. Per sbloccare un facet, individuarlo nell&#39;elenco *Facet bloccati* e fare clic sul pin blu (![Selettore pin](assets/btn-pin-blue.png)).

   Il pin diventa grigio e il facet si sposta nella sezione *Facet dinamici*.

   ![Facet bloccati e dinamici](assets/facets-pinned-unpinned.png)

>[!NOTE]
>
>L’ordinamento dei facet aggiunti potrebbe non essere coerente se sono presenti due etichette con lo stesso nome.

## Sposta facet fissato

>[!NOTE]
>
>L’ordinamento dei facet bloccati è supportato solo nelle implementazioni headless. Se sono necessari facet ordinati, utilizzare il widget PLP [!DNL Live Search].

L&#39;ordine delle sfaccettature fissate può essere modificato spostando la riga in una posizione diversa. I facet bloccati hanno un&#39;icona *Sposta* (![Sposta selettore](assets/btn-move.png)) all&#39;inizio della riga. A differenza dei facet bloccati, i facet dinamici non possono essere spostati.

1. Trova il facet nella sezione *Facet bloccati* dell&#39;elenco.
1. Utilizza l&#39;icona **Sposta** (![Sposta selettore](assets/btn-move.png)) per trascinare la riga in una nuova posizione nella sezione *Facet bloccati*.

   Dopo la pubblicazione delle modifiche, i facet riordinati vengono visualizzati nell&#39;elenco *Filtri* della vetrina.

## Elimina facet

1. Trova il facet nell&#39;elenco e fai clic su **Altro** (...) opzioni.
1. Fare clic su **Elimina**.
1. Quando viene richiesto di confermare, fare clic su **Elimina facet**.
Il facet viene rimosso dalla vetrina dopo la pubblicazione delle modifiche.

## Pubblica modifiche

1. Per aggiornare la vetrina con le modifiche, fai clic su **Pubblica modifiche**.
1. Attendi circa 15 minuti prima che gli aggiornamenti vengano visualizzati nel tuo store.
