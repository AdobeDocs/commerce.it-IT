---
title: Flusso di lavoro di implementazione
description: Scopri i passaggi per implementare correttamente [!DNL Product Recommendations] sulla vetrina.
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Flusso di lavoro di implementazione

[!DNL Product Recommendations] utilizza sia i dati comportamentali che quelli del catalogo:

- Comportamento: dati del coinvolgimento di un acquirente sul tuo sito, ad esempio visualizzazioni di prodotti, elementi aggiunti al carrello e acquisti. Adobe Commerce e Adobe AI non raccolgono informazioni personali identificabili.

- Catalogo: metadati del prodotto come nome, prezzo e disponibilità.

Quando installi `magento/product-recommendations module`, Adobe AI aggrega i dati comportamentali e di catalogo e crea [!DNL Product Recommendations] per ogni tipo di consiglio. Il servizio [!DNL Product Recommendations] distribuisce quindi tali consigli nella vetrina. Per aiutarti a implementare i consigli di prodotto nella vetrina, utilizza il seguente flusso di lavoro:

>[!NOTE]
>
> Se la vetrina è implementata tramite PWA Studio, consulta la [documentazione di PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Se utilizzi una tecnologia front-end personalizzata come React o Vue JS, scopri come [integrare](headless.md) [!DNL Product Recommendations] nella tua vetrina headless.

## Flusso di lavoro

1. **Distribuisci raccolta dati in produzione**

   La distribuzione di [!DNL Product Recommendations] richiede due [origini dati principali](type.md): catalogo e comportamento. Poiché la produzione è l’unico ambiente in cui le azioni degli acquirenti vengono acquisite e analizzate, inizia la raccolta dei dati sulla produzione il prima possibile. [Scopri](events.md) come Adobe AI addestra modelli di apprendimento automatico che offrono consigli di qualità superiore. Inoltre, quando inizi a raccogliere dati comportamentali in produzione, puoi [recuperare consigli](staging-environment.md#fetch-recommendations-from-production-environment-recommended) in base a questi dati di produzione mentre operi in ambienti non di produzione. Puoi quindi testare e sperimentare diversi consigli calcolati in base ai dati reali dell’acquirente raccolti in produzione.

   Per distribuire la raccolta dati in produzione, è necessario [installare e configurare](install-configure.md) il modulo [!DNL Product Recommendations] fornendo una [chiave API](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html?lang=it).

   >[!TIP]
   >
   > L’implementazione della raccolta dati non cambia l’aspetto della vetrina o l’esperienza degli acquirenti. Solo la creazione e la distribuzione di unità di consigli modifica l’esperienza del cliente nella vetrina. Prima di implementare in produzione, assicurati di eseguire il test nell’ambiente non di produzione. Inoltre, non creare unità di consigli fino a quando non personalizzi il modello. Vedere il passaggio successivo.

1. **Personalizza il modello in base al tuo stile**

   La vetrina rappresenta il tuo marchio, quindi assicurati di modificare il modello di consigli di prodotto in modo che corrisponda al tema del sito.

   >[!TIP]
   >
   > Personalizzando il modello, è possibile specificare il foglio di stile, sovrascrivere la posizione in cui un&#39;unità di consigli viene visualizzata in una pagina e così via.

   Per informazioni su come completare questo passaggio, consulta [Personalizza](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html?lang=it) nella documentazione per gli sviluppatori.

1. **Verifica i consigli nell&#39;ambiente non di produzione**

   È sempre consigliabile testare una nuova tecnologia nell’ambiente non di produzione prima di implementarla in produzione. Il test dei consigli sull’ambiente non di produzione consente di riprodurre con diversi tipi di unità, posizioni e pagine per i consigli. Puoi estrarre i consigli in base ai dati comportamentali già raccolti durante il test in un ambiente non di produzione, in modo che i risultati dei consigli si basino sul comportamento di acquisto dei clienti effettivi.

   >[!TIP]
   >
   > Assicurati che il catalogo dell’ambiente non di produzione sia in gran parte lo stesso di quello esistente in produzione. L’utilizzo di cataloghi simili garantisce che i prodotti restituiti nelle unità di raccomandazione imitino strettamente i prodotti in produzione.

   Per informazioni su come completare questo passaggio, consulta [Recuperare](staging-environment.md) i dati comportamentali dall&#39;ambiente di produzione.

1. **Crea e distribuisci consigli nella vetrina di produzione**

   Ora che hai implementato la raccolta di dati comportamentali in produzione, modificato il modello di consigli di prodotto e testato i consigli utilizzando il comportamento effettivo degli acquirenti, sei pronto a promuovere tutto il codice in produzione e a [creare](create.md) consigli di prodotti live.
