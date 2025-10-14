---
title: Introduzione a  [!DNL Catalog Service]
description: Scopri come accedere a  [!DNL Catalog Service]  e integrarlo con applicazioni front-end e servizi di terze parti.
role: Admin, Developer
exl-id: ee178e67-519d-4283-8de8-2634ae1f347a
source-git-commit: 377a2b9e42378640aee034eda1426b049c173aad
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Introduzione a [!DNL Catalog Service]

Dopo aver abilitato [!DNL Catalog Service], puoi accedere al servizio e utilizzarlo per recuperare i dati del catalogo, come le informazioni su prodotti e categorie, dall&#39;istanza Adobe Commerce. Il servizio è disponibile come API di GraphQL a cui è possibile accedere dall’amministratore Commerce o da qualsiasi applicazione front-end che supporta le query GraphQL.

## Accedere al servizio

[!DNL Catalog Service] è disponibile come API GraphQL a cui è possibile accedere dall&#39;amministratore Commerce o da qualsiasi applicazione front-end che supporta le query GraphQL. Il servizio è disponibile sia in ambienti SaaS che PaaS.

[!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."}

| Ambiente | Endpoint |
| ------------ | ----------: |
| **Test** | `https://catalog-service-sandbox.adobe.io/graphql` |
| **Produzione** | `https://catalog-service.adobe.io/graphql` |

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}

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
- `<tenantId>` è l&#39;identificatore univoco per l&#39;istanza specifica della tua organizzazione all&#39;interno di Adobe Experience Cloud.

Per informazioni dettagliate sull&#39;utilizzo dell&#39;API GraphQL di Catalog Service, vedere la [Guida di Catalog Service per Adobe Commerce](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) nella documentazione di *Adobe Commerce Developer*.

## Integrazione con una vetrina headless o servizi di terze parti

Per l&#39;integrazione con una vetrina headless, è necessario aggiornare la configurazione della vetrina per abilitare la comunicazione tra la vetrina e [!DNL Catalog Service] per recuperare i dati di prodotti e categorie.

Se utilizzi Adobe Commerce storefront su Edge Delivery Services, aggiungi l’endpoint Catalog Service alla configurazione della vetrina. Per informazioni dettagliate, consulta la [documentazione di Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=it#storefront-configuration).

Per altre integrazioni, consulta la documentazione di configurazione del progetto per informazioni dettagliate su come configurare le integrazioni tra il servizio e le origini dati back-end.

### Configurazione del firewall

Per consentire a [!DNL Catalog Service] di attraversare un firewall, aggiungere `commerce.adobe.io` al inserisco nell&#39;elenco Consentiti di.

## Catalog Service e Mesh API

La rete API [per Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) consente agli sviluppatori di integrare API private o di terze parti e altre interfacce con i prodotti Adobe utilizzando Adobe IO.

Per informazioni dettagliate sull&#39;installazione e la configurazione, vedere l&#39;argomento [[!DNL Catalog Service] and API Mesh](mesh.md).

## Utilizzare il dashboard di gestione dati

Utilizza [Data Management Dashboard](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-dashboard) per monitorare la sincronizzazione dei dati tra [!DNL Catalog Service] e l&#39;istanza di Adobe Commerce. Il dashboard fornisce informazioni approfondite sul processo di trasferimento dei dati, compreso lo stato delle esportazioni di dati e un elenco di prodotti sincronizzati.