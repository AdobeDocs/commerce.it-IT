---
title: Aggiungere attributi personalizzati ai profili
description: Scopri come aggiungere attributi personalizzati ai profili dei clienti.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 5489910382edc70eea5d7c0ca94da41c653b577d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Aggiungere attributi personalizzati ai profili

Gli attributi di profilo personalizzati consentono di migliorare l&#39;identificazione del profilo cliente in Experience Platform utilizzando identificatori aggiuntivi oltre a `customerId` e `emailId` predefiniti. Questi identificatori aggiuntivi consentono una corrispondenza più precisa dei clienti e una migliore integrazione dei dati tra la piattaforma Commerce e Experience Platform.

>[!NOTE]
>
>Scopri come [aggiungere attributi personalizzati](custom-attributes.md) agli ordini.

## Vantaggi

- Utilizza più identificatori per migliorare la corrispondenza dei clienti.
- Mappa i campi personalizzati con attributi di identità in base alle tue esigenze aziendali.
- Riduci i profili duplicati e migliora la precisione dei dati dei clienti.
- Abilita esperienze cliente più mirate.

## Prerequisiti

Prima di implementare attributi di identità personalizzati, assicurati di:

- [Installare l’estensione Data Connection](install.md)
- [Connetti a Adobe Experience Platform](connect-data.md)
- [Inviare dati del profilo cliente](connect-data.md#send-customer-profile-data)

## Passaggio 1: configurare lo schema di Experience Platform

1. Accedi a Adobe Experience Platform e seleziona lo schema Commerce.
1. [Aggiungi campi di identità personalizzati](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/ui/resources/schemas?lang=en#custom-fields-for-standard-groups) a livello principale:
   - `hashedPID` (stringa) - Hash identità primaria
   - `hashedSID` (stringa) - Hash identità secondaria
   - `primaryID` (stringa) - Nome campo identità primaria
   - `secondaryID` (stringa) - Nome campo identità secondario

![Configurazione schema Experience Platform](./assets/aep-schema-configuration.png)

>[!NOTE]
>
>Puoi personalizzare i nomi esatti dei campi in base alle tue esigenze. Nell&#39;esempio vengono utilizzati `hashedPID` e `hashedSID` come campi di identità.

## Passaggio 2: creare classi di processori

Crea le seguenti classi di processori PHP nel modulo personalizzato:

### Classe AddressCustomHashedId

Il processore esegue l&#39;hash di `parent_id` e `entity_id` per gli indirizzi dei clienti.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['parent_id'] ?? '';
        $sid = $eventData['entity_id'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### Classe AddressCustomId

Questo processore imposta i nomi dei campi ID primario e secondario per gli eventi degli indirizzi.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

### CustomHashedId, classe

Il processore esegue l&#39;hash di `entity_id` e `email` per i profili cliente.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['entity_id'] ?? '';
        $sid = $eventData['email'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### Classe CustomId

Questo processore imposta i nomi dei campi ID primario e secondario per gli eventi profilo.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

>[!NOTE]
>Assicurarsi che sia `primaryID` che `secondaryID` siano inviati nei dati evento. Se manca una delle due, Commerce utilizza per impostazione predefinita:
>
>- primaryID = customerId
>- secondaryID = emailId

>[!BEGINSHADEBOX]

Dopo aver completato questi due passaggi:

- Lo schema Commerce in Experience Platform può acquisire correttamente le identità personalizzate per i dati dell’evento profilo.
- Le classi di processori nel codice PHP di Commerce raccolgono informazioni di identificazione personalizzate dagli eventi di profilo.

Ora, tutti i dati evento profilo inviati da Commerce contengono le informazioni di identificazione personalizzate.

>[!ENDSHADEBOX]

## Esempi di formato dati

Gli esempi seguenti mostrano la struttura JSON prevista per gli attributi di identità personalizzati sia negli attributi di profilo che nei formati dati del profilo cliente completo.

### Formato attributi profilo

```json
{
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "warehousecode": "1256",
    "method": "ina2354",
    "source": "commerce",
    "primaryID": "hashedPID",
    "secondaryID": "hashedSID"
  }
}
```

### Struttura completa del profilo cliente

```json
{
  "id": 137,
  "entity_id": "137",
  "created_at": "2025-02-10 20:10:30",
  "updated_at": "2022-02-10 20:10:31",
  "email": "customer@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "dob": "2007-10-01 00:00:00",
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "primaryID": "137",
    "secondaryID": "customer@example.com"
  },
  "_metadata": {
    "commerceEdition": "Adobe Commerce",
    "commerceVersion": "2.4.6",
    "eventsClientVersion": "1.9.0",
    "storeId": "1",
    "websiteId": "1",
    "storeGroupId": "1",
    "websiteCode": "base",
    "storeCode": "default",
    "storeViewCode": "main_website_store"
  }
}
```

## Risoluzione dei problemi

### Manca primaryID o secondaryID

- **Sintomo:** per impostazione predefinita i dati sono customerId/emailId anziché valori personalizzati.
- **Soluzione:** Verificare che `primaryID` e `secondaryID` siano impostati nell&#39;oggetto `profileAttributes`.

### Valori hash non validi

- **Sintomo:** I valori hash sono vuoti o non validi.
- **Soluzione:** Verificare che i campi di origine (`parent_id`, `entity_id`, `email`) contengano dati validi prima di eseguire l&#39;hashing.

### Processori non in esecuzione

- **Sintomo:** Gli attributi personalizzati non vengono visualizzati nei dati evento.
- **Soluzione:** Verificare che i processori siano registrati correttamente in `events.xml` e che il modulo sia abilitato.

### Mancata corrispondenza schema Experience Platform

- **Sintomo:** I dati non vengono visualizzati in Experience Platform o in errori di convalida dello schema.
- **Soluzione:** Assicurarsi che lo schema Experience Platform includa i campi di identità personalizzati con i tipi di dati corretti.
