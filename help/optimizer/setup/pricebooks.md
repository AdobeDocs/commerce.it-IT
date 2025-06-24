---
title: Listino prezzi
description: Scopri come gestire i listini prezzi in [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Listino prezzi

In questo articolo viene descritto come definire e assegnare listini prezzi alle viste catalogo con controlli appropriati per la governance dei dati.

Consulta la [documentazione per sviluppatori](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books) per scoprire come acquisire in [!DNL Adobe Commerce Optimizer] le informazioni sul listino prezzi dedicato da un sistema di terze parti utilizzando l&#39;API Listino prezzi dedicato.

Con i listini prezzi è possibile definire le origini del catalogo dei prezzi per gestire i prezzi dei prodotti in diversi livelli cliente e mercati. I listini prezzi supportano un modello gerarchico che consente fino a tre livelli di listini prezzi figlio nidificati sotto ogni listino prezzi base. Ogni listino prezzi può fare riferimento a un listino prezzi padre, formando una struttura ad albero per le origini del catalogo di determinazione prezzi.

Il listino prezzi base definisce la valuta per se stesso e per tutti i listini prezzi figlio. I listini prezzi figlio ereditano questa valuta e non possono sostituirla.

## Concetti chiave

| Termine | Descrizione |
|------|-------------|
| **Listino prezzi** | Raggruppamento logico che definisce l’origine del catalogo dei prezzi, ad esempio un’area specifica o il livello cliente, e che viene utilizzato per gestire i prezzi dei prodotti. |
| **Fallback listino prezzi** | Il listino prezzi più alto di una gerarchia. Non ha alcun padre ed è il listino prezzi *only* che definisce la valuta per se stesso e per tutti i listini prezzi discendenti.<br/><br/>Se durante la creazione del listino prezzi non è stato definito alcun padre tramite l&#39;API, viene creato un nuovo listino prezzi di fallback. |
| **Listino prezzi principale** | Un listino prezzi di livello superiore da cui un listino prezzi dedicato figlio può ereditare i prezzi se non sono impostati in modo esplicito nel figlio. |
| **Profondità gerarchia** | Massimo 3 livelli (Fallback → Child → Grandchild)<br/><br/>non applicati al momento dell&#39;acquisizione. |
| **Valuta** | Definito solo nel listino prezzi di riserva. Ereditato da tutti i bambini, listini prezzi.<br/><br/>Se non viene specificata la valuta durante la creazione del listino prezzi di fallback (tramite l&#39;API), la valuta predefinita è USD. |
| **Prezzo del prodotto** | Il prezzo specifico assegnato a un prodotto (SKU) all’interno di un particolare listino prezzi. |
| **Sconti** | Gli sconti sono definiti in Prezzo del prodotto. Non ereditato. |
