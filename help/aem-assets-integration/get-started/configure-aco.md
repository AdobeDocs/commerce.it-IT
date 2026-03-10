---
title: Configurare AEM Assets per Commerce Optimizer
description: Scopri come configurare l'integrazione di AEM Assets per  [!DNL Adobe Commerce Optimizer].
feature: CMS, Media, Configuration, Integration
source-git-commit: 7f0970648663331fea2af19b981c4fd3b3aedcaa
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---


# Configura AEM Assets per [!DNL Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Applicabile solo ai progetti Adobe Commerce Optimizer."}

L&#39;integrazione di AEM Assets per [!DNL Adobe Commerce Optimizer] consente ai commercianti di utilizzare AEM Assets come soluzione centralizzata per la gestione delle risorse digitali per le immagini dei prodotti. Questa guida descrive la configurazione specifica di [!DNL Commerce Optimizer].

A differenza di Adobe Commerce (PaaS) o Adobe Commerce as a Cloud Service (ACCS), [!DNL Commerce Optimizer] non dispone di un&#39;interfaccia utente di configurazione amministratore. Per abilitare l&#39;integrazione, creare un ticket di supporto con i dettagli di [!DNL Adobe Commerce Optimizer] e AEM Assets. Il supporto Adobe configura l’integrazione e registra il tenant con il servizio di integrazione Assets.

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
* Dynamic Media con OpenAPI abilitata nell’ambiente AEM Assets.

## Onboarding

Per integrare AEM Assets con [!DNL Commerce Optimizer], è necessario [creare un ticket di supporto](https://experienceleague.adobe.com/it/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket).

Il supporto Adobe utilizza le informazioni contenute nel ticket per registrare il tenant con Assets Integration Service e configurare l’integrazione.

Includi le seguenti informazioni nel ticket di supporto:

* **[!DNL Adobe Commerce Optimizer]ID tenant** (ID istanza) trovato nell&#39;URL [!DNL Commerce Optimizer] o nell&#39;interfaccia utente di Commerce Cloud Manager.
* **ID programma AEM**.
* **ID ambiente AEM**.
* **Regola corrispondente**: corrisponde per SKU o [corrispondenza esterna (App Builder)](../synchronize/custom-match.md){target=_blank}.
* **Livello**: il nome del livello del catalogo con cui registrare il tenant. Se necessario, specifica un nome personalizzato. In caso contrario, viene utilizzato il valore predefinito `AEM-Assets`.
* **Impostazioni locali**: le impostazioni locali di origine del catalogo con cui registrare il tenant (ad esempio, `en-US`).

>[!IMPORTANT]
>
> L’integrazione supporta un’origine per tenant, ovvero la combinazione di una lingua e un livello.

Dopo che il supporto Adobe elabora il ticket, l’integrazione viene configurata e il tenant viene registrato con il servizio di integrazione Assets.

Una volta completato l’onboarding:

1. **Registrazione con Assets Integration Service**: il tenant [!DNL Commerce Optimizer] è registrato con Assets Integration Service utilizzando l&#39;ID tenant [!DNL Adobe Commerce Optimizer], l&#39;ID programma AEM, l&#39;ID ambiente AEM e il tenant.

1. **Sottoscrizione evento**: Assets Integration Service si abbona a:

   * Eventi AEM Assets (risorsa approvata, aggiornata, rimossa)
   * [!DNL Commerce Optimizer] eventi catalogo (prodotto creato, aggiornato)

### Limitazioni

L&#39;integrazione di [!DNL Commerce Optimizer] presenta le seguenti limitazioni:

* **Livello singolo per commerciante**: l&#39;integrazione AEM Assets supporta un livello AEM-Assets per commerciante (un&#39;origine per tenant). Al momento, la configurazione di più livelli per esercente non è supportata.
* **Solo immagini** - L&#39;integrazione non supporta video o altri tipi di file multimediali.
* **Nessuna immagine categoria** - La sincronizzazione immagine categoria non è disponibile. Le immagini delle categorie da AEM Assets per il selettore Assets (inserimento nell’interfaccia utente) non sono supportate.
* **Nessuna distinzione tra più siti**. L&#39;integrazione non gestisce più siti. Un&#39;immagine associata a un prodotto viene visualizzata allo stesso modo su tutti i canali e i criteri.
* **Posizione/ordinamento immagine**. La posizione e l&#39;ordinamento delle immagini non sono supportati.
* **Il prodotto deve esistere**. Se il prodotto non esiste in [!DNL Commerce Optimizer], il livello non verrà creato per la mappatura prodotto-risorsa.
* **Sovrascrittura campo livello** - I valori in un livello sovrascrivono il catalogo di base. Se un campo non viene inviato nel payload del livello, può essere sovrascritto con un valore vuoto. Utilizza un livello dedicato per il contenuto di AEM Assets; il riutilizzo di un livello esistente per altri scopi può causare una perdita di dati non intenzionale.

### Configurare AEM Assets

Il processo di installazione e configurazione di AEM Assets per [!DNL Commerce Optimizer] è lo stesso di Adobe Commerce as a Cloud Service. Consulta [Configurare il progetto AEM Assets per supportare i metadati di Commerce](configure-aem.md) per i passaggi completi.

Assicurati che l’ambiente AEM Assets sia pronto:

1. **Configurazione di AEM Assets**: configurare il profilo metadati di Commerce. Consulta [Configurare un profilo di metadati](configure-aem.md#configure-a-metadata-profile).

1. **Abilitazione Dynamic Media**: verifica che Dynamic Media con funzionalità OpenAPI sia abilitato nell&#39;ambiente AEM Assets.

## Configurare AEM Assets

Per abilitare la sincronizzazione prodotto-risorsa, configura l’ambiente AEM Assets.

### Passaggio 1: abilitare Dynamic Media con OpenAPI

Dynamic Media con OpenAPI deve essere abilitato nell’ambiente AEM Assets. Product Visuals e le nuove licenze AEM Assets consentono di abilitarlo in modo autonomo tramite Cloud Manager. Le licenze AEM Assets precedenti richiedono il supporto Adobe per abilitarlo. Consulta [Configurare il progetto AEM Assets](configure-aem.md#prerequisites) per i passaggi di abilitazione.

### Passaggio 2: facoltativo. Configurare il profilo di metadati Commerce

Configura il profilo metadati in AEM Assets per memorizzare i metadati specifici di Commerce.

Per istruzioni dettagliate, consulta [Configurare un profilo di metadati](configure-aem.md#step-2-optional-configure-a-metadata-profile).

### Passaggio 3: Applicare i metadati alle risorse

Aggiungi metadati Commerce alle immagini del prodotto in AEM Assets.

Consulta il [contenuto del pacchetto AEM Commerce](configure-aem.md#aem-commerce-assets-commerce-package-contents) per le definizioni dei campi e [Configura un profilo di metadati](configure-aem.md#step-2-optional-configure-a-metadata-profile) per i passaggi di configurazione.

La risorsa deve essere in uno stato **approvato** per poter attivare la sincronizzazione dati. Il salvataggio dei metadati da solo non attiva l&#39;evento.

>[!CAUTION]
>
> Assegna il livello `AEM-Assets` alla [vista catalogo](https://experienceleague.adobe.com/it/docs/commerce/optimizer/setup/catalog-view). Se il livello non è assegnato, i dati immagine prodotto potrebbero essere sovrascritti in modo imprevisto.

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
