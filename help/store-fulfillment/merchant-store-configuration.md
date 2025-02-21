---
title: Configurazione archivi commerciali
description: Imposta le origini Inventory management avanzate come negozi per esercenti.
role: Admin
level: Experienced
feature: Shipping/Delivery, Inventory, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 0%

---

# Configurazione dei Negozi commerciali (Source)

Questa soluzione migliora le funzionalità native di Inventory management estendendo le origini di magazzino con funzioni orientate alle operazioni per i commercianti.

- Aggiungere le coordinate geografiche per il percorso del punto vendita
- Indicare l&#39;origine come [!DNL Store Pickup Location] e specificare le funzionalità di spedizione disponibili (Spedisci al negozio, Spedisci dal negozio)
- Specifica le opzioni di prelievo disponibili (in negozio o a bordo campo), le istruzioni di prelievo personalizzate e altre informazioni per comunicare ai clienti dettagli e istruzioni per il prelievo

I termini _source_ e _merchant store location_ sono utilizzati in modo intercambiabile. Tutti i record sono origini di inventario, ma le origini possono anche essere ubicazioni di magazzini commerciali, a seconda delle impostazioni di configurazione.

Gestire la configurazione degli archivi commerciali dall&#39;amministratore: **[!UICONTROL Stores > Inventory > Sources >  Edit Source]**.

>[!NOTE]
>
>Durante il processo di configurazione, potrebbe essere necessario svuotare la cache dopo aver creato o aggiornato le origini esistenti.

## **Generale**

<table>
<tbody>
<tr>
<th>Campo</th>
<th>Descrizione</th>
<th>Ambito</th>
<th>Obbligatorio</th>
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordinata latitudinale del punto vendita esercente. Queste informazioni richieste vengono utilizzate nella ricerca della posizione e nel posizionamento della mappa nell’esperienza di vetrina. Il valore deve corrispondere all’indirizzo esatto dell’archivio per superare la convalida.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordinata longitudinale del punto vendita. Queste informazioni richieste vengono utilizzate nella ricerca della posizione e nel posizionamento della mappa nell’esperienza di vetrina. Il valore deve corrispondere all’indirizzo esatto dell’archivio per superare la convalida.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Imposta l'origine come posizione di ritiro da store disponibile. Questa impostazione determina se l’origine viene sincronizzata e visualizzata dai visitatori.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong><br><code>Extension Attribute: allow_ship_to_store</code></td>
<td>Configurare le funzionalità di spedizione al punto vendita a livello di origine. Per ulteriori informazioni, vedere l'opzione [Configurazione generale](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]
</tr>
<tr>
<td><strong>[!UICONTROL Latitude]</strong></br><code>Base Attribute: latitude</code></td>
<td>Coordinata latitudinale del punto vendita esercente. Queste informazioni richieste vengono utilizzate nella ricerca della posizione e nel posizionamento della mappa nell’esperienza di vetrina. Il valore deve corrispondere all’indirizzo esatto dell’archivio per superare la convalida.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Longitude]</strong></br><code>Base Attribute: Longitude</code></td>
<td>Coordinata longitudinale del punto vendita. Queste informazioni richieste vengono utilizzate nella ricerca della posizione e nel posizionamento della mappa nell’esperienza di vetrina. Il valore deve corrispondere all’indirizzo esatto dell’archivio per superare la convalida.</td>
<td>Globale</td>
<td>Sì</td>
</tr>
<tr>
<td><strong>[!UICONTROL Use as Pickup Location]</br></strong><code>Base Attribute: is_pickup_location_active</code></td>
<td>Imposta l'origine come posizione di ritiro da store disponibile. Questa impostazione determina se l’origine viene sincronizzata e visualizzata dai visitatori.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship to Store]</strong></br> <code>Extension Attribute: [!DNL allow_ship_to_store]</code></td>
<td>Configurare le funzionalità di spedizione al punto vendita a livello di origine. Per ulteriori informazioni, vedere l'opzione [Configurazione generale](enable-general.md), <strong>[!UICONTROL Enable Ship To Store]</strong>.</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
 <td>Configurare le funzionalità di spedizione dal punto vendita a livello di origine. Per ulteriori informazioni, vedere l'opzione [Configurazione generale](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td>Globale</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong><code></br><code>Extension Attribute: [!DNL use_as_shipping_source]</code></td>
<td>Configurare le funzionalità di spedizione dal punto vendita a livello di origine. Per ulteriori informazioni, vedere l'opzione [Configurazione generale](enable-general.md), [!UICONTROL Enable Ship From Store].</td>
<td>Globale</td>
<td>No</td>
</tr>
</tbody>
</table>



| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Latitude]**</br>`Base Attribute: latitude` | Coordinata latitudinale del punto vendita esercente. Queste informazioni richieste vengono utilizzate nella ricerca della posizione e nel posizionamento della mappa nell’esperienza di vetrina. Il valore deve corrispondere all’indirizzo esatto dell’archivio per superare la convalida. | Globale | Sì |
| **[!UICONTROL Longitude]**</br>`Base Attribute: Longitude` | Coordinata longitudinale del punto vendita. Queste informazioni richieste vengono utilizzate nella ricerca della posizione e nel posizionamento della mappa nell’esperienza di vetrina. Il valore deve corrispondere all’indirizzo esatto dell’archivio per superare la convalida. | Globale | Sì |
| **[!UICONTROL Use as Pickup Location]**</br>`Base Attribute:[!DNL is_pickup_location_active]` | Imposta l&#39;origine come posizione di ritiro da store disponibile. Questa impostazione determina se l’origine viene sincronizzata e visualizzata dai visitatori. | Globale | No |
| **[!UICONTROL Enable Ship to Store]**</br>`Extension Attribute: [!DNL allow_ship_to_store]` | Configurare le funzionalità di spedizione al punto vendita a livello di origine. Per ulteriori informazioni, vedere l&#39;opzione [Configurazione generale](enable-general.md), **[!UICONTROL Enable Ship To Store]**. | Globale | No |
| **[!UICONTROL Enable Ship From Store]**</br>`Extension Attribute: [!DNL use_as_shipping_source]` | Configurare le funzionalità di spedizione dal punto vendita a livello di origine. Per ulteriori informazioni, vedere l&#39;opzione [Configurazione generale](enable-general.md), [!UICONTROL Enable Ship From Store] | Globale | No |

{style="table-layout:auto"}

## Configurazione del percorso di prelievo

| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Allow In-Store Pickup]**</br>`Extension Attribute: [!DNL store_pickup_enabled]` | Una delle due opzioni di prelievo. [!DNL In-Store Pickup] si riferisce alla possibilità di consentire a un cliente di accedere al punto vendita per recuperare l&#39;ordine. </br></br>Se abilitata, questa opzione potrebbe essere presentata al cliente durante l&#39;estrazione. </br></br>Questa opzione esegue anche l&#39;override della configurazione globale a [!UICONTROL Enable In-store Pickup] configurata in [!UICONTROL Delivery Method] per [!UICONTROL In-store Pickup] | Globale | No |
| **Istruzioni per il ritiro dal negozio**</br>`Extension Attribute: store_pickup_instructions` | Messaggio personalizzabile consegnato al cliente nella notifica e-mail **Ordina pronto per il ritiro nello store**. | Globale | No |
| **Consenti Curbside**</br>`Extension Attribute: curbside_enabled` | Una delle due opzioni di prelievo. La consegna a domicilio consente al cliente di parcheggiare il proprio veicolo in un punto designato presso il negozio. In questo caso, l&#39;ordine viene consegnato al cliente da un addetto al negozio. </br></br>Se abilitata, questa opzione può essere presentata al cliente durante l&#39;estrazione. Inoltre, al cliente potrebbe essere richiesto di descrivere il veicolo e il parcheggio durante il processo di check-in. </br></br>Questa opzione sostituisce anche la configurazione globale in **Abilita prelievo in Curbside** configurata nel **metodo di consegna** per **prelievo in negozio** | Globale | No |
| **[!UICONTROL Curbside Instructions]**</br>`Extension Attribute: curbside_instructions` | Messaggio personalizzabile consegnato al cliente nella notifica e-mail [!UICONTROL Order Ready For Pickup in Store]. | Globale | No |
| **[!UICONTROL Estimated Pickup Lead Time]**</br>`Extension Attribute: pickup_lead_time` | Il numero di minuti necessari prima che un ordine venga ricevuto, prelevato e pronto per essere ritirato. </br></br>Queste informazioni vengono utilizzate per visualizzare i tempi stimati per il ritiro degli ordini ai clienti sul sito Web.</br></br> L&#39;impostazione di questa opzione sostituisce la configurazione globale per **Lead time di prelievo stimato** configurata per **Metodo di consegna** nella configurazione **Pickup in-store**. | Globale | No |
| **[!UICONTROL Estimated Pickup Time Label]**</br>`Extension Attribute: pickup_time_label` | Etichetta che visualizza il numero di minuti rimanenti al momento in cui un ordine è pronto per essere prelevato.</br></br> Quando si personalizza questa etichetta, è possibile utilizzare il codice %1 per inserire il **lead time di prelievo stimato**.</br></br> L&#39;impostazione di questa opzione sostituisce la configurazione globale per [!UICONTROL Estimated Pickup Time Label] configurata per [!UICONTROL Delivery Method] in [!UICONTROL In-store Pickup]. | Globale | No |

### **Ore di apertura**

| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Location Timezone]**</br>`Extension Attribute: timezone` | Il fuso orario della posizione del negozio di articoli commerciali. Per ogni giorno, impostare gli orari di apertura e chiusura.</br></br>Queste impostazioni vengono utilizzate per ottimizzare i tempi di ritiro stimati e nei rapporti del servizio di evasione. | Globale | Sì |
| **[!UICONTROL Opening Hours]**</br>`Internal Attribute: inventory_source_opening_hours_dynamic_rows` | Gli orari operativi del punto vendita. </br></br>Queste informazioni possono essere utilizzate per ottimizzare i tempi di ritiro stimati e nei rapporti del servizio di evasione. | Globale | Sì |

### Configurare le opzioni dell&#39;interfaccia Esperienza di archiviazione



| **Campo** | **Descrizione** | **Ambito** | **Obbligatorio** |
|---------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|--------------|
| **[!UICONTROL Use Parking Spots]**</br>`Extension Attribute: parking_spots_enabled` | Specifica se il punto vendita mercantile dispone di aree di parcheggio designate per il ritiro a bordo strada. </br></br>Se questa opzione è attivata, è possibile configurare i parcheggi disponibili. | Globale | No |
| **[!UICONTROL Is Parking Spot a Mandatory Field?]**</br>`Extension Attribute: parking_spot_mandatory` | Specifica se l’identificazione del parcheggio è necessaria per i clienti durante l’esperienza di acquisto.</br></br>Se questa opzione è attivata, al cliente viene richiesto di specificare il proprio parcheggio all&#39;arrivo. Se è disattivato, il cliente può saltare questo input. | Globale | No |
| **[!UICONTROL Parking Spots List]**</br> `Internal Attribute: inventory_source_parking_spot_dynamic_rows` | I posti auto disponibili in questo negozio di merchant posizione per il ritiro a bordo strada. Utilizza l’interfaccia fornita per assegnare un nome a ogni punto.</br></br> Non è necessario assegnare un nome a ogni posto di parcheggio, ma solo ai punti indicati per il bordo stradale. Ad esempio, puoi avere le righe da A a G di parcheggio disponibili, ma solo i primi 8 punti della riga A sono designati per il ritiro a bordo strada. In questo scenario, puoi definire 8 punti, ad esempio A1, A2, A3 e così via. | Globale | No |
| **[!UICONTROL Allow "Other" Parking Spot Field]**</br>`Extension Attribute: custom_parking_spot_enabled` | Se attivata, questa impostazione consente al cliente di descrivere il proprio parcheggio durante il check-in. | Globale | No |
| **[!UICONTROL Use Car Color]**</br>`Extension Attribute: use_car_color` | Specifica se supportare la raccolta del colore del veicolo dal cliente durante il check-in. </br></br> Le selezioni disponibili per [!UICONTROL Car Color] sono configurate nelle impostazioni di amministrazione [ sistema per l&#39;esperienza di archiviazione](check-in-experience-setup.md). | Globale | No |
| **[!UICONTROL Is Car Color a Mandatory Field?]**</br>`Extension Attribute: car_color_mandatory` | Specificare se l&#39;identificazione del colore del veicolo è necessaria per i clienti durante il check-in.</br></br>Se questa opzione è attivata, al cliente viene richiesto di specificare il colore del proprio veicolo all&#39;arrivo. Se è disattivato, il cliente può saltare questo input. | Globale | No |
| **[!UICONTROL Use Car Make]** </br>`Extension Attribute: use_car_make` | Specifica se supportare la raccolta della marca del veicolo dal cliente durante il check-in.</br></br> Le selezioni disponibili per [!UICONTROL Car Make] sono configurate nelle impostazioni di amministrazione [ sistema per l&#39;esperienza di archiviazione](check-in-experience-setup.md). | Globale | No |
| **[!UICONTROL Is Car Make a Mandatory Field?]**</br>`Extension Attribute: car_make_mandatory` | Specificare se l&#39;identificazione della marca del veicolo è necessaria per i clienti durante il check-in.</br></br>Se questa opzione è attivata, al cliente viene richiesto di specificare la marca del proprio veicolo all&#39;arrivo. Se è disattivato, il cliente può saltare questo input. | Globale | No |
| **[!UICONTROL Use Additional Information]**</br> `Extension Attribute: use_additional_information` | Specifica se supportare la raccolta di informazioni aggiuntive dal cliente durante il check-in. | Globale | No |
| **[!UICONTROL Is Additional Information a Mandatory Field?]**</br>`Extension Attribute: additional_information_mandatory` | Specificare se sono necessarie informazioni aggiuntive per i clienti durante il check-in. </br></br>Se questa opzione è attivata, al cliente viene richiesto di inserire ulteriori informazioni all&#39;arrivo. Se è disattivato, il cliente può saltare questo input. | Globale | No |
