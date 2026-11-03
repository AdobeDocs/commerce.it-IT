---
title: Risoluzione dei problemi di [!DNL App Management]
description: Risolvi i problemi più comuni relativi all’associazione, all’installazione, alla configurazione e agli aggiornamenti delle app.
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
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%
---
# Risoluzione dei problemi di [!DNL App Management]

Utilizza le seguenti soluzioni per risolvere i problemi più comuni relativi all’associazione, all’installazione, alla configurazione e agli aggiornamenti delle app.

## Prima di contattare il provider di app

Segui i passaggi per il tuo problema qui sotto. Se hai bisogno dell’aiuto dello sviluppatore o del provider di app, raccogli le seguenti informazioni:

* Nome app e versione installata, se disponibile da **[!UICONTROL Manage]** > **[!UICONTROL Details]** nella scheda dell&#39;app.
* Istanza Commerce interessata e organizzazione Adobe.
* Operazione non riuscita, ad esempio installazione o aggiornamento, e passaggio non riuscito.
* Viene visualizzato un messaggio di errore e una schermata dell’errore, se disponibile.
* Ora approssimativa dell’errore, compreso il fuso orario.
* Eventuali tentativi e i relativi risultati.

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

## Installazione non riuscita

Mantenere aperta la pagina di installazione senza aggiornamento fino al termine dell&#39;installazione. La chiusura o l&#39;aggiornamento potrebbe impedire il corretto completamento dell&#39;installazione.

Se l&#39;installazione segnala un errore:

1. Annotare l&#39;elemento non riuscito ed eventuali messaggi di errore visualizzati.

1. Verifica di aver completato le istruzioni di preinstallazione dell’app.

1. Chiedi allo sviluppatore dell’app di controllare il passaggio non riuscito e correggere la causa prima di riprovare l’installazione.

In caso di errore durante l&#39;installazione, è possibile che alcune modifiche rimangano applicate. Quando si ritenta l&#39;installazione, i passaggi personalizzati registrati come completati vengono ignorati; i passaggi non riusciti o interrotti possono essere eseguiti nuovamente. Chiedi allo sviluppatore di verificare la disponibilità di risorse create dall’esecuzione parziale.

## Aggiornamento non riuscito

Un aggiornamento non riuscito può lasciare applicate alcune operazioni. Non annullare l&#39;associazione e reinstallare l&#39;app come passaggio di ripristino di routine, poiché l&#39;annullamento dell&#39;associazione rimuove la configurazione e può eseguire script di pulizia distruttivi.

1. Identifica il passaggio non riuscito e registra eventuali messaggi di errore visualizzati.

1. Chiedi al tuo sviluppatore di app di esaminare i registri, verificare se sono già state apportate modifiche a Commerce o a risorse esterne e correggere la causa.

1. In [!DNL App Management], selezionare **[!UICONTROL Retry Upgrade]**. Questa azione è disponibile per le modalità di aggiornamento manuale e automatico.

Ogni nuovo tentativo crea un nuovo piano dallo stato corrente. I passaggi di installazione personalizzati registrati come completati sono stati ignorati; i passaggi non riusciti o interrotti possono essere eseguiti nuovamente. In modalità automatica, la nuova distribuzione dell’app attiva anche un altro tentativo di aggiornamento.

Se i tentativi ripetuti non vanno a buon fine, chiedi allo sviluppatore dell’app di mantenere gli ID esecuzione o tentativo ed eventuali ID di attivazione dell’esecuzione per la risoluzione dei problemi. Per i comandi di stato, la cronologia dei tentativi e i registri di runtime, vedere [Riprovare un aggiornamento non riuscito](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"} nella documentazione per gli sviluppatori.

## Le risorse rimangono dopo un aggiornamento

Se si rimuove un passaggio di installazione personalizzato dalla configurazione di un’app, lo script di disinstallazione non viene eseguito o non vengono rimosse le risorse create. Il piano di aggiornamento avvisa che per il passaggio rimosso non viene eseguito alcuno script e che il passaggio non viene visualizzato nella schermata di avanzamento o nei dettagli dell’app dopo l’aggiornamento.

Chiedi allo sviluppatore dell’app di confermare se le risorse sono ancora necessarie e di fornire una migrazione di pulizia quando necessario. Consulta [Aggiornare un&#39;app](manage-app.md#upgrade-an-app) per il flusso di lavoro dell&#39;amministratore.

Per la risoluzione dei problemi tecnici, vedere [Estensibilità Commerce [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} per ulteriori informazioni.
