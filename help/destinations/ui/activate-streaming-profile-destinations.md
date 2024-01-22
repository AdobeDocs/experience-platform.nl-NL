---
title: Stimulansen voor het streamen van exportdoelen voor profielen activeren
type: Tutorial
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door een publiek naar streaming op profiel gebaseerde doelen te sturen.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---


# Stimulansen voor het streamen van exportdoelen voor profielen activeren

>[!IMPORTANT]
> 
> * Om gegevens te activeren en de [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
> * Gegevens activeren zonder de opdracht [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
> 
> Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist om publieksgegevens in Adobe Experience Platform te activeren voor streaming op profielen gebaseerde doelen (ook wel bekend als [ondernemingsbestemmingen](/help/destinations/destination-types.md#streaming-profile-export)).

Dit artikel is van toepassing op de volgende drie bestemmingen:

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [HTTP API-bestemming](/help/destinations/catalog/streaming/http-destination.md).

## Vereisten {#prerequisites}

Als u gegevens naar doelen wilt activeren, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Afbeelding die het tabblad van de doelcatalogus weergeeft.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate audiences]** op de kaart die overeenkomt met de bestemming waar u uw publiek wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Afbeelding die het besturingselement voor doelgroepen activeren markeert op het tabblad Doelcatalogus.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw publiek te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Afbeelding met een selectie van twee doelen waarmee u verbinding kunt maken.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw publiek selecteren](#select-audiences).

## Uw publiek selecteren {#select-audiences}

Als u het publiek dat u wilt activeren naar het doel wilt selecteren, schakelt u het selectievakje links van de publieksnamen in en selecteert u **[!UICONTROL Next]**.

U kunt kiezen uit meerdere soorten publiek, afhankelijk van de oorsprong:

* **[!UICONTROL Segmentation Service]**: publiek dat binnen Experience Platform door de Dienst van de Segmentatie wordt geproduceerd. Zie de [segmentatiedocumentatie](../../segmentation/ui/overview.md) voor meer informatie .
* **[!UICONTROL Custom upload]**: Soorten publiek dat buiten het Experience Platform is gegenereerd en als CSV-bestanden naar Platform is geüpload. Raadpleeg de documentatie over [een publiek importeren](../../segmentation/ui/overview.md#import-audience).
* Andere soorten soorten publiek, afkomstig van andere oplossingen voor Adobe, zoals [!DNL Audience Manager].

![Afbeelding die de selectie van selectievakjes markeert in de stap Soorten publiek selecteren van de activeringsworkflow.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Profielkenmerken selecteren {#select-attributes}

In de **[!UICONTROL Mapping]** Selecteer de profielkenmerken die u naar de doelbestemming wilt verzenden.

1. In de **[!UICONTROL Select attributes]** pagina, selecteert u **[!UICONTROL Add new field]**.

   ![Afbeelding die het besturingselement Nieuw veld toevoegen in de toewijzingsstap markeert.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selecteer de pijl rechts van de knop **[!UICONTROL Schema field]** vermelding.

   ![Afbeelding die markeert hoe u een bronveld selecteert in de toewijzingsstap.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. In de **[!UICONTROL Select field]** pagina, selecteert u de XDM-kenmerken die u naar het doel wilt verzenden en kiest u **[!UICONTROL Select]**.

   ![Afbeelding met een selectie XDM-velden die u kunt selecteren als bronvelden.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Als u meer velden wilt toevoegen, herhaalt u stap 1 tot en met 3 en selecteert u vervolgens **[!UICONTROL Next]**.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Selectieoverzicht in de revisiestap.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

[Goedkeuring van het beleid](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) wordt momenteel niet gesteund in de uitvoer naar de drie ondernemingsbestemmingen - Amazon Kinesis, Azure Event Hubs, en HTTP API.

Dit betekent dat profielen waarvoor geen toestemming is gegeven, als doelprofiel kunnen worden gebruikt *worden opgenomen* in de uitvoer naar deze drie bestemmingen.

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### Controle van het gegevensgebruiksbeleid {#data-usage-policy-checks}

In de **[!UICONTROL Review]** stap, controleert het Experience Platform ook om het even welke schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor publieksactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, leest u informatie over [beleidsovertredingen voor gegevensgebruik](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) in de sectie Documentatie inzake gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

### Filter publiek {#filter-audiences}

In deze stap kunt u ook de beschikbare filters op de pagina gebruiken om alleen de doelgroepen weer te geven waarvan het schema of de toewijzing is bijgewerkt als onderdeel van deze workflow.

![De opname van het scherm die de beschikbare publieksfilters in de overzichtsstap toont.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Als u tevreden bent met de selectie en er zijn geen beleidsovertredingen vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

## Activering van publiek controleren {#verify}

Uw geëxporteerde [!DNL Experience Platform] gegevens in uw doelbestemming in JSON-indeling worden geland. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadres van een profiel dat voor een bepaald publiek is gekwalificeerd en dat een ander publiek heeft verlaten. De identiteit van dit vooruitzicht is `ECID` en `email_lc_sha256`.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
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
