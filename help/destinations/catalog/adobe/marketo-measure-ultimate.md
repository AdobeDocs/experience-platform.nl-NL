---
title: Marketo Measure Ultimate-bestemming
description: Leer hoe u verbinding maakt met en gegevens activeert voor de Marketo Measure Ultimate-bestemming.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Marketo Measure Ultimate-bestemming {#mmu-destination}

## Overzicht {#overview}

Marketo Measure (voorheen Bizible) biedt marketeers insight aan welke marketingactiviteiten het meest effectief zijn in het aansturen van inkomsten en het maximaliseren van het rendement van investeringen voor hun bedrijf. Marketo Measure is een marketingtoewijzingsoplossing die de kanaalprestaties automatisch bijhoudt en rapporteert, zodat u kunt zien in welke kanalen de meeste betrokkenheid van klanten wordt bevorderd en uw marketinguitgaven dienovereenkomstig kunt optimaliseren.

De bestemming laat de zaken-aan-zaken (B2B) gegevensstromen van Adobe Experience Platform aan Marketo Measure toe. De kaart is alleen beschikbaar voor Marketo Measure Ultimate-klanten.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Marketo Measure zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen. Deze integratie:

* Voldoet aan de complexe vereisten voor de rapportage van gegevens en prestaties van grote ondernemingen.
* Maakt B2B-toerekeningsrapportage met meerdere CRM- en marketingautomatiseringssystemen mogelijk.
* Biedt eenvoudig offline aanraakpuntgegevens van andere leveranciers.

## Vereisten {#prerequisites}

Houd rekening met de volgende voorwaarden voor de Marketo Measure-bestemming:

* Experience Platform Sandbox-toewijzing moet door de beheerder worden ingevuld op de pagina Marketo Measure-instellingen. Zonder de functie Sandbox-toewijzing kunt u de workflow niet voltooien om verbinding te maken met het doel om gegevens op te slaan en te activeren.
* Alleen gegevenssets van B2B XDM-klassen kunnen worden geëxporteerd (zie bijvoorbeeld de klassen XDM Business Account en XDM Business Opportunity). U kunt niet in veelvoudige datasets van de zelfde B2B klasse XDM voor een bepaalde gegevensbron brengen.
* Elke dataset kan slechts in één dataflow aan de bestemming van Marketo Measure worden omvat.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Dataset export]** | U exporteert onbewerkte gegevenssets, die niet zijn gegroepeerd of gestructureerd op basis van belangen of kwalificaties van het publiek. Lees meer over [ de uitvoer van de dataset ](/help/destinations/destination-types.md#dataset-export-destinations). |
| Exportfrequentie | **[!UICONTROL Batch]** | Deze batchbestemming exporteert bestanden om de twee uur naar het Marketo Measure-platform. Lees meer over [ plannend dataset de uitvoer ](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage and Activate Dataset Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. Vul de velden in de onderstaande sectie in de workflow voor het configureren van de bestemming in.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

![ verbindt met bestemmingswerkschema voor de bestemming van Marketo Measure.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Gegevenssets exporteren naar deze bestemming {#export-datasets}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u de **[!UICONTROL View Destinations]** en **[!UICONTROL Manage and Activate Dataset Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees de [ datasets van de Uitvoer ](/help/destinations/ui/export-datasets.md) leerprogramma voor uitgebreide instructies bij het uitvoeren van datasets aan deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Om een succesvolle datasetuitvoer te bevestigen, kunt u controleren dat uw dataset het aan uw [ het gegevenspakhuis van Snowflake ](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html) met succes heeft gemaakt.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
