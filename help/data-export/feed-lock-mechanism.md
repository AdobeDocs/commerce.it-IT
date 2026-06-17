---
title: Meccanismo di blocco dei feed per l’esportazione di dati SaaS
description: Scopri come [!DNL SaaS Data Export] utilizza i blocchi dei feed per evitare conflitti nelle operazioni di sincronizzazione e proteggere l'integrità dei dati durante gli aggiornamenti simultanei dei feed.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# Meccanismo di blocco dei feed per l’esportazione di dati SaaS

L&#39;estensione [!DNL SaaS Data Export] utilizza un meccanismo di blocco del feed per evitare race condition quando più processi tentano di sincronizzare lo stesso feed contemporaneamente. Ciò può verificarsi, ad esempio, quando una risincronizzazione attivata da cron si sovrappone a una chiamata CLI `saas:resync` manuale.

## Funzionamento del blocco del feed

Ogni operazione di sincronizzazione dei feed, sia attivata da un processo cron che da una chiamata CLI `saas:resync` manuale, segue la stessa sequenza:

1. Il processo tenta di acquisire il blocco del feed. Il tentativo di blocco non è di blocco e ritorna immediatamente se il blocco è già bloccato da un altro processo.
1. Se il blocco è **non disponibile**, l&#39;operazione verrà ignorata e registrata.

   Nessun dato viene perso. La successiva esecuzione cron riprende le modifiche in sospeso al termine del processo corrente.
1. Se il blocco è **acquisito**, il processo registra il nome e il PID per scopi diagnostici, quindi esegue la sincronizzazione.
1. Quando la sincronizzazione viene completata o non riesce, il blocco viene rilasciato incondizionatamente in modo che il successivo processo cron pianificato possa procedere normalmente.

Solo un&#39;operazione di sincronizzazione può mantenere il blocco del feed alla volta, indipendentemente dal fatto che sia stato avviato da cron o CLI. Il blocco del feed è implementato tramite `LockManagerInterface` di [!DNL Adobe Commerce]. Il back-end predefinito è MySQL, che utilizza le funzioni `GET_LOCK` e `RELEASE_LOCK`. Per configurare un provider di blocchi diverso, vedere [Configurare il provider di blocchi](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}.

## Messaggi di registro previsti

Il seguente messaggio in `commerce-data-export.log` è normale e non indica un problema:

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

Questo messaggio viene visualizzato quando si tenta di eseguire una sincronizzazione parziale attivata da cron mentre è già in corso una reindicizzazione completa o `saas:resync`. L’operazione saltata non viene persa. Una volta che il processo in esecuzione completa e rilascia il blocco, l’esecuzione successiva del cron rileva e sincronizza eventuali modifiche in sospeso.

>[!NOTE]
>
>Per informazioni generali sul formato del registro e sui tipi di operazioni registrati in `commerce-data-export.log`, vedere [Esaminare i registri e risolvere i problemi](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Sincronizzare i dati con l&#39;esportazione dei dati SaaS](sync-overview.md)
> - [Sincronizzare i feed utilizzando Commerce CLI](data-export-cli-commands.md)
> - [Pipeline di sincronizzazione del connettore](../aco-connector/connector-sync-pipeline.md)
> - [Configurare il provider del blocco](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
