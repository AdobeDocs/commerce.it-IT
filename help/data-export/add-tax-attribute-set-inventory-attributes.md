---
title: Aggiungere classe fiscale, serie di attributi e attributi di inventario
description: Scopri come estendere i dati dei feed di prodotto per includere gli attributi per la classificazione fiscale, la serie di attributi e le impostazioni di inventario avanzate
role: Admin, Developer
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/
source-git-commit: dd8f518028c9f2025606e6620fc20156fceac9ce
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Aggiungere classe fiscale, serie di attributi e attributi di inventario

Il modulo Adobe Commerce Extra Product Attributes estende i feed di dati di prodotto. Include attributi di prodotto aggiuntivi dalle configurazioni di prodotto Adobe Commerce:

* [Classificazione fiscale](https://experienceleague.adobe.com/it/docs/commerce-admin/stores-sales/site-store/taxes/tax-class)
* [Set di attributi](https://experienceleague.adobe.com/it/docs/commerce-admin/catalog/product-attributes/create/attribute-sets)
* [Inventario](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/configuration/product-options#advanced-product-options)

Una volta installato, il modulo funziona automaticamente. Acquisisce ed esporta gli attributi aggiuntivi durante la sincronizzazione del prodotto. Non è richiesta alcuna configurazione aggiuntiva.

## Vantaggi chiave

* **Miglioramento automatico**: arricchisce i feed di prodotto con attributi di classe fiscale, set di attributi e inventario
* **Integrazione perfetta**: fornisce il contesto essenziale per i sistemi e i servizi esterni
* **Nessuna configurazione**: funziona immediatamente dopo l&#39;installazione
* **Aggiornamenti in tempo reale**: sincronizzazione automatica con le modifiche apportate al prodotto

## Funzioni e attributi esportati

Il modulo aggiunge tre attributi aggiuntivi ai feed di dati di prodotto esistenti:

* `ac_tax_class`
* `ac_attribute_set`
* `ac_inventory`

### &#x200B;1. Informazioni sulla classe fiscale (`ac_tax_class`)

**Scopo**: fornisce informazioni sulla classificazione fiscale per ciascun prodotto

**Formato dati**: valore stringa contenente il nome della classe fiscale

**Output di esempio**:

```json
{
  "attributes": [
    {
      "code": "ac_tax_class",
      "values": ["Taxable Goods"]
    }
  ]
}
```

**Casi d&#39;uso**:

Quando si esportano dati di classi di imposta in Commerce Catalog Services, tali dati diventano disponibili per le applicazioni che supportano:

* Report di conformità fiscale
* Integrazione con i servizi di calcolo delle imposte esterni
* Categorizzazione dei prodotti per i sistemi contabili

### &#x200B;2. Informazioni sul set di attributi (`ac_attribute_set`)

**Scopo**: identifica il set di attributi assegnato a ciascun prodotto

**Formato dati**: valore stringa contenente il nome del set di attributi

**Output di esempio**:

```json
{
  "attributes": [
    {
      "code": "ac_attribute_set",
      "values": [
        "Default"
      ]
    }
  ]
}
```

**Casi d&#39;uso**:

Quando si esportano i dati del set di attributi in Commerce Catalog Services, vengono attivate funzioni avanzate di gestione dei prodotti in sistemi esterni. Queste caratteristiche includono:

* Identificazione del modello di prodotto
* Gestione e organizzazione del catalogo
* Integrazione di sistemi di terze parti che richiede il contesto del set di attributi

### &#x200B;3. Dati inventario avanzati (`ac_inventory`)

**Scopo**: fornisce le impostazioni di gestione dell&#39;inventario per ciascun prodotto

**Formato dati**: stringa con codifica JSON contenente la configurazione dell&#39;inventario

**Campi inclusi**:

* `manageStock` (booleano): se la gestione azionaria è abilitata
* `cartMinQty` (virgola mobile): quantità minima consentita nel carrello
* `cartMaxQty` (virgola mobile): quantità massima consentita nel carrello
* `backorders` (stringa): criterio ordine arretrato. Il valore è uno dei seguenti:
   * `"no"`: nessun ordine inevaso consentito
   * `"allow"`: quantità consentita inferiore a 0
   * `"allow_notify"`: consenti quantità inferiore a 0 e notifica al cliente
* `enableQtyIncrements` (booleano): se gli incrementi di quantità sono abilitati
* `qtyIncrements` (virgola mobile): valore di incremento quantità richiesto

**Output di esempio**:

```json
{
  "attributes": [
    {
      "code": "ac_inventory",
      "values": [
        "{\"manageStock\":true,\"cartMinQty\":2,\"cartMaxQty\":42,\"backorders\":\"no\",\"enableQtyIncrements\":false,\"qtyIncrements\":2}"
      ]
    }
  ]
}
```

**Casi d&#39;uso**:

Quando si esportano dati di inventario in Commerce Catalog Services, vengono attivate funzioni avanzate di gestione dell&#39;inventario in sistemi esterni. Queste caratteristiche includono:

* Integrazione dei sistemi Inventory management
* Regole di convalida del carrello
* Ottimizzazione del processo di evasione degli ordini
* Personalizzazione della customer experience

## Miglioramento del feed di esportazione dei dati

Il modulo Attributi prodotto aggiuntivi migliora i feed di prodotto esistenti. Integra automaticamente i nuovi dati attributo.

* **Feed prodotti** (`products`): migliorato con i tre attributi aggiuntivi

   * Aggiunge gli attributi `ac_tax_class`, `ac_attribute_set` e `ac_inventory` a ciascun record di prodotto
   * Mantiene invariati i dati di prodotto originali
   * Mantiene la compatibilità con le versioni precedenti dei consumatori di feed esistenti

* **Feed attributi prodotto** (`productAttributes`): migliorato con i metadati degli attributi per i nuovi attributi

   * Registra automaticamente i metadati per i tre nuovi attributi nel feed `productAttributes`
   * Fornisce i dettagli di configurazione degli attributi (tipi di dati, impostazioni di visibilità e così via)
   * Aiuta i sistemi esterni a comprendere il nuovo schema di attributi

## Installare l’estensione

**Requisiti**

* PHP 8.1, 8.2, 8.3 o 8.4
* Adobe Commerce 2.4.4+
* [Estensione Adobe Commerce Data Export](manage-extension.md#update-a-module-to-a-specific-version), versione 103.4.11 o successiva
* Accedi a [repo.magento.com](https://repo.magento.com)

  Per generare le chiavi e ottenere i diritti necessari, vedere [Ottenere le chiavi di autenticazione](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Per le installazioni cloud, consulta la [Guida di Commerce sull&#39;infrastruttura cloud](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/develop/authentication-keys).
* Accedere alla riga di comando del server applicazioni Adobe Commerce.

### Passaggi per l’installazione

Aggiungi il modulo `adobe-commerce/module-extra-product-attributes` tramite Compositore:

```shell
composer require adobe-commerce/module-extra-product-attributes
```

Per i passaggi dettagliati dell’installazione, consulta le seguenti guide:

* [Installa estensione su Adobe Commerce su infrastruttura cloud](https://experienceleague.adobe.com/it/docs/commerce-on-cloud/user-guide/configure-store/extensions)
* [Installa l&#39;estensione Adobe Commerce on-premise](https://experienceleague.adobe.com/it/docs/commerce-operations/installation-guide/tutorials/extensions)

## Sincronizzare i dati del prodotto

Dopo la ridistribuzione, l’istanza di Adobe Commerce esporta automaticamente i dati aggiuntivi durante la sincronizzazione del prodotto. È inoltre possibile utilizzare i comandi CLI `resync` per eseguire immediatamente la sincronizzazione.

```shell
# Resync the products feed (includes the new attributes)
bin/magento saas:resync --feed=products
```

```shell
# Resync the product attributes feed (includes new attribute metadata)
bin/magento saas:resync --feed=productAttributes
```

## Risoluzione dei problemi

**Attributi aggiuntivi mancanti per i prodotti:**

* Verificare che il modulo sia installato e attivato correttamente
* Esegui i comandi di risincronizzazione per aggiornare i dati del prodotto
* Verifica che i prodotti abbiano assegnazioni valide per la classe fiscale e la serie di attributi

**I dati di inventario non sono corretti:**

* Verificare che le impostazioni di inventario siano configurate correttamente in Amministrazione
* Verifica sostituzioni inventario specifiche per il sito Web
* Verifica che il modulo [Inventory management](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/guide-overview) funzioni correttamente

Per ulteriori dettagli, consulta la [Guida di Inventory management](https://experienceleague.adobe.com/it/docs/commerce-admin/inventory/guide-overview) nella *documentazione di Adobe Commerce Merchant*.

**Problemi relativi alle prestazioni:**

* Monitorare le prestazioni del processo di esportazione dopo l&#39;installazione
* Valuta la pianificazione delle risincronizzazioni durante i periodi a traffico ridotto

### Registrazione e debug

Il modulo registra gli errori e gli avvisi di esportazione nel sistema di registrazione standard di Commerce. Se riscontri problemi durante la sincronizzazione del prodotto, controlla i registri di esportazione dei dati.

Per ulteriori dettagli, vedere [Esaminare i registri e risolvere i problemi](troubleshooting-logging.md).

