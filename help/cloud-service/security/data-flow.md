---
title: Architettura di sicurezza e flusso di dati
description: Scopri l’architettura di sicurezza e il flusso di dati per Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
autotag-review: '2026-06-18T16:16:18.600Z'
TQID: 'https://experienceleague.adobe.com/2yK-VVec98nFH9LPpfSe4kQ2YvQr2yy3G0Rym5-HCbI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 387
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
