---
title: Record profilo
description: Scopri quali dati acquisisce un record di profilo.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# [!DNL Data Connection] record profilo

Di seguito sono descritti i dati del record del profilo di Commerce disponibili quando si installa l&#39;estensione [!DNL Data Connection]. I dati nei record del profilo vengono inviati a Adobe Experience Platform.

## Record profilo

Gli aggiornamenti dei record profilo sono disponibili in Experience Platform quando viene creato, aggiornato o eliminato un nuovo profilo.

### Dati raccolti dal record del profilo

Di seguito sono descritti i dati acquisiti per un record di profilo.

| Campo | Descrizione |
|---|---|
| `channel` | Contiene informazioni sull’origine dei dati. Sia `_id` che `_type` contengono [valori con spazio dei nomi](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/schema/namespaces). |
| `channel._id` | L&#39;identificatore univoco del canale, ad esempio `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica l&#39;origine dei dati del canale, ad esempio `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Contiene informazioni sul cliente. |
| `person.name` | Contiene informazioni sul nome del cliente. |
| `person.name.firstName` | Contiene il nome del cliente. |
| `person.name.lastName` | Contiene il cognome del cliente. |
| `person.birthDate` | Data di nascita dell’acquirente. |
| `personalEmail` | Un indirizzo e-mail personale. |
| `personalEmail.address` | L&#39;indirizzo tecnico, ad esempio `name@domain.com`, come comunemente definito in RFC2822 e standard successivi. |
| `billingAddress` | Indirizzo postale di fatturazione. |
| `billingAddress.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `billingAddress.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `billingAddress.city` | Il nome della città. |
| `billingAddress.state` | Nome dello stato. Questo è un campo in formato libero. |
| `billingAddress.country` | Il nome del territorio amministrato dal governo. A parte `xdm:countryCode`, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `billingAddress.primary` | Indica se si tratta dell’indirizzo di fatturazione principale. Valore sempre `False`. |
| `billingAddressPhone` | Numero di telefono associato all’indirizzo di fatturazione. |
| `billingAddressPhone.number` | Il numero di telefono. Il numero di telefono è una stringa e può includere caratteri significativi come parentesi quadre `()`, trattini `-` o caratteri per indicare identificatori di sotto-composizione come le estensioni `x`, ad esempio `1-353(0)18391111` o `+613 9403600x1234`. |
| `billingAddressPhone.primary` | Indica se si tratta del numero di telefono principale per l’indirizzo di fatturazione. Valore sempre `False`. |
| `shippingAddress` | L’indirizzo postale di spedizione. |
| `shippingAddress.street1` | Informazioni stradali primarie, numero di appartamento, numero civico e nome della strada. |
| `shippingAddress.street2` | Seconda riga facoltativa sulle informazioni stradali. |
| `shippingAddress.city` | Il nome della città. |
| `shippingAddress.state` | Nome dello stato. Questo è un campo in formato libero. |
| `shippingAddress.country` | Il nome del territorio amministrato dal governo. A parte `xdm:countryCode`, questo è un campo in formato libero che può avere il nome del paese in qualsiasi lingua. |
| `shippingAddress.primary` | Indica se si tratta dell&#39;indirizzo di spedizione principale. Valore sempre `False`. |
| `shippingAddressPhone` | Numero di telefono associato all’indirizzo di spedizione. |
| `shippingAddressPhone.number` | Il numero di telefono. Il numero di telefono è una stringa e può includere caratteri significativi come parentesi quadre `()`, trattini `-` o caratteri per indicare identificatori di sotto-composizione come le estensioni `x`, ad esempio `1-353(0)18391111` o `+613 9403600x1234`. |
| `shippingAddressPhone.primary` | Indica se si tratta del numero di telefono principale per l&#39;indirizzo di spedizione. Valore sempre `False`. |
| `userAccount` | Indica eventuali dettagli di fedeltà, preferenze, processi di accesso e altre preferenze dell’account. |
| `userAccount.startDate` | La data in cui il profilo è stato creato per la prima volta. |

>[!NOTE]
>
>Ogni record di profilo include anche il campo [`identityMap`](https://experienceleague.adobe.com/it/docs/experience-platform/xdm/field-groups/profile/identitymap), che include l&#39;ID cliente Commerce generato dal sistema come identificatore primario del profilo e un ID e-mail utilizzato come identificatore secondario.

Scopri come [creare uno schema specifico per il record del profilo](profile-data.md) in grado di acquisire i dati dai record del profilo.
