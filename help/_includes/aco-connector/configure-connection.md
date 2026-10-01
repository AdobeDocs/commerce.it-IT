---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# Ottieni dettagli istanza [!DNL Commerce Optimizer]

Ottieni l&#39;ID _tenant_ dal campo _[!DNL Instance Id]_&#x200B;nell&#39;istanza [[!DNL Instance details] page](/help/optimizer/get-started.md#manage-instances) di [!DNL Commerce Optimizer] o dall&#39;URL utilizzato per accedere all&#39;istanza. Ad esempio, in `https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`.

1. Dall&#39;amministratore di Commerce, selezionare **[!UICONTROL Adobe Commerce Optimizer]** per visualizzare la pagina di configurazione con le istruzioni.

   ![[!DNL Commerce Optimizer] pagina di configurazione](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Dalla riga di comando, [utilizzare SSH](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/develop/secure-connections) per connettersi all&#39;ambiente di staging [!DNL Adobe Commerce].

1. Per configurare l&#39;integrazione, eseguire il seguente comando CLI [!DNL Adobe Commerce], sostituendo i valori segnaposto con i valori per il progetto [!DNL Commerce Optimizer]:

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Verificare la connessione tornando all&#39;amministratore di Commerce e selezionando l&#39;opzione [!UICONTROL Adobe Commerce Optimizer].

   Quando selezioni l&#39;opzione, viene aperta l&#39;interfaccia utente [!DNL Commerce Optimizer] in una nuova scheda.
