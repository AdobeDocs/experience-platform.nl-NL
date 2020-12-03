---
keywords: mobile; braze; messaging;
title: Braze bestemming
seo-title: Braze bestemming
description: Braze is een uitgebreid platform voor klantbetrokkenheid dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt.
seo-description: Braze is een uitgebreid platform voor klantbetrokkenheid dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt.
translation-type: tm+mt
source-git-commit: 9380c9c24267f815b788eb51949da13b8c47558f
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---


# (Beta) [!DNL Braze] bestemming

>[!IMPORTANT]
>
>Het doel Braze in Adobe Experience Platform is momenteel in Bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

Het [!DNL Braze] doel helpt u profielgegevens naar te verzenden [!DNL Braze].

[!DNL Braze] is een uitgebreid platform voor klantenservice dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die zij leuk vinden, mogelijk maakt.

Als u profielgegevens naar wilt verzenden, moet u eerst verbinding maken met het doel. [!DNL Braze]

## Doelspecificaties {#destination-specs}

Let op de volgende details die specifiek zijn voor het [!DNL Braze] doel:

* U kunt elke gewenste [identiteit](../../../identity-service/namespaces.md) naar de [!DNL Braze] bestemming verzenden, zolang u de identiteit aan de bestemming toewijst [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation).
* [!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar [!DNL Braze] onder het `AdobeExperiencePlatformSegments` kenmerk.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik gebruikers in een mobiele betrokkenheidsbestemming richten, met ingebouwde segmenten [!DNL Adobe Experience Platform]. Daarnaast wil ik hen persoonlijke ervaringen bieden op basis van kenmerken van hun [!DNL Adobe Experience Platform] profielen, zodra segmenten en profielen worden bijgewerkt in [!DNL Adobe Experience Platform].

## Exporttype {#export-type}

**[!DNL Profile-based]** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam) en/of identiteiten, afhankelijk van uw veldtoewijzing.
[!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar [!DNL Braze] onder het `AdobeExperiencePlatformSegments` kenmerk.


## Verbinden met doel {#connect-destination}

Selecteer in **[!UICONTROL Verbindingen]** > **[!UICONTROL Doelen]** de optie [!DNL Braze]en selecteer **[!UICONTROL Configureren]**.

![Braze bestemming configureren](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, ziet u een knop **[!UICONTROL Activeren]** op de doelkaart. Voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]**, verwijs naar de sectie van de [Catalogus](../../ui/destinations-workspace.md#catalog) van de documentatie van de bestemmingswerkruimte.
>
>![Braze doel activeren](../../assets/catalog/mobile-engagement/braze/activate.png)

In de stap [!UICONTROL Account] moet u uw [!DNL Braze] accounttoken opgeven. Dit is uw [!DNL Braze] [!DNL API] sleutel. Hier vindt u gedetailleerde instructies voor het verkrijgen van uw [!DNL API] sleutel: [Overzicht](https://www.braze.com/docs/api/api_key/)van REST API-sleutel. Voer het token in en klik op **[!UICONTROL Verbinden met doel]**.

![Stap Braze-doelaccount](../../assets/catalog/mobile-engagement/braze/account.png)

Klik op **[!UICONTROL Next]**. In de stap [!UICONTROL Verificatie] moet u de [!DNL Braze] verbindingsgegevens invoeren:
* **[!UICONTROL Naam]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
* **[!UICONTROL Omschrijving]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Eindpuntinstantie]**: Vraag uw [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken.
* **[!UICONTROL Geval]** voor gebruik bij het in de handel brengen: marketinggevallen geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door de Adobe gedefinieerde gebruiksgevallen voor marketingdoeleinden of u kunt uw eigen gebruiksscenario voor marketingdoeleinden maken. Raadpleeg de pagina [Data Governance in Adobe Experience Platform](../../../rtcdp/privacy/data-governance-overview.md#destinations) voor meer informatie over gevallen van marketinggebruik. Voor informatie over de individuele Adobe-bepaalde het in de handel brengen gebruiksgevallen, zie het overzicht [van het het gebruiksbeleid van](../../../data-governance/policies/overview.md#core-actions)Gegevens.

![Verificatiestap Braze](../../assets/catalog/mobile-engagement/braze/authentication.png)

Klik op **[!UICONTROL Doel]** maken. Uw doel is nu gemaakt. U kunt op **[!UICONTROL Opslaan en afsluiten]** klikken als u de segmenten later wilt activeren. U kunt ook **[!UICONTROL Volgende]** selecteren om door te gaan met de workflow en de gewenste segmenten te selecteren. In beide gevallen raadpleegt u de volgende sectie Segmenten [](#activate-segments)activeren voor de rest van de workflow.

## Segmenten activeren {#activate-segments}

Zie Profielen en segmenten [activeren naar een doel](../../ui/activate-destinations.md#select-attributes) voor informatie over de workflow voor segmentactivering.

## Veldtoewijzing {#field-mapping}

Om uw publieksgegevens van [!DNL Adobe Experience Platform] naar de [!DNL Braze] bestemming correct te verzenden, moet u door de stap van de gebiedstoewijzing gaan.

Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden [!DNL Experience Data Model] (XDM) in uw [!DNL Platform] account en de bijbehorende equivalenten van de doelbestemming.

Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Braze] doelvelden:

Klik in de stap [!UICONTROL Toewijzing] op Nieuwe toewijzing **[!UICONTROL toevoegen]**.

![Braze bestemming Toewijzing toevoegen](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klik in de sectie [!UICONTROL Bronveld] op de pijlknop naast het lege veld.

![Bronttoewijzing op doel onderbreken](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

In het venster [!UICONTROL Bronveld] selecteren kunt u kiezen uit twee categorieën XDM-velden:
* [!UICONTROL Kenmerken]selecteren: gebruik deze optie om een specifiek gebied van uw schema XDM aan een [!DNL Braze] attribuut in kaart te brengen.

![Brontekeningskenmerk Braze-bestemming](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Naamruimte]selecteren: Gebruik deze optie om een naamruimte voor [!DNL Platform] identiteit toe te wijzen aan een [!DNL Braze] naamruimte.

![Bronnaamruimte voor Braze-doeltoewijzing](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Kies het bronveld en klik op **[!UICONTROL Selecteren]**.

Klik in de sectie [!UICONTROL Doelveld] op het koppelingspictogram rechts van het veld.

![Doel-toewijzing op lichtsterkte](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

In het venster Doelveld  selecteren kunt u kiezen uit drie categorieën doelvelden:
* [!UICONTROL Kenmerken]selecteren: Met deze optie kunt u uw XDM-kenmerken toewijzen aan standaardkenmerken [!DNL Braze] .
* [!UICONTROL Naamruimte]selecteren: Gebruik deze optie om naamruimten [!DNL Platform] toe te wijzen aan naamruimten [!DNL Braze] van identiteiten.
* [!UICONTROL Aangepaste kenmerken]selecteren: Met deze optie kunt u XDM-kenmerken toewijzen aan aangepaste [!DNL Braze] kenmerken die u in uw [!DNL Braze] account hebt gedefinieerd.
* U kunt deze optie ook gebruiken om de naam van bestaande XDM-kenmerken te wijzigen in [!DNL Braze]. Bijvoorbeeld, zal het in kaart brengen van een attribuut `lastName` XDM aan een douane `Last_Name` attribuut in [!DNL Braze], tot de `Last_Name` attributen binnen leiden [!DNL Braze], als het niet reeds bestaat, en zal de `lastName` attributen XDM aan het in kaart brengen.

![Doeltoewijzingsvelden van doel dempen](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Kies het doelveld en klik op **[!UICONTROL Selecteren]**.

Nu wordt de veldtoewijzing weergegeven in de lijst.

![Toewijzing bestemming wijzigen voltooid](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Herhaal de vorige stappen om meer toewijzingen toe te voegen.

### Voorbeeld {#mapping-example}

Stel dat uw XDM-profielschema en uw [!DNL Braze] instantie de volgende kenmerken en identiteiten bevatten:

|  | XDM-profielschema | [!DNL Braze] Instantie |
|---|---|---|
| Attributen | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identiteiten | <ul><li>E-mail</code></li><li>Google-advertentie-ID (GAID)</code></li><li>Apple-id voor adverteerders (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

De juiste toewijzing zou er als volgt uitzien:

![Voorbeeld van koppeling naar bestemming overslaan](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Braze] account om te controleren of gegevens naar de [!DNL Braze] bestemming zijn geëxporteerd. [!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar [!DNL Braze] onder het `AdobeExperiencePlatformSegments` kenmerk.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] afdwingt gegevensbeheer, zie [Gegevensbeheer in real time CDP](../../../rtcdp/privacy/data-governance-overview.md).

