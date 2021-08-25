---
keywords: activeer profielbestemmingen;activeer bestemmingen;activeer gegevens; e-mailmarketingbestemmingen activeren; cloudopslagdoelen activeren
title: De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen
type: Tutorial
seo-title: Activate audience data to streaming profile export destinations
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten naar streaming op profiel gebaseerde doelen te verzenden.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to streaming profile-based destinations.
source-git-commit: d13920250fafd2ba4ff37dd5d4a45d417ed3ecc7
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in op Adobe Experience Platform gebaseerde streaming profielbestemmingen, zoals Amazon Kinesis.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u [met succes hebben verbonden met een bestemming](./connect-destination.md). Als u dit niet reeds hebt gedaan, ga naar [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer het tabblad **[!UICONTROL Catalog]**.

   ![Tabblad Doelcatalogus](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de bestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Knop Segmenten activeren](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer **[!UICONTROL Next]**.

   ![Doel selecteren](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Ga naar de volgende sectie naar [selecteer uw segmenten](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de controledozen links van de segmentnamen om de segmenten te selecteren die u aan de bestemming wilt activeren, dan uitgezocht **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Profielkenmerken selecteren {#select-attributes}

Selecteer de profielkenmerken die u naar de doelbestemming wilt verzenden.

>[!NOTE]
>
> Adobe Experience Platform vult uw selectie voor met vier aanbevolen, veelgebruikte kenmerken uit uw schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Het exporteren van bestanden kan op de volgende manieren variëren, afhankelijk van het feit of `segmentMembership.status` is geselecteerd:
* Als het veld `segmentMembership.status` is geselecteerd, bevatten geëxporteerde bestanden **[!UICONTROL Active]** leden in de eerste volledige momentopname en **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in volgende incrementele exportbewerkingen.
* Als het veld `segmentMembership.status` niet is geselecteerd, nemen geëxporteerde bestanden alleen **[!UICONTROL Active]** leden op in de eerste volledige momentopname en in volgende incrementele exportbewerkingen.

![aanbevolen kenmerken](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. Selecteer **[!UICONTROL Add new field]** op de pagina **[!UICONTROL Select attributes]**.

   ![Nieuwe toewijzing toevoegen](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selecteer de pijl rechts van de **[!UICONTROL Schema field]** ingang.

   ![Bronveld selecteren](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Selecteer op de pagina **[!UICONTROL Select field]** de XDM-kenmerken die u naar de bestemming wilt verzenden en kies **[!UICONTROL Select]**.

   ![Bronveldpagina selecteren](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Als u meer toewijzingen wilt toevoegen, herhaalt u stap 1 tot en met 3 en selecteert u **[!UICONTROL Next]**.

## Controleren {#review}

Op de **[!UICONTROL Review]** pagina, kunt u een samenvatting van uw selectie zien. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw montages te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](../../rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![Controleren](../assets/ui/activate-streaming-profile-destinations/review.png)

## Segmentactivering verifiëren {#verify}

Uw geëxporteerde [!DNL Experience Platform]-gegevens worden in JSON-indeling in uw doelbestemming geplaatst. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
