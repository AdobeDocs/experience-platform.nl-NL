---
title: Marketo Engage Person Sync
description: Gebruik de connector Marketo Engage Person Sync om updates te streamen van een persoonlijk publiek naar de corresponderende records in uw Marketo Engage.
last-substantial-update: 2025-01-14T00:00:00Z
badgeBeta: label="Beta" type="Informative"
exl-id: 2c909633-b169-4ec8-9f58-276395cb8df2
source-git-commit: 7d9f06f77f2265f3ae62542fd7fc1bd09d34d078
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 6%

---

# Marketo Engage Person Sync verbinding {#marketo-engage-person-sync}

>[!IMPORTANT]
>
>Deze bestemmingsconnector bevindt zich in de bètafase en is alleen beschikbaar voor geselecteerde klanten. Neem contact op met uw Adobe-vertegenwoordiger om toegang aan te vragen.

>[!IMPORTANT]
>
>De **[!UICONTROL Marketo Engage Person Sync]** bestemmingskaart zal in **Oktober 2025** worden afgekeurd.
>
>Voor een vloeiende overgang naar de nieuwe **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)**-bestemming controleert u de volgende belangrijke punten en vereiste acties:
>
>* Alle gebruikers moeten **ophouden gebruikend de bestemming van de Synchronisatie van de Persoon van Marketo Engage** en aan de nieuwe **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** bestemming tegen Oktober 2025 migreren.
>* **Bestaande gegevensstromen zullen niet automatisch worden gemigreerd.** U moet [een nieuwe verbinding instellen](marketo-engage-connection.md#connect-to-the-destination) naar de nieuwe **[!UICONTROL Marketo Engage]**-bestemming en daar uw doelgroepen activeren.


## Overzicht {#overview}

Gebruik de connector Marketo Engage Person Sync om updates te streamen van het persoonlijke publiek naar de corresponderende records in uw Marketo Engage-instantie.

>[!IMPORTANT]
> 
>De [&#x200B; Schakelaar van de Synchronisatie van het publiek van Marketo V2 &#x200B;](/help/destinations/catalog/adobe/marketo-engage.md) zou niet op Create wijze samen met de Schakelaar van de Synchronisatie van de Update van het Profiel moeten worden gebruikt

## Ondersteunde identiteiten en kenmerken {#support-identities-and-attributes}

### Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |

{style="table-layout:auto"}

### Ondersteunde kenmerken {#supported-attributes}

U kunt kenmerken van Experience Platform toewijzen aan alle kenmerken waartoe uw organisatie in Marketo toegang heeft. In Marketo, kunt u [&#x200B; gebruiken beschrijf API &#x200B;](https://developer.adobe.com/marketo-apis/api/mapi/#tag/Leads/operation/describeUsingGET_6) verzoek om de attributengebieden terug te winnen die uw organisatie toegang heeft tot.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
| -------------------- | :-------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Segmentatieservice | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#128279;](https://experienceleague.adobe.com/nl/docs/experience-platform/segmentation/home). |
| Aangepaste uploads | ✓ | Soorten publiek dat uit CSV-bestanden in Experience Platform is geïmporteerd. |

## Type en frequentie exporteren {#export-type-and-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| ---------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Exportfrequentie | Streaming | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Doel instellen {#set-up-destination}

>[!IMPORTANT]
>
>* Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig.

Als uw bedrijf toegang tot veelvoudige organisaties heeft, zorg ervoor dat u de zelfde organisatie in zowel Marketo Engage als Real-Time CDP gebruikt, waar u opstelling de bestemmingsschakelaar aan Marketo bent.  Als u al een doel hebt geconfigureerd, kunt u een bestaande Marketo-account selecteren voor gebruik met uw nieuwe configuratie.  Als niet, klik de Schakelaar aan de herinnering van de Bestemming, die u zal toestaan om de naam, de beschrijving, en identiteitskaart van Marketo Munchkin van de gewenste bestemming te plaatsen.  De Munchkin-id van uw Marketo-instantie vindt u in het menu Admin->Munchkin.

>[!IMPORTANT]
>
>De gebruiker die opstelling de bestemming moet [&#x200B; toestemming van de Persoon &#x200B;](https://experienceleague.adobe.com/nl/docs/marketo/using/product-docs/administration/users-and-roles/descriptions-of-role-permissions#access-database) hebben uitgeven in de instantie en de verdeling van Marketo.

![&#x200B; verbind met Bestemming &#x200B;](../../assets/catalog/adobe/marketo-engage-person-sync/connect-to-destination.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Munchkin ID]**: De Munchkin-id is de unieke id voor een specifieke Marketo-instantie.
* **[!UICONTROL Partition]**: een concept in Marketo Engage dat wordt gebruikt om hoofdrecords te scheiden op bedrijfsniveau
* **[!UICONTROL First searchable field]**: veld dat moet worden gededupliceerd. Het veld moet aanwezig zijn in elke eerstvolgende record van de invoer. Standaard e-mailadres
* **[!UICONTROL First searchable field]**: Een secundair veld dat moet worden gededupliceerd. Het veld moet aanwezig zijn in elke eerstvolgende record van de invoer. Optioneel

Nadat u de instantie hebt geselecteerd, moet u ook de partitie Lead selecteren waarmee u de configuratie wilt integreren. A [&#x200B; de Verdeling van de Lood &#x200B;](https://experienceleague.adobe.com/nl/docs/marketo/using/product-docs/administration/workspaces-and-person-partitions/understanding-workspaces-and-person-partitions) is een concept in Marketo Engage dat wordt gebruikt om loodverslagen door bedrijfszorg, zoals een merk of een verkoopgebied te scheiden. Als uw Marketo-abonnement niet over de functie Werkruimten en Partities beschikt of als uw abonnement geen extra partities bevat, is alleen de standaardpartitie beschikbaar. Één enkele configuratie kan slechts loodverslagen bijwerken die in zijn gevormde verdeling bestaan.

>[!IMPORTANT]
> 
>Nadat een publiek aan de bestemming van Marketo voor het eerst is geactiveerd, kan het terugvullen van profielen die reeds in het publiek vóór de bestemmingsactivering van Marketo bestonden *tot 24 uren* nemen. Als profielen worden toegevoegd aan de doelgroep, worden ze direct toegevoegd aan Marketo.

### Deduplicatievelden {#deduplication-fields}

Wanneer updates naar Marketo worden verzonden, worden records geselecteerd op basis van de geselecteerde partitie en een of twee door de gebruiker geselecteerde velden. Als uw bestemming met de verdeling van Noord-Amerika wordt gevormd, en E-mailAdres en de Naam van het Bedrijf heeft die als deduplicatiegebieden wordt gevormd, dan moeten alle drie gebieden aanpassen om veranderingen op een bestaand verslag toe te passen. Bijvoorbeeld:

* De bestemming wordt gevormd met de verdeling van Noord-Amerika
* Persoon met e-mail <test@example.com> en Company name Example Inc. in Experience Platform komt overeen met het doelpubliek
* Tenzij er al een record met deze waarden bestaat op de Noord-Amerikaanse partitie in Marketo, wordt een nieuwe lead record gemaakt

Als er geen overeenkomende lead-record wordt gevonden, wordt een nieuwe record gemaakt.

![&#x200B; Details van de Bestemming &#x200B;](../../assets/catalog/adobe/marketo-engage-person-sync/destination-details.png)

## Soorten publiek activeren {#activate-audiences}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [&#x200B; activeer profielen en segmenten aan het stromen segment de uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

In de stap Soorten publiek activeren kunt u een publiek selecteren dat voor u zichtbaar is.

![&#x200B; activeer publiek &#x200B;](../../assets/catalog/adobe/marketo-engage-person-sync/activate-audiences.png)

## Veldtoewijzing {#field-mapping}

Voor het verzenden van wijzigingen aan een bepaald persoonkenmerk naar Marketo Engage, moet het veld worden toegewezen van een Real-Time CDP-veld naar een Marketo-veld.

![&#x200B; Toewijzing van het Gebied &#x200B;](../../assets/catalog/adobe/marketo-engage-person-sync/field-mapping.png)

Experience Platform-datatypen en Marketo-datatypen kunnen op de volgende manieren worden toegewezen:

| Experience Platform-gegevenstype | Marketo-gegevenstype |
| ----------------------------- | ------------------------------------ |
| String | Tekenreeks, tekstgebied, URL, telefoon, e-mail |
| Enum | String |
| Datum | Datum |
| Datum/tijd | Datumtijd |
| Geheel | Geheel |
| Kort | Geheel |
| Lang | Float |
| Dubbel | Valuta, zwevend, percentage |
| Boolean | Boolean |
| Array | Niet ondersteund |
| Object | Niet ondersteund |
| Kaart | Niet ondersteund |
| Byte | Niet ondersteund |

{style="table-layout:auto"}

In sommige gevallen is het wenselijk toe te staan dat integraties de waarde van een veld instellen als er geen veld is, terwijl integraties worden verhinderd updates uit te voeren naar velden die al een waarde hebben.  Als u moet voorkomen dat de doelconnector bestaande waarden in uw Marketo Engage-instantie overschrijft, kunt u velden configureren om updates te blokkeren in de sectie Admin->Veld-beheer van uw Marketo-instantie en het Adobe Experience Platform-brontype in- en uitschakelen.

![&#x200B; Updates van het Gebied van het Blok &#x200B;](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates.png)

![&#x200B; Updates van het Gebied van het Blok &#x200B;](../../assets/catalog/adobe/marketo-engage-person-sync/block-field-updates-2.png)

## Gebruik en beheer van gegevens {#data-usage-and-governance}

Alle Adobe Experience Platform-doelen zijn bij het verwerken van uw gegevens compatibel met het beleid voor gegevensgebruik. Voor gedetailleerde informatie over hoe Adobe Experience Platform gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het gegevensbeheer &#x200B;](/help/data-governance/home.md).
