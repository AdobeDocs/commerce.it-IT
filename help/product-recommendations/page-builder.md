---
title: Integrazione di [!DNL Page Builder]
description: Scopri come utilizzare  [!DNL Product Recommendations]  unità in Page Builder.
feature: Services, Recommendations, Page Builder
exl-id: 001e8e1d-3590-4b44-b5f8-dd8b9b61f370
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/it/docs/commerce/user-guides/product-solutions" tooltip="Applicabile solo ai progetti Adobe Commerce on Cloud (infrastruttura PaaS gestita da Adobe) e ai progetti on-premise."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Integrazione di [!DNL Page Builder]

I consigli di prodotto possono essere integrati in qualsiasi contenuto di Page Builder distribuito sul sito.

>[!NOTE]
>
> In una pagina nativa di Page Builder puoi avere fino a 25 unità di consigli. Le pagine di Page Builder non native possono avere fino a 5 unità di consigli. Per ulteriori informazioni, vedere [Crea nuovo consiglio](create.md).

## Utilizzo dei consigli di prodotto con il contenuto di Page Builder

1. Crea un’unità di consigli nella visualizzazione store predefinita di un sito web. Devono essere create nella vista predefinita del Negozio anche se si prevede di utilizzarle in viste diverse.

   >[!NOTE]
   >
   >Le metriche per le unità di consigli di Page Builder vengono visualizzate solo nell&#39;area di lavoro predefinita [!DNL Product Recommendations] della visualizzazione archivio. Anche se si inserisce un&#39;unità di consigli di Page Builder in una visualizzazione archivio diversa da quella predefinita, le metriche relative a tali unità di consigli di Page Builder non verranno visualizzate nell&#39;area di lavoro [!DNL Product Recommendations] della visualizzazione archivio non predefinita. Per visualizzare le metriche di Page Builder in un&#39;area di lavoro [!DNL Product Recommendations] con visualizzazione archivio non predefinita, aprire e [modificare](edit.md) l&#39;unità di consigli di Page Builder nella visualizzazione archivio non predefinita, quindi fare clic su [!UICONTROL **Salva**]. Le metriche di Page Builder vengono ora visualizzate nell&#39;area di lavoro [!DNL Product Recommendations] nella visualizzazione dello store non predefinita.

1. In Page Builder, seleziona il widget di contenuto Consigli di prodotto e inseriscilo sul tuo sito.

![Inserisci unità consigli](assets/pb-insert.png)

1. Fai clic su **Modifica consiglio prodotto**
1. Fai clic su **Seleziona**
1. Seleziona l&#39;unità di consigli creata in precedenza e fai clic su **Aggiungi selezionati**

![Inserisci unità consigli](assets/pb-select.png)

1. Apporta eventuali altre modifiche al contenuto di Page Builder e salva le modifiche.

Al momento del rendering, il contesto e l’ambito del contenuto di Page Builder vengono rispettati dall’unità di consigli.
