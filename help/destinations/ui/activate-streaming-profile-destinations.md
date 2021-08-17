---
keywords: activeer profielbestemmingen;activeer bestemmingen;activeer gegevens; e-mailmarketingbestemmingen activeren; cloudopslagdoelen activeren
title: De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen
type: Tutorial
seo-title: De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten naar streaming op profiel gebaseerde doelen te verzenden.
seo-description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten naar streaming op profiel gebaseerde doelen te verzenden.
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# De publieksgegevens van de activering aan het stromen profiel de uitvoerbestemmingen

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist voor het activeren van publieksgegevens in op Adobe Experience Platform gebaseerde streaming profielbestemmingen, zoals Amazon Kinesis.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u [met succes hebben verbonden met een bestemming](./connect-destination.md). Als u dit niet reeds hebt gedaan, ga naar [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer het tabblad **[!UICONTROL Browse]**.

   ![Tabblad Doelbladeren](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. Selecteer de **[!UICONTROL Add segments]** knoop die aan de bestemming beantwoordt waar u uw segmenten wilt activeren, zoals aangetoond in het hieronder beeld.

   ![Knoppen activeren](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

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


Voor marketingdoelen en opslagdoelen voor de cloud maakt Adobe Experience Platform een door tabs gescheiden `.csv`-bestand op de opslaglocatie die u hebt opgegeven. Verwacht dat er elke dag een nieuw bestand op uw opslaglocatie wordt gemaakt. De standaardbestandsindeling is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

De bestanden die u op drie opeenvolgende dagen ontvangt, kunnen er als volgt uitzien:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De aanwezigheid van deze bestanden op de opslaglocatie bevestigt dat de activering is gelukt. Als u wilt weten hoe de geëxporteerde bestanden zijn gestructureerd, kunt u [een voorbeeld-CSV-bestand](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv) downloaden. Dit voorbeeldbestand bevat de profielkenmerken `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` en `personalEmail.address`.
