---
title: Chiavi di accesso limitate
description: Scopri come creare, assegnare e ruotare le chiavi di accesso con restrizioni per proteggere le visualizzazioni di catalogo in [!DNL Adobe Commerce Optimizer] con autenticazione token firmato.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti as a Cloud Service e  [!DNL Adobe Commerce Optimizer]  di Adobe Commerce (infrastruttura SaaS gestita da Adobe)."
TQID: https://experienceleague.adobe.com/Jmze0Pq3kSNMIXqkkML-hmmlZnv-XKgeEgRB8Q8NZ6s
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
nudge: true
source-git-commit: 688bc6e28a4c5a94b1fe55c84f7c05401dd651bc
workflow-type: tm+mt
source-wordcount: 791
ht-degree: 0%

---

# Chiavi di accesso con restrizioni

Le chiavi di accesso con restrizioni consentono alle applicazioni client autorizzate di accedere a una [vista di catalogo privata](catalog-view.md). Solo le richieste che contengono un token firmato valido da una chiave assegnata possono recuperare i dati del catalogo. Tutte le altre richieste vengono negate, comprese quelle di acquirenti anonimi, di acquirenti a cui non è stato dato esplicitamente accesso a questa vista catalogo e di script che esaminano l’API.

## Casi d’uso chiave di accesso limitati

In [!DNL Adobe Commerce Optimizer], **[!UICONTROL Price Book ID]** determina i prezzi visualizzati da una richiesta, ovvero i prezzi, non chi può effettuare la richiesta. Qualsiasi cliente che conosce l’ID di una vista catalogo e l’ID di un listino prezzi può recuperare tali dati tramite l’API Merchandising. Le chiavi di accesso con restrizioni aggiungono un controllo separato e complementare: definiscono gli utenti che possono accedere a una visualizzazione di catalogo, indipendentemente dal listino prezzi dedicato.

Le chiavi di accesso con restrizioni sono comunemente utilizzate per:

- **Determinazione prezzi B2B basata su contratto**: limitare una visualizzazione di catalogo collegata a un listino prezzi dedicato in modo che solo l&#39;acquirente a cui si applica possa eseguire query. Le altre organizzazioni di acquisto e il pubblico non possono.
- **Portali per partner e rivenditori** - Limita un sottoinsieme del catalogo ai partner approvati che si integrano direttamente con l&#39;API Merchandising.
- **Anteprime pre-release**: consente a un sistema interno o partner attendibile di visualizzare in anteprima i prodotti in arrivo prima che siano visibili pubblicamente.

>[!IMPORTANT]
>
>La generazione di chiavi, la firma dei token e la rotazione sono attualmente gestite interamente dall’applicazione client back-end che autentica gli acquirenti. [!DNL Adobe Commerce Optimizer] non genera o ruota queste chiavi per tuo conto.

## Funzionamento delle chiavi di accesso con restrizioni

Una chiave ad accesso limitato è il componente pubblico di una coppia di chiavi RSA. L’applicazione client genera e utilizza questa chiave per dimostrare di essere autorizzata a leggere una vista di catalogo privata. In questo contesto, per &quot;applicazione client&quot; si intende il sistema back-end che autentica gli acquirenti, ad esempio una logica personalizzata su [!DNL Adobe Commerce] o un back-end di terze parti, mai il front-end storefront stesso.

I passaggi seguenti descrivono come una coppia di chiavi e un token firmato passano dalla creazione alla convalida:

1. L&#39;applicazione client genera una coppia di chiavi RSA e mantiene la chiave privata.
1. La chiave **public** in [!DNL Commerce Optimizer] è stata registrata come chiave ad accesso limitato.
1. L’applicazione client firma un token web JSON (JWT) con la chiave privata e lo include con ogni richiesta a una vista di catalogo privata.
1. [!DNL Commerce Optimizer] convalida la firma del token in base alla chiave pubblica registrata e, se valida, restituisce i dati del catalogo richiesti.

## Creare una chiave di accesso con restrizioni

Per il test iniziale delle visualizzazioni del catalogo privato, generare una coppia di chiavi utilizzando uno strumento quale [!DNL OpenSSL]. Mantieni segreta la chiave privata: solo la chiave pubblica viene caricata in [!DNL Commerce Optimizer].

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

La dimensione della chiave deve essere compresa tra 2048 e 8192 bit. `public-key.pem` contiene il valore incollato nel campo **[!UICONTROL Public key]** di seguito.

## Aggiungi una chiave di accesso con restrizioni a [!DNL Commerce Optimizer]

1. Dal menu a sinistra di [!DNL Adobe Commerce Optimizer Studio], vai a **[!UICONTROL Store setup]** e fai clic su **[!UICONTROL Restricted access keys]**.

   ![Elenco di chiavi di accesso con restrizioni, con il pulsante Aggiungi chiave di accesso con restrizioni](../assets/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Fare clic su **[!UICONTROL Add Restricted Access Key]**.

1. Immetti i dettagli chiave:

   ![Aggiungi modulo chiave di accesso limitato con titolo, data di scadenza e campi chiave pubblica](../assets/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** - Etichetta per identificare la chiave, visualizzata nell&#39;elenco delle chiavi e nel selettore delle chiavi di visualizzazione del catalogo, ad esempio `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]** - Data e ora (UTC) dopo le quali la chiave non viene più rispettata, anche per un token non ancora scaduto.
   - **[!UICONTROL Public key]**: la chiave pubblica RSA con codifica PEM in formato SPKI (Subject Public Key Info), inclusi i marcatori `-----BEGIN PUBLIC KEY-----` e `-----END PUBLIC KEY-----`. Deve essere univoco in tutto l’ambiente.

1. Fare clic su **[!UICONTROL Save]**.

Le chiavi non sono modificabili dopo la creazione. Per modificare un valore, elimina la chiave e creane una nuova. Vedere [Ruotare una chiave](#rotate-a-key) per eseguire questa operazione senza interrompere l&#39;accesso.

## Assegnare una chiave a una vista catalogo

Una chiave di accesso con restrizioni limita l&#39;accesso solo dopo che è stata assegnata a una visualizzazione catalogo con **[!UICONTROL Catalog Protection]** abilitato. Consulta [Proteggere una vista catalogo](private-catalog-view.md#protect-a-catalog-view) per i passaggi di configurazione.

## Eliminare una chiave

1. Nella pagina **[!UICONTROL Restricted access keys]** trovare la chiave che si desidera rimuovere e fare clic su **[!UICONTROL Delete]**.

   Se la chiave viene assegnata a una o più visualizzazioni catalogo, un avviso spiega che le applicazioni client che si basano su tale chiave perdono l’accesso. Le visualizzazioni del catalogo rimangono protette, non diventano accessibili al pubblico.

1. Conferma l’eliminazione.

## Ruotare una chiave

Per ruotare una chiave senza interrompere l’accesso, tieni presente che a una vista catalogo possono essere assegnate fino a tre chiavi alla volta:

1. Genera una nuova coppia di chiavi e aggiungi la nuova chiave pubblica come nuova chiave ad accesso limitato.
1. Assegna la nuova chiave alla vista catalogo insieme alla chiave esistente.
1. Inizia a firmare nuovi token con la nuova chiave privata per completare il rollover della chiave.
1. Una volta confermate tutte le applicazioni client sulla nuova chiave, rimuovi ed elimina la chiave precedente.

## Limiti

Vedi [Visualizzazioni catalogo e limiti dei criteri](../boundaries-limits.md#catalog-views-and-policies).

## Altri argomenti correlati

- [Visualizzazioni catalogo privato](private-catalog-view.md)—Scopri come proteggere una visualizzazione catalogo con chiavi di accesso limitato.

