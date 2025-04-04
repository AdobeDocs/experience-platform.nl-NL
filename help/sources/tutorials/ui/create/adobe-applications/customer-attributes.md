---
keywords: Experience Platform;home;populaire onderwerpen;klantkenmerken
solution: Experience Platform
title: Een Source Connection met klantkenmerken maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een bronverbinding maakt in de gebruikersinterface om profielgegevens van klantkenmerken over te brengen naar Adobe Experience Platform.
exl-id: 66bdab8f-c00e-4ebe-8b8e-f9e12cf86bbe
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Een bronverbinding voor klantkenmerken maken in de gebruikersinterface

Deze zelfstudie bevat stappen voor het maken van een bronverbinding in de gebruikersinterface om profielgegevens van klantkenmerken over te brengen naar Adobe Experience Platform. Voor meer informatie over de Attributen van de Klant, zie het [ overzicht van de Attributen van de Klant ](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/attributes.html).

>[!IMPORTANT]
>
>De bron Klantkenmerken ondersteunt momenteel niet het in- of uitschakelen van gegevensstromen.

## Een bronverbinding maken

>[!NOTE]
>
>Als u al een bronverbinding hebt gemaakt voor de profielgegevens van Klantkenmerken, is de optie om verbinding te maken met de bron uitgeschakeld.

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een verbinding kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL Adobe applications] de optie **[!UICONTROL Customer Attributes]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ catalogus ](../../../../images/tutorials/create/customer-attributes/catalog.png)

### Gegevensbron van klantkenmerken selecteren

In het scherm [!UICONTROL Add data] worden alle beschikbare gegevensbronnen voor Klantkenmerken weergegeven. Er kan slechts één gegevensset worden geselecteerd per bronverbinding Klantkenmerken.

>[!NOTE]
>
>De groepen van het gebied, de schema&#39;s, en de datasets worden gecreeerd uit-van-doos als deel van stroomlevering. Ze blijven ongewijzigd en u moet ze indien nodig handmatig verwijderen.

De evolutie van het schema wordt niet gesteund door de bron van klantenattributen. Als de schema-invoer van een klantkenmerkgegevensbron wordt gewijzigd, wordt deze niet meer compatibel met Experience Platform. Als alternerende actie, kunt u een bestaande gegevensstroom van klantenattributen, samen met zijn bijbehorende dataset, schema, en gebiedsgroep schrappen, en dan nieuwe creëren met het bijgewerkte schema en de gegevensbron.

>[!IMPORTANT]
>
>Terwijl u een gegevens van klantenattributen kunt schrappen dataflow, zal zijn overeenkomstige dataset zelfs na schrapping van dataflow blijven. Zie de gids bij [ het schrappen van een dataset ](../../../../../catalog/datasets/user-guide.md) voor stappen op hoe te om een dataset manueel te schrappen.

Als u een nieuwe verbinding wilt maken, selecteert u een gegevensbron in de lijst en selecteert u vervolgens **[!UICONTROL Next]** .

![ toe:voegen-gegevens ](../../../../images/tutorials/create/customer-attributes/add-data.png)

### Gegevens over gegevensstroom opgeven

De stap [!UICONTROL Dataflow detail] wordt weergegeven, zodat u een naam en een korte beschrijving voor de gegevensstroom kunt opgeven. Tijdens dit proces kunt u ook instellingen configureren voor [!UICONTROL Error diagnostics] , [!UICONTROL Partial ingestion] en [!UICONTROL Alerts] .

In [!UICONTROL Error diagnostics] kunnen gedetailleerde foutberichten worden gegenereerd voor onjuiste records in de gegevensstroom, terwijl u in [!UICONTROL Partial ingestion] gegevens met fouten kunt invoeren tot een bepaalde drempel die u handmatig definieert. Zie het [ gedeeltelijke overzicht van partijingestie ](../../../../../ingestion/batch-ingestion/partial.md) voor meer informatie.

U kunt waarschuwingen inschakelen om meldingen te ontvangen over de status van uw gegevensstroom. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bronalarm gebruikend UI ](../../alerts.md).

Wanneer u klaar bent met het opgeven van details voor de gegevensstroom, selecteert u **[!UICONTROL Next]** .

![ dataflow-detail ](../../../../images/tutorials/create/customer-attributes/dataflow-detail.png)

### Gegevensstroom controleren

De stap [!UICONTROL Review] wordt weergegeven, zodat u de nieuwe gegevensstroom kunt bekijken voordat deze wordt gemaakt. De details worden gegroepeerd in de volgende categorieën:

* **[!UICONTROL Connection]**: geeft het brontype, het relevante pad van het gekozen bronbestand en het aantal kolommen in dat bronbestand weer.
* **[!UICONTROL Assign dataset & map fields]**: Toont welke dataset de brongegevens worden opgenomen in, met inbegrip van het schema dat de dataset volgt aan.

![ overzicht ](../../../../images/tutorials/create/customer-attributes/review.png)

## Volgende stappen

Zodra de verbinding wordt gecreeerd, wordt een doelschema en een dataset automatisch gecreeerd om de inkomende gegevens te bevatten. Wanneer de eerste invoer is voltooid, kunnen de klantkenmerkgegevens worden gebruikt door Experience Platform-services die aan de afhandeling zijn toegewezen, zoals [!DNL Real-Time Customer Profile] en [!DNL Segmentation Service] . Raadpleeg de volgende documenten voor meer informatie:

* [[!DNL Real-Time Customer Profile]-overzicht](../../../../../profile/home.md)
* [[!DNL Segmentation Service]-overzicht](../../../../../segmentation/home.md)
