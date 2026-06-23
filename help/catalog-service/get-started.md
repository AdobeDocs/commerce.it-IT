---
title: Introduzione a  [!DNL Catalog Service]
description: Scopri come accedere a  [!DNL Catalog Service]  e integrarlo con applicazioni front-end e servizi di terze parti.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
TQID: https://experienceleague.adobe.com/KBdWesEoKJu-qWsY-Ny1Om-msUkyUPfUTQWftEqSg1g
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10a91a91337778648e99078bcbf0c9ef25a49f86
workflow-type: tm+mt
source-wordcount: 437
ht-degree: 0%

---

# Introduzione a [!DNL Catalog Service]

Dopo aver abilitato [!DNL Catalog Service], puoi accedere al servizio e utilizzarlo per recuperare i dati del catalogo, come le informazioni su prodotti e categorie, dall&#39;istanza Adobe Commerce. Il servizio è disponibile come API di GraphQL a cui è possibile accedere dall’amministratore Commerce o da qualsiasi applicazione front-end che supporta le query GraphQL.

{{aco-merchandising-services}}

## Accedere al servizio

[!DNL Catalog Service] è disponibile come API GraphQL a cui è possibile accedere dall&#39;amministratore Commerce o da qualsiasi applicazione front-end che supporta le query GraphQL. Il servizio è disponibile sia in ambienti SaaS che PaaS.

[!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."}

| Ambiente | Endpoint |
| ------------ | ----------: |
| **Test** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Produzione** | `https://catalog-service.adobe.io/graphql` |

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}

| Ambiente | Endpoint |
| ----------- | --------:|
| Test | `https://na1-sandbox.api.commerce.adobe.com/{{tenant-id}}/graphql` |
| Produzione (non ancora disponibile) | `https://na1.api.commerce.adobe.com/{{tenant-id}}/graphql` |

**Struttura URL per endpoint SaaS**

```text
https://<region>-<environment>.api.commerce.adobe.com/<tenantId>/graphql
```

- `<region>` è l&#39;area cloud in cui è distribuita l&#39;istanza.
- `<environment>` è il tipo di ambiente, ad esempio `sandbox`. Se l’ambiente è la produzione, questo valore viene omesso.
- `<tenantId>` è l&#39;identificatore univoco dell&#39;istanza specifica della tua organizzazione in Adobe Experience Cloud.

Per informazioni dettagliate sull&#39;utilizzo dell&#39;API GraphQL di Catalog Service, vedere la [Guida di Catalog Service per Adobe Commerce](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) nella documentazione di *Adobe Commerce Developer*.

## Integrazione con una vetrina headless o servizi di terze parti

Per l&#39;integrazione con una vetrina headless, è necessario aggiornare la configurazione della vetrina per abilitare la comunicazione tra la vetrina e [!DNL Catalog Service] per recuperare i dati di prodotti e categorie.

Se utilizzi Adobe Commerce storefront su Edge Delivery Services, aggiungi l’endpoint Catalog Service alla configurazione della vetrina. Per informazioni dettagliate, consulta la [documentazione di Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/#storefront-configuration).

Per altre integrazioni, consulta la documentazione di configurazione del progetto per informazioni dettagliate su come configurare le integrazioni tra il servizio e le origini dati back-end.

### Configurazione del firewall

Per consentire a [!DNL Catalog Service] di passare attraverso un firewall, aggiungere `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## Catalog Service e Mesh API

La rete API [per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) consente agli sviluppatori di integrare API private o di terze parti e altre interfacce con i prodotti Adobe utilizzando Adobe IO.

Per informazioni dettagliate sull&#39;installazione e la configurazione, vedere l&#39;argomento [[!DNL Catalog Service] and API Mesh](mesh.md).

## Monitorare e risolvere i problemi di esportazione dei dati

{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

Utilizzare [Commerce CLI](../data-export/data-export-cli-commands.md) per risincronizzare manualmente i feed quando necessario. Per le opzioni di risincronizzazione e i passaggi aggiuntivi per la risoluzione dei problemi, vedi [Gestione sincronizzazione](../data-export/data-sync-manage.md) nella _Guida all&#39;esportazione dei dati SaaS_.

{{install-data-sync-feed-status}}
