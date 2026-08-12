---
title: Collega un altro conto PayPal per un sito Web
description: Completa l’onboarding di PayPal nell’Admin per collegare un account esercente PayPal diverso a un singolo sito web.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# Collega un altro conto PayPal per un sito Web

Per le istanze di Commerce con **più siti Web**, potrebbero essere necessari **diversi account esercente PayPal**. [!DNL Payment Services] abilita l&#39;onboarding di **siti Web** PayPal dopo l&#39;onboarding di **global**.

>[!NOTE]
>
> Questa funzione supporta solo la connessione di nuovi account.

## Prerequisiti per l’onboarding nell’ambito del sito web

L’onboarding a livello di sito web è disponibile solo quando il negozio soddisfa i seguenti requisiti:

- Installazione di [Commerce Services Connector](https://experienceleague.adobe.com/it/docs/commerce/user-guides/integration-services/saas) completata.
- Un conto PayPal è connesso all&#39;ambito globale (configurazione predefinita).

Per confermare, controlla che nell’ambito predefinito siano compilati i campi seguenti:

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

Se questi campi sono vuoti, devi prima [completare l&#39;onboarding globale](configure-admin.md). Il pulsante **[!UICONTROL Connect different account]** è disattivato fino a quando non si completano i prerequisiti.

## Avvia la connessione a livello di sito Web

1. Nella barra laterale _Admin_, vai a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**&#x200B;e scegli **[!UICONTROL Payment Methods]**.
1. Nel selettore dell&#39;ambito nell&#39;angolo in alto a sinistra, passa da **[!UICONTROL Default Config]** a **[!UICONTROL Website]** che desideri incorporare.
1. Fare clic su **[!UICONTROL Connect different account]**.

   Se il pulsante è disabilitato, l&#39;archivio non ha soddisfatto i [prerequisiti](#prerequisites-global-scope) indicati sopra.

## Completare la finestra modale di onboarding

Viene visualizzata una finestra popup.

1. Seleziona **[!UICONTROL Country]** dal menu a discesa.
1. Scegli il tipo di onboarding: **[!UICONTROL Basic]** o **[!UICONTROL Advanced]**.
1. Fare clic su **[!UICONTROL Next]**.

>[!NOTE]
>
> Se effettui l&#39;onboarding in Ungheria, Spagna o Austria, devi aprire e visualizzare il collegamento Termini e condizioni prima di fare clic sul pulsante **[!UICONTROL I Accept]**. Il pulsante è disattivato fino all&#39;apertura dei Termini e Condizioni.

## Accedi a PayPal

Dopo essere stato reindirizzato all’accesso a PayPal, accedi e completa i passaggi di onboarding in PayPal.

>[!IMPORTANT]
>
> Dopo aver fatto clic su **[!UICONTROL Confirm and Continue]**, la sessione per l&#39;ambito globale termina e inizia la connessione a livello di sito Web. Se hai fatto clic accidentalmente su **[!UICONTROL Connect different account]**, puoi annullare selezionando **[!UICONTROL Cancel]** o facendo clic sull&#39;icona **X** prima di confermare.

## Termina e torna all’Amministratore

1. Dopo aver completato i passaggi di PayPal, chiudi la finestra PayPal.
1. Fai clic su **[!UICONTROL Finish]** o su **X** nell&#39;angolo in alto a destra per chiudere il popup di onboarding.
1. La pagina di configurazione di Commerce si aggiorna automaticamente.

## Conferma il risultato

Dopo l’aggiornamento della pagina, controlla la pagina di configurazione dell’ambito del sito web per:

- **[!UICONTROL PayPal Merchant ID]** aggiornato per quel sito Web.
- Un’etichetta di stato che mostra il risultato dell’onboarding:

| Stato | Significato |
| --- | --- |
| `ACTIVE` | Onboarding completato |
| `PENDING` | L’onboarding è ancora in corso |
| `ERROR` | Onboarding non completato correttamente |

Se viene visualizzato lo stato `ERROR`, viene visualizzato un messaggio di errore che spiega il problema. Riprovare il processo di onboarding facendo nuovamente clic su **[!UICONTROL Connect different account]**.
