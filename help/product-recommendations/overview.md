---
title: Introduzione a  [!DNL Product Recommendations]
description: '[!DNL Product Recommendations] è un potente strumento di marketing che puoi utilizzare per aumentare le conversioni, incrementare i ricavi e stimolare il coinvolgimento degli acquirenti.'
recommendations: noCatalog
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Introduzione a [!DNL Product Recommendations]

I consigli di prodotto sono un potente strumento di marketing che puoi utilizzare per aumentare le conversioni, incrementare i ricavi e stimolare il coinvolgimento degli acquirenti. I prodotti consigliati da Adobe Commerce sono basati su [Adobe Sensei](https://www.adobe.com/sensei.html), che utilizza algoritmi di intelligenza artificiale e machine learning per eseguire un&#39;analisi approfondita dei dati aggregati dei visitatori. Quando vengono combinati con il tuo catalogo Adobe Commerce, questi dati offrono un’esperienza altamente coinvolgente, rilevante e personalizzata.

I consigli di prodotto vengono visualizzati sullo storefront come unità con etichette, ad esempio &quot;Hanno visto anche i clienti che hanno visualizzato questo prodotto&quot;. Puoi creare, gestire e distribuire consigli nelle viste dello store direttamente dall’amministratore di Adobe Commerce.

Se la vetrina è implementata tramite PWA Studio, consulta la [documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se utilizzi una tecnologia front-end personalizzata come React o Vue JS, scopri come [integrare](headless.md) [!DNL Product Recommendations] nella tua vetrina headless.

>[!NOTE]
>
>Esistono molti modi per sviluppare un’implementazione headless o personalizzata. Questa guida descrive un modo per farlo, utilizzando PWA Studio. Non copre tutti gli scenari o le eventualità.

## Privacy

La raccolta dei dati ai fini di [!DNL Product Recommendations] non include informazioni personali identificabili (PII). Inoltre, tutti gli identificatori degli utenti come gli ID cookie e gli indirizzi IP sono rigorosamente anonimi. Per ulteriori informazioni, consulta [Informativa sulla privacy di Adobe](https://www.adobe.com/privacy/policy.html).

[!DNL Product Recommendations] utenti possono fare riferimento a [Data Management Dashboard](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html) per ulteriori dati sulla sincronizzazione dei dati.

## Consigli di prodotto e relazioni di prodotto

Date le complessità in continua evoluzione dello shopping online, ciò che funziona meglio per la vetrina è spesso una combinazione di più tecnologie chiave. L&#39;utilizzo di [!DNL Product Recommendations] e [relazioni tra prodotti](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html) offre maggiore flessibilità durante la promozione dei prodotti. Puoi sfruttare [!DNL Product Recommendations] con tecnologia Adobe Sensei per automatizzare in modo intelligente i consigli su larga scala. Puoi quindi sfruttare le [Regole prodotto correlate](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html) quando devi intervenire manualmente e assicurarti che sia stato fatto un consiglio specifico a un segmento di acquirenti target o quando devono essere raggiunti determinati obiettivi aziendali.

I consigli sui prodotti consentono di:

- Scegli tra nove tipi di consigli intelligenti distinti in base alle seguenti aree: basati su acquirente, basati su articolo, basati sulla popolarità, basati sulle tendenze e sulla similarità
- Utilizza i dati comportamentali per personalizzare i consigli nel percorso di vetrina dell’acquirente
- Misura le metriche chiave rilevanti per ogni consiglio, in modo da comprendere l’impatto dei consigli

## Demo di [!DNL Product Recommendations]

Guarda questo video per saperne di più su [!DNL Product Recommendations]:

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## Criteri di conservazione dei dati del catalogo

Se non si invia una query per i dati del catalogo nell&#39;ambiente di test per 90 giorni consecutivi, i dati del catalogo vengono impostati sulla modalità di sospensione e non vengono restituiti dati per alcuna query. I dati del catalogo nell’ambiente di produzione non sono interessati da questo criterio.

Per riattivare i dati del catalogo nell&#39;ambiente di test, [invia una richiesta di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) con il titolo: &quot;Riattiva [!DNL Product Recommendations]&quot; e includi gli ID ambiente. I dati del catalogo nell’ambiente di test devono essere ripristinati entro un paio d’ore.
