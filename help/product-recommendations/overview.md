---
title: Cosa sono i consigli di prodotto?
description: Scopri i consigli di prodotto in Adobe Commerce. Scopri le unità vetrina basate sull’intelligenza artificiale, la privacy, i percorsi di amministrazione e vetrina e i principali criteri di conservazione dei dati.
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
TQID: https://experienceleague.adobe.com/kRTCG6D5k17Ah-1Q-XNZq4o48xqIwlpI8vDQJDTEeoU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bbbea26f-9621-49eb-9ab8-e06fb3bbce8cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 738
ht-degree: 0%

---

# Cosa sono [!DNL Product Recommendations]?

[!DNL Product Recommendations] ti aiuta a mostrare consigli di prodotti personalizzati sugli store di Adobe Commerce utilizzando [Adobe AI](https://business.adobe.com/ai.html) e machine learning sul comportamento aggregato degli acquirenti e sul tuo catalogo. Questa panoramica descrive i vincoli del servizio (incluso HIPAA), i dati e la privacy, dove vengono visualizzate le unità per i consigli, i percorsi di implementazione della vetrina, il modo in cui i consigli integrano le relazioni tra i prodotti e la conservazione dei dati nei cataloghi.

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]non è un servizio compatibile con HIPAA.** Non abilitare o utilizzare [!DNL Product Recommendations] in alcuna implementazione di Adobe Commerce che utilizza l&#39;offerta compatibile con HIPAA o elabora in altro modo informazioni sanitarie protette (PHI). [!DNL Product Recommendations] fa parte dei servizi SaaS di Commerce attualmente classificati come non pronti HIPAA.
>
>Per informazioni dettagliate sulle funzionalità di Adobe Commerce pronte per HIPAA e sui servizi che non devono essere utilizzati con PHI, vedere [Preparazione HIPAA in Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) e [Operazioni](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

## Gestione dei dati e privacy

La raccolta dati per [!DNL Product Recommendations] non include informazioni personali identificabili (PII). Tutti gli identificatori utente, come gli ID cookie e gli indirizzi IP, sono rigorosamente anonimi. Per ulteriori informazioni, consulta [Informativa sulla privacy di Adobe](https://www.adobe.com/privacy/policy.html).

Per ulteriori informazioni sulla sincronizzazione dei dati, vedere [Dashboard di gestione dati](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html).

## Dove vengono visualizzati i consigli

I consigli vengono visualizzati nella vetrina come unità con etichette, ad esempio &quot;Hanno visualizzato anche i clienti che hanno visualizzato questo prodotto&quot;. Dall’amministratore di Adobe Commerce puoi creare, gestire e distribuire consigli nelle viste dello store. Se il progetto Commerce utilizza il [Connettore Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce/aco-optimizer-connector/overview), puoi creare, gestire e distribuire consigli tramite [Adobe Commerce Optimizer](../optimizer/overview.md).

## Implementazioni storefront

Scegli la documentazione che corrisponde alla tua vetrina:

- **PWA Studio** — [Documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **Front-end personalizzati (ad esempio, React o Vue.js)** — [Integrare [!DNL Product Recommendations]](headless.md) in una vetrina headless
- **Commerce Edge Delivery Services (EDS)** — [Documentazione Adobe Commerce Storefront per EDS](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)

>[!NOTE]
>
>Le impostazioni headless e personalizzate variano in base allo stack. Questa area di prodotto documenta un percorso PWA Studio e un modello generale di integrazione headless; non copre tutti gli scenari di terze parti o personalizzati.

## Consigli di prodotto e relazioni di prodotto

Date le complessità in continua evoluzione dello shopping online, ciò che funziona meglio per la vetrina è spesso una combinazione di più tecnologie chiave. L&#39;utilizzo di [!DNL Product Recommendations] e [relazioni tra prodotti](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html) offre maggiore flessibilità durante la promozione dei prodotti. Puoi sfruttare [!DNL Product Recommendations] con tecnologia Adobe AI per automatizzare in modo intelligente i consigli su larga scala. Puoi quindi sfruttare le [Regole prodotto correlate](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html) quando devi intervenire manualmente e assicurarti che sia stato fatto un consiglio specifico a un segmento di acquirenti target o quando devono essere raggiunti determinati obiettivi aziendali.

I consigli sui prodotti consentono di:

- Scegli tra nove tipi di consigli intelligenti distinti in base alle seguenti aree: basati su acquirente, basati su articolo, basati sulla popolarità, basati sulle tendenze e sulla similarità
- Utilizza i dati comportamentali per personalizzare i consigli nel percorso di vetrina dell’acquirente
- Misura le metriche chiave rilevanti per ogni consiglio, in modo da comprendere l’impatto dei consigli

## Demo sui consigli di prodotto

Guarda questo video per saperne di più su [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## Criteri di conservazione dei dati del catalogo

Il servizio [!DNL Product Recommendations] dipende dai dati del catalogo che rimangono sincronizzati con il tuo ambiente Adobe Commerce. I cataloghi o gli ambienti inattivi che interrompono l&#39;esecuzione di query sui dati possono entrare in modalità di sospensione, che influisce sui risultati restituiti dal servizio fino alla riattivazione.

Se non si invia una query per i dati del catalogo nell&#39;ambiente **testing** per 90 giorni consecutivi, i dati del catalogo vengono impostati sulla modalità di sospensione e non vengono restituiti dati per alcuna query. I dati del catalogo nell&#39;ambiente **produzione** non sono interessati dalla regola dei 90 giorni.

Se nell&#39;ambiente è presente un **catalogo vuoto** 45 giorni dopo la creazione, i dati del catalogo vengono impostati sulla modalità di sospensione e non vengono restituiti dati per alcuna query. Questo vale sia per gli ambienti di produzione che per quelli di test.

### Riattiva dati catalogo

Per ripristinare i dati del catalogo dopo la sospensione, [invia una richiesta di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) con il titolo &quot;Riattiva [!DNL Product Recommendations]&quot; e includi gli ID ambiente. I dati del catalogo devono essere ripristinati entro un paio d’ore.
