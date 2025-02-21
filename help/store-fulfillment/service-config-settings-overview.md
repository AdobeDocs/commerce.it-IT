---
title: Panoramica sulla configurazione per l'evasione del punto vendita
description: Scopri i tipi di impostazioni di configurazione dell’amministratore disponibili per personalizzare le funzionalità di implementazione estesa fornite dalla soluzione Store Fulfillment e crea un collegamento alle istruzioni per completare la configurazione.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Panoramica sulla configurazione per il Store Fulfillment

In Adobe Commerce Admin, le impostazioni di configurazione per Store Fulfillment Services di Walmart Commerce Technologies sono suddivise per tipo.

**Archivia impostazioni configurazione evasione per tipo**

| **Tipo** | **Descrizione** | **API configurabile** |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| [Configurazione generale](enable-general.md) | Integrazione generale impostata per la soluzione Store Fulfillment, le relative funzioni attive e le credenziali per la connessione ai servizi di evasione. | No |
| [Configurazione e-mail vendite](sales-emails.md) | Impostare ulteriori modelli di posta elettronica per le notifiche dei clienti inviate durante il processo di archiviazione. | No |
| [Configurazione archivio esercenti](merchant-store-configuration.md) | Imposta le origini Inventory management avanzate come negozi per esercenti. | Sì |
| [Gestione magazzino prodotto](product-stock.md) | Configura i messaggi sulle azioni e le funzioni disponibili per i clienti. | Sì |
| [Trasferimento Source Inventory management](inventory-stock-transfer.md) | Impostare un nuovo magazzino e trasferire il magazzino al di fuori del magazzino predefinito. | Sì |
| [Configurazione più siti Web/ambito](multi-site-and-scope-config.md) | Configura le scorte e i metodi di consegna per più siti Web/ambiti di archiviazione. | No |
| [Configurazione sistema processi in background](background-processes.md) | Configurare le pianificazioni dei processi in background utilizzati nella sincronizzazione dei dati con i servizi di evasione. | No |
| [Impostazione percorso archivio e mappatura](store-location-map-provider-setup.md) | Configurare la possibilità di utilizzare un provider di servizi a distanza per cercare negozi al dettaglio e visualizzare queste informazioni nella mappa SLS | Sì |
| [Configurazione esperienza di archiviazione](check-in-experience-setup.md) | Configura il colore dell&#39;auto e le opzioni di creazione dell&#39;auto che saranno disponibili durante il check-in | Sì |
| [Configurazione utente](user-setup.md) | Gestisci gli account utente, i ruoli e le autorizzazioni per gli associati allo store che utilizzano l&#39;app Store Assist. ambiti. | Sì |
| [Configurazione app](app-setup.md) | Verifica le configurazioni disponibili per l’app Store Assist necessaria per completare il processo di onboarding. Queste impostazioni non possono essere configurate dall’amministratore di Adobe Commerce. | Sì |

## Utilizza il riferimento di configurazione

Visualizzare il riferimento alla configurazione per ogni tipo di impostazione selezionando il nome del tipo nella tabella _Archivia impostazioni di configurazione del completamento per tipo_.

Nel riferimento di configurazione per ciascun tipo, i dettagli di configurazione vengono visualizzati in una tabella con le seguenti intestazioni di colonna:

- **Il campo** fa riferimento al nome del campo da configurare

- **Descrizione** fornisce dettagli importanti sullo scopo e sul comportamento del campo

- **Ambito** indica l&#39;ambito di configurazione Adobe Commerce per l&#39;impostazione (globale, sito Web, archivio)

- Il valore **Required** indica se è necessario impostare un valore nel campo

Per informazioni tecniche, puoi anche trovare il percorso di configurazione interno di ciascun campo.
