---
title: Listino prezzi
description: Scopri come gestire i listini prezzi in [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 1c720bc3ba755639eff2f17912fb3a3446e367f6
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Listino prezzi

I listini prezzi consentono di definire i prezzi dei prodotti per un&#39;origine catalogo su diversi livelli cliente e mercati. I listini prezzi supportano un modello gerarchico che consente fino a tre livelli di listini prezzi figlio nidificati sotto ogni listino prezzi base. Ogni listino prezzi può fare riferimento a un listino prezzi padre, formando una struttura ad albero per le origini del catalogo di determinazione prezzi.

![Gerarchia listino prezzi](../assets/price-book-hier.png)

Il listino prezzi base definisce la valuta per se stesso e per tutti i listini prezzi figlio. I listini prezzi figlio ereditano questa valuta e non possono sostituirla.

## Aggiungi listini prezzi a Commerce Optimizer

Puoi aggiungere listini prezzi a Commerce Optimizer utilizzando l’API Listino prezzi. Per informazioni su come creare, aggiornare ed eliminare i listini prezzi per [, consulta la &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/)documentazione per sviluppatori[!DNL Adobe Commerce Optimizer].

## Visualizza listini prezzi in Commerce Optimizer

Dopo aver acquisito i listini prezzi in Commerce Optimizer, puoi visualizzare l&#39;elenco dei listini prezzi e gli ID corrispondenti nella pagina **Visualizzazione catalogo**.

1. Vai a _Configurazione archivio_ e fai clic su **[!UICONTROL Catalog views]**.

1. Fare clic su **[!UICONTROL Create catalog view]**. &#x200B;

   Nella finestra di dialogo Configura i dettagli della visualizzazione catalogo selezionare uno dei listini prezzi disponibili.

   ![Nomi e ID listino prezzi](../assets/price-book-name-ids.png)

## Concetti chiave

| Termine | Descrizione |
|------|-------------|
| **Listino prezzi** | Raggruppamento logico che definisce i prezzi per un’origine di catalogo, ad esempio area geografica specifica o livello cliente, e viene utilizzato per gestire i prezzi dei prodotti. |
| **Fallback listino prezzi** | Il listino prezzi più alto di una gerarchia. Non ha alcun padre ed è il listino prezzi *only* che definisce la valuta per se stesso e per tutti i listini prezzi discendenti.<br/><br/>Se durante la creazione del listino prezzi non è stato definito alcun padre tramite l&#39;API, viene creato un nuovo listino prezzi di fallback. |
| **Listino prezzi principale** | Un listino prezzi di livello superiore da cui un listino prezzi dedicato figlio può ereditare i prezzi se non sono impostati in modo esplicito nel figlio. |
| **Profondità gerarchia** | Massimo di tre livelli (Fallback -> Figlio -> Nipote)<br/><br/>non applicato al momento dell&#39;acquisizione. |
| **Valuta** | Definito solo per il listino prezzi di riserva. Ereditato da tutti i libri prezzi per bambini.<br/><br/>Se non viene specificata la valuta durante la creazione del listino prezzi di fallback (tramite l&#39;API), la valuta predefinita è USD. |
| **Prezzo del prodotto** | Il prezzo specifico assegnato a un prodotto (SKU) all’interno di un particolare listino prezzi. |
| **Sconti** | Gli sconti sono definiti nel prezzo del prodotto. Non ereditato. |
