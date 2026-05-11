---
title: Visualizzare e gestire i registri
description: Scopri dove trovare e gestire i registri per l’integrazione di AEM Assets per Commerce.
feature: CMS, Media, Integration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
TQID: https://experienceleague.adobe.com/im5QUgqayCNj9lZfZ-7UvxiUW9NmgHyhVbyBdjjPxAA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 0%

---

# Visualizzare e gestire i registri

L’integrazione di AEM Assets fornisce i seguenti file di registro nell’istanza di Commerce:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Chiedere all&#39;amministratore di sistema di controllare la pianificazione della rotazione dei file di registro per questi registri per evitare che diventino troppo grandi. In alcuni ambienti, i registri ruotano automaticamente; in altri, è necessario configurare manualmente la rotazione dei registri.  Per ulteriori informazioni, vedere i seguenti argomenti:

- Per le installazioni locali di Adobe Commerce, chiedi all&#39;amministratore di sistema di impostare [la rotazione del registro](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=it#server-settings).
- Per i progetti Adobe Commerce su infrastrutture cloud, consulta [Visualizzare e gestire i registri](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=it).
