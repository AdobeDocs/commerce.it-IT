---
title: Visualizza stato di sincronizzazione di AEM Assets
description: Esamina le risorse sincronizzate in un elenco incentrato sulle risorse in Commerce Admin.
feature: CMS, Media, Integration
source-git-commit: 446739ffad0da97e2e923e6e02be3f8f6b3eb2b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Visualizza stato di sincronizzazione di AEM Assets

La visualizzazione **[!UICONTROL Sync Status]** fornisce un elenco delle risorse incentrato sulle risorse sincronizzate tramite l&#39;integrazione AEM Assets. Puoi utilizzarlo per trovare, esaminare e risolvere i problemi delle risorse in base ai loro attributi, anziché navigare prodotto per prodotto nel catalogo.

![Visualizzazione stato sincronizzazione AEM Assets](../assets/aem-assets-sync-status-view.png){width="700" zoomable="yes"}

>[!NOTE]
>
> [!UICONTROL Sync Status] non è disponibile per [!DNL Adobe Commerce Optimizer].

## Apri stato sincronizzazione

Nella barra laterale _Admin_, passa a **[!UICONTROL System]** > **[!UICONTROL AEM Assets]** > **[!UICONTROL Sync Status]**.

![Stato sincronizzazione AEM Assets nel menu di sistema](../assets/aem-assets-configuration-admin-menu.png){width="600" zoomable="yes"}

## Integrazione sincronizzata integrità

Nella parte superiore della pagina, il banner **Stato di sincronizzazione di AEM** riepiloga lo stato della pipeline e il numero di eventi in attesa di elaborazione. Selezionare **[!UICONTROL Refresh]** per aggiornare il banner di integrità della sincronizzazione.

## Elenco risorse

Nella griglia sono elencate le risorse elaborate dalla pipeline di sincronizzazione di AEM Assets e il relativo stato di sincronizzazione corrente. Ogni riga rappresenta una risorsa e il relativo stato di sincronizzazione in Commerce. Non rappresenta un record di prodotto.

| Colonna | Descrizione |
|--------|-------------|
| **ID risorsa** | Identificatore di risorsa AEM (ad esempio, `urn:aaid:aem:…`). |
| **Stato** | Risultato dell’ultimo tentativo di sincronizzazione per la risorsa. I valori possibili sono **Operazione completata**, **Operazione non riuscita** o **In attesa**. |
| **Elaborazione** | Elaborazione data e ora iniziata per la risorsa. |
| **Inviato** | Data e ora di invio dell&#39;evento di sincronizzazione. |
| **Errore** | Messaggio di errore quando **Stato** indica un errore; vuoto quando la sincronizzazione è riuscita. |

### Filtrare le risorse

1. Selezionare **[!UICONTROL Filters]** per espandere il pannello dei filtri.

1. Immettere un **ID risorsa** o scegliere un valore **Stato**.

1. Selezionare **[!UICONTROL Apply Filters]** per aggiornare la griglia oppure **[!UICONTROL Cancel]** per chiudere il pannello senza applicare modifiche.

I filtri si applicano ai dati a livello di risorsa, consentendo di isolare le sincronizzazioni non riuscite o di tracciare una risorsa specifica senza aprire singoli prodotti.

## sincronizzazioni non riuscite

Quando **Stato** mostra un errore, controlla la colonna **Errore** nella griglia per il messaggio restituito dalla pipeline di sincronizzazione.

Esaminare il messaggio di errore completo e i dettagli dell&#39;ultimo tentativo di sincronizzazione per diagnosticare l&#39;errore.

[!BADGE Solo PaaS]{type=Informative tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe)."} Per ulteriori informazioni sulla risoluzione dei problemi, vedere [Corrispondenza automatica predefinita](../synchronize/default-match.md). I file di log di integrazione sono disponibili in `/var/log/aem-assets-integration.log` e `/var/log/aem-assets-integration-errors.log` nell&#39;istanza di Commerce.
