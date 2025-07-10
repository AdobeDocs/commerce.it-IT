---
title: Corrispondenza automatica predefinita
description: Scopri in che modo la regola di corrispondenza automatica predefinita consente una sincronizzazione perfetta tra Adobe Commerce e l’integrazione AEM Assets, garantendo che le risorse siano collegate automaticamente alle entità di merchandising corrette.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
source-git-commit: 6640635fca5c53fe4b06b9bbb3120fffc46cb0b8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Corrispondenza automatica predefinita

L&#39;integrazione AEM Assets per Commerce fornisce un meccanismo di corrispondenza automatica predefinito (**[!UICONTROL Match by product SKU]**) basato sulla configurazione dei metadati **AEM Assets**. Questa regola abilita la sincronizzazione perfetta tra **Adobe Commerce** e **AEM Assets**, garantendo che le risorse siano collegate automaticamente alle entità di merchandising corrette.

## Configurare il meccanismo di corrispondenza automatica

1. Dall&#39;amministratore di Commerce, passare a **[!UICONTROL Store]** > Configurazione > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Specificare **[!UICONTROL Match by SKU]** come regola corrispondente.

   ![regola di corrispondenza automatica predefinita](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. Immetti il nome del campo metadati utilizzato per l’identificazione delle risorse in AEM Assets.

   >[!NOTE]
   >
   > Se è stato seguito il processo di onboarding standard, questo valore deve essere impostato su `commerce:skus`.

## Funzionamento del meccanismo di abbinamento automatico

Quando la regola di corrispondenza **[!UICONTROL Match by product SKU]** è configurata in Commerce Admin, i file di risorse Commerce vengono sincronizzati automaticamente da AEM Assets al progetto Commerce in base ai metadati delle risorse configurati per ciascun file. Puoi configurare i metadati dalla scheda AEM **Commerce** nell&#39;ambiente **AEM Assets author**:

![Esempio di metadati](../assets/example-metadata.png){width="600" zoomable="yes"}

1. In AEM Assets, aggiorna i metadati dell&#39;immagine per aggiungere l&#39;associazione Adobe Commerce, `Commerce=yes`.

1. Configurare i metadati ([!UICONTROL SKU], [!UICONTROL position] e [!UICONTROL role]) che collegano la risorsa allo SKU del prodotto associato.

   >[!NOTE]
   >
   > Se una risorsa viene utilizzata per più prodotti, configura i metadati per ogni SKU associata.

Questo approccio garantisce che le risorse digitali siano collegate e visualizzate correttamente in Adobe Commerce. Consente inoltre a commercianti e addetti al marketing di gestire ruoli e posizionamento delle risorse direttamente all’interno di AEM Assets, fornendo un meccanismo coerente e centralizzato per la selezione e l’ordinamento delle immagini su tutti i canali di coinvolgimento.
