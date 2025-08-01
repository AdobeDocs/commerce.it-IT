---
title: Caso di utilizzo end-to-end per Storefront e Catalog Administrator
description: Scopri come utilizzare [!DNL Adobe Commerce Optimizer] per gestire il catalogo utilizzando le viste e i criteri del catalogo e come impostare la vetrina in base alla configurazione del catalogo.
role: Admin, Developer
feature: Personalization, Integration
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce as a Cloud Service e Adobe Commerce Optimizer (infrastruttura SaaS gestita da Adobe)."
exl-id: d11663f8-607e-4f1d-b68f-466a69bcbd91
source-git-commit: 1ab7ee5673f261b43db25caf0ad340a0fd9e3341
workflow-type: tm+mt
source-wordcount: '2158'
ht-degree: 0%

---

# Caso di utilizzo end-to-end per Storefront e Catalog Administrator

Questo caso d’uso si basa su un conglomerato automobilistico fittizio denominato Carvelo Automobile, che dispone di una configurazione operativa complessa. Viene illustrato come utilizzare [!DNL Adobe Commerce Optimizer] per gestire un catalogo che supporta più marchi, concessionari e listini prezzi, offrendo al contempo un&#39;esperienza di vetrina personalizzata.

## Prerequisiti

Questo caso d&#39;uso è progettato per amministratori e sviluppatori che desiderano imparare a configurare una vetrina e gestire un catalogo utilizzando [!DNL Adobe Commerce Optimizer]. Si presuppone che tu abbia una conoscenza di base di [!DNL Adobe Commerce Optimizer] e delle sue funzionalità.

**Tempo stimato per il completamento:** 45-60 minuti

### Configurazione necessaria

Prima di iniziare questa esercitazione, accertati di disporre dei seguenti prerequisiti:

- **Istanza Adobe Commerce Optimizer**
   - Accesso a un’istanza di test in Cloud Manager
   - Consulta [Introduzione](../get-started.md) per le istruzioni di installazione

- **Autorizzazioni utente**
   - Accesso amministratore a Adobe Admin Console
   - Consulta [Gestione utente](../user-management.md) per la configurazione dell&#39;account
   - Se non disponi dell’accesso, contatta il rappresentante del tuo account Adobe.

- **Dati di esempio**
   - Carvelo Automobile: dati del catalogo caricati nell’istanza
   - Segui le istruzioni nell&#39;[Archivio per l&#39;acquisizione dei dati del catalogo di esempio](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion)
   - È possibile eliminare i dati di esempio dopo il completamento utilizzando lo script `reset.js` incluso

- **Ambiente vetrina**
   - Ambiente di sviluppo locale con Node.js
   - Progetto boilerplate storefront clonato e configurato
   - Per istruzioni dettagliate, consulta [Configurazione vetrina](../storefront.md)

## Iniziamo

In questo caso d’uso, stai lavorando con quanto segue:

1. Interfaccia utente [!DNL Adobe Commerce Optimizer]: configura le visualizzazioni e i criteri del catalogo per gestire la configurazione operativa complessa del catalogo per il caso d&#39;uso Carvelo.

1. Commerce Storefront - Eseguire il rendering della vetrina utilizzando i dati del catalogo di esempio caricati nell&#39;istanza [!DNL Adobe Commerce Optimizer] e nei file di configurazione Commerce Storefront, `fstab.yaml` e `config.json`.

>[!NOTE]
>
> Scopri di più sui file di configurazione della vetrina consultando l&#39;argomento [Esplora la versione standard](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/boilerplate-project/) nella documentazione di Adobe Commerce Storefront.

### ‌Soluzioni principali

Entro la fine di questo articolo:

- Scopri le nozioni di base di [!DNL Adobe Commerce Optimizer] con il suo modello dati catalogo scalabile ed performante.
- Scopri come il modello dati del catalogo si integra con i componenti della vetrina indipendenti dalla piattaforma e costruiti da Adobe.
- Scopri come utilizzare le viste e i criteri del catalogo di Adobe Commerce Optimizer per creare viste di catalogo personalizzate e filtri di accesso ai dati e inviare i dati a una vetrina Adobe Commerce con tecnologia Edge Delivery.

## Scenario di business - Carvelo Automobile

Carvelo Automobile è un conglomerato automobilistico fittizio con una configurazione operativa complessa.

![Automobile Carvelo](../assets/carvelo.png)

In questo grafico vedete che Carvelo vende prodotti automobilistici di tre marche. Ogni marchio è un’azienda figlia diversa:

- Aurora (veicoli elettrici)
- Bullone (SUV)
- Cruz (ibrido)

Vende questi marchi attraverso tre dealer:

- Arkbridge
- Kingsbluff
- Celport

Questi dealer appartengono a due diverse società madri di dealer:

- West Coast Inc. (Arkbridge)
- East Coast Inc. (Kingsbluff, Celport)

Ogni azienda ha due listini prezzi che vengono utilizzati per vendere prodotti a un prezzo specifico per acquirenti diversi (base, VIP).

- `west_coast_inc` e `vip_west_coast_inc`
- `east_coast_inc` e `vip_east_coast_inc`

Come puoi vedere, si tratta di un caso d’uso aziendale molto complesso. Con [!DNL Adobe Commerce Optimizer], un commerciante può supportare una struttura aziendale complessa utilizzando un singolo catalogo di base per diffondere i dati senza duplicazione del catalogo, scalare i listini prezzi (oltre 30.000 listini prezzi) e consegnare tutti questi dati a una vetrina Edge Delivery Services.

Ora che hai una panoramica del caso d’uso aziendale, ecco il tuo obiettivo mentre lavori attraverso questa esercitazione:

>[!BEGINSHADEBOX]

Carvelo vuole vendere parti dei suoi tre marchi (Aurora, Bolt e Cruz) attraverso i diversi concessionari (Arkbridge, Kingsbluff e Celport). Carvelo vuole garantire che i concessionari abbiano accesso solo alle parti e ai prezzi corretti secondo i rispettivi accordi di licenza.

In definitiva, Carvelo ha due obiettivi principali:

1. Gestisci un sito web &quot;globale&quot;, che ha tutte le SKU per tutti e tre i marchi.
1. Offrire ai dealer un percorso per creare i propri punti vendita in base alla visibilità SKU e ai prezzi per ogni SKU. Il tutto utilizzando un singolo catalogo di base, che elimina la duplicazione dei cataloghi.

>[!ENDSHADEBOX]

## &#x200B;1. Accedere all&#39;istanza [!DNL Adobe Commerce Optimizer]

Passa all’URL dell’applicazione Commerce Optimizer preconfigurata con i dati di esempio. Puoi trovare l’URL in Commerce Cloud Manager dai dettagli dell’istanza per il progetto Commerce Optimizer o recuperarlo dall’amministratore di sistema. (Vedi [Accedere a un&#39;istanza](../get-started.md#access-an-instance).)

All&#39;avvio di [!DNL Adobe Commerce Optimizer], vengono visualizzati i seguenti elementi:

![[!DNL Adobe Commerce Optimizer] UI](../assets/user-interface.png)

>[!NOTE]
>
>Consulta l&#39;articolo [overview](../overview.md) per informazioni sui componenti chiave dell&#39;interfaccia utente di [!DNL Adobe Commerce Optimizer].

Nel menu di navigazione a sinistra, espandi la sezione _Store setup_ e fai clic su **[!UICONTROL Catalog views]**. Tieni presente che i concessionari Arkbridge e Kingsbluff dispongono già di viste catalogo create:

![Visualizzazioni catalogo esistenti configurate per i dati di esempio](../assets/existing-channels-list.png)

>[!NOTE]
>
>Per il momento puoi ignorare la visualizzazione del catalogo **Global**.

Fai clic sull’icona info per esaminare i dettagli della vista catalogo.

Arkbridge dispone dei seguenti criteri:

- Marchio
- Modello
- Marchi West Coast Inc
- Categorie di parti di Arkbridge

Kingsbluff dispone dei seguenti criteri:

- Marchio
- Modello
- Marchi East Coast Inc
- Categorie di parti Kingsbluff

Nella sezione successiva verranno create una vista catalogo e le policy per il concessionario Celport.

## &#x200B;2. Creare una vista criterio e catalogo

Il responsabile commerciale di Carvelo deve impostare una nuova vetrina per un dealer chiamato *Celport* che appartiene all&#39;azienda *East Coast Inc*. Celport venderà freni e sospensioni per i marchi Bolt e Cruz.

![Rivenditore Celport](../assets/celport-dealer.png)

Utilizzando [!DNL Adobe Commerce Optimizer], il responsabile Commerce:

1. Creare un nuovo criterio denominato *Categorie di parti Celport* per consentire a Celport di vendere solo parti di freni e sospensioni.
1. Crea una nuova vista catalogo per la vetrina Celport.

   Questa visualizzazione catalogo utilizza i criteri appena creati *Categorie di parti Celport* e i *Marchi East Coast Inc* esistenti per garantire che Celport possa vendere solo i marchi Bolt e Cruz come parte dell&#39;accordo con East Coast Inc. La visualizzazione catalogo Celport utilizza il listino prezzi `east_coast_inc` per supportare i programmi di prezzo dei prodotti in linea con gli accordi di licenza dei marchi.
1. Aggiorna la configurazione della vetrina commerce per utilizzare i dati della vista del catalogo Celport creata.

Al termine di questa sezione, Celport sarà pronto a vendere i prodotti Carvelo.

### Creare un criterio

Creiamo un nuovo criterio denominato *Categorie di parti Celport* per filtrare gli SKU venduti dal dealer Celport, che includono parti di freni e sospensioni.

1. Nella barra a sinistra, espandi la sezione _Store setup_ e fai clic su **[!UICONTROL Policies]**.

1. Fare clic su **[!UICONTROL Create Policy]**.

   Viene visualizzata una nuova pagina per aggiungere i dettagli del criterio.

1. Aggiungi i dettagli richiesti:

   **Nome** = *Categorie Di Parti Celport*

1. Fare clic su **[!UICONTROL Add Filter]**.

   Viene visualizzata una finestra di dialogo per aggiungere i dettagli del filtro.

1. Aggiungi i dettagli del filtro:

   - **Attributo** = *categoria_parte*
   - **Operatore** = **IN**
   - **Valore Source** = **STATICO**
   - **Valore** = *freni*, *sospensione*

   >[!IMPORTANT]
   >
   >Assicurati che il nome dell’attributo specificato corrisponda esattamente al nome dell’attributo SKU nel catalogo.

   Per ulteriori informazioni sulla differenza tra un&#39;origine di valore STATIC e TRIGGER, vedere [tipi di origine di valore](../setup/policies.md#value-source-types).

1. Nella finestra di dialogo **[!UICONTROL Filter details]**, fare clic su **[!UICONTROL Save]**.

1. Per abilitare il filtro appena creato, fare clic sui punti azione (...) e selezionare **Abilita**.

1. Fare clic su **[!UICONTROL Save]**.

   >[!NOTE]
   >
   >Se il pulsante **[!UICONTROL Save]** non è attivo (blu), è possibile che il nome del criterio non sia presente. Fai clic sull&#39;icona a forma di matita accanto a *Nuovo criterio* per aggiungerlo.

1. Torna all’elenco dei criteri facendo clic sulla freccia indietro.

   Il nuovo criterio *Categorie di parti Celport* verrà visualizzato nell&#39;elenco.

**Verificare che il passaggio sia stato completato correttamente:**

- Il criterio viene visualizzato nell&#39;elenco dei criteri
- Lo stato del criterio è abilitato (indicatore verde)
- I dettagli del filtro mostrano &quot;part_category IN (freni, sospensione)&quot;
- Il nome del criterio è &quot;Celport Part Categories&quot;

### Creare una vista catalogo

Crea una nuova visualizzazione catalogo per il dealer *Celport* e collega i seguenti criteri: *Marchi East Coast Inc* e *Categorie parte Celport*.

1. Nella barra a sinistra, espandi la sezione _Store setup_ e fai clic su **[!UICONTROL Catalog views]**.

   Osserva le viste catalogo esistenti: *Arkbridge*, *Kingsbluff* e *Global*.

   ![Pagina visualizzazioni catalogo esistente](../assets/existing-channels-list.png)

1. Fare clic su **[!UICONTROL Add catalog view]**.

1. Inserisci i dettagli della vista catalogo:

   - **Nome** = *Celport*
   - **Origini catalogo** = *en-US*
   - **Criteri** (usa elenco a discesa) = *Marchi East Coast Inc*; *Categorie parte Celport*; *Marchio*; *Modello*                          
1. Fare clic su **[!UICONTROL Add]** per creare la visualizzazione del catalogo.

   La pagina Visualizzazioni catalogo viene aggiornata per visualizzare la nuova visualizzazione catalogo.

   ![Elenco visualizzazioni catalogo aggiornato](../assets/updated-catalog-view-list.png)

1. Ottieni l’ID della vista catalogo Celport.

   Fai clic sull&#39;icona delle informazioni per la visualizzazione del catalogo Celport nella pagina **Visualizzazioni catalogo**.

   ![Celport ID visualizzazione catalogo](../assets/celport-channel-id.png)

   Copia e salva l’ID della vista catalogo. Questo ID è necessario quando aggiorni la configurazione della vetrina per inviare i dati al nuovo catalogo Celport.

   **Verificare che il passaggio sia stato completato correttamente:**
   - Il nome della vista catalogo è &quot;Celport&quot;
   - La vista Catalogo mostra 4 criteri associati
   - Viene visualizzato l’ID della vista Catalogo che può essere copiato
   - L’origine del catalogo mostra &quot;en-US&quot;

Dopo aver creato la vista Catalogo Celport e i criteri associati, il passaggio successivo consiste nel configurare la vetrina per l&#39;utilizzo del nuovo catalogo Celport.

## &#x200B;3. Aggiorna la vetrina

L&#39;ultima parte di questo tutorial prevede l&#39;aggiornamento della vetrina che [hai già creato](#prerequisite) per inviare dati al nuovo catalogo Celport. In questa sezione sostituisci l’ID della vista catalogo nel file di configurazione della vetrina con l’ID della vista catalogo di Celport.

1. Nell’ambiente di sviluppo locale, apri la cartella in cui hai clonato l’archivio GitHub con i file di configurazione boilerplate della vetrina.

1. Nella directory principale della cartella, aprire il file `config.json`.

   +++Codice config.json

   ```json
   {
    "public": {
      "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
         "cs": {
            "ac-view-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
            "ac-price-book-id": "west_coast_inc",
            "ac-source-locale": "en-US"
           }
         },
         "analytics": {
            "base-currency-code": "USD",
            "environment": "Production",
            "store-id": 1,
            "store-name": "ACO Demo",
            "store-url": "https://www.aemshop.net",
            "store-view-id": 1,
            "store-view-name": "Default Store View",
            "website-id": 1,
            "website-name": "Main Website"
          }
       }
      }
   }
   ```

   L’intestazione della vista catalogo include i seguenti valori:

   - `commerce-endpoint`: `"https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql"`
   - `ac-view-id`:`"9ced53d7-35a6-40c5-830e-8288c00985ad"`
   - `ac-price-book-id`: `"west_coast_inc"`
   - `ac-source-locale`: `"en-US"`

1. Nel valore `commerce-endpoint`, sostituisci l&#39;ID tenant nell&#39;URL con l&#39;URL per l&#39;istanza [!DNL Adobe Commerce Optimizer].

   Puoi trovare l’ID tenant nell’URL per l’interfaccia utente di Commerce Optimizer. Ad esempio, nell&#39;URL seguente, l&#39;ID tenant è `XDevkG9W6UbwgQmPn995r3`.

   ```text
   https://experience.adobe.com/#/@commerceprojectbeacon/in:XDevkG9W6UbwgQmPn995r3/commerce-optimizer-studio/catalog
   ```

1. Sostituisci il valore `ac-view-id` con l&#39;ID della vista catalogo Celport copiato in precedenza.

1. Sostituire il valore `ac-price-book-id` con `"east_coast_inc"`.

   Dopo aver apportato queste modifiche, il file `config.json` dovrebbe essere simile al seguente, con i segnaposto `ACO-tenant-id` e `celport-catalog-view-id` sostituiti dai valori:

   ```json
   {
     "public": {
        "default": {
        "commerce-core-endpoint": "https://www.aemshop.net/graphql",
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{{ACO-tenant-id}}/graphql",
        "headers": {
            "cs": {
                "ac-view-id": "{{celport-catalog-view-id}}",
                "ac-price-book-id": "east_coast_inc",
                "ac-source-locale": "en-US"
              }
            },
            "analytics": {
                "base-currency-code": "USD",
                "environment": "Production",
                "store-id": 1,
                "store-name": "ACO Demo",
                "store-url": "https://www.aemshop.net",
                "store-view-id": 1,
                "store-view-name": "Default Store View",
                "website-id": 1,
                "website-name": "Main Website"
             }
         }
     }
   }
   ```

1. Salva il file.

   Quando si salvano le modifiche, si aggiorna la configurazione del catalogo in modo da utilizzare la vista del catalogo Carvelo configurata per vendere solo parti del freno e della sospensione.

## &#x200B;4. Anteprima della vetrina

Ora che hai aggiornato la configurazione della vetrina per utilizzare la vista Catalogo Celerra, puoi visualizzare in anteprima la vetrina per vedere come riproduce i dati del catalogo.

1. Avvia la vetrina per visualizzare l’esperienza del catalogo specifica per Celport creata dalla configurazione della vetrina.

   1. Dalla finestra del terminale nell’IDE, avvia l’anteprima della vetrina locale.

      ```shell
      npm start
      ```

      Il browser si apre all&#39;anteprima di sviluppo locale in `http://localhost:3000`.

      Se il comando non riesce o se il browser non si apre, esaminare le [istruzioni per lo sviluppo locale](../storefront.md) nell&#39;argomento relativo alla configurazione di Storefront.

1. Nel browser, cercare `brakes` e premere **Invio**.

   La vetrina si aggiorna per visualizzare la pagina dell&#39;elenco dei prodotti con le parti dei freni.

   ![Pagina elenco prodotti per freni](../assets/brakes-listing-page.png)

   Fare clic sull&#39;immagine di una parte del freno per visualizzare i dettagli del prodotto con le informazioni sul prezzo e annotare le informazioni sul prezzo del prodotto.

1. Cerca `tires`, che è un&#39;altra categoria di parte disponibile nei dati del caso d&#39;uso nell&#39;istanza [!DNL Adobe Commerce Optimizer].

   ![Configurazione vetrina con intestazioni non corrette](../assets/storefront-configuration-with-incorrect-headers.png)

   Non viene restituito alcun risultato. Questo perché la vista catalogo Celport è stata configurata per vendere solo parti di freni e sospensioni.

1. Prova ad aggiornare il file di configurazione della vetrina (`config.json`).

   1. Modificare i valori `ac-view-id` e `ac-price-book`.

   Ad esempio, è possibile modificare l&#39;ID della vista catalogo in vista catalogo Kingsbluff e l&#39;ID del listino prezzi in `east_coast_inc`. È possibile visualizzare le categorie di parti disponibili per Kingsbluff consultando il criterio *Categorie di parti Kingsbluff*.

   1. Salva il file.

      Quando si salva il file, l&#39;anteprima della vetrina locale viene aggiornata automaticamente.

   1. Visualizzate l&#39;anteprima delle modifiche nel browser utilizzando la funzione di ricerca per trovare le parti dei pneumatici.

      Osservare i diversi tipi di parti disponibili e i prezzi assegnati alla vista del catalogo Kingsbluff.

   Questi esperimenti dimostrano la flessibilità di Adobe Commerce Optimizer: puoi passare rapidamente da una visualizzazione di catalogo all’altra e impostare listini prezzi personalizzati per diversi tipi di pubblico senza duplicare i dati del catalogo.

## Risoluzione dei problemi

Se riscontri problemi durante questa esercitazione, prova le seguenti soluzioni:

### Problemi relativi alla creazione dei criteri

**Problema:** il pulsante Salva non è attivo

- **Soluzione:** Verificare che il nome del criterio sia stato immesso e che tutti i campi obbligatori siano stati completati

**Problema:** il filtro non funziona come previsto

- **Soluzione:** Verificare che il nome dell&#39;attributo corrisponda esattamente all&#39;attributo SKU nel catalogo

### Problemi relativi alla vista catalogo

**Problema:** la visualizzazione del catalogo non viene visualizzata nell&#39;elenco

- **Soluzione:** Verificare che tutti i criteri associati siano abilitati e configurati correttamente

### Problemi di configurazione della vetrina

**Problema:** Storefront non caricato

- **Soluzione:** verifica che l&#39;ID tenant e l&#39;ID della vista catalogo siano immessi correttamente nel file config.json

**Problema:** nessun prodotto visualizzato

- **Soluzione:** Verificare che l&#39;ID del listino prezzi dedicato corrisponda a quello disponibile nell&#39;istanza di Adobe Commerce Optimizer

**Problema:** La ricerca non restituisce alcun risultato

- **Soluzione:** Verificare che i criteri di visualizzazione del catalogo consentano la categoria di prodotti cercata

Per ulteriori informazioni, consulta la [documentazione di Adobe Commerce Optimizer](../overview.md) o contatta il supporto Adobe.

## Riepilogo

In questa esercitazione, esegui correttamente le seguenti operazioni:

- Creato un nuovo criterio per filtrare le categorie di prodotti per il dealer Celport
- Impostare una vista catalogo con più criteri per controllare la visibilità dei prodotti
- Configurazione di una vetrina per l&#39;utilizzo della nuova vista catalogo
- Verifica della configurazione tramite test della visibilità e del prezzo del prodotto

## Passaggi successivi

Per continuare a conoscere Adobe Commerce Optimizer:

- Esplora le [funzionalità di merchandising](../merchandising/overview.md) per personalizzare l&#39;esperienza di acquisto
- Scopri le [configurazioni avanzate dei criteri](../setup/policies.md)
- Configura [altre visualizzazioni catalogo](../setup/catalog-view.md) per altri dealer
- Consulta la [documentazione API](https://developer.adobe.com/commerce/services/optimizer/) per la gestione programmatica del catalogo
- Scopri come configurare i componenti di rilascio per la vetrina Edge Delivery Services per creare esperienze vetrina personalizzate per l’individuazione dei prodotti, raccomandazioni e altre funzionalità. Consulta la [documentazione di Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)
