---
title: Note sulla versione
description: Informazioni aggiornate sulla versione dell'estensione  [!DNL Data Connection]  di Adobe Commerce.
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 90fcaa2cdd7c869ceddaeea7525cac00a41d94c5
workflow-type: tm+mt
source-wordcount: '1257'
ht-degree: 1%

---

# Note sulla versione

>[!IMPORTANT]
>
>Il connettore Experience Platform è stato rinominato in [!DNL Data Connection].

Queste note sulla versione contengono aggiornamenti all&#39;estensione [!DNL Data Connection] e includono:

![Nuovo](../assets/new.svg) - Nuove funzionalità
![Correzione](../assets/fix.svg) - Correzioni e miglioramenti
![Bug](../assets/bug.svg) - Problemi noti

Per le modifiche e le correzioni delle funzionalità relative alle estensioni utilizzate dall&#39;estensione [!DNL Data Connection], vedere **Aggiornamenti dei servizi supportati**.

Per informazioni sulle pianificazioni e sul supporto, consulta le [prossime versioni](https://experienceleague.adobe.com/it/docs/commerce-operations/release/planning/schedule).

Consulta la documentazione per gli sviluppatori per [scoprire quali versioni di Commerce supportano questo modulo](https://experienceleague.adobe.com/it/docs/commerce-operations/release/product-availability).

## Aggiornamenti dei servizi supportati

Queste note sulla versione descrivono modifiche e correzioni di funzionalità relative alle estensioni utilizzate dall&#39;estensione [!DNL Data Connection].

+++Aggiornamenti dei servizi supportati

_7 agosto 2025_

![Nuovo](../assets/new.svg) - Con la versione 3.3.0, ora puoi aggiungere [attributi personalizzati ai profili](custom-identities.md).

_2 agosto 2024_

![Correzione](../assets/fix.svg) - È stato corretto l&#39;importo totale dei pagamenti quando il totale dell&#39;ordine è configurato per includere le imposte.
![Nuovo](../assets/new.svg) - Aggiunto un campo `taxAmount` per ordinare eventi di acquisto.
![Nuovo](../assets/new.svg) - Aggiunta la possibilità di aggiungere dati personalizzati agli eventi. Vedi quanto segue per un [esempio](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md).

_24 gennaio 2024_

![Nuovo](../assets/new.svg) - Aggiornamento dell&#39;estensione `data-services-b2b` per includere un nuovo evento richiesta di acquisto denominato `deleteRequisitionList` per i commercianti B2B.

_16 novembre 2023_

![Correzione](../assets/fix.svg) - È stato risolto un problema che causava la visualizzazione errata di un messaggio di errore quando si effettuava un ordine con più indirizzi di spedizione.
![Correzione](../assets/fix.svg) - È stato risolto un problema nell&#39;evento `productPageView` a causa del quale il campo dell&#39;evento `productListItems.priceTotal` non convertiva il prezzo dopo aver cambiato la valuta nella visualizzazione dello store.
![Correzione](../assets/fix.svg) - È stato risolto un problema nel campo evento `productListItems` a causa del quale il codice valuta non veniva aggiornato quando il commerciante cambiava la visualizzazione dell&#39;archivio.

_10 ottobre 2023_

![Nuovo](../assets/new.svg) - Aggiunti nuovi eventi di stato ordine: [Ordine fatturato](events-backoffice.md#orderinvoiced), [Restituzione articolo ordine avviata](events-backoffice.md#orderitemsreturninitiated) e [Restituzione articolo ordine completata](events-backoffice.md#orderitemreturncompleted).
![Correzione](../assets/fix.svg) - È stato risolto un problema a causa del quale le modifiche alla configurazione della valuta non venivano applicate negli eventi dopo l&#39;aggiornamento della cache.
![Correzione](../assets/fix.svg): è stato corretto un errore che si verificava quando non veniva visualizzato il messaggio di conferma dell&#39;ordine se era abilitato il posizionamento asincrono dell&#39;ordine.
![Nuovo](../assets/new.svg) - Sono stati aggiunti dati all&#39;evento `addToRequisitionList` per i prodotti semplici nella pagina di visualizzazione Categoria.
![Correzione](../assets/fix.svg) - È stato risolto un problema nei dati `selectedOptions` nell&#39;evento `addToRequisitionList` quando i prodotti vengono aggiunti dalla pagina di conferma dell&#39;ordine.
![Nuovo](../assets/new.svg) - Aggiunti dati prodotto all&#39;evento `addToRequisitionList` quando i prodotti vengono aggiunti all&#39;elenco richieste dalla pagina di visualizzazione Categoria.
![Nuovo](../assets/new.svg) - Aggiunto l&#39;evento `addToRequisitionList` quando i prodotti configurabili vengono aggiunti all&#39;elenco richieste dalla pagina di visualizzazione Prodotto.
![Nuovo](../assets/new.svg) - Sono stati aggiunti `addToRequisitionList` e `removeFromRequisitionList` eventi quando la quantità di prodotto viene aumentata e/o diminuita da un elenco di richieste di acquisto.

_10 giugno 2023_

![Correzione](../assets/fix.svg) - È stato risolto un problema che impediva a `orderId` di passare nel contesto a causa di prefissi nell&#39;identificatore dell&#39;ordine di Commerce.
![Correzione](../assets/fix.svg) - Configurazioni criteri di sicurezza dei contenuti aggiornate.

_30 marzo 2023_

![Nuovo](../assets/new.svg) - Aggiunta di un&#39;estensione denominata `data-services-b2b` che include [eventi elenco richieste](events.md#b2b-events) per i commercianti B2B.
![Nuovo](../assets/new.svg) - Aggiunta del campo `uniqueIdentifier` a [eventi di ricerca](events.md#search-events). Questo nuovo campo consente ai commercianti di fare riferimento incrociato tra le richieste di ricerca e le risposte di ricerca.

_12 ottobre 2022_

![Nuovo](../assets/new.svg) - Sono stati aggiunti due [eventi storefront](events.md), `openCart` e `removeFromCart` a Adobe Commerce Storefront Events SDK and Collector.
![Nuovo](../assets/new.svg) - Aggiunto supporto per una [vetrina AEM](overview.md#aem-support).

+++

## 3,3,0

_21 marzo 2025_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) aggiunto supporto PHP 8.4.

## 3.2.1.

_17 gennaio 2025_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) - Aggiunta dell&#39;estensione [compatibile con HIPAA](hipaa-readiness.md) a [!DNL Data Connection] per consentire ai commercianti di condividere [!DNL Commerce] dati di eventi di back office con Experience Platform e mantenere la conformità HIPAA.
![Correzione](../assets/fix.svg) - È stato risolto un problema a causa del quale l&#39;estensione [!DNL Data Connection] sovrascriveva i dati di `eventForwarding` e impostava il flag `HIPAA` per tutti i clienti. Ora l’estensione imposta solo il flag per i clienti HIPAA.

## 3.2.0

_7 ottobre 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) - Aggiunta la possibilità di creare [attributi di ordine personalizzati](custom-attributes.md) per i dati di back office.
![Nuovo](../assets/new.svg) - Aggiunta nuova tabella [Attributi ordine personalizzati](connect-data.md#data-customization) per visualizzare eventuali attributi personalizzati configurati in [!DNL Commerce] e inviati ad Experience Platform.
![Nuovo](../assets/new.svg) - Aggiunta la possibilità di [raccogliere e inviare record del profilo](connect-data.md#send-customer-profile-data) e dati ad Experience Platform.

## 3.2.0-beta3

_27 agosto 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) - Se partecipi alla versione beta, assicurati che il tuo file `composer.json` abbia le seguenti caratteristiche a livello di radice: ` "minimum-stability": "beta"`. Aggiungi anche `composer require "magento/customers-connector: ^1.2.0"` per inviare i profili cliente dall&#39;istanza Commerce a SaaS.
![Nuovo](../assets/new.svg) - Questa versione contiene le patch rilasciate nelle versioni 3.1.1, 3.1.2, 3.1.3 e 3.1.4.

## 3.1.4.

_9 agosto 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) - Il metapackage `experience-platform-connector` è stato aggiornato per rimuovere altri esportatori e indicizzatori di dati inutilizzati.

## 3.1.3.

_22 luglio 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) - Il metapackage `experience-platform-connector` è stato aggiornato per rimuovere gli esportatori e gli indicizzatori di dati inutilizzati.

## 3.1.2.

_5 giugno 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Correzione](../assets/fix.svg) - È stato risolto un problema che causava l&#39;utilizzo di un formato di data errato durante l&#39;avvio di una [sincronizzazione cronologica](connect-data.md#specify-order-history-date-range).
![Correzione](../assets/fix.svg) - È stato risolto un problema a causa del quale l&#39;evento `startCheckout` non veniva inviato in Adobe Commerce 2.4.7.

## 3.1.1.

_4 aprile 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) - Aggiunta del supporto per PHP 8.3 per tutte le estensioni [!DNL Data Connection].
![Nuovo](../assets/new.svg) - È stato aggiunto un articolo su come [integrare](mobile-sdk-epc.md) Adobe Experience Platform Mobile SDK con Commerce.

## 3.2.0-beta2

_4 marzo 2024_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) - Se partecipi alla versione beta, assicurati che il tuo file `composer.json` abbia le seguenti caratteristiche a livello di radice: ` "minimum-stability": "beta"`. Aggiungi anche `composer require "magento/customers-connector: ^1.2.0"` per inviare i profili cliente dall&#39;istanza Commerce a SaaS.
![Nuovo](../assets/new.svg) - Aggiunta della possibilità di [aggiungere attributi personalizzati](custom-attributes.md).
![Nuovo](../assets/new.svg) - Aggiunta la possibilità di [raccogliere e inviare record del profilo](connect-data.md#send-customer-profile-data) e dati ad Experience Platform.

## 3.1.0.

_16 novembre 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

![Nuovo](../assets/new.svg) - Il connettore Experience Platform è stato rinominato in [!DNL Data Connection].
![Correzione](../assets/fix.svg) - Aggiunta la possibilità di registrare la risposta di errore se Adobe IMS non è in grado di generare il token di accesso.
![Correzione](../assets/fix.svg) - È stato aggiunto un messaggio di notifica se si tenta di sincronizzare gli ordini cronologici ma non sono state specificate le credenziali dell&#39;account.

## 3,0,0

_10 ottobre 2023_

[!BADGE Compatibilità]{type=Informative tooltip="Compatibilità"} Adobe Commerce versioni 2.4.4 e successive

Questa è una versione principale. [Modifica](install.md#update-the-data-connection) il file compositore.json principale del progetto.

![Nuovo](../assets/new.svg) - Disponibilità generale per [inviare dati e stato dell&#39;ordine cronologico](connect-data.md#send-historical-order-data) ad Experience Platform.
![Nuovo](../assets/new.svg) - Aggiunta del supporto per OAuth 2.0 quando [configuri](connect-data.md#connect-commerce-data-to-adobe-experience-platform) l&#39;estensione [!DNL Data Connection].
![Nuovo](../assets/new.svg) - Supporto terminato per Adobe Commerce 2.4.3.

## 2.3.0.

_27 giugno 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Nuovo](../assets/new.svg) - Aggiunta la possibilità di [disattivare l&#39;invio di eventi storefront](connect-data.md#data-collection) ad Experience Platform.
![Correzione](../assets/fix.svg) - Configurazioni criteri di sicurezza dei contenuti aggiornate.
![Correzione](../assets/fix.svg): è stato corretto il supporto per gli eventi di back office nella versione 2.4.7 di Commerce.
![Nuovo](../assets/new.svg) - È stato aggiunto un messaggio di notifica sull&#39;annullamento della validità della cache quando si salvano le modifiche al modulo dell&#39;estensione [!DNL Data Connection].

## 3.0.0-beta1 (solo interno)

_13 giugno 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Nuovo](../assets/new.svg) - (Beta) Aggiunta la possibilità di [inviare dati e stato relativi all&#39;ordine cronologico](connect-data.md#beta-send-historical-order-data) ad Experience Platform.

## 2.2.0.

_30 marzo 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Nuovo](../assets/new.svg) - Le dipendenze `commerce-data-export` e `saas-export` sono state unite all&#39;estensione `experience-platform-connector`. In precedenza, era necessario installare queste dipendenze separatamente. Queste dipendenze, insieme alla configurazione dell&#39;esercente, consentono l&#39;elaborazione lato server di [eventi back office](events-backoffice.md).
![Nuovo](../assets/new.svg) - Aggiunto nuovo evento di back office denominato [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted).

## 2.1.1.

_28 febbraio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Nuovo](../assets/new.svg) - Aggiunta del supporto per PHP 8.2 per tutte le estensioni [!DNL Data Connection].

## 2.1.0.

_17 gennaio 2023_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Nuovo](../assets/new.svg) - Aggiornamento dell&#39;[[!DNL Data Connection] estensione Admin](connect-data.md) per consentire di specificare la propria AEP Web SDK (alloy).
![Correzione](../assets/fix.svg) è stato modificato in utilizzando `identityMap` invece di `personID` durante l&#39;impostazione dell&#39;identità primaria per tutti i dati inviati al server Edge.

## 2.0.1.

_10 novembre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Correzione](../assets/fix.svg) - Ora il contesto Adobe Experience Platform viene impostato solo dopo il caricamento di Storefront Event Collector e Storefront Event SDK.

## 2,0,0

_12 ottobre 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Nuovo](../assets/new.svg) - Aggiunta la possibilità di specificare il proprio AEP Web SDK quando [connette](connect-data.md) l&#39;istanza Adobe Commerce all&#39;Experience Platform.
![Correzione](../assets/fix.svg) - È stato aggiornato il requisito dell&#39;ambito dello stream di dati in modo che gli ID dello stream di dati debbano essere inclusi nell&#39;ambito del sito Web anziché della visualizzazione archivio.

## 1,0,0

_9 agosto 2022_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versioni 2.4.3 e successive

![Nuovo](../assets/new.svg) - Versione di disponibilità generale.
