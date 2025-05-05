---
title: Posizione archivio e configurazione del sistema di mappatura
description: Configurare un provider di servizi a distanza per supportare la mappatura della posizione del negozio nell'interfaccia utente della vetrina. Le soluzioni Store Fulfillment richiedono un fornitore a distanza per abilitare la ricerca nel punto vendita al dettaglio e altre funzionalità di mappatura e pianificazione per il flusso di lavoro di implementazione end-to-end.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Impostazione della posizione del negozio e della mappatura

Abilitare le funzionalità di mappatura e posizione del negozio per il completamento del negozio configurando un provider di [distanza](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/configuration/distance-priority-algorithm) per la ricerca di posizioni del negozio al dettaglio.

**Requisiti**

Durante il processo di configurazione, fornisci una chiave API Google per la piattaforma Google Maps. In caso contrario, [generarne uno dalla piattaforma Google Maps](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps).

Per configurare il provider di distanze:

1. Dalla configurazione **[!UICONTROL Stores > General]** in Admin, aggiungi l&#39;integrazione Google Maps per il tipo di contenuto Map.

   - Vai a **[!UICONTROL Stores > Configuration  > General > Content Management]**.

   - Aggiungi la chiave API Google al campo **[!UICONTROL Google Maps API Key]**.

1. Dalla configurazione **[!UICONTROL Stores > Inventory]** nell&#39;amministratore, selezionare il provider di distanza per il completamento del punto vendita.

   - Vai a **[!UICONTROL Stores > Configuration > Catalog > Inventory]**.

   - Espandere la sezione **[!UICONTROL Distance Provider for Distance Based SSA]**.

   - Impostare **Provider** su **Google Map**.

1. Configurare le impostazioni per **[!UICONTROL Google Distance Provider]**.

   - Aggiungi la tua **chiave API Google**.

   - Imposta **[!UICONTROL Computation Mode]** su `Driving` e **[!UICONTROL Value]** su `Distance`
