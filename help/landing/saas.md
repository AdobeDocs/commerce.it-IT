---
title: Connettore servizi Commerce
description: Scopri come integrare la tua istanza di Adobe Commerce o Magento Open Source nei servizi utilizzando le chiavi API di produzione e sandbox.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: a1e7da7e4c49967e2975dfa133e246490bcff732
workflow-type: tm+mt
source-wordcount: '1563'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Alcune funzionalità di Adobe Commerce e Magento Open Source sono basate su [!DNL Commerce Services] e distribuite come SaaS (software as a service). Per utilizzare questi servizi, è necessario connettere l&#39;istanza [!DNL Commerce] utilizzando le chiavi API di produzione e sandbox e specificare lo spazio dati nella [configurazione](#saas-configuration). È sufficiente configurare la connessione una sola volta per ogni istanza.

Solo il proprietario della licenza [!DNL Commerce] può generare queste chiavi API. Se non sei il proprietario della licenza, richiedi le chiavi alla persona o al team proprietario della licenza Commerce per il tuo negozio.

## Servizi disponibili {#availableservices}

Di seguito sono elencate le funzionalità di [!DNL Commerce] a cui è possibile accedere tramite [!DNL Commerce Services Connector]:

| Servizio | Disponibilità |
| --- | --- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) con tecnologia Adobe AI | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) con tecnologia Adobe AI | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | ADOBE COMMERCE e MAGENTO OPEN SOURCE |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Architettura

A un livello avanzato, [!DNL Commerce Services Connector] è costituito dai seguenti elementi principali:

![Architettura di Commerce Services Connector](assets/saas-config-sync-workflow.png)

Le sezioni seguenti descrivono ciascuno di questi elementi in modo più dettagliato.

## Credenziali {#apikey}

Le chiavi API di produzione e sandbox sono generate dall&#39;account [!DNL Commerce] del [proprietario licenza](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). L&#39;account Commerce è identificato da un ID [!DNL Commerce] univoco (MageID). Il proprietario della licenza per l’organizzazione del commerciante può generare chiavi API per servizi come Product Recommendations o Live Search, purché l’account sia in buono stato.

Le chiavi possono essere condivise in base alla necessità di sapere con l&#39;integratore di sistemi o il team di sviluppo che gestisce progetti e ambienti per conto del titolare della licenza. Gli sviluppatori a cui il proprietario della licenza ha concesso [!DNL Shared Access] non possono generare le chiavi per conto del proprietario della licenza anche se l&#39;organizzazione del commerciante è presente nel menu a discesa [!DNL Switch Accounts] sul loro account.

Inoltre, gli integratori di soluzioni sono autorizzati a utilizzare [!DNL Commerce Services]. Se sei un integratore di soluzioni, il firmatario del contratto partner [!DNL Commerce] deve generare le chiavi API.

Gli identificatori chiave *Produzione* e *Sandbox* fanno riferimento agli ambienti di spazio dei dati SaaS in cui [!DNL Commerce Services] memorizza i dati (non agli ambienti Adobe Commerce). Puoi utilizzare lo stesso set di chiavi API negli ambienti Adobe Commerce locali, di sviluppo, di staging e di produzione; ciò che conta è incollare la coppia di chiavi corretta per lo spazio dati configurato.

Il proprietario della licenza è in genere il contatto principale sull’account Adobe Commerce e non è sempre lo stesso del proprietario del progetto di infrastruttura cloud Adobe Commerce on.

### Generare le chiavi API di produzione e sandbox {#genapikey}

1. Accedi al tuo account [!DNL Commerce] all&#39;indirizzo [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. Nella scheda **Magento**, seleziona **API Portal** nella barra laterale.

1. Dal menu _Ambiente_, seleziona **Produzione** o **Sandbox**.

1. Immetti un nome nella sezione _Chiavi API_ e fai clic su **Aggiungi nuovo** per aprire la finestra di dialogo e scaricare la nuova chiave.

   ![Scarica chiave privata](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Puoi copiare o scaricare la chiave privata una sola volta. Conservarlo in modo sicuro.

1. Fai clic su **Scarica** per salvare la chiave privata, quindi chiudi la finestra di dialogo.

1. Ripeti i passaggi precedenti per ogni ambiente (produzione e sandbox).

   Nella sezione **Chiavi API** sono ora visualizzate le chiavi API (pubbliche). Sono necessarie tutte e quattro le chiavi (sia quelle di produzione che quelle di sandbox, Public+Private) quando si [seleziona o si crea un progetto SaaS](#createsaasenv) in uno qualsiasi degli ambienti o delle installazioni associati alla licenza.

## Configurazione SaaS {#saasenv}

[!DNL Commerce] istanze devono essere configurate con un progetto SaaS e uno spazio dati SaaS in modo che [!DNL Commerce Services] possa inviare dati alla posizione giusta. Un progetto SaaS raggruppa tutti gli spazi di dati SaaS. Gli spazi di dati SaaS vengono utilizzati per raccogliere e archiviare dati che consentono il funzionamento di [!DNL Commerce Services]. Alcuni di questi dati possono essere esportati dall&#39;istanza [!DNL Commerce] e altri possono essere raccolti dal comportamento dell&#39;acquirente nella vetrina. Tali dati vengono quindi salvati in modo permanente nell’archiviazione cloud protetta.

Per [!DNL Product Recommendations] e [!DNL Live Search], lo spazio dati SaaS contiene dati di catalogo e comportamentali. È possibile indirizzare un&#39;istanza [!DNL Commerce] a uno spazio dati SaaS [selezionandola](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) nella configurazione [!DNL Commerce].

>[!WARNING]
>
> Utilizza il tuo **spazio dati SaaS di produzione** solo con l&#39;installazione di [!DNL Commerce] di produzione. Se lo utilizzi in ambienti non di produzione, è possibile combinare test e dati live (ad esempio, URL di staging o dati del catalogo di test). In questo caso, [invia una richiesta di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) per richiedere la pulizia dei dati.

Se non riesci a trovare i campi di configurazione Live Search nell’amministratore, verifica di aver inserito la coppia di chiavi API corretta per lo spazio di dati selezionato (gli spazi di dati di produzione utilizzano le chiavi di produzione; i test degli spazi di dati utilizzano le chiavi sandbox). Se configuri chiavi non corrette, i servizi SaaS come Live Search non sono disponibili in tale ambiente Adobe Commerce.

### Eliminare una chiave API {#delapikey}

>[!WARNING]
>
>L’eliminazione di una chiave ancora in uso comporta l’interruzione immediata dei servizi connessi.

Prima di eliminare una chiave API, genera e memorizza in modo sicuro una chiave sostitutiva. Aggiorna tutte le integrazioni per utilizzare la nuova chiave e verifica che i servizi dipendenti funzionino come previsto.

Se non trovi i campi di configurazione **[!DNL Live Search]** nel pannello di amministrazione, conferma di aver immesso la chiave API SaaS corretta per tale ambiente. Utilizza la chiave SaaS di produzione per lo spazio di dati di produzione e la chiave di staging per lo spazio di dati di staging. Se viene configurata la chiave errata, i servizi SaaS (incluso **[!DNL Live Search]**) non saranno disponibili nell&#39;ambiente Adobe Commerce.

Nella chiave API da rimuovere, fare clic su **[!UICONTROL Delete]**. Quando richiesto, confermare l&#39;operazione per rimuovere definitivamente la chiave.

### Provisioning dello spazio dati SaaS

Tutti i commercianti di Adobe Commerce possono accedere a uno spazio di dati di produzione e due spazi di dati di test per ciascun progetto SaaS.

Puoi utilizzare gli spazi di dati di test in ambienti non di produzione, ma evita di utilizzare lo stesso spazio di dati in più ambienti contemporaneamente. Se desideri spostare uno spazio di dati di test in un ambiente diverso, esegui una pulizia dei dati prima di selezionarlo e configurarlo nel nuovo ambiente.

Per i progetti Adobe Commerce Cloud Pro con più ambienti di staging, puoi richiedere spazi di dati di test aggiuntivi per ogni ambiente di staging [inviando una richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support). Tuttavia, se disponi di un solo ambiente di staging e richiedi spazi di dati di test aggiuntivi, disponi delle seguenti opzioni:

- Contatta il team Customer Success o il Customer Success Manager designato per richiedere un ambiente di staging aggiuntivo.

- [Inviare una richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support) per richiedere spazio dati di test aggiuntivo e indicare la giustificazione aziendale per tale spazio. Questa richiesta è soggetta ad approvazione.

I clienti Magento Open Source che utilizzano Adobe Payment Services possono richiedere anche uno spazio di dati aggiuntivo. Contatta il team dei pagamenti per ottenere l&#39;approvazione preventiva degli spazi di dati aggiuntivi prima di inviare una [richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support) per richiedere lo spazio di dati di prova.

I clienti che possiedono più progetti Cloud o installazioni on-premise (live/production) possono anche richiedere spazi di dati aggiuntivi per la produzione e il test per ciascun progetto o istanza [inviando una richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support).

### Selezionare o creare un progetto SaaS {#createsaasenv}

Per selezionare o creare un progetto SaaS, richiedere le chiavi API [!DNL Commerce] al proprietario della licenza [!DNL Commerce] per l&#39;archivio:

1. Nella barra laterale _Admin_, vai a **Sistema** > Servizi > **Connettore servizi Commerce**.

   Se non vedi la sezione **[!UICONTROL Commerce Services Connector]**, installa i moduli [!DNL Commerce] per il [[!DNL Commerce] servizio](#availableservices) desiderato e assicurati che il pacchetto `magento/module-services-id` sia installato.

1. Nelle sezioni _[!UICONTROL Sandbox API Keys]_e_[!UICONTROL Production API Keys]_, incolla i valori chiave.

   - Le chiavi private devono includere `-----BEGIN PRIVATE KEY-----` all&#39;inizio della chiave e `-----END PRIVATE KEY-----` alla fine.
   - Se non disponi di una copia delle chiavi effettive, chiedi al proprietario della licenza di inserirle, quindi collega i valori nella configurazione.

   Non incollare i valori chiave copiati da un backup o da uno snapshot del database. Quando la configurazione viene salvata, viene applicato un ulteriore livello di crittografia e le chiavi non funzioneranno.

1. Fai clic su **Salva**.

   Tutti i progetti SaaS associati alle chiavi vengono visualizzati nel campo **Progetto** della sezione **Identificatore SaaS**.

1. Se non esistono progetti SaaS, fare clic su **Crea progetto**. Quindi nel campo **Progetto**, inserisci un nome per il progetto SaaS.

   Per evitare confusione, non utilizzare un servizio Commerce specifico come nome del progetto (ad esempio, *Live Search*, *Consigli di prodotto* o *Connessione dati*). A meno che la licenza non sia stata fornita per più progetti SaaS, è possibile utilizzare lo stesso progetto SaaS per più servizi.

1. Seleziona lo **Spazio dati** da utilizzare per la configurazione corrente dell&#39;archivio [!DNL Commerce].

   Se si dispone di istanze separate da integrare con Commerce Services, [inviare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) per richiedere un nuovo progetto SaaS per ogni istanza aggiuntiva. Dopo aver creato il progetto SaaS, configura l’integrazione per l’istanza utilizzando le stesse chiavi API e selezionando il nuovo progetto SaaS per lo spazio dati.

>[!WARNING]
>
> Se generi nuove chiavi nel portale API, aggiorna immediatamente le chiavi API nella configurazione Admin. Se l’amministratore utilizza ancora chiavi obsolete, le estensioni SaaS cessano di funzionare e la raccolta dei dati viene interrotta.

Per modificare i nomi del progetto SaaS o dello spazio dati, fare clic su **Rinomina** accanto a uno dei due. La modifica del nome non influisce sul servizio, in quanto il nome è solo un’etichetta per identificare e distinguere tra progetti e spazi di dati.

## Organizzazione IMS (opzionale) {#organizationid}

Per collegare la tua istanza di Adobe Commerce a Adobe Experience Platform, accedi al tuo account di Adobe utilizzando il tuo Adobe ID. Dopo l’accesso, l’organizzazione IMS associata al tuo account Adobe viene visualizzata in questa sezione.

## Esportazione dati SaaS

Quando l&#39;istanza [!DNL Commerce] si connette a [!DNL Commerce Services], il processo di esportazione dei dati SaaS esporta i dati Commerce dal server [!DNL Commerce] in [!DNL Commerce SaaS Services] in modo che possano essere sincronizzati con i servizi Commerce connessi. In Admin, puoi controllare lo stato di sincronizzazione utilizzando [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Per informazioni dettagliate, vedere la [Guida all&#39;esportazione dei dati SaaS](../data-export/overview.md).
