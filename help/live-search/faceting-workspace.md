---
title: Faceting Workspace
description: Scopri come aggirare l'area di lavoro  [!DNL Live Search] faceting.
exl-id: 7108e41b-44a7-4943-b20f-6ee544d099e9
TQID: https://experienceleague.adobe.com/LsVM4inUqk2EozfVN--FH1Ukggt8A8QBIQXW-SmnxZs
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
source-wordcount: 229
ht-degree: 0%

---

# Faceting Workspace

L&#39;area di lavoro *Faceting* elenca tutti i facet attualmente disponibili e fornisce l&#39;accesso agli strumenti necessari per impostare e gestire i facet. I facet bloccati vengono visualizzati per primi nell&#39;elenco dei facet esistenti, seguiti dai facet dinamici. L’elenco può essere filtrato per mostrare tutti i facet oppure solo quelli bloccati o dinamici.

![Area di lavoro di faceting](assets/faceting-workspace.png)

## Impostare l&#39;ambito

Se l&#39;installazione di Adobe Commerce include più visualizzazioni dello store, impostare **Ambito** sulla [visualizzazione dello store](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) in cui si applicano le impostazioni del facet.

## Filtrare l’elenco

1. Fare clic sul controllo **Filtra per**.
1. Scegliere una delle opzioni seguenti:

   * Tutti i filtri
   * Bloccato
   * Dinamico

## Aggiungi un facet

1. Fare clic su **Aggiungi facet**.
1. Per istruzioni dettagliate, consulta [Aggiungi facet](facets-add.md).

## Descrizioni delle colonne

| Colonna | Descrizione |
|--- |--- |
| (prima colonna) | Elenca i facet bloccati e dinamici dall&#39;[etichetta](facets-type.md) che è visibile all&#39;acquirente. |
| Tipo di ordinamento | [ordinamento](facets-type.md) dei valori facet. I facet sono ordinati alfabeticamente per tutti i [!DNL Commerce] storefront. Per le implementazioni [headless], i facet possono essere ordinati alfabeticamente o per conteggio. Opzioni: Alfabetico, Conteggio (solo headless) |
| Valore massimo | Il numero di valori di facet disponibili nella vetrina come filtri, con un massimo di 10. |

## Controlli

| Controllo | Descrizione |
|--- |--- |
| Aggiungi facet | Apre l&#39;[editor facet](facets-add.md). |
| Filtra per | Determina il [tipo di facet](facets-type.md) visualizzati nell&#39;elenco. Opzioni: Tutto, Bloccato, Dinamico |
