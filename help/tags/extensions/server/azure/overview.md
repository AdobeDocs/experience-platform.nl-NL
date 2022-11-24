---
title: Microsoft Azure Extension Overview
description: Meer informatie over de Microsoft Azure-extensie voor het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# [!DNL Microsoft Azure] extensieoverzicht

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) is een hoogst scalable, real-time dienst van de gegevenstoegang die u toestaat om de enorme hoeveelheden gegevens te verwerken en te analyseren die door uw verbonden apparaten en toepassingen worden geproduceerd. Zodra de gegevens in een gebeurtenishub worden verzameld, kan het worden omgezet en worden opgeslagen gebruikend om het even welke levering van de analyses in real time of het partij/opslagadapters.

De [!DNL Microsoft Azure] [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) extensiefuncties [!DNL Event Hubs] om gebeurtenissen van Adobe Experience Platform Edge Network te verzenden naar [!DNL Azure] voor verdere verwerking. Deze gids behandelt hoe te om de uitbreiding te installeren en zijn mogelijkheden in een gebeurtenis aan te wenden die regel door:sturen.

## Vereisten

Als u deze extensie wilt gebruiken, moet u over een geldige [!DNL Azure] account met toegang tot [!DNL Event Hubs]. U moet ook [een gebeurtenishub maken met de [!DNL Azure] portaal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) voordat u de onderstaande stappen uitvoert.

## De extensie installeren

De Microsoft installeren [!DNL Azure] de extensie, navigeert u naar de gebruikersinterface van de gegevensverzameling of het Experience Platform en selecteert u **[!UICONTROL Event Forwarding]** in de linkernavigatie. Van hier, selecteer een bezit om de uitbreiding aan toe te voegen, of een nieuw bezit in plaats daarvan tot stand te brengen.

Als u de gewenste eigenschap hebt geselecteerd of gemaakt, selecteert u **[!UICONTROL Extensions]** in de linkernavigatie, dan selecteer **[!UICONTROL Catalog]** tab. Zoeken naar [!UICONTROL Microsoft Azure] kaart, dan selecteren **[!UICONTROL Install]**.

![De [!UICONTROL Install] knop die wordt geselecteerd voor de [!UICONTROL Microsoft Azure] in de UI voor gegevensverzameling.](../../../images/extensions/server/azure/install.png)

Aangezien de extensie geen configuratie-eigenschappen heeft, wordt deze direct toegevoegd aan de lijst met geïnstalleerde extensies. U kunt nu beginnen met [!DNL Event Hub] actietypen wanneer het vormen van gebeurtenis die regels door:sturen.

## Vorm een gebeurtenis door:sturen regel {#rule}

Begin creërend een nieuwe gebeurtenis door:sturen regel en vorm zijn voorwaarden zoals gewenst. Selecteer bij het selecteren van de handelingen voor de regel de optie **[!UICONTROL Microsoft Azure]** voor de extensie selecteert u vervolgens **[!UICONTROL Send Data to Event Hubs]** voor actietype.

![De [!UICONTROL Send Data to Event Hubs] actietype dat voor een regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/azure/select-action-type.png)

Het rechterdeelvenster wordt bijgewerkt om configuratieopties weer te geven voor de manier waarop de gegevens moeten worden verzonden. Specifiek, moet u toewijzen [gegevenselementen](../../../ui/managing-resources/data-elements.md) aan de verschillende eigenschappen die uw vertegenwoordigen [!DNL Event Hub] configuratie.

![De configuratieopties voor de [!UICONTROL Send Data to Event Hubs] actietype dat in UI wordt getoond.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Namespace] | De naam van de [!DNL Event Hubs] naamruimte die u hebt gemaakt toen [de gebeurtenishub instellen](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | De naam van de gebeurtenishub. |
| [!UICONTROL SAS Authorization Rule Name] | De naam van de gedeelde regel van de toegangsvergunning voor uw volledige [!DNL Event Hubs] naamruimte of de specifieke instantie van de gebeurtenishub waarnaar u gegevens wilt verzenden. Zie het aanhangsel over [waarden voor SAS-autorisaties verkrijgen](#sas) voor meer informatie . |
| [!UICONTROL SAS Access Key] | De primaire sleutel van de gedeelde toegangsvergunningsregel voor uw volledig [!DNL Event Hubs] naamruimte of de specifieke instantie van de gebeurtenishub waarnaar u gegevens wilt verzenden. Zie het aanhangsel over [waarden voor SAS-autorisaties verkrijgen](#sas) voor meer informatie . |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] staat u toe [verzendt gebeurtenissen rechtstreeks naar specifieke partities](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Als u deze functie wilt gebruiken, moet u de id opgeven van de partitie die u de gebeurtenissen wilt ontvangen. |

{style=&quot;table-layout:auto&quot;}

**Gegevens**

| Invoer | Beschrijving |
| --- | --- |
| [!UICONTROL Payload] | Dit veld bevat de gegevens die worden doorgestuurd naar de [!DNL Event Hubs]. De gegevens kunnen een JSON-object, een tekenreeks of een gegevenselement zijn. |

{style=&quot;table-layout:auto&quot;}

Als u klaar bent, selecteert u **[!UICONTROL Keep Changes]** om de actie aan de regelconfiguratie toe te voegen. Als u tevreden bent met de regel, selecteert u **[!UICONTROL Save to Library]**.

Ten slotte publiceert u een nieuwe gebeurtenis die wordt doorgestuurd [build](../../../ui/publishing/builds.md) om de wijzigingen in de bibliotheek in te schakelen.

## Volgende stappen

In deze handleiding wordt beschreven hoe gegevens worden verzonden naar [!DNL Event Hubs] met de [!DNL Microsoft Azure] gebeurtenis die uitbreiding door:sturen. Voor meer informatie over gebeurtenis die mogelijkheden in Experience Platform door:sturen, verwijs naar [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).

## Aanhangsel: SAS-autorisatiewaarden verkrijgen {#sas}

Externe toepassingen krijgen toegang tot [!DNL Event Hubs] doorheen [handtekening voor gedeelde toegang (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Elk [!DNL Event Hubs] namespace en de instantie van de gebeurtenishub hebben automatisch een standaard SAS vergunningsregel die bij verwezenlijking wordt toegewezen, maar u kunt extra beleid voor elk middel ook tot stand brengen als u wenst.

Wanneer [het vormen van een gebeurtenis door:sturen regel](#rule) met de [!DNL Azure] extensie, moet u de naam en de primaire sleutel opgeven voor de machtigingsregel voor de naamruimte of specifieke gebeurtenishub waarnaar u gegevens wilt verzenden. Voor meer informatie over hoe u deze waarden kunt verkrijgen via de [!DNL Azure] het portaal, verwijs naar de volgende secties in [!DNL Azure] documentatie:

* [SAS-waarden verkrijgen voor een [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [SAS-waarden verkrijgen voor een specifieke gebeurtenishub in een naamruimte](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Zodra u de vereiste waarden hebt, kan de naam van de vergunningsregel direct als koord in config input worden verstrekt of u kunt een koord-type gegevenselement tot stand brengen om het in plaats daarvan van verwijzingen te voorzien. De primaire sleutel, echter, moet eerst binnen een gebeurtenis worden bevat die geheim door:sturen alvorens het in de regelconfiguratie kan worden verstrekt om uw gegevensveiligheid te beschermen.

Binnen de gebeurtenis die UI door:sturen, [een nieuw geheim maken](../../../ui/event-forwarding/secrets.md) en selecteert u **[!UICONTROL Token]** als het geheime type. Geef voor de tokenwaarde zelf de primaire sleutel op die u eerder hebt gekopieerd. Nadat u het geheim hebt gemaakt, maakt u een gegevenselement met het type **[!UICONTROL Secret]** en selecteert u de [!DNL Event Hubs] geheim in de lijst. Zodra het geheime gegevenselement opstelling is, kunt u dat gegevenselement in verwijzen **[!UICONTROL SAS Access Key]** veld.
