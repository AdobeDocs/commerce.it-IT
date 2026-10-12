---
title: Risoluzione dei problemi di [!DNL App Management]
description: Risolvi i problemi comuni relativi all’associazione e alla configurazione delle app.
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%
---
# Risoluzione dei problemi di [!DNL App Management]

Utilizza le seguenti soluzioni per risolvere i problemi comuni relativi all’associazione e alla configurazione delle app.

## L’app non viene visualizzata

Se l’app non viene visualizzata nell’elenco dopo la distribuzione, verifica i passaggi seguenti:

1. Verifica che l’app sia implementata e disponibile all’interno dell’organizzazione.

1. Conferma di aver effettuato l’accesso all’organizzazione Adobe corretta in Developer Console.

1. Assicurati che l’app sia pronta per la connessione (lo sviluppatore o il partner dell’app può confermare).

Se l&#39;app non viene ancora visualizzata, contatta lo sviluppatore dell&#39;app o consulta la documentazione di [Commerce Extensibility [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} per informazioni tecniche.

## Sincronizzazione ambito non riuscita

Se la sincronizzazione dell&#39;ambito non riesce durante l&#39;associazione di un&#39;app, provare a eseguire le operazioni seguenti:

1. Verifica che l’istanza di Commerce sia accessibile e online.

1. Verifica che le credenziali API siano valide e che dispongano delle autorizzazioni corrette.

1. Prova a eseguire la sincronizzazione manualmente da **[!UICONTROL Manage Scopes]** nella configurazione dell&#39;app.

## Configurazione non salvata

Se le modifiche alla configurazione non vengono salvate, provare a eseguire le operazioni seguenti:

1. Verifica che tutti i campi obbligatori siano compilati e validi.

1. Assicurati di disporre delle autorizzazioni corrette per modificare la configurazione dell’app.

1. Prova ad aggiornare la pagina e a salvare di nuovo.

Se il problema persiste, controlla la console del browser per individuare eventuali errori o contatta lo sviluppatore dell’app.

Per la risoluzione dei problemi tecnici, vedere [Estensibilità Commerce [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} per ulteriori informazioni.
