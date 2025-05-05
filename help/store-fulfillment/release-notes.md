---
title: Note sulla versione [!DNL Store Fulfillment by Walmart Commerce Technologies]
description: Consulta le note sulla versione per informazioni su tutte le  [!DNL Store Fulfillment by Walmart Commerce Technologies]  versioni.
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Note sulla versione

Queste note sulla versione descrivono la versione iniziale di [!DNL Store Fulfillment Services by Walmart Commerce Technologies] e includono:

![Nuove](../assets/new.svg) nuove funzionalità
![Problema risolto](../assets/fix.svg) correzioni e miglioramenti
![Problema noto](../assets/bug.svg) Problemi noti

Per informazioni sulle pianificazioni e sul supporto, consulta le [prossime versioni](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html).

Consulta [Disponibilità del prodotto](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html) per sapere quali versioni di Adobe Commerce supportano questa estensione.

## v1.5.0

*3 agosto 2023*

[!BADGE Supportato]{type=Informative tooltip="Supportato"}[Adobe Commerce da 2.4.4 a 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html), incluse le versioni delle patch di sicurezza 2.4.6-p1, 2.4.5-p3 e 2.4.4-p4

Questa versione contiene i seguenti aggiornamenti:

![Nuovo](../assets/fix.svg) Aggiornamento dell&#39;estensione per supportare [Versioni delle patch di sicurezza di Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html) 2.4.6-p1, 2.4.5-p3 e 2.4.4-p4.

![New](../assets/new.svg)<!-- WMTP-918 --> ha aggiunto il supporto per l&#39;opzione di configurazione [Invio asincrono](sales-emails.md) per e-mail vendite. I commercianti che eseguono l’aggiornamento alla versione 1.5.0 possono inviare le e-mail immediatamente (impostazione predefinita) o in modo asincrono.

![Nuovo](../assets/new.svg)<!-- WMTP-916--> È stata aggiornata la configurazione [Origini](merchant-store-configuration.md) per supportare i formati dei numeri di telefono internazionali.

![Nuovo](../assets/new.svg) aggiunta della logica per impedire che gli importi di rimborso superino l&#39;importo rimanente o fatturato.

![New](../assets/new.svg)<!-- WMTP-882 --> ha sostituito l&#39;oggetto `google.map.LatLng` con valori letterali JSON per supportare la compatibilità con le versioni precedenti di [!DNL Google Maps].

![Problema risolto](../assets/fix.svg)<!-- WMTP- --> Aggiornato lo script che crea gli attributi di prodotto `[!DNL Available for Store Pickup]` e `[!DNL Available for Home Delivery]` per evitare conflitti di categoria degli attributi.

![È stato risolto un problema](../assets/fix.svg)<!-- WMTP-915 --> che causava un ciclo infinito durante il caricamento e il salvataggio di alcune entità.

![È stato risolto un problema](../assets/fix.svg)<!-- WMTP-921 --> che impediva l&#39;attivazione della convalida delle offerte [!DNL Ship to Store] quando un elemento veniva aggiunto al carrello da una pagina di dettagli prodotto (PDP).

![È stato risolto un problema](../assets/fix.svg)<!-- WMTP- 932 --> che consentiva ai clienti di selezionare il metodo di consegna a domicilio per gli elementi non idonei per la consegna a domicilio.

![Problema risolto](../assets/fix.svg) Aggiornamenti all&#39;installazione:

- &#x200B;<!-- WMTP-880--> È stato risolto un problema che causava la restituzione di un codice del sito Web errato durante l&#39;installazione dell&#39;estensione [!DNL Store Fulfillment].

- &#x200B;<!-- WMTP-878--> È stato risolto un problema relativo ai valori SKU integer che richiedeva il cast del tipo di dati al tipo stringa durante l’installazione.

![È stato risolto un problema](../assets/fix.svg)<!-- WMTP-915--> a causa del quale si verificava un errore dovuto a un codice di errore di archiviazione mancante.

![È stato corretto un problema](../assets/fix.svg)<!-- WMTP-932 --> È stato corretto un bug relativo al rifiuto parziale durante le operazioni di dispensazione.

![Nuovo](../assets/new.svg)<!-- WMTP-953 --> Aggiornamento dell&#39;endpoint API Cancel per utilizzare il parametro di stato come oggetto facoltativo.

![Nuovo](../assets/new.svg)<!-- WMTP-960 --> Sono stati migliorati i dettagli di registrazione per l&#39;endpoint API Dispense.

## v1.4.0

*13 aprile 2023*

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

![Nuovo](../assets/fix.svg) [!DNL Store Fulfillment] è ora [compatibile con [!DNL Adobe Commerce] 2.4.4 a 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html).


## v1.3.0

*27 febbraio 2023*

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

Questa versione contiene i seguenti aggiornamenti:

![Nuovo](../assets/fix.svg)<!-- WMTP-795 --> è stata aggiunta la possibilità di disabilitare la soluzione Store Fulfillment per un sito specifico modificando l&#39;ambito predefinito per l&#39;impostazione Configurazione di sistema da sito Web a globale.

## v1.2.0

*27 settembre 2022*

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

Questa versione contiene i seguenti aggiornamenti:

![Nuovo](../assets/fix.svg) [!DNL Store Fulfillment] è ora [compatibile con [!DNL Adobe Commerce] 2.4.4 a 2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html).


## v1.1.0

*15 luglio 2022*

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

Stabilità: disponibilità generale

![Nuovo](../assets/fix.svg)<!-- WMTP-731 --> ha semplificato la [configurazione dell&#39;esperienza di archiviazione](check-in-experience-setup.md) per l&#39;app Store Assist aggiungendo le selezioni predefinite per la marca dell&#39;auto e il modello. Nella versione precedente, i commercianti dovevano configurare manualmente le selezioni di marca e modello dell&#39;auto.

## v1.0.0

*4 marzo 2022*

[!BADGE Supportato]{type=Informative tooltip="Supportato"}

Stabilità: disponibilità generale

## App Store Assist

Per informazioni sulle nuove versioni dell&#39;app Store Assist, vedi le informazioni sull&#39;app in [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} o [Google Play store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.
