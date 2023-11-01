---
title: Marketo Measure Ultimate-bestemming
description: Leer hoe u verbinding maakt met en gegevens activeert voor de Marketo Measure Ultimate-bestemming.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# Marketo Measure Ultimate-doel {#mmu-destination}

## Overzicht {#overview}

Marketo Measure (voorheen Bizible) geeft de marketeers inzicht in welke marketinginspanningen het meest effectief zijn in het aansturen van inkomsten en het maximaliseren van het rendement van investeringen voor hun bedrijf. Marketo Measure is een marketingtoewijzingsoplossing die de kanaalprestaties automatisch bijhoudt en rapporteert, zodat u kunt zien in welke kanalen de meeste betrokkenheid van klanten wordt bevorderd en uw marketinguitgaven dienovereenkomstig kunt optimaliseren.

De bestemming laat de zaken-aan-zaken (B2B) gegevensstromen van Adobe Experience Platform aan Marketo Measure toe. De kaart is alleen beschikbaar voor Marketo Measure Ultimate-klanten.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Marketo Measure zou moeten gebruiken, zijn hier voorbeelden van gebruiksgevallen die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen. Deze integratie:

* Voldoet aan de complexe vereisten voor de rapportage van gegevens en prestaties van grote ondernemingen.
* Maakt B2B-toerekeningsrapportage met meerdere CRM- en marketingautomatiseringssystemen mogelijk.
* Biedt eenvoudig offline aanraakpuntgegevens van andere leveranciers.

## Vereisten {#prerequisites}

Houd rekening met de volgende voorwaarden voor de Marketo Measure-bestemming:

* Sandbox-toewijzing van Experience Platform moet door de beheerder worden ingevuld op de pagina Marketo Measure-instellingen. Zonder de functie Sandbox-toewijzing kunt u de workflow niet voltooien om verbinding te maken met het doel om gegevens op te slaan en te activeren.
* Alleen gegevenssets van B2B XDM-klassen kunnen worden geëxporteerd (zie bijvoorbeeld de klassen XDM Business Account en XDM Business Opportunity). U kunt niet in veelvoudige datasets van de zelfde B2B klasse XDM voor een bepaalde gegevensbron brengen.
* Elke dataset kan slechts in één dataflow aan de bestemming van Marketo Measure worden omvat.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Dataset export]** | U exporteert onbewerkte gegevenssets, die niet zijn gegroepeerd of gestructureerd op basis van belangen of kwalificaties van het publiek. Meer informatie over [uitvoer gegevensset](/help/destinations/destination-types.md#dataset-export-destinations). |
| Exportfrequentie | **[!UICONTROL Batch]** | Deze batchbestemming exporteert bestanden om de twee uur naar het Marketo Measure-platform. Meer informatie over [gegevensset exporteren plannen](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). Vul de velden in de onderstaande sectie in de workflow voor het configureren van de bestemming in.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

![De Connect to-bestemmingsworkflow voor de Marketo Measure-bestemming.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Gegevenssets exporteren naar deze bestemming {#export-datasets}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL Manage and Activate Dataset Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lees de [(bètaversie) Gegevensbestanden exporteren](/help/destinations/ui/export-datasets.md) zelfstudie voor uitgebreide instructies over het exporteren van datasets naar deze bestemming.

## Gegevens exporteren valideren {#exported-data}

Om een succesvolle uitvoer van datasets te bevestigen, kunt u controleren dat uw dataset het aan uw met succes heeft gemaakt [Snowflake data magazijn](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html).

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).
