---
title: Microsoft Azure Extension Overview
description: Meer informatie over de Microsoft Azure-extensie voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# [!DNL Microsoft Azure] overzicht van extensies

In [!DNL Microsoft Azure], [[!DNL Event Hubs] &#x200B;](https://azure.microsoft.com/en-us/products/event-hubs/#overview) is een hoogst scalable, real time dienst van de gegevenstoegang die u toestaat om de enorme hoeveelheden gegevens te verwerken en te analyseren die door uw verbonden apparaten en toepassingen worden geproduceerd. Zodra de gegevens in een gebeurtenishub worden verzameld, kan het worden omgezet en worden opgeslagen gebruikend om het even welke levering van de analyses in real time of het partij/opslagadapters.

De [!DNL Microsoft Azure] [&#x200B; gebeurtenis die &#x200B;](../../../ui/event-forwarding/overview.md) uitbreidingshefboomwerkingen [!DNL Event Hubs] door:sturen om gebeurtenissen van Adobe Experience Platform Edge Network naar [!DNL Azure] voor verdere verwerking te verzenden. Deze gids behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in een gebeurtenis aan te wenden die regel door:sturen.

## Vereisten

Als u deze extensie wilt gebruiken, moet u een geldige [!DNL Azure] -account hebben met toegang tot [!DNL Event Hubs] . U moet ook [&#x200B; tot een gebeurtenishub leiden gebruikend het  [!DNL Azure]  portaal &#x200B;](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) alvorens de stappen hieronder te volgen.

## De extensie installeren

Als u de extensie Microsoft [!DNL Azure] wilt installeren, navigeert u naar de gebruikersinterface van de gegevensverzameling of de gebruikersinterface van Experience Platform en selecteert u **[!UICONTROL Event Forwarding]** in de linkernavigatie. Selecteer van hieruit een eigenschap waaraan u de extensie wilt toevoegen of maak een nieuwe eigenschap.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie en selecteert u vervolgens de tab **[!UICONTROL Catalog]** . Zoek de [!UICONTROL Microsoft Azure] -kaart en selecteer vervolgens **[!UICONTROL Install]** .

![&#x200B; de [!UICONTROL Install] knoop die voor de [!UICONTROL Microsoft Azure] uitbreiding in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/azure/install.png)

Aangezien de extensie geen configuratie-eigenschappen heeft, wordt deze direct toegevoegd aan de lijst met geïnstalleerde extensies. U kunt nu de actietypen van [!DNL Event Hub] gebruiken wanneer het vormen van gebeurtenis door:sturen regels.

## Vorm een gebeurtenis door:sturen regel {#rule}

Begin creërend een nieuwe gebeurtenis door:sturen regel en vorm zijn voorwaarden zoals gewenst. Wanneer u de handelingen voor de regel selecteert, selecteert u **[!UICONTROL Microsoft Azure]** voor de extensie en selecteert u **[!UICONTROL Send Data to Event Hubs]** voor het handelingstype.

![&#x200B; het [!UICONTROL Send Data to Event Hubs] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/azure/select-action-type.png)

Het rechterdeelvenster wordt bijgewerkt om configuratieopties weer te geven voor de manier waarop de gegevens moeten worden verzonden. Specifiek, moet u [&#x200B; gegevenselementen &#x200B;](../../../ui/managing-resources/data-elements.md) aan de diverse eigenschappen toewijzen die uw [!DNL Event Hub] configuratie vertegenwoordigen.

![&#x200B; de configuratieopties voor het [!UICONTROL Send Data to Event Hubs] actietype dat in UI wordt getoond.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Namespace] | De naam van [!DNL Event Hubs] namespace die u creeerde toen [&#x200B; vestiging de gebeurtenishub &#x200B;](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | De naam van de gebeurtenishub. |
| [!UICONTROL SAS Authorization Rule Name] | De naam van de regel voor gedeelde toegangsmachtigingen voor de gehele naamruimte [!DNL Event Hubs] of de specifieke instantie van de gebeurtenishub waarnaar u gegevens wilt verzenden. Zie de bijlage sectie over [&#x200B; het verkrijgen van de toestemmingswaarden van SAS &#x200B;](#sas) voor meer informatie. |
| [!UICONTROL SAS Access Key] | De primaire sleutel van de gedeelde toegangsautorisatieregel voor uw volledige [!DNL Event Hubs] namespace of de specifieke instantie van de gebeurtenishub waarnaar u gegevens wilt verzenden. Zie de bijlage sectie over [&#x200B; het verkrijgen van de toestemmingswaarden van SAS &#x200B;](#sas) voor meer informatie. |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] staat u toe om gebeurtenissen [&#x200B; rechtstreeks naar specifieke verdelingen &#x200B;](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka) te verzenden. Als u deze functie wilt gebruiken, moet u de id opgeven van de partitie die u de gebeurtenissen wilt ontvangen. |

{style="table-layout:auto"}

**Gegevens**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Payload] | Dit veld bevat de gegevens die naar de [!DNL Event Hubs] worden doorgestuurd. De gegevens kunnen een JSON-object, een tekenreeks of een gegevenselement zijn. |

{style="table-layout:auto"}

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de handeling aan de regelconfiguratie toe te voegen. Selecteer **[!UICONTROL Save to Library]** als u tevreden bent met de regel.

Tot slot publiceer een nieuwe gebeurtenis door:sturen [&#x200B; bouwt &#x200B;](../../../ui/publishing/builds.md) om de veranderingen in de bibliotheek toe te laten.

## Volgende stappen

In deze handleiding wordt beschreven hoe u gegevens naar [!DNL Event Hubs] kunt verzenden met de extensie [!DNL Microsoft Azure] voor het doorsturen van gebeurtenissen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar de [&#x200B; gebeurtenis die overzicht &#x200B;](../../../ui/event-forwarding/overview.md) door:sturen.

## Aanhangsel: Waarden voor SAS-autorisaties verkrijgen {#sas}

De externe toepassingen worden verleend toegang tot [!DNL Event Hubs] door [&#x200B; gedeelde toegangshandtekeningen (SAS) &#x200B;](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Elke [!DNL Event Hubs] namespace en instantie van de gebeurtenishub heeft een standaard SAS vergunningsregel automatisch toegewezen bij verwezenlijking, maar u kunt extra beleid voor elke middel ook tot stand brengen als u wenst.

Wanneer [&#x200B; vormend een gebeurtenis door:sturen regel &#x200B;](#rule) gebruikend de [!DNL Azure] uitbreiding, moet u de naam en de primaire sleutel voor de vergunningsregel verstrekken die namespace of specifieke gebeurtenishub besturen u gegevens wilt verzenden naar. Raadpleeg de volgende secties in de [!DNL Azure] -documentatie voor meer informatie over het verkrijgen van deze waarden via de [!DNL Azure] portal:

* [&#x200B; verkrijgt SAS waarden voor a  [!DNL Event Hubs]  namespace &#x200B;](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [&#x200B; verkrijg SAS waarden voor een specifieke gebeurtenishub in a namespace &#x200B;](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Zodra u de vereiste waarden hebt, kan de naam van de vergunningsregel direct als koord in config input worden verstrekt of u kunt een koord-type gegevenselement tot stand brengen om het in plaats daarvan van verwijzingen te voorzien. De primaire sleutel, echter, moet eerst binnen een gebeurtenis worden bevat die geheim door:sturen alvorens het in de regelconfiguratie kan worden verstrekt om uw gegevensveiligheid te beschermen.

Binnen gebeurtenis die UI door:sturen, [&#x200B; creeer een nieuw geheim &#x200B;](../../../ui/event-forwarding/secrets.md) en selecteer **[!UICONTROL Token]** als geheim type. Geef voor de tokenwaarde zelf de primaire sleutel op die u eerder hebt gekopieerd. Nadat u het geheim hebt gemaakt, maakt u een gegevenselement met het type **[!UICONTROL Secret]** en selecteert u het [!DNL Event Hubs] -geheim in de lijst. Nadat het element met geheime gegevens is ingesteld, kunt u naar dat gegevenselement verwijzen in het veld **[!UICONTROL SAS Access Key]** .
