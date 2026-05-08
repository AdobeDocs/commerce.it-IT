---
title: Architettura di sicurezza e flusso di dati
description: Scopri l’architettura di sicurezza e il flusso di dati per Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Architettura di sicurezza e flusso di dati

L&#39;esempio seguente illustra il flusso tipico dei dati in [!DNL Adobe Commerce as a Cloud Service]:

![Diagramma del flusso di dati di Adobe Commerce as a Cloud Service](../assets/data-flow-1.png)

## Descrizione del flusso di dati

**Passaggio 1**: l&#39;acquirente digita l&#39;URL della vetrina del commerciante nel browser, che invia l&#39;URL alla rete di distribuzione dei contenuti (CDN esterna) di Commerce Storefront.

**Passaggio 2**: se l&#39;URL del sito è memorizzato nella cache, Storefront CDN lo restituisce all&#39;acquirente. Se non è già memorizzata nella cache, il che potrebbe verificarsi se si tratta della prima richiesta di una risorsa, la rete CDN esterna inoltra la richiesta dell’acquirente alla rete CDN interna e memorizza nella cache la risposta per le richieste successive.

**Passaggio 2a**: se la richiesta è per immagini o video, viene inviata a [!DNL Product Visuals] per l&#39;evasione e restituita alla vetrina.

**Passaggio 3**: se l&#39;URL del sito è memorizzato nella cache della rete CDN interna, viene restituito da tale cache. In caso contrario, viene inviato a [!DNL API Mesh] e la risposta viene memorizzata nella cache per le richieste successive.

**Passaggio 4**: [!DNL API Mesh] funge da livello di orchestrazione e determina se inviare la richiesta a [!DNL Adobe Commerce as a Cloud Service] o a un sistema di terze parti per soddisfare la richiesta.

>[!NOTE]
>
>[!DNL API Mesh] invierà richieste a sistemi di terze parti solo se hai personalizzato la configurazione mesh per farlo.

**Passaggio 5**: le richieste inviate a [!DNL Adobe Commerce as a Cloud Service] passano attraverso un firewall dell&#39;applicazione Web (WAF) che blocca le richieste sospette o dannose. Se l&#39;URL richiesto è memorizzato nella cache della rete CDN [!DNL Commerce], viene distribuito da tale cache. Se non è memorizzato in cache, viene restituito da uno o più microservizi [!DNL Adobe Commerce as a Cloud Service] (ad esempio Foundation, Search e Recommendations) e quindi memorizzato nella cache per le richieste future.

**Passaggio 5a**: se la richiesta viene inviata a un sistema di terze parti, la risposta verrà restituita a [!DNL API Mesh].

**Passaggio 5b**: se la richiesta è per l&#39;elaborazione del pagamento, il provider di pagamenti esegue il rendering di un iframe nella vetrina per consentire al cliente di immettere in modo sicuro le informazioni sulla carta di credito e completare la transazione di pagamento.

**Passaggio 6**: una volta ricevute le risposte di [!DNL Adobe Commerce as a Cloud Service] o di servizi di terze parti da [!DNL API Mesh], queste vengono unite in un grafico unificato e restituite a [!DNL Commerce Storefront] per soddisfare la richiesta dell&#39;acquirente.
