---
title: Overzicht AWS-extensie
description: Meer informatie over de AWS-extensie voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# [!DNL AWS] extensieoverzicht

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) is een platform voor cloud computing dat een groot aantal verschillende services biedt, zoals gedistribueerd computergebruik, databaseopslag, levering van inhoud en beheer van klantrelaties (CRM).

De [!DNL AWS] [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) extensiefuncties [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) om gebeurtenissen van Adobe Experience Platform Edge Network te verzenden naar [!DNL AWS] voor verdere verwerking. Deze gids behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in een gebeurtenis aan te wenden die regel door:sturen.

## Vereisten

U moet beschikken over een [!DNL AWS] met een bestaande [!DNL Kinesis] gegevensstroom om deze extensie te gebruiken. Als u geen reeds bestaande gegevensstroom hebt, zie [!DNL AWS] documentatie over [een nieuwe gegevensstroom maken met de [!DNL AWS] Beheerconsole](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## De extensie installeren {#install}

Als u het dialoogvenster [!DNL AWS] de extensie, navigeert u naar de gebruikersinterface van de gegevensverzameling of het Experience Platform en selecteert u **[!UICONTROL Event Forwarding]** in de linkernavigatie. Van hier, selecteer een bezit om de uitbreiding aan toe te voegen, of een nieuw bezit in plaats daarvan tot stand te brengen.

Als u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie, dan selecteer **[!UICONTROL Catalog]** tab. Zoeken naar [!UICONTROL AWS] kaart, dan selecteren **[!UICONTROL Install]**.

![De [!UICONTROL Install] knop die wordt geselecteerd voor de [!UICONTROL AWS] in de UI voor gegevensverzameling.](../../../images/extensions/server/aws/install.png)

In het volgende scherm moet u de verbindingsgegevens opgeven voor uw [!DNL AWS] account. Specifiek, moet u uw verstrekken [!DNL AWS] toegangssleutel-id en geheime toegangssleutel. Als u deze waarden niet kent, raadpleegt u de [!DNL AWS] documentatie over [hoe te om uw toegangs belangrijkste identiteitskaart en geheime toegangssleutel te verkrijgen](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![De toegangs belangrijkste identiteitskaart en geheime toegangssleutel die in de mening van de uitbreidingsconfiguratie worden toegevoegd.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Een toegangsbeleid moet aan het [!DNL AWS] account die wordt gebruikt om de toegangsreferenties te genereren. Dit beleid moet worden gevormd om toegangsrechten te verlenen om gegevens naar te verzenden [!DNL Kinesis] gegevensstroom. Zie **Voorbeeld 2** in de [!DNL AWS] document op [voorbeeldbeleid voor [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) om te zien hoe het beleid moet worden gedefinieerd.

Als u klaar bent, selecteert u **[!UICONTROL Save]** en de extensie is geïnstalleerd.

## Vorm een gebeurtenis door:sturen regel {#rule}

Na het installeren van de uitbreiding, creeer een nieuwe gebeurtenis door:sturen [regel](../../../ui/managing-resources/rules.md) en configureer de voorwaarden naar wens. Wanneer het vormen van de acties voor de regel, selecteer **[!UICONTROL AWS]** extensie selecteert u vervolgens **[!UICONTROL Send Data to Kinesis Data Stream]** voor het actietype.

![De [!UICONTROL Send Data to Kinesis Data Stream] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/aws/select-action-type.png)

Het rechterdeelvenster wordt bijgewerkt om configuratieopties weer te geven voor de manier waarop de gegevens moeten worden verzonden. Specifiek, moet u toewijzen [gegevenselementen](../../../ui/managing-resources/data-elements.md) aan de verschillende eigenschappen die uw vertegenwoordigen [!DNL Event Hub] configuratie.

![De configuratieopties voor de [!UICONTROL Send Data to Kinesis Data Stream] actietype dat in UI wordt getoond.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream Details]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Stream Name] | De naam van de stroom aan dat deze gebeurtenis die regel door:sturen zal gegevensverslagen naar verzenden. |
| [!UICONTROL AWS Region] | De [!DNL AWS] regio waar [!DNL Kinesis] gegevensstroom wordt gemaakt. |
| [!UICONTROL Partition Key] | De [partitietoets](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) dat de extensie wordt gebruikt wanneer gegevens naar de gegevensstroom worden verzonden.<br><br>[!DNL Kinesis Data Streams] Hiermee worden de gegevensrecords die bij een stream horen, op meerdere locaties gescheiden. Het gebruikt de verdelingssleutel die met elk gegevensverslag wordt verzonden om te bepalen tot welk deel een bepaald gegevensverslag behoort.<br><br>Een goede verdelingssleutel voor het verdelen van klanten zou het klantenaantal kunnen zijn, aangezien het voor elke klant verschillend is. Een slechte verdelingssleutel zou hun postcode kunnen zijn omdat zij allen in het zelfde gebied dichtbij kunnen leven. In het algemeen, zou u een verdelingssleutel moeten kiezen die de hoogste waaier van verschillende potentiële waarden heeft. Zie de [!DNL AWS] artikel over [uw [!DNL Kinesis] gegevensstromen](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) voor beste praktijken bij het beheren van verdelingssleutels. |

{style=&quot;table-layout:auto&quot;}

**[!UICONTROL Data]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Payload] | Dit veld bevat de gegevens die worden doorgestuurd naar de [!DNL Kinesis] gegevensstroom, in JSON-indeling.<br><br>Onder de **[!UICONTROL Raw]** kunt u het JSON-object rechtstreeks in het opgegeven tekstveld plakken of het pictogram voor het gegevenselement selecteren (![Dataset-pictogram](../../../images/extensions/server/aws/data-element-icon.png)) om een keuze te maken uit een lijst met bestaande gegevenselementen die de lading vertegenwoordigen.<br><br>U kunt ook de opdracht **[!UICONTROL JSON Key-Value Pairs Editor]** optie om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar er kan ook een gegevenselement worden geselecteerd. |

{style=&quot;table-layout:auto&quot;}

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de actie aan de regelconfiguratie toe te voegen. Als u tevreden bent met de regel, selecteert u **[!UICONTROL Save to Library]**.

Ten slotte publiceert u een nieuwe gebeurtenis die wordt doorgestuurd [build](../../../ui/publishing/builds.md) om de wijzigingen in de bibliotheek in te schakelen.

## Volgende stappen

In deze handleiding wordt beschreven hoe gegevens worden verzonden naar [!DNL Kinesis Data Streams] met de [!DNL AWS] gebeurtenis die uitbreiding door:sturen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).
