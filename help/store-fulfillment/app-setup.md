---
title: Configurazione app
description: Imposta l'app  [!DNL Store Assist]  per gestire i flussi di lavoro e i processi di evasione del punto vendita end-to-end per l'acquisto online e il ritiro degli ordini del punto vendita.
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Configurazione dell’app

Store Assist è un&#39;app di piattaforma per la realizzazione di contenuti come servizio (FaaS) basata su Walmart Commerce Technologies. L&#39;app fornisce funzionalità di evasione in-store per gestire gli ordini [!DNL buy online, pick up in store] (BOPIS). Con Store Assist, i dipendenti del negozio possono vedere quali articoli sono stati ordinati dai clienti, scegliere gli articoli corretti più rapidamente e impostare ordini evasi per la consegna in-store o con prelievo a blocchi ai clienti.

L&#39;app Store Assist riceve tutte le informazioni relative agli ordini e ai clienti, dai dettagli degli ordini per prelevare i tempi di consegna, e rende i dati disponibili online per gli associati dello store, attraverso i dispositivi mobili. L&#39;app include [!UICONTROL Pick], [!UICONTROL Stage], [!UICONTROL Handoff] e [!UICONTROL Orders] moduli per aiutare gli associati dello store a svolgere attività di evasione come le seguenti:

- Assegnare date e ore di consegna dell&#39;ordine.
- Ricevi notifiche dai clienti quando arrivano per il ritiro dell’ordine.
- Fase degli ordini per la consegna ai clienti.
- Tenere traccia dello stato dell&#39;ordine per tutti gli ordini nelle ubicazioni di magazzino assegnate.

>[!NOTE]
>
>Ulteriori informazioni sull&#39;app Store Assist consultando l&#39;argomento [Flussi di lavoro per l&#39;esecuzione di Store Assist](store-assist-modules.md).

## Configurare l’app Store Assist

L&#39;app Store Assist richiede due tipi di configurazione:

- Impostazioni di Adobe Commerce Admin System per [gestire gli account utente, i ruoli utente, le autorizzazioni per le risorse](user-setup.md) e [la creazione di automobili e le selezioni di modelli disponibili per i clienti durante il processo di archiviazione](check-in-experience-setup.md).

- Impostazioni di configurazione front-end per personalizzare l’interfaccia dell’app Store Assist e altre impostazioni, tra cui:

   - **Assegna il marchio all&#39;app Store Assist**. Personalizza l&#39;interfaccia utente dell&#39;app con il logo e i colori della tua azienda.

   - **Aggiorna le istruzioni predefinite**—Personalizza le istruzioni nei moduli Prelievo assistenza store, Staging, Handoff e Ordine per guidare gli associati al negozio attraverso ogni passaggio del flusso di lavoro di evasione per la tua azienda.

   - **Localizzazione** - Seleziona la lingua disponibile per l&#39;app. Scegliere il formato di data e ora e selezionare le unità di misura predefinite e la valuta predefinita.

   - **Tempo di inattività** - Specifica per quanto tempo l&#39;app deve essere inattiva prima della disconnessione.

   - **Annullamento dall&#39;archivio**—Specificare se gli ordini possono essere annullati dall&#39;archivio e quali ruoli dispongono delle autorizzazioni di annullamento

   - **Finestra di pulizia dell&#39;ordine**—Specificare quanto tempo è trascorso dal [Lead time di prelievo stimato](enable-general.md#delivery-method-title-configuration) per cui un ordine prelevato rimane nella gestione temporanea prima di essere riassortito—ad esempio, tre giorni. Il valore predefinito è sette giorni. Se questa configurazione è attivata, l&#39;ordine viene automaticamente annullato alla scadenza di questo periodo di tempo. Gli articoli vengono riassortimenti e il commerciante riceve un’e-mail di cancellazione.

   - Personalizza tutto nelle istruzioni dell’app (prelievo, staging, consegna).

   - **Notifiche di prelievo**—Specificare se inviare una notifica push per avviare il processo di prelievo dopo che un cliente ha effettuato un ordine.

   - **Archivia notifiche**—Specificare se inviare una notifica push durante il processo di archiviazione per i prelievi degli ordini- dopo il check-in, dopo che il tempo di attesa del cliente supera un determinato periodo di tempo. Oppure, disattiva la notifica.

   - **Processo di consegna** - Abilita i processi facoltativi quando l&#39;associato store consegna l&#39;ordine al cliente, ad esempio richiede una firma del cliente o richiede all&#39;associato di controllare l&#39;ID cliente.

   - **Abilita il rifiuto dell&#39;articolo al momento della consegna**. Consenti ai clienti di restituire o annullare gli articoli dell&#39;ordine durante la consegna dell&#39;ordine.

  Collabora con il team di Walmart Commerce Technologies Client Services per completare la configurazione front-end per l&#39;app Store Assist.

## Download e installazione dell’app

Dopo che l&#39;app Store Assist è stata configurata, gli associati possono scaricare, installare e accedere all&#39;app Store Assist dai loro dispositivi mobili.

- Verificare che il dispositivo mobile soddisfi i [requisiti hardware e software](solution-requirements.md#store-assist-app-requirements) per la soluzione Store Fulfillment.

- Scarica l&#39;app Store Assist da [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} o [Google Play Store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.

- Per l&#39;accesso, gli Associati archivio richiedono le seguenti informazioni:

   - **[!UICONTROL Company name]** associato all&#39;account Store Assist

   - **Archivia credenziali account Assist**: credenziali nome utente e password per l&#39;account.

  Un amministratore di Adobe Commerce può creare e gestire gli account utente [!DNL Store Assist app] per tutte le posizioni di archivio in cui è abilitata la [selezione in-store](merchant-store-configuration.md#pickup-location-configuration) nelle impostazioni di Admin Stores.
