---
title: Overzicht AWS-extensie
description: Meer informatie over de AWS-extensie voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# [!DNL AWS] overzicht van extensies

[[!DNL Amazon Web Services]  ([!DNL AWS]) &#x200B;](https://aws.amazon.com/) is een wolk verwerkend platform dat een brede verscheidenheid van de diensten zoals gedistribueerde gegevensverwerking, gegevensbestandopslag, inhoudslevering, en software-as-a-dienst (SaaS) integratiediensten voor het beheer van de klantenverhouding (CRM) en ondernemingsmiddel planning (ERP) aanbiedt.

De [!DNL AWS] [&#x200B; gebeurtenis die &#x200B;](../../../ui/event-forwarding/overview.md) uitbreidingshefboomwerkingen [[!DNL Amazon Kinesis Data Streams] &#x200B;](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) door:sturen om gebeurtenissen van Adobe Experience Platform Edge Network naar [!DNL AWS] voor verdere verwerking te verzenden. Deze gids behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in een gebeurtenis aan te wenden die regel door:sturen.

## Vereisten

U moet een [!DNL AWS] -account met een bestaande [!DNL Kinesis] -gegevensstroom hebben om deze extensie te kunnen gebruiken. Als u geen reeds bestaande gegevensstroom hebt, zie de [!DNL AWS] documentatie over [&#x200B; het creëren van een nieuwe gegevensstroom gebruikend de  [!DNL AWS]  Console van het Beheer &#x200B;](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## De extensie installeren {#install}

Als u de extensie [!DNL AWS] wilt installeren, navigeert u naar de gebruikersinterface van de gegevensverzameling of de gebruikersinterface van Experience Platform en selecteert u **[!UICONTROL Event Forwarding]** in de linkernavigatie. Selecteer van hieruit een eigenschap waaraan u de extensie wilt toevoegen of maak een nieuwe eigenschap.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie en selecteert u vervolgens de tab **[!UICONTROL Catalog]** . Zoek de [!UICONTROL AWS] -kaart en selecteer vervolgens **[!UICONTROL Install]** .

![&#x200B; de [!UICONTROL Install] knoop die voor de [!UICONTROL AWS] uitbreiding in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/aws/install.png)

In het volgende scherm moet u de verbindingsgegevens voor uw [!DNL AWS] -account opgeven. U moet met name de toegangssleutel-id van [!DNL AWS] en de sleutel voor geheime toegang opgeven. Als u deze waarden niet kent, zie de [!DNL AWS] documentatie over [&#x200B; hoe te om uw toegangs zeer belangrijke identiteitskaart en geheime toegangssleutel &#x200B;](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html) te verkrijgen.

![&#x200B; Toegangs zeer belangrijke identiteitskaart en geheime toegangstoets die in de mening van de uitbreidingsconfiguratie worden toegevoegd.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>Een toegangsbeleid moet aan de [!DNL AWS] rekening worden vastgemaakt die wordt gebruikt om de toegangsgeloofsbrieven te produceren. Dit beleid moet worden gevormd om toegangsrechten te verlenen om gegevens naar de [!DNL Kinesis] gegevensstroom te verzenden. Verwijs naar **Voorbeeld 2** in het [!DNL AWS] document op [&#x200B; voorbeeldbeleid voor  [!DNL Kinesis Data Streams] &#x200B;](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) om te zien hoe het beleid zou moeten worden bepaald.

Wanneer u klaar bent, selecteert u **[!UICONTROL Save]** en wordt de extensie geïnstalleerd.

## Vorm een gebeurtenis door:sturen regel {#rule}

Na het installeren van de uitbreiding, creeer een nieuwe gebeurtenis door:sturen [&#x200B; regel &#x200B;](../../../ui/managing-resources/rules.md) en vorm zijn voorwaarden zoals gewenst. Wanneer u de handelingen voor de regel configureert, selecteert u de extensie **[!UICONTROL AWS]** en vervolgens **[!UICONTROL Send Data to Kinesis Data Stream]** voor het actietype.

![&#x200B; het [!UICONTROL Send Data to Kinesis Data Stream] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/aws/select-action-type.png)

Het rechterdeelvenster wordt bijgewerkt om configuratieopties weer te geven voor de manier waarop de gegevens moeten worden verzonden. Specifiek, moet u [&#x200B; gegevenselementen &#x200B;](../../../ui/managing-resources/data-elements.md) aan de diverse eigenschappen toewijzen die uw [!DNL Event Hub] configuratie vertegenwoordigen.

![&#x200B; de configuratieopties voor het [!UICONTROL Send Data to Kinesis Data Stream] actietype dat in UI wordt getoond.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream Details]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Stream Name] | De naam van de stroom aan dat deze gebeurtenis die regel door:sturen zal gegevensverslagen naar verzenden. |
| [!UICONTROL AWS Region] | Het [!DNL AWS] -gebied waar de [!DNL Kinesis] -gegevensstroom wordt gemaakt. |
| [!UICONTROL Partition Key] | De [&#x200B; verdelingssleutel &#x200B;](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) die de uitbreiding zal gebruiken wanneer het verzenden van gegevens naar de gegevensstroom.<br><br>[!DNL Kinesis Data Streams] segregeert de gegevensrecords die bij een stream horen in meerdere domeinen. Het gebruikt de verdelingssleutel die met elk gegevensverslag wordt verzonden om te bepalen tot welk deel een bepaald gegevensverslag behoort.<br><br> een goede verdelingssleutel voor het verdelen van klanten zou het klantenaantal kunnen zijn, aangezien het voor elke klant verschillend is. Een slechte verdelingssleutel zou hun postcode kunnen zijn omdat zij allen in het zelfde gebied dichtbij kunnen leven. In het algemeen, zou u een verdelingssleutel moeten kiezen die de hoogste waaier van verschillende potentiële waarden heeft. Zie het [!DNL AWS] artikel op [&#x200B; schrapend uw  [!DNL Kinesis]  gegevensstromen &#x200B;](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) voor beste praktijken bij het beheren van verdelingssleutels. |

{style="table-layout:auto"}

**[!UICONTROL Data]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Payload] | Dit veld bevat de gegevens die in JSON-indeling naar de [!DNL Kinesis] -gegevensstroom worden doorgestuurd.<br><br> onder de **[!UICONTROL Raw]** optie, kunt u het voorwerp JSON in het verstrekte tekstgebied direct kleven, of u kunt het pictogram van het gegevenselement (![&#x200B; pictogram Dataset &#x200B;](/help/images/icons/database.png)) selecteren uit een lijst van bestaande gegevenselementen om de nuttige lading te vertegenwoordigen.<br><br> u kunt de **[!UICONTROL JSON Key-Value Pairs Editor]** optie ook gebruiken om elk zeer belangrijk-waardepaar door een redacteur manueel toe te voegen UI. Elke waarde kan worden vertegenwoordigd door een onbewerkte invoer, maar in plaats daarvan kan ook een gegevenselement worden geselecteerd. |

{style="table-layout:auto"}

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de handeling aan de regelconfiguratie toe te voegen. Selecteer **[!UICONTROL Save to Library]** als u tevreden bent met de regel.

Tot slot publiceer een nieuwe gebeurtenis door:sturen [&#x200B; bouwt &#x200B;](../../../ui/publishing/builds.md) om de veranderingen in de bibliotheek toe te laten.

## Volgende stappen

In deze handleiding wordt beschreven hoe u gegevens naar [!DNL Kinesis Data Streams] kunt verzenden met de extensie [!DNL AWS] voor het doorsturen van gebeurtenissen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar de [&#x200B; gebeurtenis die overzicht &#x200B;](../../../ui/event-forwarding/overview.md) door:sturen.
