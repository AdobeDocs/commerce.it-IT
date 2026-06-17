---
title: Risoluzione dei problemi relativi a  [!DNL Adobe Commerce Optimizer Connector]
description: Diagnosticare e risolvere il comportamento imprevisto in [!DNL Adobe Commerce Optimizer Connector]  causato da configurazione errata o interpretazione errata dei risultati di sincronizzazione.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 0%

---


# Risoluzione dei problemi relativi a [!DNL Adobe Commerce Optimizer Connector]

In questa pagina sono descritti i comportamenti che è possibile osservare durante l&#39;utilizzo di [!DNL Adobe Commerce Optimizer Connector] che sono in genere causati da una configurazione errata o da un&#39;interpretazione errata dei risultati di sincronizzazione. Utilizza le descrizioni di seguito per identificare la causa principale e applicare la risoluzione appropriata.

## Lo stato del feed indica &quot;Completato&quot;, ma i dati non sono visibili in [!DNL Adobe Commerce Optimizer]

**Problema:** la pagina **[!UICONTROL Data Feed Sync Status]** riporta una sincronizzazione riuscita, ma prodotti, prezzi e così via non vengono visualizzati come previsto in [!DNL Adobe Commerce Optimizer].

**Causa:** Uno stato di feed corretto indica che i dati sono stati accettati dall&#39;endpoint di acquisizione, non che la propagazione sia stata completata tramite [!DNL Adobe Commerce Optimizer]. La propagazione può richiedere diversi minuti dopo l’acquisizione.

**Soluzione:**

- Attendere alcuni minuti e aggiornare la visualizzazione [!DNL Adobe Commerce Optimizer].
- Verificare che l&#39;ID tenant configurato in [!DNL Adobe Commerce] corrisponda all&#39;ambiente [!DNL Commerce Optimizer] che si sta controllando.
- Verificare che l&#39;[origine catalogo](../../optimizer/setup/catalog-sources.md) (codice visualizzazione archivio) o il listino prezzi dedicato corretto sia selezionato in [!DNL Commerce Optimizer].

## Prodotti mancanti nel catalogo esportato

**Problema:** alcuni prodotti non vengono visualizzati in [!DNL Adobe Commerce Optimizer] dopo una sincronizzazione completa del catalogo.

**Causa:** Se durante l&#39;esportazione i prodotti non superano la convalida, vengono omessi dalla sincronizzazione. I prodotti disabilitati o non visibili nel catalogo non verranno restituiti dall’API dei prodotti.

**Soluzione:**

- Conferma che i prodotti interessati siano assegnati al sito Web e alla vista store utilizzati come origine del catalogo.
- Verifica che i prodotti siano abilitati e impostati su una visibilità che includa le inserzioni nel catalogo.
- Rivedi i dettagli di errore per elemento per il feed del catalogo in **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

## Prezzi errati o mancanti in [!DNL Adobe Commerce Optimizer]

**Problema:** i prodotti vengono visualizzati in [!DNL Adobe Commerce Optimizer] ma non visualizzano alcun prezzo restituito con [prodotti GraphQL query](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} oppure il prezzo non corrisponde a quello configurato in [!DNL Adobe Commerce].

**Causa:** Il feed del listino prezzi utilizza un ambito mappato a un sito Web e a un gruppo di clienti specifici. Una configurazione errata della [vista catalogo](../../optimizer/setup/catalog-view.md) può causare prezzi mancanti o errati.

**Soluzione:**

- Verifica che il sito web sia configurato per la sincronizzazione nella configurazione di esportazione del connettore. Consulta [Personalizzare la configurazione di esportazione dei dati](../get-started.md#customize-the-commerce-scopes-export-configuration).
- Verificare che l&#39;ID del listino prezzi utilizzato in [!DNL Commerce Optimizer] sia presente nella configurazione della [visualizzazione catalogo](../../optimizer/setup/catalog-view.md){target="_blank"} utilizzata per eseguire la query prodotti.

## I dati in [!DNL Adobe Commerce Optimizer] sono stati sovrascritti o modificati in modo imprevisto dopo la sincronizzazione

**Problema:** le modifiche ai dati applicate direttamente in [!DNL Adobe Commerce Optimizer] da un sistema esterno (ad esempio un PIM o un ERP) vengono perse o ripristinate dopo che il connettore ha eseguito una sincronizzazione.

**Causa:** Quando sistemi diversi da [!DNL Adobe Commerce] scrivono direttamente in [!DNL Adobe Commerce Optimizer], ad esempio un sistema PIM o un altro sistema esterno, possono verificarsi conflitti di dati. Il connettore sincronizza i dati *in un modo*, da [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer], e non sincronizza le modifiche in [!DNL Adobe Commerce]. Di conseguenza, i dati scritti direttamente in [!DNL Adobe Commerce Optimizer] non vengono riflessi in [!DNL Adobe Commerce] e possono essere sovrascritti durante una sincronizzazione successiva.


**Soluzione:**

Invece di scrivere le modifiche del catalogo direttamente in [!DNL Adobe Commerce Optimizer], utilizza [livelli catalogo](../../optimizer/setup/catalog-layer.md){target="_blank"} per applicare le modifiche al di fuori di [!DNL Adobe Commerce]. I livelli del catalogo consentono ai sistemi esterni di arricchire o sostituire i dati del catalogo in [!DNL Adobe Commerce Optimizer] senza creare conflitti con la sincronizzazione del connettore.

## Risoluzione dei problemi relativi a [!DNL SaaS Data Export] problemi comuni

Per i problemi relativi a [!DNL SaaS Data Export] sottostante che possono interessare il connettore, vedi [Scenari di risoluzione dei problemi per  [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md).
