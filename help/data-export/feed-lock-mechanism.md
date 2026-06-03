---
title: Meccanismo di blocco dei feed per l’esportazione di dati SaaS
description: Scopri come [!DNL SaaS Data Export] utilizza i blocchi dei feed per evitare conflitti nelle operazioni di sincronizzazione e proteggere l'integrità dei dati durante gli aggiornamenti simultanei dei feed.
role: Admin, Developer
feature: Services
source-git-commit: cfa1002653bf66afd3f6b8484b33076adcd1b7d4
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Meccanismo di blocco dei feed per l’esportazione di dati SaaS

L&#39;estensione [!DNL SaaS Data Export] utilizza un meccanismo di blocco del feed per evitare race condition quando più processi tentano di sincronizzare lo stesso feed contemporaneamente. Ciò può verificarsi, ad esempio, quando una risincronizzazione attivata da cron si sovrappone a una chiamata CLI `saas:resync` manuale.

## Funzionamento del blocco del feed

Ogni operazione di sincronizzazione dei feed, sia attivata da un processo cron che da una chiamata CLI `saas:resync` manuale, segue la stessa sequenza:

1. Il processo tenta di acquisire il blocco del feed. Il tentativo di blocco non è di blocco e ritorna immediatamente se il blocco è già bloccato da un altro processo.
1. Se il blocco è **non disponibile**, l&#39;operazione [viene ignorata e registrata].

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
>Per informazioni generali sul formato del registro e sui tipi di operazioni registrati in `commerce-data-export.log`, vedere [Esaminare i registri e risolvere i problemi](troubleshooting-logging.md).

## Ulteriori informazioni su questo argomento

- [Sincronizzare i dati con l’esportazione di dati SaaS](data-synchronization.md)
- [Sincronizzare i feed utilizzando Commerce CLI](data-export-cli-commands.md)
- [Configurare il provider di blocchi](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
