---
source-git-commit: b6b737220a6dadf55b03da54e8d74226ed578cd0
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%
---
# Chiavi di accesso limitate

Le chiavi di accesso con restrizioni consentono alle applicazioni client autorizzate di accedere a una [vista di catalogo privata](private-catalog-view.md). Solo le richieste che contengono un token firmato valido da una chiave assegnata possono recuperare i dati del catalogo. Tutte le altre richieste vengono rifiutate, incluse quelle di acquirenti che non hanno accesso esplicito a questa vista catalogo e gli script che esaminano l’API di Adobe Commerce Merchandising Services.

Il provisioning delle chiavi di accesso con restrizioni può avvenire in uno dei due modi seguenti:

- **Automaticamente, per cataloghi condivisi B2B**: il sistema esegue il provisioning e assegna la chiave iniziale per le visualizzazioni catalogo associate a un catalogo condiviso B2B. Quindi gestisci le chiavi e l’assegnazione delle chiavi dall’amministratore di Commerce. Vedi [Autenticazione della vista catalogo](https://experienceleague.adobe.com/it/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage) nella *Guida dell&#39;amministratore di Commerce*. Il provisioning automatico è disponibile nelle seguenti distribuzioni:

  - **Adobe Commerce as a Cloud Service con CCDM** per Adobe Commerce B2B.
  - **Adobe Commerce su cloud o locale** integrato con Adobe Commerce Optimizer tramite [!DNL Adobe Commerce Optimizer Connector for B2B]. È necessaria l’estensione B2B per il connettore.

- **Manualmente, per qualsiasi vista catalogo**. Per proteggere autonomamente una vista catalogo, ad esempio per un portale partner o per un&#39;anteprima pre-release, seguire i passaggi descritti in questo argomento a partire da [Creare una chiave di accesso con restrizioni](#create-a-restricted-access-key).

## Casi d’uso chiave di accesso limitati

**[!UICONTROL Price Book ID]** determina i prezzi visualizzati da una richiesta. Ha una valutazione dei prezzi, non di chi può effettuare la richiesta. Qualsiasi cliente che conosce l’ID di una vista catalogo e l’ID di un listino prezzi può recuperare tali dati tramite l’API Merchandising Services. Le chiavi di accesso con restrizioni aggiungono un controllo separato e complementare: definiscono gli utenti che possono accedere a una visualizzazione di catalogo, indipendentemente dal listino prezzi dedicato.

Le chiavi di accesso con restrizioni sono comunemente utilizzate per:

- **Determinazione prezzi B2B basata su contratto**: limitare una visualizzazione di catalogo collegata a un listino prezzi dedicato in modo che solo l&#39;acquirente a cui si applica possa eseguire query. Le altre organizzazioni di acquisto e il pubblico non possono. Per i cataloghi condivisi B2B, viene impostato automaticamente. Consulta [Gestione chiavi e rotazione](#key-management-and-rotation).
- **Portali per partner e rivenditori** - Limita un sottoinsieme del catalogo ai partner approvati che si integrano direttamente con l&#39;API dei servizi di merchandising.
- **Anteprime pre-release**: consente a un sistema interno o partner attendibile di visualizzare in anteprima i prodotti in arrivo prima che siano visibili pubblicamente.

## Funzionamento delle chiavi di accesso con restrizioni

Una chiave ad accesso limitato è il componente pubblico di una coppia di chiavi RSA. L’applicazione client genera e utilizza questa chiave per dimostrare di essere autorizzata a leggere una vista di catalogo privata. In questo contesto, _l&#39;applicazione client_ fa riferimento al sistema di back-end che autentica gli acquirenti, ad esempio la logica personalizzata su [!DNL Adobe Commerce] o un back-end di terze parti, mai il front-end storefront stesso.

I passaggi seguenti descrivono come una coppia di chiavi e un token firmato passano dalla creazione alla convalida per le viste catalogo che non fanno parte di un catalogo condiviso B2B.

1. L&#39;applicazione client genera una coppia di chiavi RSA e mantiene la chiave privata.
1. Registrare la chiave **public** nel sistema come chiave ad accesso limitato.
1. L’applicazione client firma un token web JSON (JWT) con la chiave privata e lo include con ogni richiesta a una vista di catalogo privata.

   Il sistema convalida la firma del token in base alla chiave pubblica registrata e, se valida, restituisce i dati del catalogo richiesti.

## Accedere all’area di lavoro della chiave di accesso limitato

La modalità di apertura dell&#39;area di lavoro dei codici di accesso con restrizioni dipende dal prodotto utilizzato:

- **Amministratore Adobe Commerce** (Adobe Commerce as a Cloud Service)—Seleziona *Sistema* > *Trasferimento dati* > **Chiavi di accesso con restrizioni**.
- **Adobe Commerce Optimizer Studio**—Selezionare *Configurazione archivio* > **Chiavi di accesso con restrizioni**.

## Creare una chiave di accesso con restrizioni

>[!NOTE]
>
>Questa sezione e le due che seguono descrivono il processo manuale per gestire le chiavi di accesso con restrizioni. Per i cataloghi condivisi B2B con provisioning automatico delle chiavi, gestisci le chiavi dall’amministratore di Commerce. Vedi [Chiavi di accesso limitate](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

### Aggiungere una chiave di accesso con restrizioni

Seleziona la scheda per lo strumento utilizzato per gestire le chiavi: Commerce Admin o Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Amministratore Adobe Commerce]

I clienti che utilizzano Adobe Commerce as a Cloud Service con CCDM o Adobe Commerce Optimizer connesso ad Adobe Commerce tramite il connettore possono generare coppie di chiavi RSA dall’amministratore Commerce. Vedi [Gestire le chiavi con restrizioni di accesso](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys).

>[!TAB Adobe Commerce Optimizer Studio - gestione manuale delle chiavi]

I clienti che utilizzano Adobe Commerce Optimizer Studio devono generare e gestire le proprie coppie di chiavi RSA e quindi aggiungere la chiave pubblica al sistema. Si tratta del flusso di lavoro richiesto per Adobe Commerce Optimizer con un back-end di terze parti. Anche i clienti che utilizzano il connettore possono utilizzare questo flusso di lavoro al posto dell’amministratore di Commerce.

**Generare una coppia di chiavi RSA**

Per il test iniziale delle visualizzazioni del catalogo privato, generare una coppia di chiavi utilizzando uno strumento quale [!DNL OpenSSL]. Mantieni segreta la chiave privata. Solo la chiave pubblica viene caricata nel sistema come chiave ad accesso limitato.

```bash
openssl genrsa -out private-key.pem 2048
openssl rsa -in private-key.pem -pubout -out public-key.pem
```

La dimensione della chiave deve essere compresa tra 2048 e 8192 bit. `public-key.pem` contiene il valore incollato nel campo **[!UICONTROL Public key]** di seguito.

**Aggiungi la chiave pubblica al sistema**

1. Nell&#39;area di lavoro con chiave Accesso limitato fare clic su **[!UICONTROL Add Restricted Access Key]**.

   ![Elenco di chiavi di accesso con restrizioni, con il pulsante Aggiungi chiave di accesso con restrizioni](/help/assets/ccdm-shared/setup/restricted-access-keys.png){width="70%" zoomable="yes"}

1. Immetti i dettagli chiave:

   ![Aggiungi modulo chiave di accesso limitato con titolo, data di scadenza e campi chiave pubblica](/help/assets/ccdm-shared/setup/restricted-access-keys-add.png){width="70%" zoomable="yes"}

   - **[!UICONTROL Title]** - Etichetta per identificare la chiave, visualizzata nell&#39;elenco delle chiavi e nel selettore delle chiavi di visualizzazione del catalogo, ad esempio `ACME Corp wholesale portal — Tier 1 pricing`.
   - **[!UICONTROL Expiration date]** - Data e ora (UTC) dopo le quali la chiave non viene più rispettata, anche per un token non ancora scaduto.
   - **[!UICONTROL Public key]**: la chiave pubblica RSA con codifica PEM in formato SPKI (Subject Public Key Info), inclusi i marcatori `-----BEGIN PUBLIC KEY-----` e `-----END PUBLIC KEY-----`. Deve essere univoco in tutto l’ambiente.

1. Fare clic su **[!UICONTROL Save]**.

>[!ENDTABS]

Le chiavi non sono modificabili dopo la creazione. Per modificare un valore, elimina la chiave e creane una nuova. Vedere [Ruotare una chiave](#rotate-a-key) per eseguire questa operazione senza interrompere l&#39;accesso.

## Assegnare una chiave a una vista catalogo

Una chiave di accesso con restrizioni autentica l&#39;accesso solo dopo che è stato assegnato a una vista catalogo con **[!UICONTROL Catalog Protection]** abilitato. Consulta [Proteggere una vista catalogo](private-catalog-view.md#protect-a-catalog-view) per i passaggi di configurazione.

## Eliminare una chiave

1. Nell&#39;area di lavoro **[!UICONTROL Restricted access keys]** trovare la chiave che si desidera rimuovere ed eliminare.

   Se la chiave viene assegnata a una o più visualizzazioni catalogo, un avviso spiega che le applicazioni client che si basano su tale chiave perdono l’accesso. Le visualizzazioni del catalogo rimangono protette, non diventano accessibili al pubblico.

1. Conferma l’eliminazione.

## Gestione delle chiavi e rotazione

Le chiavi di accesso con restrizioni vengono gestite in due modi, a seconda di come si utilizza la protezione del catalogo:

- **Automaticamente, per i cataloghi condivisi B2B**: per le distribuzioni B2B di Adobe Commerce che utilizzano Merchandising Services con CCDM e per le distribuzioni Adobe Commerce Optimizer integrate tramite [!DNL Adobe Commerce Optimizer Connector for B2B] (che richiede l&#39;estensione B2B), il servizio genera e assegna automaticamente la prima chiave di accesso limitato al momento della creazione di una vista catalogo. Ogni vista catalogo ha la propria chiave. Successivamente, puoi gestire ogni chiave dalle pagine Catalogo condiviso o Account aziendale. Puoi anche visualizzare e gestire le chiavi dalla pagina Amministratore Commerce **Chiavi di accesso con restrizioni** (**Sistema** > **Trasferimento dati**). Consulta [Gestire la configurazione della visualizzazione del catalogo](https://experienceleague.adobe.com/it/docs/commerce-admin/b2b/shared-catalogs/catalog-views-manage).

  Ogni combinazione di un catalogo condiviso e di una visualizzazione archivio viene proiettata come una visualizzazione catalogo separata. Una proiezione è costituita dalla vista catalogo, dai criteri, dal riferimento al listino prezzi e dai dati chiave di configurazione ad accesso limitato esportati nel livello dati di Merchandising Services per tale combinazione. Pertanto, un catalogo condiviso assegnato a più visualizzazioni dello store produce più visualizzazioni del catalogo, ciascuna con la propria chiave. Modifica o ruota una chiave per una vista catalogo senza influire sulle altre.

  Le chiavi hanno per impostazione predefinita un periodo di scadenza lungo. Se devi ruotare una chiave, aggiungi il sostituto nell’amministratore e mantieni entrambi attivi fino a quando non rimuovi quello vecchio.

- **Manualmente, per qualsiasi vista catalogo**. La modalità di generazione e gestione delle chiavi dipende dal contesto del prodotto. In entrambi i casi, il client backend che autentica gli acquirenti firma i token.

  - **Amministratore Commerce (Adobe Commerce as a Cloud Service con CCDM o Adobe Commerce Optimizer con il connettore)** - Genera coppie di chiavi RSA nell&#39;amministratore Commerce e crea, assegna ed elimina chiavi nella pagina **Chiavi di accesso limitate**. Adobe Commerce non ruota automaticamente i tasti. Per ruotare una chiave, vedere [Ruotare una chiave](#rotate-a-key).
  - **Adobe Commerce Optimizer Studio**—Studio non genera chiavi. Si tratta del flusso di lavoro richiesto per Adobe Commerce Optimizer con un back-end di terze parti ed è utilizzabile anche dai clienti dei connettori. Utilizzare l&#39;applicazione client per generare la coppia di chiavi RSA, mantenere la chiave privata e aggiungere la chiave pubblica come chiave ad accesso limitato. Utilizzare i passaggi precedenti in questo argomento per creare, aggiungere ed eliminare chiavi. Per ruotare una chiave, vedere [Ruotare una chiave](#rotate-a-key).

### Ruotare una chiave

Per ruotare una chiave senza interrompere l’accesso, tieni presente che a una vista catalogo possono essere assegnate fino a tre chiavi alla volta:

Seleziona la scheda per lo strumento utilizzato per gestire le chiavi: Commerce Admin o Adobe Commerce Optimizer Studio.

>[!BEGINTABS]

>[!TAB Amministratore Adobe Commerce]

Vedi [Selezione chiave e rotazione](https://experienceleague.adobe.com/it/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys#key-selection-and-rotation). Questo vale per Adobe Commerce as a Cloud Service con CCDM e per i progetti Adobe Commerce integrati con Adobe Commerce Optimizer tramite il connettore Adobe Commerce Optimizer.

>[!TAB Adobe Commerce Optimizer Studio (gestione manuale delle chiavi)]

Questa procedura è necessaria per Adobe Commerce Optimizer con un back-end di terze parti. I clienti che utilizzano il connettore possono anche utilizzarlo al posto dell’amministratore di Commerce.

1. Genera una nuova coppia di chiavi e aggiungi la nuova chiave pubblica come nuova chiave ad accesso limitato.
1. Assegna la nuova chiave alla vista catalogo insieme alla chiave esistente.
1. Inizia a firmare nuovi token con la nuova chiave privata per completare il rollover della chiave.
1. Una volta confermate tutte le applicazioni client sulla nuova chiave, rimuovi ed elimina la chiave precedente.

>[!ENDTABS]

## Limiti

Vedi [Visualizzazioni catalogo e limiti dei criteri](https://experienceleague.adobe.com/it/docs/commerce/optimizer/boundaries-limits).

## Altri argomenti correlati

- [Visualizzazioni catalogo privato](private-catalog-view.md)—Scopri come proteggere una visualizzazione catalogo con chiavi di accesso limitato.
