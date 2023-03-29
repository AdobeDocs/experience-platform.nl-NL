---
keywords: activeer profielbestemmingen;activeer bestemmingen;activeer gegevens; e-mailmarketingbestemmingen activeren; cloudopslagdoelen activeren
title: De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen
type: Tutorial
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten naar streaming op profiel gebaseerde doelen te verzenden.
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen

>[!IMPORTANT]
> 
> * Om gegevens te activeren en de [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
> * Gegevens activeren zonder de opdracht [toewijzingsstap](#mapping) van de workflow hebt u de **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions).
> 
> Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in op Adobe Experience Platform gebaseerde streaming profielbestemmingen, zoals Amazon Kinesis.

## Vereisten {#prerequisites}

Als u gegevens naar doelen wilt activeren, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Afbeelding die het tabblad van de doelcatalogus weergeeft.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de bestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Afbeelding die de activesegmentcontrole markeert op het tabblad Doelcatalogus.](../assets/ui/activate-streaming-profile-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Afbeelding met een selectie van twee doelen waarmee u verbinding kunt maken.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw segmenten selecteren](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de selectievakjes links van de segmentnamen om de segmenten te selecteren die u wilt activeren naar het doel en selecteer vervolgens **[!UICONTROL Next]**.

![Afbeelding die de selectie van selectievakjes markeert in de stap Segmenten selecteren van de activeringsworkflow.](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Profielkenmerken selecteren {#select-attributes}

In de **[!UICONTROL Mapping]** Selecteer de profielkenmerken die u naar de doelbestemming wilt verzenden.

>[!NOTE]
>
> Adobe Experience Platform vult uw selectie voor met vier aanbevolen, veelgebruikte kenmerken uit uw schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Het exporteren van bestanden kan als volgt variëren, afhankelijk van of `segmentMembership.status` is geselecteerd:
* Als de `segmentMembership.status` veld is geselecteerd, geëxporteerde bestanden bevatten **[!UICONTROL Active]** leden in de eerste volledige momentopname en **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in latere incrementele uitvoer.
* Als de `segmentMembership.status` veld is niet geselecteerd, geëxporteerde bestanden bevatten alleen **[!UICONTROL Active]** leden in de eerste volledige momentopname en in de daaropvolgende incrementele uitvoer.

![Afbeelding met de vooraf ingevulde, aanbevolen kenmerken in de toewijzingsstap.](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. In de **[!UICONTROL Select attributes]** pagina, selecteert u **[!UICONTROL Add new field]**.

   ![Afbeelding die het besturingselement Nieuw veld toevoegen in de toewijzingsstap markeert.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Selecteer de pijl rechts van de knop **[!UICONTROL Schema field]** vermelding.

   ![Afbeelding die markeert hoe u een bronveld selecteert in de toewijzingsstap.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. In de **[!UICONTROL Select field]** pagina, selecteert u de XDM-kenmerken die u naar het doel wilt verzenden en kiest u **[!UICONTROL Select]**.

   ![Afbeelding met een selectie XDM-velden die u kunt selecteren als bronvelden.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Als u meer toewijzingen wilt toevoegen, herhaalt u stap 1 tot en met 3 en selecteert u **[!UICONTROL Next]**.

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Selectieoverzicht in de revisiestap.](/help/destinations/assets/ui/activate-streaming-profile-destinations/review.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

Als uw organisatie is aangeschaft **Adobe Healthcare Shield** of **Adobe Privacy- en beveiligingsschild**, selecteert u **[!UICONTROL View applicable consent policies]** na te gaan welk toestemmingsbeleid wordt toegepast en hoeveel profielen als gevolg daarvan in de activering worden opgenomen. Meer informatie [goedkeuring beleidsevaluatie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) voor meer informatie .

### Controle van het gegevensgebruiksbeleid {#data-usage-policy-checks}

In de **[!UICONTROL Review]** stap, controleert het Experience Platform ook om het even welke schendingen van het beleid van het gegevensgebruik. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, raadpleegt u [beleidsovertredingen voor gegevensgebruik](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) in de sectie Documentatie inzake gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

### Segmenten filteren {#filter-segments}

In deze stap kunt u ook de beschikbare filters op de pagina gebruiken om alleen de segmenten weer te geven waarvan het schema of de toewijzing is bijgewerkt als onderdeel van deze workflow.

![De opname van het scherm die de beschikbare segmentfilters in de overzichtsstap toont.](/help/destinations/assets/ui/activate-streaming-profile-destinations/filter-segments-review-step.gif)

Als u tevreden bent met de selectie en er zijn geen beleidsovertredingen vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

## Segmentactivering verifiëren {#verify}

Uw geëxporteerde [!DNL Experience Platform] gegevens in uw doelbestemming in JSON-indeling worden geland. De gebeurtenis hieronder bevat bijvoorbeeld het kenmerk E-mailadresprofiel van een publiek dat voor een bepaald segment is gekwalificeerd en een ander segment heeft verlaten. De identiteiten voor dit vooruitzicht zijn ECID en e-mail.

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
