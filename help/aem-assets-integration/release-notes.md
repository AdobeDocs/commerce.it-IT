---
title: Note sulla versione dell’integrazione AEM Assets
description: Consulta le note sulla versione per informazioni su tutte le versioni di Integrazione di AEM Assets.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: a5cb5dc4e2a5bd73bb89961591e361e050319c74
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Note sulla versione dell’integrazione AEM Assets

Queste note sulla versione descrivono la versione iniziale dell’integrazione di AEM Assets e includono:

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

## v1.2.4

_17 ottobre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-1155 -->. È stata migliorata la stabilità complessiva degli attributi personalizzati. Gli attributi personalizzati ora vengono aggiornati correttamente quando si utilizzano API asincrone.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-1074 --> Ora, la [sincronizzazione prodotto-risorsa](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank} non ha esito negativo quando viene definito un URL di collegamento di base.

## v1.2.3

_2 ottobre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto un problema](../assets/fix.svg)<!-- Issue ACAP-1135 --> che impediva l&#39;aggiornamento degli attributi del prodotto. Gli attributi del prodotto ora vengono aggiornati come previsto e viene restituito un errore appropriato invece di una risposta 200 quando gli aggiornamenti non riescono.

## v1.2.2

_18 settembre 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-1110 -->. È stata migliorata la stabilità generale dell&#39;immagine per il mini carrello, il carrello e le pagine di pagamento. Le immagini su queste pagine ora vengono caricate correttamente.

## v1.2.0

_7 agosto 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-1018 --> Ora i commercianti possono scegliere l&#39;origine per le risorse immagine e multimediali selezionando un [Proprietario visualizzazione](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} durante la configurazione dell&#39;integrazione Assets dall&#39;amministratore.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-1078 --> Aggiornamento degli [endpoint di corrispondenza automatica personalizzati](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} con un nuovo attributo `asset_matches`. Questa modifica ti consente di implementare una tua logica di corrispondenza per restituire tutte le risorse associate a un `productSku` specifico.

## v1.1.2

_11 giugno 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-1041 --> Aggiunto supporto per Adobe Commerce 2.4.8 e PHP 8.4.

## v1.1.0

_23 aprile 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-955 --> Ora è possibile utilizzare un [URL di dominio personalizzato](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) al posto dell&#39;URL di consegna di AEM. Se un commerciante imposta un **nome di dominio personalizzato** nel dashboard di AEM, è necessario aggiungere questo **URL di dominio personalizzato** in Commerce.

![È stato risolto il problema](../assets/fix.svg)<!-- Issue ACAP-987 -->. Sono stati migliorati i registri generali per i processi di sincronizzazione AEM Assets.

## v1.0.22

_12 marzo 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo problema](../assets/new.svg)<!-- Issue ACAP-xx --> Ora, il [ID client IMS del selettore Assets](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization) è richiesto dal selettore Assets per abilitare la mappatura delle immagini AEM Assets con le categorie di prodotto e il contenuto generato da Page Builder.

## v1.0.20

_11 febbraio 2025_

[!BADGE Supportato]{type=Informative tooltip="Supportato"} Adobe Commerce versione 2.4.5 e successive.

![Nuovo](../assets/new.svg)<!-- Issue ACAP-xx --> rilascio di disponibilità generale.
