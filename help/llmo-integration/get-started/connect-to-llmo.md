---
title: Connetti [!DNL Adobe Commerce] a [!DNL Adobe LLM Optimizer]
description: Abilita i servizi Commerce richiesti, configura la connessione LLM Optimizer, convalida l’accesso al catalogo e conferma la preparazione del tenant prima di rivedere le opportunità o distribuire gli aggiornamenti.
role: Admin, User
recommendations: noCatalog
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Connetti [!DNL Adobe Commerce] a [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>L’accesso a questa integrazione è limitato. Per ulteriori informazioni, contatta il tuo Technical Account Manager.

In questo articolo viene illustrato come connettere il catalogo [!DNL Adobe Commerce] disponibile a LLM Optimizer.

>[!NOTE]
>
>Questo articolo si concentra sul lato Commerce dell’integrazione. Per informazioni generali su LLM Optimizer, consulta la [documentazione del prodotto LLM Optimizer](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/home).

## Abilita servizi Commerce richiesti {#enable-commerce-services}

Rivolgiti all’amministratore di Commerce o al partner di implementazione per ottenere i seguenti risultati:

- I dati del catalogo che LLM Optimizer deve leggere sono **esportati o sincronizzati** in base all&#39;architettura (compresi eventuali connettori o utilità di esportazione dati SaaS nella distribuzione).
- L&#39;accesso API, le credenziali e gli URL dell&#39;ambiente (sandbox e produzione) corrispondono al **tenant** che intendi utilizzare in LLM Optimizer.

## Configurare la connessione Commerce in LLM Optimizer {#configure-commerce-connection}

**Per configurare la connessione Commerce:**

1. Nell&#39;interfaccia utente [!DNL Adobe LLM Optimizer], apri **Configurazione cliente**, quindi seleziona la scheda **[!UICONTROL Commerce]**.

   ![Configurazione Commerce nella scheda Configurazione cliente](../assets/llmo-commerce-config.png)

1. Fare clic su **[!UICONTROL Add Store View]** per creare una nuova riga o espandere una voce della visualizzazione archivio esistente per modificarla.
1. Immettere **[!UICONTROL Store View URL]** (obbligatorio).

   Utilizzare l&#39;URL storefront per la visualizzazione archivio, inclusi eventuali prefissi delle impostazioni locali o del percorso, ad esempio `https://brand.example.com/` o `https://brand.example.com/fr/`.

1. Immetti **[!UICONTROL Environment ID]** (obbligatorio): l&#39;identificatore dell&#39;ambiente Adobe Commerce a cui LLM Optimizer deve connettersi.
1. Immettere **[!UICONTROL Website Code]**, **[!UICONTROL Store Code]** e **[!UICONTROL Store View Code]** (obbligatorio).

   Questi valori devono corrispondere ai codici presenti nell&#39;amministratore di Commerce per la visualizzazione del sito Web, dello store e dello store a cui ci si connette.

1. Facoltativo: immettere **[!UICONTROL Host Name]** con il nome host dell&#39;istanza di Commerce (ad esempio, `www.example.com`) se il valore è diverso dall&#39;URL.
1. Immetti **[!UICONTROL Adobe Commerce Endpoint]**: l&#39;URL di base dell&#39;istanza Adobe Commerce utilizzata per l&#39;accesso API.
1. Immetti o incolla **[!UICONTROL API Key]** utilizzato per autenticare le richieste alle API Commerce.

   Fai clic su **[!UICONTROL Copy]** accanto al campo se devi copiare la chiave altrove in modo sicuro.

1. Fare clic su **[!UICONTROL Save]** per archiviare la configurazione.

Dopo il salvataggio, attendere il completamento di qualsiasi **sincronizzazione iniziale** o processo di convalida prima di basarsi sui risultati del catalogo o del controllo di audit per la visualizzazione dell&#39;archivio.

Per rimuovere una configurazione della visualizzazione archivio, aprire la voce e fare clic su **[!UICONTROL Delete]**.

### Descrizioni dei campi {#commerce-connection-fields}

| Campo | Descrizione |
| --- | --- |
| URL visualizzazione store | L’URL pubblico della visualizzazione archivio LLM Optimizer deve essere considerato nell’ambito dei flussi di lavoro di catalogo e controllo. |
| ID ambiente | Identificatore dell’ambiente Commerce (dal cloud, dalla documentazione di implementazione o dall’amministratore, se applicabile). |
| Codice del sito web | Commerce **[!UICONTROL Website Code]** per il sito Web proprietario del catalogo. |
| Codice store | Commerce **[!UICONTROL Store Code]** per l&#39;archivio in tale sito Web. |
| Codice visualizzazione store | Commerce **[!UICONTROL Store View Code]** per la visualizzazione archivio, ad esempio `default`. |
| Nome host | Nome host della vetrina o dell’istanza Commerce quando il modulo lo richiede in aggiunta ad altri URL. |
| Endpoint Adobe Commerce | URL dell’istanza utilizzato da LLM Optimizer per raggiungere le API Commerce. |
| Chiave API | Chiave segreta per l’autenticazione API; trattala come qualsiasi credenziale di produzione. |

## Conferma preparazione tenant e ambiente {#confirm-tenant-readiness}

- Verificare che i progetti **sandbox** connessi non siano combinati con i dati di Commerce **production**, a meno che ciò non sia intenzionale.
- Allinea **i ruoli utente** in Experience Cloud e Commerce in modo che le persone che approvano le azioni di distribuzione dispongano delle autorizzazioni appropriate per entrambi i lati.

## Passaggi successivi {#next-steps}

[Utilizza LLM Optimizer con Adobe Commerce](use-llmo-with-commerce.md) per esaminare le opportunità, distribuire gli aggiornamenti del catalogo e comprendere il comportamento di sostituzione.
