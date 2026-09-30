---
title: Verifica la disponibilità di aggiornamenti per le estensioni
description: Scopri come Adobe Commerce verifica e notifica agli amministratori le nuove versioni dell’estensione di integrazione di AEM Assets, incluso il controllo manuale CLI.
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7950f5d171b35054be42ca60d19bafcf43c53cd6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# Verifica la disponibilità di aggiornamenti per le estensioni

Con l’estensione AEM Assets Integration versione 1.4.6 e successive, Adobe Commerce controlla automaticamente se è disponibile una versione più recente dell’estensione e ne informa gli amministratori di Admin. Questo controllo viene eseguito in modo asincrono come parte dell’elaborazione pianificata e non blocca il rendering della pagina di amministrazione.

## Funzionamento del controllo di aggiornamento

* Il controllo degli aggiornamenti confronta la versione del pacchetto `aem-assets-integration` installata con la versione più compatibile disponibile da [repo.magento.com](https://repo.magento.com/admin/dashboard).
* I risultati vengono memorizzati nella cache. Il caricamento di una pagina di amministrazione legge il risultato memorizzato nella cache più recente, anziché attivare una richiesta di rete in tempo reale.
* Se `repo.magento.com` non è disponibile o i metadati restituiti non sono validi, Commerce mantiene l&#39;ultimo risultato memorizzato nella cache e non blocca l&#39;amministratore.

>[!NOTE]
>
>Il controllo dell’aggiornamento è destinato alle distribuzioni Adobe Commerce on-premise e sul cloud.

## Visualizza notifiche di aggiornamento

Gli amministratori possono visualizzare una notifica di aggiornamento disponibile in una delle posizioni seguenti:

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* Menu a discesa di notifica dell’amministratore

Ogni notifica visualizza:

* Versione installata
* Versione disponibile
* Classificazione della versione
* Un collegamento alle note sulla versione

Selezionare **[!UICONTROL Remind me later]** per ignorare completamente la notifica per questa istanza di Commerce o per non ricevere tutte le notifiche di aggiornamento.

## Esegui un controllo di aggiornamento manuale

Per verificare immediatamente la disponibilità di un aggiornamento, eseguire il comando seguente dalla directory principale di Commerce:

```bash
bin/magento aem:assets:check-update
```

Questo comando controlla e segnala solo gli aggiornamenti disponibili. Non modifica i file Composer né distribuisce un aggiornamento. Per installare un aggiornamento, seguire le istruzioni del Compositore in [Installare i pacchetti Adobe Commerce](configure-commerce.md).

## Metadati di rilascio per i pacchetti di estensione

Il controllo di aggiornamento legge i metadati della versione dalla sezione `extra` del file `composer.json` del pacchetto installato:

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/it...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## Passaggio successivo

* [Installare pacchetti Adobe Commerce](configure-commerce.md)
