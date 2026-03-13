---
title: Note sulla versione dell’integrazione AEM Assets
description: Consulta le note sulla versione per informazioni su tutte le versioni di Integrazione di AEM Assets.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 85579e3f2f8fc49f46f9201f31908602ee5d3259
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Note sulla versione dell’integrazione AEM Assets

Queste note sulla versione descrivono tutte le versioni per l’integrazione AEM Assets e includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Problema risolto](../assets/fix.svg) correzioni e miglioramenti
![Problema noto](../assets/bug.svg) Problemi noti

Per le modifiche e le correzioni delle funzionalità rilasciate al di fuori della normale versione di rilascio delle funzionalità, controlla le sezioni _Aggiornamenti dei servizi ospitati_.

Ulteriori informazioni sulle prossime versioni, sul supporto del prodotto e sulle versioni di Adobe Commerce che supportano l&#39;estensione per l&#39;integrazione di AEM Assets. Consulta gli argomenti [Pianificazione delle versioni](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) e [Disponibilità del prodotto](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) di Adobe Commerce.

## Aggiornamenti dei servizi in hosting

Queste note sulla versione descrivono le modifiche e le correzioni apportate alle funzioni e sono state rilasciate al di fuori delle normali versioni del servizio ospitato.

+++Aggiornamenti dei servizi in hosting

_11 settembre 2025_

![Nuovo problema](../assets/new.svg) Aggiornamento degli [endpoint di corrispondenza automatica personalizzati](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} con un nuovo attributo `asset_matches`.

_11 febbraio 2025_

![Nuovo problema](../assets/new.svg) Ora gli esercenti possono sincronizzare le immagini per prodotti e categorie.

+++

## v1.3.4

_March 11, 2026_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![New issue](../assets/new.svg)<!-- Issue PAY-1041 --> Added support for Adobe Commerce 2.4.9-beta1 and PHP 8.5.

![New issue](../assets/new.svg)<!-- Issue ACCS-169 --> The **[!UICONTROL Program ID]**, **[!UICONTROL Environment ID]**, and [**[!UICONTROL Domain mapping]**](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/domain-mappings/add-domain-mapping){target=_blank} fields now auto-populate as dropdowns based on the [user&#39;s IMS session](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#ims-and-user-permissions){target=_blank}.

## v1.2.14

_13 febbraio 2026_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACCS-171 --> di [corrispondenza personalizzata](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match) a causa del quale i dati dell&#39;area di lavoro non salvati venivano visualizzati nel menu a discesa delle azioni di runtime dopo il ricaricamento della pagina.

## v1.2.13

_10 febbraio 2026_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACCS-171 --> Aggiunto un campo **[!UICONTROL Adobe I/O Workspace Configuration]** che semplifica la configurazione di [corrispondenza personalizzata](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank}. Gli esercenti ora possono caricare il file App Builder `workspace.json` per compilare automaticamente le credenziali OAuth e gli endpoint di azione di runtime.

## v1.2.12

_29 gennaio 2026_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto un problema](../assets/fix.svg)<!-- Issue ACAP-1206 --> che impediva la rimozione di `no_selection` valori obsoleti negli attributi personalizzati per i ruoli delle risorse durante la sincronizzazione delle risorse e impediva la corretta visualizzazione di alcune immagini in Edge Delivery Services.

## v1.2.11

_15 gennaio 2026_

[!BADGE Versione supportata]{type=Informative tooltip="Supportato"} di Adobe Commerce 2.4.5 e successive.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-1180 -->. La pagina di modifica del prodotto è stata migliorata nascondendo le dimensioni e le dimensioni dei file per le risorse AEM, in quanto sono ottimizzate dinamicamente da CDN. Ora le pagine vengono renderizzate correttamente quando è attivata l’integrazione AEM Assets.

## v1.2.10

_12 gennaio 2026_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto un problema](../assets/fix.svg)<!-- Issue ACAP-1178 --> che impediva l&#39;aggiornamento degli attributi personalizzati del prodotto tramite API REST se il prodotto conteneva un&#39;immagine e l&#39;integrazione AEM Assets era abilitata. Ora gli attributi personalizzati del prodotto vengono aggiornati correttamente tramite API REST.

![È stato risolto un problema](../assets/fix.svg)<!-- Issue ACAP-1172 --> a causa del quale le immagini nascoste dei prodotti non venivano visualizzate come nascoste nell&#39;interfaccia utente di amministrazione nella pagina di modifica del prodotto. Ora lo stato di visibilità delle immagini viene visualizzato correttamente.

![È stato risolto un problema](../assets/fix.svg)<!-- Issue ACAP-1170 --> che impediva la sincronizzazione delle immagini di prodotto da AEM Assets con Adobe Commerce a causa di un errore di deserializzazione. Ora tutti gli attributi immagine (`image`, `small_image` e `swatch_image`) vengono sincronizzati correttamente.

## v1.2.7

_6 novembre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto un problema](../assets/fix.svg)<!-- Issue ACAP-1169 --> a causa del quale le immagini delle miniature dei prodotti venivano visualizzate in modo incoerente dopo l&#39;abilitazione dell&#39;integrazione di AEM Assets nelle pagine **Mini carrello**, **Carrello** e **Pagine estratte**. Adesso, le immagini del prodotto vengono riprodotte in modo coerente su tutte le pagine, anche dopo l’aggiornamento della pagina.

## v1.2.6

_24 ottobre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto un problema](../assets/fix.svg)<!-- Issue ACAP-1163 --> a causa del quale le richieste consecutive di aggiornamento in blocco dei prodotti potevano lasciare il flag di tracciamento dello stato bloccato, impedendo la corretta elaborazione degli aggiornamenti successivi. Ora lo stato viene reimpostato anche in caso di errore.

## v1.2.5

_22 ottobre 2025_

[!BADGE Versione supportata]{type=Informative tooltip="Supportato"} di Adobe Commerce 2.4.5 e successive.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1161 --> Fixed an issue where updating the position of an existing image mapping in the Adobe Commerce Admin resulted in a PHP type error.

## v1.2.4

_17 ottobre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-1155 -->. È stata migliorata la stabilità complessiva degli attributi personalizzati. Gli attributi personalizzati ora vengono aggiornati correttamente quando si utilizzano API asincrone.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-1074 --> Ora, la [sincronizzazione prodotto-risorsa](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank} non ha esito negativo quando viene definito un URL di collegamento di base.

## v1.2.3

_2 ottobre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Fixed issue](../assets/fix.svg)<!-- Issue ACAP-1135 --> Fixed an issue with updating product attributes. Gli attributi del prodotto ora vengono aggiornati come previsto e viene restituito un errore appropriato invece di una risposta 200 quando gli aggiornamenti non riescono.

## v1.2.2

_18 settembre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-1110 -->. È stata migliorata la stabilità generale dell&#39;immagine per il mini carrello, il carrello e le pagine di pagamento. Le immagini in queste pagine ora vengono caricate correttamente.

## v1.2.0

_7 agosto 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![New issue](../assets/new.svg)<!-- Issue ACAP-1018 --> Now, merchants can choose the source for image and media assets by selecting a [Visualization Owner](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} when configuring the Assets integration from the Admin.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-1078 --> Aggiornamento degli [endpoint di corrispondenza automatica personalizzati](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} con un nuovo attributo `asset_matches`. Questa modifica ti consente di implementare una tua logica di corrispondenza per restituire tutte le risorse associate a un `productSku` specifico.

## v1.1.2

_11 giugno 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-1041 --> Aggiunto supporto per Adobe Commerce 2.4.8 e PHP 8.4.

## v1.1.0

_23 aprile 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-955 --> Ora è possibile utilizzare un [URL di dominio personalizzato](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) al posto dell&#39;URL di consegna di AEM. Se un commerciante imposta un **nome di dominio personalizzato** nel dashboard di AEM, è necessario aggiungere questo **URL di dominio personalizzato** in Commerce.

![Problema risolto](../assets/fix.svg)<!-- Issue ACAP-987 --> Registri complessivi migliorati per i processi di sincronizzazione di AEM Assets.

## v1.0.22

_12 marzo 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-xx --> Ora, il [ID client IMS del selettore Assets](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization) è richiesto dal selettore Assets per abilitare la mappatura delle immagini AEM Assets con le categorie di prodotto e il contenuto generato da Page Builder.

## v1.0.20

_11 febbraio 2025_

[!BADGE Versione supportata]{type=Informative tooltip="Supportato"} di Adobe Commerce 2.4.5 e successive.

![Nuova](../assets/new.svg)<!-- Issue ACAP-xx --> versione di disponibilità generale.
