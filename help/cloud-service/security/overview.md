---
title: Panoramica sulla sicurezza
description: Scopri le funzioni di sicurezza di Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '581'
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
