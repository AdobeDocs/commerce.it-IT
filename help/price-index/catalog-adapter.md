---
title: Estensione scheda catalogo
description: Utilizzo di Catalog Adapter per il rendering dei prezzi da Commerce Services
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# Adattatore catalogo

L&#39;estensione `[!DNL Catalog Adapter]` disabilita l&#39;indicizzatore prezzi prodotto predefinito incluso nell&#39;applicazione Commerce e utilizza invece i prezzi forniti da [Catalog Service](../catalog-service/overview.md).

La scheda è progettata per funzionare con l&#39;[esportazione dati SaaS](../data-export/overview.md) e il servizio Adobe Commerce. L&#39;esportazione dei dati SaaS è responsabile dell&#39;invio dei prezzi e [!DNL Catalog Adapter] recupera tutti i prezzi dal servizio Adobe Commerce.

Quando si abilita [!DNL Catalog Adapter], l&#39;indicizzazione dei prezzi e le operazioni vengono influenzate nei seguenti modi:

- L’indicizzatore prezzi incluso nell’applicazione Adobe Commerce è disabilitato.
- I prezzi vengono gestiti tramite l&#39;esportazione di dati SaaS e l&#39;[indicizzatore di prezzi SaaS](price-indexing.md).
- Quando un cliente apre un prodotto, una categoria o un’altra pagina che mostra i prezzi dei prodotti, questi vengono recuperati dal servizio Adobe Commerce.
- I prezzi vengono inviati al servizio Adobe Commerce sincronizzando i dati dall&#39;[esportazione di dati SaaS](../data-export/overview.md).
- Il Checkout ricalcola i prezzi in modo dinamico.

È possibile riabilitare l&#39;indicizzazione dei prezzi nell&#39;applicazione Commerce rimuovendo o disabilitando l&#39;estensione Catalog Adapter.

## Requisiti

- Adobe Commerce 2.4.4+
- Installare uno dei seguenti servizi Commerce:

   - [Live Search](../live-search/install.md)
   - [Consigli di prodotto](../product-recommendations/install-configure.md)
   - [Servizio catalogo](../catalog-service/installation.md)

## Installazione

L&#39;estensione Catalog Adapter è un metapacchetto Compositore che installa i seguenti moduli:

- **Indicizzatore prezzi Disabler**-Questo modulo disattiva l&#39;indice dei prezzi nell&#39;applicazione Commerce in modo che i prezzi vengano consegnati tramite l&#39;indicizzazione dei prezzi SaaS. Impossibile attivare l&#39;indicizzatore prezzi prodotto nell&#39;applicazione Commerce quando è installata l&#39;estensione per l&#39;indicizzazione prezzi SaaS.
- **Provider prezzi**-Questo modulo fornisce i prezzi per i prodotti del servizio Adobe Commerce. Crea la query di ricerca e ottiene i prezzi per i prodotti sul front-end.
- **Scheda di ricerca del servizio catalogo**-Questo modulo trasferisce i prezzi dall&#39;applicazione Adobe Commerce a un servizio Adobe Commerce in risposta a una richiesta di ricerca del prodotto.

## Passaggi per l’installazione

>[!BEGINTABS]

>[!TAB Infrastruttura cloud]

Utilizzare questo metodo per installare [!DNL Catalog Adapter] per un&#39;istanza di Commerce Cloud.

1. Sulla workstation locale, passa alla directory del progetto per il progetto Adobe Commerce su infrastruttura cloud.

   >[!NOTE]
   >
   >Per informazioni sulla gestione locale degli ambienti di progetto Commerce, vedere [Gestione dei rami con CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) nella _Guida utente di Adobe Commerce on Cloud Infrastructure_.

1. Consulta il ramo dell’ambiente da aggiornare utilizzando Adobe Commerce Cloud CLI.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Aggiungere il modulo adattatore catalogo.

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Aggiornare le dipendenze del pacchetto.

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. Modifiche al codice di commit e push per i file `composer.json` e `composer.lock`.

1. Aggiungere, eseguire il commit e inviare le modifiche al codice per i file `composer.json` e `composer.lock` all&#39;ambiente cloud.

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   Il push degli aggiornamenti all&#39;ambiente cloud avvia il [processo di distribuzione cloud di Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) per applicare le modifiche. Controllare lo stato della distribuzione dal [registro distribuzione](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Locale]

Utilizzare questo metodo per installare [!DNL Catalog Adapter] per un&#39;istanza locale.

1. Aggiungi l&#39;adattatore catalogo al progetto utilizzando il Compositore:

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Aggiorna le dipendenze e installa l’estensione:

   ```bash
   composer update  "magento/catalog-adapter"
   ```

1. Aggiorna Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Cancella la cache:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >In alcuni casi, in particolare durante la distribuzione in produzione, potrebbe essere opportuno evitare di cancellare il codice compilato perché potrebbe richiedere del tempo. Prima di apportare qualsiasi modifica, assicurati di eseguire il backup del sistema.

>[!ENDTABS]


## Riattiva l’indicizzatore dei prezzi del prodotto Adobe Commerce

Se esistono applicazioni di terze parti che si basano sull’indicizzatore prezzi del prodotto Adobe Commerce predefinito, puoi abilitarlo nuovamente con i seguenti comandi:

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## Disattiva l&#39;indicizzatore del prezzo del prodotto per lo scenario Headless Storefront

Se disponi di un’istanza Commerce headless, potresti dover disabilitare l’indicizzatore dei prezzi del prodotto Adobe Commerce per ridurre il carico sull’istanza Adobe Commerce. È possibile completare questa attività installando il modulo `magento/module-price-indexer-disabler`:

```bash
composer require magento/module-price-indexer-disabler
```

## Scenari di utilizzo

Di seguito sono riportati alcuni scenari `[!DNL Catalog Adapter]` comuni.

### Nessuna dipendenza dall’indicizzatore dei prezzi dei prodotti Adobe Commerce

- Sei un commerciante Luma o Adobe Commerce Core GraphQL con installato un servizio richiesto (Live Search, Product Recommendations, Catalog Service)
- Nessuna integrazione con estensioni di terze parti basate sull’indicizzatore dei prezzi del prodotto di Adobe Commerce

1. Installa [!DNL Catalog Adapter].

### Con dipendenze dall’indicizzatore dei prezzi dei prodotti Adobe Commerce

- Sei un commerciante Luma o Adobe Commerce Core GraphQL con installato un servizio supportato (Live Search, Product Recommendations, Catalog Service)
- Puoi utilizzare un’estensione di terze parti basata sull’indicizzatore dei prezzi del prodotto Adobe Commerce

1. Installa [!DNL Catalog Adapter].
1. Abilita nuovamente l’indicizzatore prezzi prodotto Adobe Commerce predefinito.

### Istanze Commerce headless

- Un commerciante con un’istanza Commerce headless con i servizi richiesti installati (Live Search, Product Recommendations, Catalog Service)
- Nessuna dipendenza dall&#39;indicizzatore prezzi prodotto Adobe Commerce predefinito

1. Installa il modulo `magento/module-price-indexer-disabler` dal pacchetto [!DNL Catalog Adapter].

