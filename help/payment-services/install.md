---
title: Installa [!DNL Payment Services]
description: Installare l'estensione Payments Services.
exl-id: babaa91a-9376-4acb-b934-a89f9df52016
role: Admin
feature: Payments, Checkout, Install, Upgrade, Paas
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Installa [!DNL Payment Services]

Per iniziare a utilizzare Payment Services per [!DNL Adobe Commerce] e [!DNL Magento Open Source], è necessario completare alcuni passaggi di onboarding.

>[!INFO]
>
> Per ulteriori informazioni, guarda il video [Configure [!DNL Payment Services] for Adobe Commerce](https://experienceleague.adobe.com/it/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services).

Il download e l&#39;installazione dell&#39;estensione [!DNL Payment Services] per [!DNL Adobe Commerce] e [!DNL Magento Open Source] è un passaggio preliminare per l&#39;utilizzo di [!DNL Payment Services].

## Scaricare l’estensione

È necessario scaricare l&#39;estensione da [Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html?lang=it) prima di installarla.

1. Passare all&#39;estensione [Payment Services in Commerce Marketplace](https://commercemarketplace.adobe.com/magento-payment-services.html).
1. Per scegliere l&#39;edizione e la versione, selezionare **[!UICONTROL Edition]** e **[!UICONTROL Your store version]** in base alle proprie preferenze.
1. Fare clic su **[!UICONTROL Add to Cart]**.
1. Completare l&#39;estrazione e fare clic su **[!UICONTROL Place Order]**.
1. Per informazioni dettagliate e conferma dell’ordine, controlla l’e-mail associata al download per Marketplace.

>[!NOTE]
>
> Per Adobe Commerce sono disponibili le versioni 2.4.7 o successive [!DNL Payment Services] pronte all’uso.

## Installare l’estensione

È possibile installare l&#39;estensione [!DNL Payment Services] sia per [!DNL Adobe Commerce] sull&#39;infrastruttura cloud che per le istanze locali, che sono collegate all&#39;account Commerce [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys) fornito nel processo di abbonamento.
[!DNL Magento Open Source] clienti utilizzano le istruzioni locali.

Composer utilizza queste chiavi durante l&#39;installazione iniziale di [!DNL Adobe Commerce] o in situazioni in cui le chiavi del Composer non sono state salvate in precedenza nel file `auth.json`.

Per ulteriori informazioni su come ottenere le chiavi del Compositore, vedere [Ottieni le chiavi di autenticazione](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/prerequisites/authentication-keys).

Per ulteriori informazioni su cosa considerare prima di scaricare e installare un&#39;estensione, vedere [Installare un&#39;estensione](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/extensions).

### [!DNL Adobe Commerce] sull&#39;infrastruttura cloud

Questo metodo viene utilizzato per installare l&#39;estensione [!DNL Payment Services] per un&#39;istanza di Commerce Cloud.

1. Aggiorna il file `composer.json`:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizzare il comando `composer update` per aggiornare tutte le dipendenze radice.

1. Eseguire il commit e inviare le modifiche.

### Configurazioni locali e di altro tipo

Questo metodo viene utilizzato per installare l&#39;estensione [!DNL Payment Services] per un&#39;istanza locale e [!DNL Magento Open Source] clienti.

1. Per ottenere l’estensione, esegui i seguenti comandi:

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizzare il comando `composer update` per aggiornare tutte le dipendenze radice.

1. Aggiorna l’istanza:

   ```bash
   bin/magento setup:upgrade
   ```

1. Cancella la cache:

   ```bash
   bin/magento cache:clean
   ```

1. Conferma modifiche.
1. Per garantire che il codice confermato sia distribuito, aggiorna l’istanza .

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1 è compatibile con le versioni 7.x di PHP. Tuttavia, si consiglia vivamente di aggiornare alla versione più recente di [!DNL Payment Services].

## Aggiornare l’estensione

Quando viene rilasciata una nuova versione di [!DNL Payment Services], è possibile aggiornare facilmente l&#39;estensione.

1. Per ottenere la versione più recente del pacchetto:

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilizzare il comando `composer update` per aggiornare tutte le dipendenze radice.

1. Dopo l&#39;aggiornamento del compositore, eseguire:

   ```bash
   bin/magento setup:upgrade
   ```

1. Eseguire il commit e inviare le modifiche.

## Risoluzione dei problemi

È possibile che vengano visualizzati errori durante il tentativo di installare l&#39;estensione [!DNL Payment Services]. Per risolvere gli errori, utilizzare i seguenti metodi di risoluzione dei problemi.

### Elenco degli archivi

Verifica che `repo.magento.com` sia presente nell&#39;elenco degli archivi.

### Tasti composizione errati

Se viene visualizzato il seguente errore che indica la presenza di chiavi di composizione errate:

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Verifica che le chiavi del Compositore siano valide e di avere accesso ad altri pacchetti Magento.

Per vedere quali chiavi del Compositore sono configurate:

1. Trovare il percorso del file `auth.json`:

   ```bash
   composer config --global home
   ```

1. Visualizza il file `auth.json`:

   ```bash
   cat /path/to/auth.json
   ```

1. Consulta [quali chiavi sono associate al tuo account Commerce `MageID`](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/prerequisites/authentication-keys).

### Memoria insufficiente per PHP

Se viene visualizzato il seguente errore che indica che non si dispone di memoria sufficiente per PHP:

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[Aumentare il limite di memoria](https://experienceleague.adobe.com/it/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit) per PHP nell&#39;ambiente in `php.ini`.

In alternativa, è possibile specificare il limite di memoria utilizzando questo comando: `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`.

Ad esempio:

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
