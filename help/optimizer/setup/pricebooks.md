---
title: Listino prezzi
description: Scopri come gestire i listini prezzi in [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e [!DNL Adobe Commerce Optimizer] (infrastruttura SaaS gestita da Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
TQID: https://experienceleague.adobe.com/-vL79MMePcUdhE-gPwjFJZStZUtNLKAUxpePm4Fvmfk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: cde6d0c92f4c169588164c22c948d1b287873bdd
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%
---
# Listino prezzi

I listini prezzi definiscono i prezzi dei prodotti per un&#39;origine catalogo per i diversi livelli cliente e mercati. Supportano un modello gerarchico, che consente fino a tre livelli di listini prezzi figlio nidificati sotto ogni listino prezzi base. Ogni listino prezzi può fare riferimento a un listino prezzi padre, formando una struttura ad albero per le origini del catalogo di determinazione prezzi.

![Gerarchia listino prezzi](../assets/price-book-hier.png)

Il listino prezzi base definisce la valuta per se stesso e per tutti i listini prezzi figlio. I listini prezzi figlio ereditano questa valuta e non possono sostituirla.

## Concetti chiave

| Termine | Descrizione |
| ------ | ------------- |
| **Listino prezzi** | Raggruppamento logico che definisce i prezzi per un’origine di catalogo, ad esempio area geografica specifica o livello cliente, e viene utilizzato per gestire i prezzi dei prodotti. |
| **Fallback listino prezzi** | Il listino prezzi più alto di una gerarchia. Non ha alcun padre ed è il listino prezzi *only* che definisce la valuta per se stesso e per tutti i listini prezzi discendenti.<br/><br/>Se durante la creazione del listino prezzi non è stato definito alcun padre tramite l&#39;API, viene creato un nuovo listino prezzi di fallback. |
| **Listino prezzi principale** | Un listino prezzi di livello superiore da cui un listino prezzi dedicato figlio può ereditare i prezzi se non sono impostati in modo esplicito nel figlio. |
| **Profondità gerarchia** | Massimo di tre livelli (Fallback -> Figlio -> Nipote)<br/><br/>non applicato al momento dell&#39;acquisizione. |
| **Valuta** | Definito solo per il listino prezzi di riserva. Ereditato da tutti i libri prezzi per bambini.<br/><br/>Se non viene specificata la valuta durante la creazione del listino prezzi di fallback (tramite l&#39;API), la valuta viene impostata automaticamente su USD. |
| **Prezzo del prodotto** | Il prezzo specifico assegnato a un prodotto (SKU) all’interno di un particolare listino prezzi. |
| **Sconti** | Gli sconti sono definiti nel prezzo del prodotto. Non ereditato. |

## Implementazione del listino prezzi dedicato

L’implementazione del listino prezzi varia in base all’implementazione di Commerce.

* Nelle istanze Adobe Commerce Optimizer con backend Commerce di terze parti, i listini prezzi vengono creati utilizzando l’API REST per l’acquisizione dei dati. Puoi assegnarli e gestirli dall’area di lavoro Visualizzazione catalogo in Commerce Optimizer Studio.

* In Adobe Commerce as a Cloud Service con il modello dati catalogo componibile (CCDM), i listini prezzi vengono mappati dai dati di catalogo e di determinazione prezzi di Adobe Commerce. È possibile visualizzare i listini prezzi assegnati a ogni vista catalogo dall&#39;amministratore di Commerce.

* In Adobe Commerce su infrastrutture cloud o implementazioni on-premise con il connettore Adobe Commerce Optimizer, i listini prezzi vengono mappati anche dai dati di catalogo e prezzi di Adobe Commerce. È possibile visualizzare i listini prezzi assegnati a ogni vista catalogo dall&#39;area di lavoro Vista catalogo nell&#39;istanza di Commerce Optimizer connessa.

## Aggiungi listini prezzi

È possibile aggiungere listini prezzi a [!DNL Adobe Commerce Optimizer] utilizzando l&#39;API Listino prezzi. Per informazioni su come creare, aggiornare ed eliminare i listini prezzi per [!DNL Adobe Commerce Optimizer], consulta la [documentazione per sviluppatori](https://developer.adobe.com/commerce/services/reference/rest/).

## Visualizza listini prezzi

Dopo aver acquisito i listini prezzi in [!DNL Adobe Commerce Optimizer], puoi visualizzare l&#39;elenco dei listini prezzi e gli ID corrispondenti nella **visualizzazione catalogo** pagina.

>[!NOTE]
>
>Una visualizzazione del catalogo privato (con [!UICONTROL Catalog Protection] abilitato) può fare riferimento a un solo listino prezzi dedicato. Consulta [Restrizione del listino prezzi dedicato alle visualizzazioni di cataloghi privati](private-catalog-view.md#price-book-restriction-on-private-catalog-views).

1. Vai a _Configurazione archivio_ e fai clic su **[!UICONTROL Catalog views]**.

1. Fare clic su **[!UICONTROL Create catalog view]**. &#x200B;

   Nella finestra di dialogo Configura i dettagli della visualizzazione catalogo selezionare uno dei listini prezzi disponibili.

   ![Nomi e ID listino prezzi](../assets/price-book-name-ids.png)

## Configura disponibilità listino prezzi dedicato

Specificare i dati di determinazione prezzi disponibili per ogni vista di catalogo configurando la disponibilità del listino prezzi per ogni vista.

1. Dall&#39;area di lavoro **Visualizzazione catalogo**, selezionare la visualizzazione catalogo che si desidera configurare.

1. Nella sezione [!UICONTROL Price Books] selezionare le opzioni del listino prezzi dedicato per configurare i prezzi disponibili per i negozi supportati dalla vista catalogo.

1. Fare clic su **[!UICONTROL Save]** per applicare le modifiche alla visualizzazione del catalogo.
