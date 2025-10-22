---
title: Confronto tra Adobe Commerce SaaS e PaaS
description: Confronto tra i modelli SaaS di Adobe Commerce e PaaS per determinare l’approccio di implementazione migliore per le esigenze aziendali.
role: Developer
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Confronto delle funzioni

Adobe Commerce offre tre modelli di distribuzione:

- [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."} [Adobe Commerce su Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) (locale)

Questo confronto si concentra sulle differenze tra i modelli software-as-a-service (SaaS) e platform-as-a-service (PaaS), che forniscono diversi livelli di personalizzazione, estensibilità e controllo sull’implementazione commerce.

>[!NOTE]
>
>Il modello on-premise condivide funzionalità simili con il modello PaaS, quindi questo confronto si applica anche quando si considerano le implementazioni SaaS rispetto a quelle on-premise.

## Funzioni di gestione dello store

L&#39;[interfaccia utente amministratore di Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) è l&#39;interfaccia principale per l&#39;accesso alle funzioni di gestione delle operazioni di back-end store, inventario, prezzi, promozioni e interazioni con i clienti. Tuttavia, [!DNL Adobe Commerce as a Cloud Service] offre soluzioni univoche che sostituiscono alcune delle note funzionalità disponibili nei progetti Adobe Commerce on-premise e cloud.

Nella tabella seguente sono descritte le funzionalità e le soluzioni sostitutive disponibili in [!DNL Adobe Commerce as a Cloud Service]:

<table>
    <thead>
        <tr>
            <th>Modello PaaS [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."}</th>
            <th>Modello SaaS [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}</th>
            <th>Dettagli</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Gestione delle risorse digitali</a></td>
            <td><a href="../aem-assets-integration/overview.md">Integrazione con AEM Assets</a></td>
            <td>Un solido sistema di gestione delle risorse digitali (DAM) che si integra con Adobe Experience Manager per la gestione dei contenuti rich media. In alternativa, la funzione predefinita per la gestione delle risorse e dei file digitali fornisce strumenti di base per la gestione delle risorse digitali.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">Sistema di gestione dei contenuti (CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
            <td rowspan="3">Un CMS che consente agli utenti di creare e gestire facilmente contenuti di vetrina tramite l’authoring di documenti o un editor visivo e include funzionalità di sperimentazione native.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">Page Builder</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">Riscritture URL</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">Staging dei contenuti</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">Servizio catalogo</a></td>
            <td rowspan="2">Servizio per visualizzazione avanzata (sola lettura) per la gestione dei dati del catalogo e il rendering delle esperienze vetrina relative ai prodotti.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Visual Merchandiser</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">Pagamenti</a></td>
            <td><a href="../payment-services/guide-overview.md">Servizi di pagamento</a></td>
            <td>Un servizio di pagamento integrato che agevoli transazioni sicure ed efficienti.</td>
        </tr>
    </tbody>
</table>

## Estensibilità e caratteristiche della piattaforma

La tabella seguente confronta le funzionalità della piattaforma e le funzioni di estensibilità per comprendere le differenze e decidere con cognizione di causa quale modello soddisfa al meglio i requisiti aziendali prima di avviare un’implementazione.

<table>
    <thead>
        <tr>
            <th>Funzionalità</th>
            <th>Modello PaaS [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."}</th>
            <th>Modello SaaS [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Si applica solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Funzionalità della piattaforma</strong></td>
        </tr>
        <tr>
            <td>Funzionalità B2B</td>
            <td>Funzionalità B2B complete disponibili dopo l'installazione</td>
            <td>Preinstallato con funzionalità B2B di base<sup>1</sup></td>
        </tr>
        <tr>
            <td>Sperimentazione</td>
            <td>Componente aggiuntivo per determinati livelli</td>
            <td>Test A/B per ottimizzare coinvolgimento e conversione</td>
        </tr>
        <tr>
            <td>Aggiornamenti di funzionalità e sicurezza</td>
            <td>Richiede l'aggiornamento manuale e l'applicazione di patch</td>
            <td>Distribuito automaticamente</td>
        </tr>
        <tr>
            <td>Infrastruttura di hosting</td>
            <td>Singolo tenant</td>
            <td>Multi-tenant</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personalizzazione dell’amministratore di Commerce</strong></td>
        </tr>
        <tr>
            <td>Schermate di amministrazione core estensibili</td>
            <td>Personalizzazione completa del layout e delle funzionalità</td>
            <td>Filtri preimpostati, controlli di visibilità</td>
        </tr>
        <tr>
            <td>Nuove schermate di amministrazione estensibili</td>
            <td>Integrazione standard tra l’interfaccia utente di amministrazione e iniezione di app esterne (SDK interfaccia di amministrazione)</td>
            <td>Iniezione in app esterna (SDK interfaccia utente amministratore)</td>
        </tr>
        <tr>
            <td>Tema Admin personalizzabile</td>
            <td>Framework tematico estensibile</td>
            <td>Nessun framework di temi</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Estensibilità</strong></td>
        </tr>
        <tr>
            <td>Modello di estensibilità</td>
            <td>In-process (personalizzazione PHP) e out-of-process (API, eventi, App Builder)</td>
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
            <td>Attributi personalizzati per entità core e B2B<sup>2</sup></td>
        </tr>
        <tr>
            <td>Tecnologie</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, CLI, HTML, JS, Node</td>
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
            <td>Libreria di stati di App Builder (solo file)<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> funzionalità <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B di base</a>, come la gestione e le quotazioni aziendali, sono disponibili come funzionalità predefinite in SaaS. Tuttavia, le personalizzazioni specifiche del settore possono richiedere considerazioni aggiuntive sull’implementazione.
                <br><br>
                L'estensibilità del modello dati <sup>2</sup> in SaaS supporta <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">l'estensione delle entità principali</a> oltre il prodotto e il cliente, incluse le entità B2B. Tuttavia, i modelli di dati specifici per il settore (ad esempio, attributi specifici per i dealer) potrebbero richiedere considerazioni architetturali aggiuntive.
                <br><br>
                <sup>3</sup> Adobe sta lavorando attivamente all'integrazione di Document DB per soddisfare le esigenze di archiviazione persistente per SaaS. Attualmente, le implementazioni che richiedono lo storage dei dati a lungo termine possono richiedere il provisioning e la manutenzione di infrastrutture aggiuntive.
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
>- Prendi in considerazione API Mesh per estendere le funzionalità API.
>- Monitora la continua evoluzione della piattaforma Adobe e le nuove versioni di funzionalità.
>- Valuta i requisiti del modello dati specifici del settore in base alle opzioni di estensibilità disponibili.
>- È consigliabile adottare [Servizi di merchandising basati su visualizzazioni catalogo e criteri](../optimizer/setup/catalog-view.md).
