---
title: 'Gestione delle richieste di accesso a dati personali da parte dei servizi  [!DNL Commerce] '
description: Scopri come [!DNL Commerce] i servizi gestiscono le richieste di accesso ed eliminazione dei dati.
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
TQID: https://experienceleague.adobe.com/KhsveSMPR0tKmNzViEaWWHDu8fWve0GZjwsl2oyvx1k
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
subfeature_v2:
  - id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: d00e9f03-e50b-4162-b143-0c0817c937c2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 595
ht-degree: 1%

---

# Richieste di accesso a dati personali

Adobe Experience Platform Privacy Service fornisce un’API RESTful e un’interfaccia utente che consentono di gestire le richieste di dati dei clienti. Con Privacy Service, puoi inviare richieste di accesso e cancellazione dei dati personali dei clienti dalle applicazioni Adobe Experience Cloud, facilitando la conformità automatica alle normative legali e organizzative sulla privacy.

Per ulteriori informazioni su Privacy Service e su come creare e gestire le richieste di privacy, consulta la documentazione di Adobe Experience Platform:

* [Panoramica di Privacy Service](https://experienceleague.adobe.com/it/docs/experience-platform/privacy/home)
* [Gestione dei processi relativi alla privacy nell’interfaccia utente di Privacy Service](https://experienceleague.adobe.com/it/docs/experience-platform/privacy/ui/user-guide)

## Gestire le richieste di privacy dei dati di singoli utenti

È possibile inviare singole richieste per accedere ed eliminare i dati dei consumatori da [!DNL Commerce] in due modi:

* Tramite l&#39;**interfaccia utente di Privacy Service**. Consulta la documentazione [qui](https://experienceleague.adobe.com/it/docs/experience-platform/privacy/ui/user-guide#_blank).
* Tramite **API Privacy Service**. Consulta la documentazione [qui](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank) e le informazioni API [qui](https://developer.adobe.com/experience-platform-apis/#_blank).

Privacy Service supporta due tipi di richieste: **accesso ai dati** e **eliminazione dati**.

>[!NOTE]
>
>Questo articolo si concentra sull&#39;esecuzione di richieste di privacy per [!DNL Commerce]. Se prevedi di effettuare richieste di accesso a dati personali per [Platform data lake](https://experienceleague.adobe.com/it/docs/experience-platform/catalog/privacy), [Real-Time Customer Profile](https://experienceleague.adobe.com/it/docs/experience-platform/profile/privacy) o [Identity Service](https://experienceleague.adobe.com/it/docs/experience-platform/identity/privacy), consulta le rispettive guide utente. Tieni presente che le richieste di eliminazione e di accesso devono essere effettuate singolarmente per ogni sistema, in quanto una richiesta di accesso a dati personali inviata a Commerce non rimuove i dati da tutti questi sistemi.

## Accesso ai dati

Per **richieste di accesso**, specifica &quot;Commerce (Personalization)&quot; dall&#39;interfaccia utente (oppure `commerceMarketingData` come codice prodotto nell&#39;API).

## Eliminazione dei dati

Per le richieste di eliminazione, Privacy Service elimina i dati [!DNL Commerce] memorizzati nei servizi SaaS di Commerce a scopo di marketing, il che significa che i profili e gli ordini delle persone interessate non vengono più inviati alle applicazioni di marketing Adobe per l&#39;utilizzo in campagne e percorsi di clienti. Tuttavia, Privacy Service non elimina i dati nell&#39;applicazione [!DNL Commerce], in quanto potrebbero essere necessari per le esigenze transazionali degli esercenti. I commercianti sono responsabili di qualsiasi richiesta di eliminazione/accesso ai dati nell&#39;applicazione [!DNL Commerce]. Per ulteriori informazioni, consulta [Modello operativo e di sicurezza con responsabilità condivisa](https://experienceleague.adobe.com/it/docs/commerce-operations/security-and-compliance/shared-responsibility).

[!DNL Commerce] invierà ai commercianti le richieste di eliminazione inviando loro le informazioni per i soggetti interessati che richiedono l&#39;eliminazione di alcuni dati.

## Come creare richieste di accesso ed eliminazione

### Prerequisiti

Per richiedere l&#39;accesso e l&#39;eliminazione dei dati per Adobe [!DNL Commerce], è necessario disporre di:

* un ID organizzazione IMS
* un identificatore di identità della persona su cui desideri agire e i corrispondenti spazi dei nomi. Per ulteriori informazioni sugli spazi dei nomi delle identità in Adobe [!DNL Commerce] e Experience Platform, vedere [Panoramica sullo spazio dei nomi delle identità](https://experienceleague.adobe.com/it/docs/experience-platform/identity/features/namespaces).

### Esempio di accesso alle richieste/eliminazioni RGPD:

Per **richieste di accesso**, specifica &quot;Commerce (Personalization)&quot; dall&#39;interfaccia utente (o &quot;commerceMarketingData&quot; come codice prodotto nell&#39;API).

Per **richieste delete**, assicurarsi che la casella di controllo &quot;Commerce (Personalization)&quot; sia abilitata. Inoltre, se i dati del profilo cliente e dell&#39;ordine sono già stati inviati da [!DNL Commerce] a Adobe Experience Platform, è necessario inviare le richieste di eliminazione ai seguenti servizi downstream.

* Profilo (codice prodotto: &quot;profileService&quot;)
* AEP Data Lake (codice prodotto: &quot;AdobeCloudPlatform&quot;)
* Identità (codice prodotto: &quot;identity&quot;)

Per inviare le richieste di accesso ed eliminazione tramite l’API Privacy, devi autenticare e gestire le autorizzazioni per Privacy Service:

* [Autenticazione e accesso all’API di Privacy Service](https://experienceleague.adobe.com/it/docs/experience-platform/privacy/api/getting-started)
* [Gestire le autorizzazioni per Privacy Service](https://experienceleague.adobe.com/it/docs/experience-platform/privacy/permissions)

**Intestazioni richieste**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**Richiesta**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**Risposta**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
