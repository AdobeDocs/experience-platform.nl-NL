---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creeer een van de klantenattributen bronschakelaar in UI
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---


# Creeer een van de klantenattributen bronschakelaar in UI

Deze zelfstudie biedt stappen voor het maken van een bronaansluiting in de gebruikersinterface voor het verzamelen van profielgegevens van klantkenmerken naar Adobe Experience Platform. Raadpleeg het [overzichtsdocument](https://docs.adobe.com/content/help/nl-NL/core-services/interface/customer-attributes/attributes.html)voor meer informatie over klantkenmerken.

## Een bronverbinding maken

Meld u aan bij [Adobe Experience Platform](https://platform.adobe.com) en selecteer vervolgens **[!UICONTROL Bronnen]** in de linkernavigatiebalk voor toegang tot de werkruimte Bronnen. In het scherm **[!UICONTROL Catalog]** worden beschikbare bronnen weergegeven om binnenkomende verbindingen te maken met. Elke bron toont het aantal bestaande verbindingen dat aan deze verbindingen is gekoppeld. Selecteer de optie voor **[!UICONTROL Klantkenmerken]** en selecteer vervolgens Gegevens **** toevoegen. Toestaan dat de verbinding enige tijd kan duren, wordt u omgeleid als een verbinding tot stand is gebracht.

>[!NOTE]
>
>Als u reeds een bronschakelaar voor de profielgegevens van klantenattributen hebt gevestigd, zal de optie om met de bron te verbinden gehandicapt zijn.

![](../../../../images/tutorials/create/customer-attributes/catalog.png)

In het scherm *Bronactiviteit* worden alle eerder ingestelde verbindingen voor profielgegevens van klantkenmerken weergegeven. U kunt een nieuwe verbinding maken door op Gegevens **** selecteren te klikken.

>[!NOTE]
>
>De veelvoudige binnenkomende verbindingen aan een bron kunnen voor het brengen van verschillende gegevens worden gemaakt.

![](../../../../images/tutorials/create/customer-attributes/source_activity.png)

Van de lijst van beschikbare het profieldatasets van klantenattributen, selecteer één u in Platform wilt brengen en **daarna** klikken.

>[!NOTE]
>
>Slechts één dataset kan per de bronverbinding van klantenattributen worden geselecteerd.

![](../../../../images/tutorials/create/customer-attributes/select_data.png)

De stap *Revisie* wordt weergegeven, zodat u de nieuwe binnenkomende verbinding kunt controleren voordat deze wordt gemaakt. De details van de verbinding worden gegroepeerd per categorieën, die omvatten:

* *Brongegevens*: Hiermee geeft u het type van de bronverbinding en de geselecteerde brongegevens weer.
* *Doelgegevens*: Wanneer het creëren van andere bronschakelaars, toont deze container welke dataset de brongegevens opnemen in, met inbegrip van het schema de dataset zich aan houdt. Klantkenmerkprofielgegevens worden automatisch toegewezen en opgenomen in realtime profielen van klanten.

![](../../../../images/tutorials/create/customer-attributes/review.png)

## Volgende stappen

Zodra de verbinding wordt gecreeerd, wordt een doelschema en een dataset automatisch gecreeerd om de inkomende gegevens te bevatten. Wanneer de aanvankelijke opname voltooit, kunnen de gegevens van het klantenkenmerkprofiel door de stroomafwaartse diensten van het Platform zoals het Profiel van de Klant In real time en de Dienst van de Segmentatie worden gebruikt. Raadpleeg de volgende documenten voor meer informatie:

* [Overzicht van het realtime klantprofiel](../../../../../profile/home.md)
* [Overzicht van segmentatieservice](../../../../../segmentation/home.md)
