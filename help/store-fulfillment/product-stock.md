---
title: Gestione magazzino prodotto
description: Configura i messaggi sulle azioni e le funzioni disponibili per i clienti.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Gestione magazzino prodotto

In qualità di commerciante, puoi utilizzare le opzioni di azioni e origini di Adobe Commerce [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction). È inoltre possibile utilizzare la soluzione di evasione del punto vendita per controllare altre opzioni di disponibilità del magazzino correlate alle operazioni del punto vendita esercente.

- Opzione di consegna a domicilio da negozi mercantili

- Consenti/Disponibile per ritiro negozio

- UPC / SKU / Altri identificatori di prodotto univoci

- Soglia esaurita

- Diminuzione delle scorte da ubicazioni specifiche in base all&#39;ordine

Configurare le opzioni Stock di prodotto dall&#39;amministratore: **[!UICONTROL Catalog > Products > Select Product]**

## **Opzioni Stock Di Prodotto**

| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|--------------|
| **Disponibile per la consegna a domicilio** | <p>Imposta la disponibilità della consegna a domicilio (dal punto vendita) per il prodotto. Quando questa opzione è abilitata, tutte le ubicazioni di negozi commerciali assegnate con scorte disponibili per il prodotto sono considerate idonee per l’opzione Consegna a domicilio. Quando questa opzione è disabilitata, il prodotto non è mai idoneo per la consegna a domicilio.</p>Di solito, è sufficiente impostare questa opzione a livello di negozio di esercenti. Tuttavia, potrebbero esserci casi specifici per prodotti specifici, come quelli soggetti a restrizioni federali di spedizione, che non dovrebbero essere idonei per la consegna a domicilio.</p> | Sito Web | No |
| **[!UICONTROL Available for Store Pickup]** | <p>Imposta la disponibilità del ritiro dello store per il prodotto. Quando questa opzione è abilitata, tutte le ubicazioni di negozi mercantili assegnate con scorte disponibili per il prodotto sono considerate idonee per l’opzione Ritiro da store. Se disabilitato, il prodotto non è mai idoneo per il ritiro dal negozio.</p><p>Questa opzione può essere utile per tenere traccia dell’inventario dei commercianti nel sistema che non desideri vendere dal tuo canale di e-commerce.</p> | Sito Web | No |
| **[!UICONTROL UPC / SKU / Custom Scannable Identifier]** | Questo attributo deve esistere come attributo di prodotto e fa riferimento all&#39;impostazione **[!UICONTROL Barcode Source / Barcode Type]**. Questo attributo viene utilizzato per tenere traccia di un codice a barre digitalizzabile per i prodotti. Questo valore può essere inviato quando un ordine viene inviato ai negozi esercenti per il prelievo. Gli associati al negozio possono utilizzare il valore con la distinta di prelievo per far corrispondere i prodotti sullo scaffale utilizzando uno scanner con codice a barre. | Visualizzazione store | No |

{style="table-layout:auto"}

## Origini per inventario a livello di prodotto

| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Out of Stock Threshold]** | <p>Impostare la soglia del magazzino per l&#39;articolo all&#39;interno di ogni origine. Quando le scorte scendono al di sotto della soglia, vengono considerate esaurite alla fonte.</p><p>Per utilizzare l&#39;impostazione Configurazione archivio globale, selezionare l&#39;opzione **[!UICONTROL Use Default]**.</p> | Globale | No |
| **[!UICONTROL Allow Store Pickup]** | <p>Imposta in modo esplicito se l&#39;articolo è disponibile per il prelievo dal negozio, indipendentemente dalla configurazione disponibile dell&#39;ubicazione del magazzino o del negozio esercente.</p><p>Per utilizzare l&#39;impostazione a livello di prodotto, deselezionare l&#39;opzione [!UICONTROL Use Default] ed effettuare la selezione. In caso contrario, questa impostazione viene scelta in base alla configurazione per **[!UICONTROL Allow In-Store Pickup]** impostata sull&#39;origine stock.</p> | Globale | No |

{style="table-layout:auto"}

