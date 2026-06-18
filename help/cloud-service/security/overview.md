---
title: Panoramica sulla sicurezza
description: Scopri le funzioni di sicurezza di Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
autotag-review: '2026-06-18T16:18:52.695Z'
TQID: 'https://experienceleague.adobe.com/AmkzZgLeOa9zJkPE8kWM6lFcFNtBAAOmJeULI-y4gOw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: adedf3b3-e153-47a3-ae73-b5d65067b544
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
source-wordcount: 581
ht-degree: 0%

---


# Panoramica sulla sicurezza

[!DNL Adobe Commerce as a Cloud Service] è progettato con la sicurezza al centro, offrendo una piattaforma di e-commerce SaaS moderna che offre protezione di livello enterprise, resilienza operativa e tranquillità per le aziende di tutte le dimensioni.

A differenza dei modelli PaaS tradizionali, il modello SaaS elimina il carico di patch manuali, manutenzione dell&#39;infrastruttura e cicli di aggiornamento. La sicurezza è incorporata in ogni livello della piattaforma, dall&#39;infrastruttura gestita da Adobe e dalle pipeline di distribuzione automatizzate alla gestione delle identità e degli accessi tramite [!DNL Adobe IMS].

[!DNL Adobe Commerce as a Cloud Service] sfrutta il framework globale di sicurezza e conformità di Adobe, garantendo l&#39;allineamento con gli standard del settore quali ISO 27001, SOC 2 e RGPD. I clienti traggono vantaggio da un [modello di responsabilità condivisa](./shared-responsibility.md) che delinea chiaramente il ruolo di Adobe nella protezione della piattaforma e il ruolo del cliente nella gestione dei dati e dell&#39;accesso.

Grazie alle protezioni integrate quali il firewall dell&#39;applicazione Web (WAF), la mitigazione DDoS, il provisioning sicuro e la scansione continua delle vulnerabilità, [!DNL Adobe Commerce as a Cloud Service] consente alle aziende di innovare più rapidamente senza compromettere la sicurezza.

Questo documento descrive l&#39;architettura di sicurezza, le salvaguardie operative e la posizione di conformità di [!DNL Adobe Commerce as a Cloud Service], consentendo ai clienti di prendere decisioni informate e scalare in modo affidabile le operazioni di e-commerce digitale.

## Rete per la distribuzione di contenuti (CDN) e firewall per applicazioni web (WAF)

### CDN vetrina

I commercianti possono scegliere di distribuire una rete CDN gestita da Adobe o acquistare una propria soluzione CDN per proteggere la vetrina basata su Commerce.

>[!IMPORTANT]
>
>Se i clienti scelgono di distribuire una rete CDN gestita da Adobe, non possono configurare le regole CDN. Le regole di caching personalizzate o le regole WAF possono essere configurate dai clienti quando utilizzano una propria rete CDN per proteggere gli Storefront.

### CDN [!DNL API Mesh for Adobe Developer App Builder]

Il livello CDN di [!DNL API Mesh] termina TLS, esegue il gateway GraphQL come processi di lavoro, fornisce il caching edge globale e DDoS/WAF automatico ed espone `edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io` come endpoint mesh pubblici; i clienti possono aggiungere prima la propria rete CDN, ma la rete CDN di [!DNL API Mesh] è fissa e gestita da Adobe e i clienti non possono configurare le proprie regole WAF.

Per ulteriori informazioni sulle funzionalità di sicurezza di [!DNL API Mesh], consulta la [documentazione di API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}.

### CDN back-end

Una rete CDN integrata protegge [!DNL Adobe Commerce as a Cloud Service].

A causa dell&#39;architettura [!DNL Adobe Commerce as a Cloud Service], quando un commerciante esegue il provisioning di un&#39;istanza in una cella composita, ad esempio `na1`, `eu1`, `au1` o altre aree geografiche, vengono esposte tre superfici pubbliche:

| Superficie | Esempio di pattern URL |
| --- | --- |
| Interfaccia utente amministratore | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| API REST | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| API GRAPHQL | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service] utilizza una rete WAF e una rete CDN combinate:

- **WAF** - Protezione del firewall dell&#39;applicazione Web per tutte le [!DNL Adobe Commerce as a Cloud Service] superfici pubbliche.
- **CDN** - Memorizzazione in cache di Edge per risorse statiche e risposte GraphQL memorizzabili nella cache.

WAF e CDN sono gestiti dalla piattaforma [!DNL Adobe Commerce as a Cloud Service] e non possono essere configurati dai clienti.

### Protezione DoS

La rete CDN e WAF integrate forniscono protezione DDoS sia a livello di rete che a livello HTTP. [!DNL Adobe Commerce as a Cloud Service] non espone i registri WAF o DDoS direttamente ai commercianti.

## Archiviazione e crittografia dei dati

Se i dati vengono archiviati in [!DNL App Builder], un commerciante può fare riferimento alle [!DNL App Builder] [opzioni di archiviazione](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/). [!DNL App Builder] applica l&#39;isolamento del tenant e l&#39;accesso ai dati archiviati in questi servizi è limitato allo spazio dei nomi di runtime in cui viene eseguita l&#39;azione. Nessuna crittografia dei dati nell&#39;archiviazione.

Quando si utilizza [!DNL API Mesh], i segreti devono essere archiviati nel file `secrets.yaml` nella configurazione mesh. [!DNL API Mesh] crittografa questi segreti utilizzando la crittografia AES-256 ([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/)).

Tutti i dati archiviati in [!DNL Adobe Commerce as a Cloud Service] vengono crittografati a riposo utilizzando la crittografia AES a 256 bit e tutti i dati vengono crittografati tramite HTTPS utilizzando TLS 1.2 o versione successiva in transito.
