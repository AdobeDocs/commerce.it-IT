---
title: Verifica accesso al servizio di migrazione
description: Scopri come verificare l’accesso end-to-end all’API del servizio di migrazione dati di Commerce, confermando la raggiungibilità della rete, l’autenticazione IMS e l’autorizzazione del tenant.
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 1%

---

# Verificare l’accesso al servizio di migrazione

{{bulk-data-early-access}}

Utilizza questa guida per verificare l’accesso end-to-end all’API Commerce Data Migration Service (CDMS) dal tuo ambiente. Una chiamata con esito positivo convalida simultaneamente la raggiungibilità di rete dagli IP in uscita (IP in uscita), dall’autenticazione IMS e dall’autorizzazione del tenant.

Completa questa guida dopo aver completato tutti gli elementi nella [Lista di controllo preparazione cliente](readiness-checklist.md) e prima di eseguire la migrazione descritta nella [guida alla migrazione](migration-guide.md).

## Prerequisiti

- Credenziali server-to-server OAuth 2.0 (ID client e segreto client) create in [Adobe Developer Console](https://developer.adobe.com/console/).
- ID organizzazione IMS, nel formato `<org>@AdobeOrg`. L’organizzazione deve essere proprietaria del tenant di destinazione.
- L&#39;ID tenant IMS alfanumerico di destinazione `tenantId`, di 22 caratteri.
- Indirizzi IP in uscita inviati e inseriti nell&#39;elenco Consentiti da Adobe per il gateway CDMS. In caso di dubbi sugli indirizzi IP o sul loro stato, effettua le coordinate con il team di Adobe.
- L&#39;host del servizio specifico dell&#39;area dalla tabella [Host del servizio per ambiente e area](#service-hosts-by-environment-and-region).

## Generare un token di accesso IMS

Genera un token di accesso utilizzando le credenziali server-to-server OAuth 2.0 con la concessione `client_credentials`. L’host IMS in questo passaggio è lo stesso per tutte le aree di dati. Solo l’host CDMS cambia per area geografica.

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## Chiamare l’API List Migrations

La richiesta seguente recupera l’elenco delle migrazioni per il tenant e richiede il token di accesso del passaggio precedente. Selezionare l&#39;host per la propria area dalla tabella [Host del servizio per ambiente e area](#service-hosts-by-environment-and-region). Il flag `-i` stampa la riga di stato HTTP e le intestazioni di risposta in modo da poter confermare il risultato.

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## Interpretare la risposta

| Codice HTTP | Significato | Esempio di corpo della risposta |
| --- | --- | --- |
| 200 | Operazione completata. Connettività, autenticazione e autorizzazione tenant sono tutte passate. Il corpo della risposta contiene l&#39;elenco delle migrazioni per il tenant. | `{"migrations":[...]}` |
| 401 | Token Bearer mancante o non valido, rifiutato prima di raggiungere il servizio. [Rigenerare il token](#generate-an-ims-access-token). | Varia (generato da gateway) |
| 403 | L’utente autenticato non dispone delle autorizzazioni di migrazione per questo tenant. | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | Errore interno del server. | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>Se la richiesta scade o la connessione viene rifiutata e non viene restituito alcuno stato HTTP, è probabile che l’IP in uscita non venga inserito nell&#39;elenco Consentiti o che si stia utilizzando un host errato. Conferma l’host della regione nella tabella seguente e gli IP inseriti nell&#39;elenco Consentiti.

## Host di servizio per ambiente e area geografica

| Area geografica o ambiente | Host |
| --- | --- |
| Sandbox o pre-produzione | `https://na1-sandbox.api.commerce.adobe.com` |
| Nord America | `https://na1.api.commerce.adobe.com` |
| Europa | `https://eu1.api.commerce.adobe.com` |
| India | `https://in1.api.commerce.adobe.com` |
| Regno Unito | `https://uk1.api.commerce.adobe.com` |
| Australia e Nuova Zelanda | `https://au1.api.commerce.adobe.com` |

## Passaggi successivi

Dopo aver confermato l&#39;accesso, passare alla [guida alla migrazione](migration-guide.md) per avviare la configurazione dell&#39;ambiente e l&#39;esecuzione della migrazione.
