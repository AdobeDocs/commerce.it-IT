---
title: Integrare Adobe Experience Platform Mobile SDK con Commerce
description: Scopri come utilizzare Adobe Experience Platform Mobile SDK con la tua vetrina Commerce headless o personalizzata.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Integrare Adobe Experience Platform Mobile SDK con Commerce

>[!IMPORTANT]
>
>Adobe Experience Platform Mobile SDK per iOS supporta iOS 11 o versione successiva.

L&#39;integrazione di [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) con l&#39;app mobile Commerce consente ai commercianti di inviare [dati evento](events.md) Commerce al server Edge di Experience Platform.

Quando i dati dell’evento Commerce sono disponibili al perimetro, sono accessibili ad altre applicazioni Adobe Experience Cloud. Ad esempio, puoi utilizzare i dati per creare tipi di pubblico in Real-Time CDP e poi [utilizzarli](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=it) per personalizzare la tua app mobile Commerce.

## Configurazione

Per iniziare a utilizzare Adobe Experience Platform Mobile SDK con Commerce, installa e configura SDK in Experience Platform. Quindi, finalizza la configurazione in Commerce.

### Experience Platform

1. Scopri le funzionalità delle app mobili consultando l&#39;esercitazione [Adobe Experience Cloud nelle app per dispositivi mobili](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=it).

1. [Installa e configura](https://developer.adobe.com/client-sdks/documentation/getting-started/) SDK in Experience Platform.

   >[!NOTE]
   >
   >Lo schema creato e configurato in Experience Platform è lo stesso utilizzato nel codice dell&#39;applicazione nell&#39;app mobile Commerce.

### Commerce

Dopo aver completato la configurazione di SDK per Experience Platform, aggiungi la configurazione di SDK a Commerce.

1. Per inviare i dati dell’evento Commerce a Experience Platform tramite SDK, devi fornire uno schema XDM nel codice dell’applicazione. Questo schema deve corrispondere allo schema [configurato](https://developer.adobe.com/client-sdks/home/getting-started/set-up-schemas-and-datasets/) per SDK in Experience Platform.

   Nell&#39;esempio seguente viene illustrato come tenere traccia dell&#39;evento `web.webpagedetails.pageViews` e impostare `identityMap` utilizzando il campo e-mail.

   ```swift
   let stateName = "luma: content: ios: us: en: home"
   var xdmData: [String: Any] = [
       "eventType": "web.webpagedetails.pageViews",
       "web": [
           "webPageDetails": [
               "pageViews": [
                   "value": 1
               ],
               "name": "Home page"
           ]
       ]
   ]
   
   let experienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: experienceEvent)
   
   // Adobe Experience Platform - Update Identity
   
   let emailLabel = "mobileuser@example.com"
   
   let identityMap: IdentityMap = IdentityMap()
   identityMap.add(item: IdentityItem(id: emailLabel), withNamespace: "Email")
   Identity.updateIdentities(with: identityMap)
   ```

1. Connettersi all’ambiente Commerce Cloud.

   Nelle impostazioni di build del progetto, aggiungi l’URL all’endpoint Commerce GraphQL. Ad esempio:

   - Debug: http://_debug_.commerce.cloud/graphql/
   - Versione: http://_release_.commerce.cloud/graphql/

1. Per recuperare i dati dagli endpoint Commerce GraphQL, genera innanzitutto i file e le directory necessari nel progetto utilizzando il [generatore di codice Apollo](https://www.apollographql.com/docs/ios/).

   1. Dalla directory del progetto, [installa](https://www.apollographql.com/docs/ios/get-started#1-install-the-apollo-frameworks) Apollo iOS.

   1. [Inizializzare](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#initialize) l&#39;interfaccia CLI del Codegen Apollo.

      Verrà creato un file `apollo-codegen-configuration.json`.

   1. Generare i file e le directory GraphQL necessari nel progetto sostituendo il contenuto del file `apollo-codegen-configuration.json` con quanto segue:

      ```json
      {
      "schemaName" : "MagentoAPI",
      "input" : {
          "operationSearchPaths" : [
          "**/*.graphql"
          ],
          "schemaSearchPaths" : [
          "**/*.graphqls"
          ]
      },
      "output" : {
          "testMocks" : {
          "none" : {
          }
          },
          "schemaTypes" : {
          "path" : "../MagentoAPI",
          "moduleType" : {
              "swiftPackageManager" : {
              }
          }
          },
          "operations" : {
          "inSchemaModule" : {
          }
          }
      },
      "schemaDownloadConfiguration": {
          "downloadMethod": {
              "introspection": {
                  "endpointURL": "http://magento24.com/graphql/",
                  "httpMethod": {
                      "POST": {}
                  },
                  "includeDeprecatedInputValues": false,
                  "outputFormat": "SDL"
              }
          },
          "downloadTimeout": 60,
          "headers": [],
          "outputPath": "magento.graphqls"
      }
      }
      ```

   1. [Recupera](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#fetch-schema) lo schema Commerce GraphQL.

      Verificare che il percorso sia del file `./apollo-codegen-config.json`, che contiene il riferimento allo schema Commerce GraphQL.

   1. [Generare](https://www.apollographql.com/docs/ios/code-generation/codegen-cli/#generate) il codice sorgente.

      Verificare che il percorso sia del file `./apollo-codegen-config.json`, che contiene le informazioni di configurazione per generare i file e le directory necessari.

   1. Nella cartella **GraphQLGenerated** appena creata, aggiungi o modifica i tipi di GraphQL. Ad esempio, è possibile aggiungere un tipo `DynamicBlocks.graphql` con il seguente contenuto:

      ```graphql
      query dynamicBlocks($input: DynamicBlocksFilterInput){
          dynamicBlocks(input: $input)
          {
              items {
                  content {
                      html
                  }
              }
          }
      }
      ```

   Ora hai integrato Adobe Experience Platform Mobile SDK con la tua app mobile Commerce. I dati dell’evento fluiscono dall’app verso il server Edge di Experience Platform.

## Come distinguere gli eventi Commerce generati dalle applicazioni mobili

Tutti i [eventi](events.md) contengono un campo denominato `channel`. Il campo `channel` contiene `channel._id` e `channel._type` che per una vetrina Luma hanno valori di spazio dei nomi rispettivamente di `"https://ns.adobe.com/xdm/channels/web"` e `"https://ns.adobe.com/xdm/channel-types/web"`. Per una vetrina mobile, tuttavia, i valori dello spazio dei nomi sono rispettivamente `"https://ns.adobe.com/xdm/channels/mobile-app"` e `"https://ns.adobe.com/xdm/channel-types/mobile"`.

## Passaggi successivi

Per informazioni su come recuperare i tipi di pubblico di Real-Time CDP dall&#39;app Commerce per dispositivi mobili per informare le regole di prezzo del carrello, i blocchi dinamici e le regole di prodotto correlate, consulta [Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=it#retrieve-audiences-using-the-adobe-experience-platform-mobile-sdk).
