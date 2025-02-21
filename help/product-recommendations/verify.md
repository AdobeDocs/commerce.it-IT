---
title: Verifica raccolta eventi
description: Scopri come verificare che i dati comportamentali vengano inviati ad Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Verifica raccolta eventi

Dopo aver [installato e configurato](install-configure.md) il modulo `magento/product-recommendations`, puoi verificare che i dati comportamentali vengano inviati ad Adobe Commerce. Puoi utilizzare gli strumenti per sviluppatori disponibili in Chrome o installare l’estensione Snowplow Chrome. Se hai bisogno di ulteriore assistenza, consulta [Risoluzione dei problemi [!DNL Product Recommendations] modulo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html) nella Knowledge Base di supporto.

## Verifica tramite gli strumenti per sviluppatori in Chrome

Per assicurarsi che il file JS dell&#39;agente di raccolta eventi venga caricato su tutte le pagine del sito:

1. In Chrome, scegli **Personalizza e controlla Google Chrome**, quindi seleziona **Altri strumenti** > **Strumenti per sviluppatori**.
1. Scegli la scheda **Rete**, quindi seleziona il tipo **JS**.
1. Filtra per `ds.`
1. Ricarica la pagina.
1. Dovresti visualizzare `ds.js` o `ds.min.js` nella colonna **Name**.

![JS raccolta eventi](assets/filter-ds.png)
_JS agente di raccolta eventi_

Per garantire che gli eventi vengano attivati sulle pagine del sito (home, prodotto, pagamento e così via):

1. Assicurati di disabilitare i blocchi degli annunci sul browser e accettare i cookie sul sito.
1. In Chrome, scegli **Personalizza e controlla Google Chrome** (i tre punti verticali nell&#39;angolo superiore destro del browser), quindi seleziona **Altri strumenti** > **Strumenti per sviluppatori**.
1. Scegliere la scheda **Rete** e filtrare per `tp2`.
1. Ricarica la pagina.
1. Dovresti vedere le chiamate in `tp2` nella colonna **Name**.

![Eventi di attivazione](assets/filter-tp2.png)
_Verifica che gli eventi vengano attivati_

## Verifica tramite l’estensione Snowplow Chrome

Installa l&#39;estensione [Snowplow Analytics Debugger per Chrome](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm). Questa estensione visualizza gli eventi raccolti e inviati ad Adobe Commerce.

1. Assicurati di disabilitare i blocchi degli annunci sul browser e accettare i cookie sul sito.

1. In Chrome, scegli **Personalizza e controlla Google Chrome** (i tre punti verticali nell&#39;angolo superiore destro del browser), quindi seleziona **Altri strumenti** > **Strumenti per sviluppatori**.

1. Scegliere la scheda **Debugger di Analytics**.

1. Nella colonna **Evento** selezionare **Evento strutturato**.

1. Scorri verso il basso fino a visualizzare **Dati contestuali _n_**. Cerca l&#39;istanza storefront nello **Schema**.

1. Verificare che l&#39;ID dello spazio dati [SaaS](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html) sia impostato correttamente.

![Filtro spazzaneve](assets/snowplow-filter.png)
_Filtro Snowplow_

>[!NOTE]
>
> Un valore di `Data validity : NOT FOUND` nel debugger indica uno schema interno. Il plug-in Snowplow Chrome non può convalidare gli eventi con uno schema interno. Questo non ha alcun impatto sulle funzionalità effettive.

## Verificare che gli eventi si attivino correttamente

Per verificare che gli eventi utilizzati per le metriche si attivino correttamente, cerca gli eventi `impression-render`, `view` e `rec-click` nel debugger di Snowplow Analytics. Visualizza l&#39;[elenco completo degli eventi](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html).

>[!NOTE]
>
> Se è abilitata la modalità di restrizione dei cookie [](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html), Adobe Commerce non raccoglie dati comportamentali fino al consenso dell&#39;acquirente. Se la Modalità di restrizione cookie è disabilitata, i dati comportamentali vengono raccolti per impostazione predefinita.
