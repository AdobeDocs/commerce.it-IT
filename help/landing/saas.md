---
title: Connettore servizi Commerce
description: Scopri come integrare la tua istanza di Adobe Commerce o Magento Open Source nei servizi utilizzando le chiavi API di produzione e sandbox.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: abd0bcdd5ab50ace469e92c8d8e727cc35e2f667
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Alcune funzionalità di Adobe Commerce e Magento Open Source sono basate su [!DNL Commerce Services] e distribuite come SaaS (software as a service). Per utilizzare questi servizi, è necessario connettere l&#39;istanza [!DNL Commerce] utilizzando le chiavi API di produzione e sandbox e specificare lo spazio dati nella [configurazione](#saas-configuration). È sufficiente configurare la connessione una sola volta per ogni istanza.

Se non sei il proprietario della licenza, devi ottenere le chiavi API di Commerce dalla persona o dal team a cui appartiene la licenza di Commerce per il tuo store.

>[!NOTE]
>
>Le chiavi API possono essere generate solo dal proprietario della licenza. Non è disponibile alcuna funzionalità di accesso condiviso per consentire ad altri utenti di generarli.

## Servizi disponibili {#availableservices}

Di seguito sono elencate le funzionalità di [!DNL Commerce] a cui è possibile accedere tramite [!DNL Commerce Services Connector]:

| Servizio | Disponibilità |
| ---|--- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) con tecnologia Adobe Sensei | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) con tecnologia Adobe Sensei | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | ADOBE COMMERCE e MAGENTO OPEN SOURCE |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Architettura

A un livello avanzato, [!DNL Commerce Services Connector] è costituito dai seguenti elementi principali:

![Architettura di Commerce Services Connector](assets/saas-config-sync-workflow.png)

Le sezioni seguenti descrivono ciascuno di questi elementi in modo più dettagliato.

## Credenziali {#apikey}

Le chiavi API di produzione e sandbox sono generate dall&#39;account [!DNL Commerce] del [proprietario licenza](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). L&#39;account Commerce è identificato da un ID [!DNL Commerce] univoco (MageID). Il proprietario della licenza per l’organizzazione del commerciante può generare chiavi API per servizi come Product Recommendations o Live Search, purché l’account sia in buono stato.

Le chiavi possono essere condivise in base alla necessità di sapere con l&#39;integratore di sistemi o il team di sviluppo che gestisce progetti e ambienti per conto del titolare della licenza. Gli sviluppatori a cui il proprietario della licenza ha concesso [!DNL Shared Access] non possono generare le chiavi per loro conto anche se l&#39;organizzazione del commerciante è presente nel menu a discesa [!DNL Switch Accounts] sul loro account.

Inoltre, gli integratori di soluzioni sono anche autorizzati a utilizzare [!DNL Commerce Services]. Se sei un integratore di soluzioni, il firmatario del contratto partner [!DNL Commerce] deve generare le chiavi API.

>[!NOTE]
>Gli identificatori chiave *Produzione* e *Sandbox* non fanno riferimento al tuo ambiente. Utilizza lo stesso set di chiavi API per ogni ambiente, ad esempio locale, di sviluppo, di staging o di produzione.
>
>Il proprietario della licenza è in genere il contatto principale sull’account Adobe Commerce e non è sempre lo stesso del proprietario del progetto di infrastruttura cloud Adobe Commerce on.

### Generare le chiavi API di produzione e sandbox {#genapikey}

1. Accedi al tuo account [!DNL Commerce] all&#39;indirizzo [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. Nella scheda **Magento**, seleziona **API Portal** nella barra laterale.

1. Dal menu _Ambiente_, seleziona **Produzione** o **Sandbox**.

   >[!NOTE]
   >
   >*Produzione* e *Sandbox* fanno riferimento agli ambienti di spazio dati in cui i dati vengono memorizzati nei sistemi back-end SaaS di Adobe. Non fa riferimento agli ambienti commerce in cui utilizzerai le chiavi.

1. Immetti un nome nella sezione _Chiavi API_ e fai clic su **Aggiungi nuovo** per aprire la finestra di dialogo e scaricare la nuova chiave.

   ![Scarica chiave privata](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Questa finestra di dialogo offre l’unica opportunità di copiare o scaricare le chiavi.

1. Fai clic su **Scarica**, quindi su **Annulla**.

1. Ripeti i passaggi precedenti per ogni ambiente (produzione e sandbox).

   Nella sezione **Chiavi API** sono ora visualizzate le chiavi API (pubbliche). Sono necessarie tutte e quattro le chiavi (sia quelle di produzione che quelle di sandbox, Public+Private) quando si [seleziona o si crea un progetto SaaS](#createsaasenv) in uno qualsiasi degli ambienti o delle installazioni associati alla licenza.

## Configurazione SaaS {#saasenv}

[!DNL Commerce] istanze devono essere configurate con un progetto SaaS e uno spazio dati SaaS in modo che [!DNL Commerce Services] possa inviare dati alla posizione giusta. Un progetto SaaS raggruppa tutti gli spazi di dati SaaS. Gli spazi di dati SaaS vengono utilizzati per raccogliere e archiviare dati che consentono il funzionamento di [!DNL Commerce Services]. Alcuni di questi dati possono essere esportati dall&#39;istanza [!DNL Commerce] e altri possono essere raccolti dal comportamento dell&#39;acquirente nella vetrina. Tali dati vengono quindi salvati in modo permanente nell’archiviazione cloud protetta.

Per [!DNL Product Recommendations], lo spazio dati SaaS contiene dati di catalogo e comportamentali. È possibile indirizzare un&#39;istanza [!DNL Commerce] a uno spazio dati SaaS [selezionandola](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) nella configurazione [!DNL Commerce].

>[!WARNING]
>
> Utilizza lo spazio dati **SaaS di produzione** solo nell&#39;installazione di [!DNL Commerce] di produzione per evitare conflitti di dati. In caso contrario, si rischia di inquinare i dati del sito di produzione con i dati di test, causando ritardi nell’implementazione. Ad esempio, i dati del prodotto di produzione potrebbero essere erroneamente sovrascritti dai dati di staging, come gli URL di staging.
> In questo caso, [invia una richiesta di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) per richiedere la pulizia dei dati.

Se non riesci a trovare i campi di configurazione LiveSearch nel pannello di amministrazione, verifica di aver immesso la chiave API SaaS corretta.  Assicurati di aver aggiunto la chiave SaaS di produzione durante la configurazione dello spazio di dati di produzione e di aver aggiunto la chiave di staging durante la configurazione dello spazio di dati di staging. Se configuri la chiave errata, i servizi SaaS, come LiveSearch, non sono disponibili nell’ambiente Adobe Commerce.

### Provisioning dello spazio dati SaaS

Tutti i commercianti di Adobe Commerce possono accedere a uno spazio di dati di produzione e due spazi di dati di test per ciascun progetto SaaS.

È possibile utilizzare gli spazi di dati di test in qualsiasi ambiente non di produzione, purché non si utilizzi lo stesso spazio di dati in più ambienti contemporaneamente. Per utilizzare lo spazio dati di test in un ambiente diverso, eseguire una pulizia dei dati prima di selezionare e configurare lo spazio dati in tale ambiente.

Per i progetti Adobe Commerce Cloud Pro con più ambienti di staging, puoi richiedere spazi di dati di test aggiuntivi per ogni ambiente di staging [inviando una richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support). Tuttavia, se disponi di un solo ambiente di staging e richiedi spazi di dati di test aggiuntivi, disponi delle seguenti opzioni:

- Contatta il team Customer Success o il Customer Success Manager designato per richiedere un ulteriore ambiente di staging.

- [Inviare una richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support) per richiedere spazio dati di test aggiuntivo e indicare la giustificazione aziendale per lo spazio dati aggiuntivo. Questa richiesta è soggetta ad approvazione.

I clienti Magento Open Source che utilizzano Adobe Payment Services possono richiedere anche uno spazio di dati aggiuntivo. Contatta il team dei pagamenti per ottenere l&#39;approvazione preventiva degli spazi di dati aggiuntivi prima di inviare una [richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support) per richiedere lo spazio di dati di prova.

I clienti che possiedono più progetti Cloud o installazioni on-premise (live/production) possono anche richiedere spazi di dati aggiuntivi per la produzione e il test per ciascun progetto o istanza [inviando una richiesta di supporto](https://experienceleague.adobe.com/home?support-tab=home#support).

### Selezionare o creare un progetto SaaS {#createsaasenv}

Per selezionare o creare un progetto SaaS, richiedere la chiave API [!DNL Commerce] al proprietario della licenza [!DNL Commerce] per l&#39;archivio:

>[!NOTE]
>
> Se la sezione **[!UICONTROL Commerce Services Connector]** non è visualizzata nella configurazione di [!DNL Commerce], è necessario installare i moduli [!DNL Commerce] per il [[!DNL Commerce] servizio](#availableservices) desiderato.

1. Nella barra laterale _Admin_, vai a **Sistema** > Servizi > **Connettore servizi Commerce**.

   Se non vedi la sezione **[!UICONTROL Commerce Services Connector]** nella configurazione [!DNL Commerce], installa i moduli [!DNL Commerce] per il [[!DNL Commerce] servizio](#availableservices) desiderato. Verificare inoltre che il pacchetto `magento/module-services-id` sia installato.

1. Nelle sezioni _[!UICONTROL Sandbox API Keys]_&#x200B;e_[!UICONTROL Production API Keys]_, incolla i valori chiave.

   - Le chiavi private devono includere `----BEGIN PRIVATE KEY---` all&#39;inizio della chiave e `----END PRIVATE KEY----` alla fine.
   - Se non disponi di una copia delle chiavi effettive, chiedi al proprietario dell’account di inserirle, quindi collega i valori nella configurazione.

   >[!WARNING]
   >
   > Se si aggiungono valori chiave eseguendo una query su un backup o uno snapshot del database e si incollano i valori nella configurazione, viene applicato un ulteriore livello di crittografia e le chiavi non funzioneranno.

1. Fai clic su **Salva**.

Tutti i progetti SaaS associati alle chiavi vengono visualizzati nel campo **Progetto** della sezione **Identificatore SaaS**.

1. Se non esistono progetti SaaS, fare clic su **Crea progetto**. Quindi nel campo **Progetto**, inserisci un nome per il progetto SaaS.

>[!NOTE]
>
>Per evitare confusione, non utilizzare un servizio Commerce specifico come nome del progetto, ad esempio *Live Search*, *Product Recommendations* o *Data Connection*.  A meno che la licenza non sia stata fornita per più progetti SaaS, è possibile utilizzare lo stesso progetto SaaS per più servizi.

1. Seleziona lo **Spazio dati** da utilizzare per la configurazione corrente dell&#39;archivio [!DNL Commerce].

>[!NOTE]
>
>Se si dispone di istanze separate da integrare con Commerce Services, [inviare un ticket di supporto](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) per richiedere un nuovo progetto SaaS per ogni istanza aggiuntiva. Dopo aver creato il progetto SaaS, configura l’integrazione dei servizi Commerce per l’istanza utilizzando la stessa chiave API e selezionando il nuovo progetto SaaS per lo spazio dati.

>[!WARNING]
>
> Se generi nuove chiavi nella sezione Portale API di Il mio account, aggiorna immediatamente le chiavi API nella configurazione Amministratore. Se generi nuove chiavi e non le aggiorni nell’amministratore, le estensioni SaaS non funzioneranno più e perderai dati preziosi.

Per modificare i nomi del progetto SaaS o dello spazio dati, fare clic su **Rinomina** accanto a uno dei due. La modifica del nome non influisce sul servizio, in quanto il nome è solo un’etichetta per identificare e distinguere tra progetti e spazi di dati.

## Organizzazione IMS (opzionale) {#organizationid}

Per collegare la tua istanza di Adobe Commerce a Adobe Experience Platform, accedi al tuo account di Adobe utilizzando il tuo Adobe ID. Dopo l’accesso, l’organizzazione IMS associata al tuo account Adobe viene visualizzata in questa sezione.

## Esportazione dati SaaS

Quando l&#39;istanza [!DNL Commerce] si connette a [!DNL Commerce Services], il processo di esportazione dei dati SaaS esporta i dati Commerce dal server [!DNL Commerce] in [!DNL Commerce SaaS Services] in modo che possano essere sincronizzati con i servizi Commerce connessi. In Admin, puoi controllare lo stato di sincronizzazione utilizzando [Data Management dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Per informazioni dettagliate, vedere la [Guida all&#39;esportazione dei dati SaaS](../data-export/overview.md).
