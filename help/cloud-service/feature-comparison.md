---
title: Confronto tra Adobe Commerce SaaS e PaaS
description: Confronto tra i modelli SaaS di Adobe Commerce e PaaS per determinare l’approccio di implementazione migliore per le esigenze aziendali.
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
autotag-review: '2026-06-18T16:00:51.353Z'
TQID: 'https://experienceleague.adobe.com/6Iui3BCjT7GqaD0lC5hyw-xSrDs8SVwIB4PazXx8mGU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 1019
ht-degree: 0%

---

# Confronto delle funzioni

Adobe Commerce offre tre modelli di distribuzione:

- [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."} [Adobe Commerce su Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) (locale)

Questo confronto si concentra sulle differenze tra i modelli software-as-a-service (SaaS) e platform-as-a-service (PaaS). Questi modelli forniscono diversi livelli di personalizzazione, estensibilità e controllo sull’implementazione di Commerce.

>[!NOTE]
>
>Il modello on-premise condivide funzionalità simili con il modello PaaS, quindi questo confronto si applica anche quando si considerano le implementazioni SaaS rispetto a quelle on-premise.

## Funzioni di gestione dello store

L&#39;[interfaccia utente amministratore di Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) è l&#39;interfaccia principale per l&#39;accesso alle funzioni di gestione delle operazioni di back-end store, inventario, prezzi, promozioni e interazioni con i clienti. Tuttavia, [!DNL Adobe Commerce as a Cloud Service] offre soluzioni univoche che sostituiscono alcune delle funzionalità note disponibili in [!DNL Adobe Commerce on Cloud] e nei progetti locali.

Nella tabella seguente sono descritte le funzionalità e le soluzioni sostitutive disponibili in [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>Funzionalità</th>
            <th>Modello PaaS [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce su cloud (infrastruttura PaaS gestita da Adobe) e ai progetti locali."}</th>
            <th>Modello SaaS [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Gestione delle risorse digitali</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Raccolta file multimediali</a></td>
            <td><a href="../aem-assets-integration/overview.md">Visualizzazioni prodotto</a></td>
        </tr>
        <tr>
            <td>Gestione dei contenuti</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">Sistema di gestione dei contenuti (CMS)</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">Generatore pagine</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">Riscrittura URL</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
        </tr>
        <tr>
            <td>Catalogo merchandising</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">Gestione temporanea dei contenuti</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
            <td><a href="../catalog-service/overview.md">Servizio catalogo</a></td>
        </tr>
        <tr>
            <td>Pagamenti</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">Soluzioni di pagamento</a></td>
            <td><a href="../payment-services/guide-overview.md">Servizi di pagamento</a></td>
        </tr>
        <tr>
            <td>Funzionalità B2B</td>
            <td>Funzionalità B2B complete disponibili dopo l'installazione</td>
            <td>Preinstallato con funzionalità B2B di base<sup>1</sup></td>
        </tr>
        <tr>
            <td>Sperimentazione</td>
            <td>Componente aggiuntivo per determinati livelli</td>
            <td>Test A/B nativi per ottimizzare coinvolgimento e conversione</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> funzionalità <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B di base</a>, come la gestione e le quotazioni aziendali, sono disponibili come funzionalità predefinite in SaaS. Tuttavia, le personalizzazioni specifiche del settore possono richiedere considerazioni aggiuntive sull’implementazione.
            </td>
        </tr>
    </tfoot>
</table>

## Estensibilità e caratteristiche della piattaforma

Nella tabella seguente vengono confrontate le funzionalità della piattaforma e le funzioni di estensibilità per comprendere le differenze e decidere quale modello soddisfa al meglio i requisiti aziendali prima di avviare un’implementazione.

<table>
    <thead>
        <tr>
            <th>Funzionalità</th>
            <th>Modello PaaS [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce su cloud (infrastruttura PaaS gestita da Adobe) e ai progetti locali."}</th>
            <th>Modello SaaS [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Funzionalità della piattaforma</strong></td>
        </tr>
        <tr>
            <td>Aggiornamenti di funzionalità e sicurezza</td>
            <td>Richiede l'aggiornamento manuale e l'applicazione di patch. Sei versioni patch e una versione minore all’anno.</td>
            <td>Aggiornato automaticamente da Adobe tramite un modello SaaS senza versione</td>
        </tr>
        <tr>
            <td>Infrastruttura di hosting</td>
            <td>Singolo tenant</td>
            <td>Multi-tenant</td>
        </tr>
        <tr>
            <td>Prestazioni e scalabilità</td>
            <td>Ridimensionamento automatico orizzontale per un'architettura scalata. Il ridimensionamento automatico verticale per il livello web viene introdotto nell’accesso anticipato per tutti i commercianti, inclusa l’architettura non scalata.</td>
            <td>Applicazione multi-tenant nativa per il cloud con scalabilità automatica completa nello stack</td>
        </tr>
        <tr>
            <td>Osservabilità</td>
            <td>[!DNL New Relic] accesso per i clienti al monitoraggio e alla gestione dell'ambiente</td>
            <td>Gestione di Adobe. I clienti possono utilizzare [!DNL OpenTelemetry] per le app [!DNL App Builder] e le dashboard RUM per la vetrina. Licenza [!DNL New Relic] non inclusa. I clienti possono configurare [!DNL API Mesh] e [!DNL App Builder] per inviare dati al proprio account [!DNL New Relic].</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] incluso</td>
            <td>CDN Edge completamente gestita, strettamente abbinata a Commerce Storefront. Supporto di BYO-CDN.</td>
        </tr>
        <tr>
            <td>Sicurezza e conformità</td>
            <td>SOC2, PCI, certificazioni ISO per provider di hosting, HIPAA</td>
            <td>SOC2, PCI, ISO, RGPD. HIPAA attualmente non disponibile.</td>
        </tr>
        <tr>
            <td>Disaster recovery e SLA</td>
            <td>99,99% infrastruttura, 99,9% applicazione (Managed Services)</td>
            <td>99,9% (infrastruttura e applicazione), RPO/RTO più veloci</td>
        </tr>
        <tr>
            <td>Aree geografiche di hosting</td>
            <td>Azure (24 posizioni), AWS (22 posizioni), GCP (8 posizioni, non standard)</td>
            <td>Disponibile a livello globale. Per informazioni sugli ambienti di produzione della tua area geografica, contatta il rappresentante dell’assistenza clienti. Ubicazioni aggiuntive distribuite in base alla domanda.</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personalizzazione dell’amministratore di Commerce</strong></td>
        </tr>
        <tr>
            <td>Estensibilità di Admin Console</td>
            <td>Personalizzazione e temi PHP, estensibilità App Builder (consigliata)</td>
            <td>Estensibilità di App Builder</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Estensibilità</strong></td>
        </tr>
        <tr>
            <td>Modello di estensibilità</td>
            <td>In-process (personalizzazione PHP) e out-of-process (Consigliato:API, eventi, App Builder)</td>
            <td>Solo out-of-process (API, eventi, App Builder)</td>
        </tr>
        <tr>
            <td>API web estensibili</td>
            <td>Estensibilità REST/GraphQL nativa e Mesh API con risolutori personalizzati</td>
            <td>Mesh API con risolutori personalizzati</td>
        </tr>
        <tr>
            <td>Estensibilità del modello dati</td>
            <td>Personalizzazione completa del modello dati</td>
            <td>Attributi personalizzati per entità core e B2B<sup>1</sup></td>
        </tr>
        <tr>
            <td>Tecnologie</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Node</td>
        </tr>
        <tr>
            <td>App marketplace</td>
            <td>[Magento Marketplace](https://marketplace.magento.com/) (estensioni PHP) e [Exchange Marketplace](https://commercemarketplace.adobe.com) per [!DNL App Builder] app (scelta consigliata)</td>
            <td>[!DNL App Builder] app da [[!DNL Exchange Marketplace]](https://commercemarketplace.adobe.com)</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Dati e archiviazione</strong></td>
        </tr>
        <tr>
            <td>Personalizzazioni dell’indice di ricerca</td>
            <td>Personalizzazione della ricerca nativa</td>
            <td>Richiede soluzioni di terze parti</td>
        </tr>
        <tr>
            <td>Tipi di e-mail personalizzati</td>
            <td>Personalizzazione e-mail completa</td>
            <td>Solo modelli e-mail standard</td>
        </tr>
        <tr>
            <td>Archiviazione dati personalizzata</td>
            <td>DB, file, cache, coda</td>
            <td>La libreria di stato di App Builder (solo file)<sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">Archiviazione database per App Builder</a> è attualmente in fase di accesso anticipato.</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                L'estensibilità del modello dati <sup>1</sup> in SaaS supporta <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">l'estensione delle entità principali</a> oltre il prodotto e il cliente, incluse le entità B2B. Tuttavia, i modelli di dati specifici per il settore (ad esempio, attributi specifici per i dealer) potrebbero richiedere considerazioni architetturali aggiuntive.
                <br><br>
                <sup>2</sup> Adobe sta lavorando attivamente all'integrazione di Document DB per soddisfare le esigenze di archiviazione persistente per SaaS. Attualmente, le implementazioni che richiedono lo storage dei dati a lungo termine possono richiedere il provisioning e la manutenzione di infrastrutture aggiuntive.
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>Quando consideri la migrazione a SaaS, Adobe consiglia di:
>
>- Se possibile, spostare le funzionalità appropriate per l&#39;estensibilità fuori processo.
>- Ridurre l&#39;area di superficie che richiede la transizione.
>- Considerare [!DNL API Mesh] per estendere la funzionalità API.
>- Monitora la continua evoluzione della piattaforma Adobe e le nuove versioni di funzionalità.
>- Valuta i requisiti del modello dati specifici del settore in base alle opzioni di estensibilità disponibili.

