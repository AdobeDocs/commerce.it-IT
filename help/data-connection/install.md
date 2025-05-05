---
title: Installa [!DNL Data Connection]
description: Scopri come installare, aggiornare e disinstallare l'estensione  [!DNL Data Connection]  da Adobe Commerce.
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Installa [!DNL Data Connection]

Prima di installare l&#39;estensione, [controlla i prerequisiti](overview.md#prereqs).

## Installare l’estensione

L&#39;estensione [!DNL Data Connection] è disponibile nel [Marketplace Adobe](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html). Quando installi questa estensione dalla riga di comando del server, questa si connette all&#39;installazione di Adobe Commerce come [servizio](../landing/saas.md). Al termine del processo, **[!DNL Data Connection]** e **Commerce Services Connector** sono visualizzati nel menu **System** in **Services** in Commerce _Admin_.

Visualizzazione amministratore dell&#39;estensione ![[!DNL Data Connection]](assets/epc-adminui.png)

>[!IMPORTANT]
>
>Anche se il nome dell&#39;estensione è cambiato da connettore Experience Platform a [!DNL Data Connection], il nome del pacchetto rimane `experience-platform-connector` per supportare la compatibilità con le versioni precedenti.

1. Per scaricare il pacchetto `experience-platform-connector`, eseguire quanto segue dalla riga di comando:

   ```bash
   composer require magento/experience-platform-connector
   ```

   Questo metapacchetto contiene i moduli e le estensioni seguenti:

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. (Facoltativo) Per includere [!DNL Live Search] dati, che comprendono [eventi di ricerca](events.md#search-events), installare l&#39;estensione [[!DNL Live Search]](../live-search/install.md).

1. (Facoltativo) Per includere i dati B2B, che comprendono [eventi richiesta](events.md#b2b-events), installare l&#39;estensione [B2B](#install-the-b2b-extension).

1. (Facoltativo) Se sei un commerciante sanitario, installa l&#39;estensione [Data Services HIPAA](#install-the-data-services-hipaa-extension) in modo che i tuoi dati di back office [!DNL Commerce] siano pronti per HIPAA.

### Installare Adobe I/O Events e configurare il modulo customer-connector

Dopo aver installato l&#39;estensione `experience-platform-connector`, è necessario installare Adobe I/O Events per Adobe Commerce e configurare il modulo `customers-connector`.

I seguenti passaggi si applicano sia all’infrastruttura cloud di Adobe Commerce che alle installazioni on-premise.

1. Se si esegue Commerce 2.4.4 o 2.4.5, utilizzare il comando seguente per caricare i moduli di eventi:

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6 e versioni successive carica automaticamente questi moduli.

1. Aggiornare le dipendenze del progetto.

   ```bash
   composer update
   ```

1. Abilita i nuovi moduli:

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

Completa l’installazione in base al tipo di distribuzione: Adobe Commerce su infrastruttura Cloud o on-premise.

#### Infrastruttura cloud

Nell&#39;infrastruttura Adobe Commerce on Cloud, abilita la variabile globale `ENABLE_EVENTING` in `.magento.env.yaml`. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html?lang=it#enable_eventing).

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

Esegui il commit e invia i file aggiornati all’ambiente Cloud. Al termine della distribuzione, abilita l’invio di eventi con il seguente comando:

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### On-premise

Negli ambienti locali, devi abilitare manualmente la generazione del codice e gli eventi Adobe Commerce:

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### Installare l’estensione B2B

Per i commercianti B2B, installa la seguente estensione per includere [dati evento elenco richieste](events.md#b2b-events).

Scaricare l&#39;estensione `magento/experience-platform-connector-b2b` eseguendo quanto segue dalla riga di comando:

```bash
composer require magento/experience-platform-connector-b2b
```

### Installare l’estensione HIPAA di Data Services

Per gli operatori sanitari, installare la seguente estensione per garantire che i dati degli eventi di back office siano pronti per HIPAA.

Scaricare l&#39;estensione `magento/module-data-services-hipaa` eseguendo quanto segue dalla riga di comando:

```bash
composer require magento/module-data-services-hipaa
```

## Aggiorna l&#39;estensione [!DNL Data Connection] {#update}

Per aggiornare l&#39;estensione [!DNL Data Connection], eseguire quanto segue dalla riga di comando:

```bash
composer update magento/experience-platform-connector --with-dependencies
```

Oppure, per gli esercenti B2B:

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

Per eseguire l&#39;aggiornamento a una versione principale, ad esempio da 2.0.0 a 3.0.0, modificare il file `.json` principale del progetto come segue:[!DNL Composer]

1. Aprire il file radice `composer.json` e cercare `magento/experience-platform-connector`.

1. Nella sezione `require`, aggiornare il numero di versione come segue:

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **Salva** `composer.json`. Quindi, esegui quanto segue dalla riga di comando:

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   Oppure, per gli esercenti B2B:

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## Disinstalla l&#39;estensione [!DNL Data Connection] {#uninstall}

Per disinstallare l&#39;estensione [!DNL Data Connection], consultare [moduli di disinstallazione](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html?lang=it).
