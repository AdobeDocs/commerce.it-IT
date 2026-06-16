---
title: Configurare AEM Assets per Commerce Optimizer
description: Scopri come configurare l'integrazione di AEM Assets per  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 2cc7b70a6923687c74fe3f4b88448eaada6d16af
workflow-type: tm+mt
source-wordcount: '1453'
ht-degree: 0%

---


# Configura AEM Assets per [!DNL Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Applicabile solo ai progetti Adobe Commerce Optimizer."}

L&#39;integrazione di AEM Assets per [!DNL Adobe Commerce Optimizer] consente ai commercianti di utilizzare AEM Assets come soluzione centralizzata per la gestione delle risorse digitali per le immagini dei prodotti. Questa guida descrive la configurazione specifica di [!DNL Commerce Optimizer].

A differenza di Adobe Commerce (PaaS) o [!DNL Adobe Commerce as a Cloud Service], [!DNL Commerce Optimizer] non dispone di un&#39;interfaccia utente di configurazione amministratore. Per abilitare l&#39;integrazione, creare un ticket di supporto con i dettagli di [!DNL Adobe Commerce Optimizer] e AEM Assets. Il supporto Adobe configura l’integrazione e registra il tenant con il servizio di integrazione Assets.

**Prepara AEM Assets prima di inviare il ticket.** La registrazione del tenant presuppone che il lato AEM sia utilizzabile per Commerce. Ad esempio, dopo aver distribuito il pacchetto AEM Commerce `assets-commerce` in modo che i metadati e gli eventi funzionino come descritto. **L&#39;apertura di un ticket prima della configurazione di AEM può ritardare l&#39;onboarding.**

Il diagramma seguente offre una panoramica della sincronizzazione dei prodotti tra [!DNL Adobe Commerce Optimizer] e l&#39;integrazione di AEM Assets.

![Flusso da AEM Assets a [!DNL Commerce Optimizer]](../assets/aco-asset-sync-architecture.png){width="700"}

Questa integrazione ha due flussi principali:

* **Da AEM Assets**: quando una risorsa viene approvata, rifiutata o rimossa, l&#39;evento passa attraverso la pipeline di Adobe al servizio di integrazione di Assets. Il servizio associa le risorse ai prodotti utilizzando `match-by-SKU` (basato su metadati) o un [programma di corrispondenza personalizzato (App Builder)](../synchronize/custom-match.md){target=_blank}, quindi invia i mapping `product-asset` a Commerce Optimizer, dove vengono memorizzati come livelli di prodotto.

* **Da[!DNL Adobe Commerce Optimizer]**: quando un prodotto viene aggiornato in [!DNL Commerce Optimizer], l&#39;evento passa attraverso la pipeline di Adobe al servizio di integrazione di Assets. Il servizio sincronizza eventuali mapping di risorse corrispondenti con [!DNL Adobe Commerce Optimizer].

## Prerequisiti

Prima di configurare l’integrazione, assicurati di disporre di:

* Un&#39;istanza [!DNL Adobe Commerce Optimizer] attiva con adesione a Product Visuals o qualsiasi licenza AEM Assets con Dynamic Media.
* Accesso a un ambiente AEM Assets as a Cloud Service.
* Sia [!DNL Commerce Optimizer] che AEM Assets nella stessa organizzazione Adobe IMS.
* Dynamic Media con OpenAPI abilitato nell&#39;ambiente AEM Assets (consulta [Configurare il progetto AEM Assets](configure-aem.md#prerequisites) per i passaggi di abilitazione).

## Configurare prima AEM Assets

Completa i passaggi di AEM Assets **prima** di [aprire un ticket di supporto](#onboarding) per la registrazione del tenant. Il modello di installazione corrisponde a Adobe Commerce as a Cloud Service. Vedere [Configurare il progetto AEM Assets per il supporto dei metadati di Commerce](configure-aem.md).

### Passaggio 1: distribuire il pacchetto AEM Commerce

Installa e distribuisci il pacchetto `assets-commerce` nel progetto AEM in modo che siano disponibili schemi di metadati, eventi e interfaccia utente di Commerce.

Completare la procedura completa in [Installare il pacchetto `assets-commerce`](configure-aem.md#step-1-install-the-assets-commerce-package). Prima di aprire un ticket di supporto, effettua le seguenti operazioni:

1. Clona l&#39;archivio Git di Cloud Manager e copia il codice dell&#39;[archivio Commerce di AEM Assets](https://github.com/ankumalh/assets-commerce) nel progetto.

1. In tutti i file `filter.xml` e `pom.xml` del progetto, sostituisci tutte le occorrenze di &lt;my-app> con il nome dell&#39;app.

1. Eseguire il commit, il push, l&#39;esecuzione della pipeline di distribuzione e verificare che la scheda **[!UICONTROL Commerce]** sia visualizzata nelle proprietà della risorsa.

Consulta [Installare il pacchetto `assets-commerce`](configure-aem.md#step-1-install-the-assets-commerce-package) per le schermate di Cloud Manager, i passaggi della pipeline e la risoluzione dei problemi se manca la scheda **[!UICONTROL Commerce]**.

### Passaggio 2: abilitare Dynamic Media con OpenAPI

Dynamic Media con funzionalità OpenAPI deve essere abilitato nell’ambiente AEM Assets. I percorsi self-service (ad esempio Cloud Manager per i visualizzatori di prodotto) e le route di supporto Adobe sono descritti in [Configura il progetto AEM Assets](configure-aem.md#prerequisites).

### Passaggio 3: applicare i metadati di Commerce e approvare le risorse

Aggiungi metadati Commerce alle immagini del prodotto in AEM Assets. Per le definizioni dei campi, vedi [Contenuto del pacchetto AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents).

La risorsa deve essere in uno stato **approvato** per poter attivare la sincronizzazione dati. Il salvataggio dei metadati da solo non attiva l&#39;evento.

### Passaggio 4: facoltativo — configurare un profilo di metadati Commerce

Se scegli di utilizzare i profili di metadati di AEM per semplificare l&#39;authoring, configurali **dopo** che il pacchetto viene distribuito e il tuo team comprende i campi Commerce obbligatori; lo stesso pattern facoltativo di **Configurare il progetto AEM Assets**.

Consulta [Configurare un profilo di metadati](configure-aem.md#step-2-optional-configure-a-metadata-profile).

## Limitazioni

L&#39;integrazione di [!DNL Commerce Optimizer] presenta le seguenti limitazioni:

### Vincoli relativi ai livelli

Leggi questa sezione **prima** di scegliere un nome di livello catalogo nel ticket di supporto. La scelta o la condivisione di livelli senza questo contesto è una causa frequente di casi di supporto prevenibili.

**Utilizza un livello dedicato per il contenuto di AEM Assets.** I payload inviati da AEM Assets popolano un catalogo Commerce Optimizer **layer**. I valori in tale livello **sovrascrivono** gli attributi del catalogo di base in cui vengono forniti i campi. Quando l’integrazione omette un campo nel payload, i valori corrispondenti in quel livello possono essere sovrascritti con valori vuoti. La condivisione di un livello con flussi di lavoro Commerce non correlati, o il riutilizzo di un livello che già memorizza dati di prodotto non AEM-Assets, può causare **perdita di dati non intenzionale** o sovrascritture confuse. Pianifica la scelta del livello **prima** di aprire il ticket di supporto e riservane il nome (ad esempio **`AEM-Assets`** predefinito) principalmente per la sincronizzazione delle immagini del prodotto basata su AEM.

>[!IMPORTANT]
>
>L&#39;integrazione supporta **un&#39;origine catalogo per tenant**: una singola lingua e **un livello denominato**. Al momento, la configurazione di più livelli AEM-Assets o di più impostazioni locali per lo stesso tenant non è supportata.

### Altri vincoli

* **Solo immagini**: l&#39;integrazione non supporta video o altri tipi di file multimediali in questa fase.
* **Nessuna immagine categoria**: la sincronizzazione immagine categoria non è disponibile. Le immagini delle categorie da AEM Assets per il selettore Assets (inserimento nell’interfaccia utente) non sono supportate.
* **Nessuna distinzione tra più siti**: l&#39;integrazione non gestisce più siti. Un&#39;immagine associata a un prodotto viene visualizzata allo stesso modo su tutti i canali e i criteri.
* **Posizione/ordinamento immagine**: la posizione e l&#39;ordinamento delle immagini non sono supportati.
* **Il prodotto deve esistere**: se il prodotto non esiste in [!DNL Commerce Optimizer], il livello non viene creato per la mappatura prodotto-risorsa.

## Onboarding

Per integrare AEM Assets con [!DNL Commerce Optimizer], è necessario [creare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

Il supporto Adobe utilizza le informazioni contenute nel ticket per registrare il tenant con Assets Integration Service e configurare l’integrazione.

Prima di inviare il ticket, assicurati di aver completato [la configurazione di AEM Assets](#configure-aem-assets-first).

Includi le seguenti informazioni nel ticket di supporto:

* **[!DNL Adobe Commerce Optimizer]ID tenant** (ID istanza) trovato nell&#39;URL [!DNL Commerce Optimizer] o nell&#39;interfaccia utente di Commerce Cloud Manager.
* **ID programma AEM**.
* **ID ambiente AEM**.
* **Regola corrispondente**: corrisponde per SKU o [corrispondenza esterna (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Livello**: il nome del livello del catalogo con cui registrare il tenant (vedi **Vincoli relativi ai livelli**). Specificare un nome personalizzato solo se intenzionale. In caso contrario, verrà utilizzato il nome predefinito **`AEM-Assets`**.
* **Impostazioni locali**: le impostazioni locali di origine del catalogo con cui registrare il tenant (ad esempio, `en-US`). Deve corrispondere alle impostazioni internazionali utilizzate nella vista catalogo e nei dati del catalogo prodotti.

Dopo che il supporto Adobe elabora il ticket, l’integrazione viene configurata e il tenant viene registrato con il servizio di integrazione Assets.

Una volta completato l’onboarding:

1. **Registrazione con Assets Integration Service**: il tenant [!DNL Commerce Optimizer] è registrato con Assets Integration Service utilizzando l&#39;ID tenant [!DNL Adobe Commerce Optimizer], l&#39;ID programma AEM, l&#39;ID ambiente AEM, la regola corrispondente, le impostazioni locali e il nome del livello forniti nel ticket.

1. **Sottoscrizione evento**: Assets Integration Service si abbona a:

   * Eventi AEM Assets (risorsa approvata, aggiornata, rimossa)
   * [!DNL Commerce Optimizer] eventi catalogo (prodotto creato, aggiornato)

Configura la [vista catalogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) in modo che in vetrina e nelle API vengano visualizzati i dati immagine basati su AEM:

* **Origine del catalogo (impostazioni locali)** - Selezionare le stesse impostazioni locali specificate nel ticket di supporto (ad esempio **`en-US`**). L’integrazione registra una lingua per tenant; una mancata corrispondenza impedisce la visualizzazione delle immagini sincronizzate nella vista catalogo prevista.
* **Livello catalogo** - Assegna il livello **`AEM-Assets`** (o il nome del livello personalizzato dal ticket) a tale vista catalogo.

Se le impostazioni locali o il livello non sono assegnati correttamente, è possibile che i dati dell&#39;immagine **non vengano visualizzati** o che si comportino in modo imprevisto, anche se la sincronizzazione è riuscita a monte.

## Ssincronizzazione

Una volta configurata, l&#39;integrazione sincronizza automaticamente `product-asset` mappature.

Per ulteriori informazioni, vedere [Corrispondenza automatica personalizzata](../synchronize/custom-match.md).

### Esempio di flusso di lavoro Corrispondenza per SKU

Un flusso tipico quando si aggiunge una risorsa esistente a un nuovo prodotto:

1. Crea il prodotto in [!DNL Commerce Optimizer] (tramite API o acquisizione dati). Il prodotto può esistere inizialmente senza immagini.

1. In AEM Assets, apri la risorsa da mappare sul prodotto.

1. Aggiungi lo SKU del prodotto ai metadati **commerce:skus** e assegna i ruoli immagine (ad esempio, `thumbnail`, `image`).

1. Approva la risorsa per la consegna. Questo attiva l’evento elaborato da Assets Integration Service.

1. Il servizio di integrazione di Assets invia la mappatura prodotto-immagine a [!DNL Commerce Optimizer]. Il prodotto in [!DNL Commerce Optimizer] è stato aggiornato con le immagini della risorsa.

1. Verifica che l’immagine sia visibile. Attendere il completamento della sincronizzazione (in genere entro pochi minuti), quindi controllare il prodotto nell&#39;interfaccia utente [!DNL Commerce Optimizer] (ad esempio, Sincronizzazione dati o visualizzazione catalogo) oppure eseguire una query sulle API storefront (Catalog Service, Live Search, API Storefront GraphQL) per confermare che l&#39;immagine è stata restituita.

## Gestione ruolo immagine

Quando un prodotto dispone di più risorse che utilizzano lo stesso ruolo immagine (ad esempio, due risorse con il ruolo `thumbnail`), l&#39;integrazione assicura che solo una risorsa mantenga tale ruolo per evitare ruoli duplicati nel livello [!DNL Commerce Optimizer] e comportamenti imprevisti nella vetrina.

**Comportamento:** Quando viene inviato un aggiornamento da AEM Assets, la risorsa aggiornata più di recente riceve il ruolo immagine (ad esempio, `thumbnail`) e il ruolo viene rimosso dalla risorsa precedente che lo aveva. Questo impedisce la visualizzazione di ruoli immagine duplicati nella vetrina.

## Altri argomenti correlati

* [Visualizzazioni prodotto](../../optimizer/setup/product-visuals.md)
* [Configurare il progetto AEM Assets](configure-aem.md)
* [Corrispondenza automatica personalizzata](../synchronize/custom-match.md)
* [Panoramica dell’integrazione di AEM Assets](../overview.md)
