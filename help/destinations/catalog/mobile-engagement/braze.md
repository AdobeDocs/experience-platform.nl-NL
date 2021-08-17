---
keywords: mobiel; schil; berichten;
title: Braze verbinding
description: Braze is een uitgebreid platform voor klantbetrokkenheid dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# (Bèta) [!DNL Braze] verbinding

>[!IMPORTANT]
>
>Het doel Braze in Adobe Experience Platform is momenteel in Bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

Met de bestemming [!DNL Braze] kunt u profielgegevens naar [!DNL Braze] verzenden.

[!DNL Braze] is een uitgebreid platform voor klantenservice dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die zij leuk vinden, mogelijk maakt.

Als u profielgegevens naar [!DNL Braze] wilt verzenden, moet u eerst verbinding maken met het doel.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor het doel [!DNL Braze]:

* [!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar  [!DNL Braze] onder het  `AdobeExperiencePlatformSegments` kenmerk.

>[!NOTE]
>
>Onthoud dat het verzenden van extra aangepaste kenmerken naar [!DNL Braze] kan leiden tot een toename van het verbruik van [!DNL Braze] gegevenspunten. Neem contact op met uw [!DNL Braze]-accountmanager voordat u aanvullende aangepaste kenmerken verzendt.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik gebruikers in een mobiele betrokkenheidsbestemming richten, met segmenten die in [!DNL Adobe Experience Platform] worden gebouwd. Daarnaast wil ik persoonlijke ervaringen aan hen aanbieden op basis van kenmerken uit hun [!DNL Adobe Experience Platform]-profielen, zodra segmenten en profielen worden bijgewerkt in [!DNL Adobe Experience Platform].

## Ondersteunde identiteiten {#supported-identities}

[!DNL Braze] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| external_id | Aangepaste [!DNL Braze]-id die het toewijzen van elke identiteit ondersteunt. | U kunt elke [identity](../../../identity-service/namespaces.md) naar de [!DNL Braze] bestemming verzenden, zolang u het aan [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation) in kaart brengt. |

## Exporttype {#export-type}

**[!DNL Profile-based]** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam) en/of identiteiten, afhankelijk van uw veldtoewijzing.
[!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar  [!DNL Braze] onder het  `AdobeExperiencePlatformSegments` kenmerk.

## Verbinden met de bestemming {#connect}

Om met deze bestemming te verbinden, volg de stappen in [het leerprogramma van de bestemmingsconfiguratie](../../ui/connect-destination.md) worden beschreven.

### Verbindingsparameters {#parameters}

Terwijl [vestiging](../../ui/connect-destination.md) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Braze account token]**: Dit is uw  [!DNL Braze] [!DNL API] sleutel. Hier vindt u gedetailleerde instructies voor het verkrijgen van uw [!DNL API]-toets: [REST API Key Overview](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Name]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Endpoint Instance]**: Vraag uw  [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken.

## Segmenten naar dit doel activeren {#activate}

Zie [De publieksgegevens van Activate aan het stromen segment de uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies op het activeren van publiekssegmenten aan deze bestemming.

## Toewijzingsoverwegingen {#mapping-considerations}

Om uw publieksgegevens van [!DNL Adobe Experience Platform] aan [!DNL Braze] bestemming correct te verzenden, moet u door de stap van de gebiedstoewijzing gaan.

Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden [!DNL Experience Data Model] (XDM) in uw [!DNL Platform]-account en de bijbehorende equivalenten van de doelbestemming.

Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Braze]-doelvelden:

Klik in de stap [!UICONTROL Mapping] op **[!UICONTROL Add new mapping]**.

![Braze bestemming Toewijzing toevoegen](../../assets/catalog/mobile-engagement/braze/mapping.png)

Klik in de sectie [!UICONTROL Source Field] op de pijlknop naast het lege veld.

![Bronttoewijzing op doel onderbreken](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

In het venster [!UICONTROL Select source field] kunt u kiezen uit twee categorieën XDM-velden:
* [!UICONTROL Select attributes]: gebruik deze optie om een specifiek gebied van uw schema XDM aan een  [!DNL Braze] attribuut in kaart te brengen.

![Brontekeningskenmerk Braze-bestemming](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Gebruik deze optie om een naamruimte voor  [!DNL Platform] identiteit toe te wijzen aan een  [!DNL Braze] naamruimte.

![Bronnaamruimte voor Braze-doeltoewijzing](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Kies het bronveld en klik op **[!UICONTROL Select]**.

Klik in de sectie [!UICONTROL Target Field] op het koppelingspictogram rechts van het veld.

![Doel-toewijzing op lichtsterkte](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

In het venster [!UICONTROL Select target field] kunt u kiezen uit drie categorieën doelvelden:
* [!UICONTROL Select attributes]: Gebruik deze optie om uw XDM-kenmerken toe te wijzen aan standaard [!DNL Braze] kenmerken.
* [!UICONTROL Select identity namespace]: Gebruik deze optie om  [!DNL Platform] naamruimten toe te wijzen aan  [!DNL Braze] naamruimten.
* [!UICONTROL Select custom attributes]: Met deze optie kunt u XDM-kenmerken toewijzen aan aangepaste  [!DNL Braze] kenmerken die u in uw  [!DNL Braze] account hebt gedefinieerd.
* U kunt deze optie ook gebruiken om de naam van bestaande XDM-kenmerken te wijzigen in [!DNL Braze]. Als bijvoorbeeld een `lastName` XDM-kenmerk wordt toegewezen aan een aangepast `Last_Name`-kenmerk in [!DNL Braze], wordt het `Last_Name`-kenmerk in [!DNL Braze] gemaakt als dit nog niet bestaat en wordt het XDM-kenmerk `lastName` eraan toegewezen.

![Doeltoewijzingsvelden van doel dempen](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Kies het doelveld en klik op **[!UICONTROL Select]**.

Nu wordt de veldtoewijzing weergegeven in de lijst.

![Toewijzing bestemming wijzigen voltooid](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Herhaal de vorige stappen om meer toewijzingen toe te voegen.

## Voorbeeld van toewijzing {#mapping-example}

Stel dat uw XDM-profielschema en uw [!DNL Braze]-instantie de volgende kenmerken en identiteiten bevatten:

|  | XDM-profielschema | [!DNL Braze] Instantie |
|---|---|---|
| Attributen | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identiteiten | <ul><li>E-mail</code></li><li>Google-advertentie-id (GAID)</code></li><li>Apple-id voor adverteerders (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

De juiste toewijzing zou er als volgt uitzien:

![Voorbeeld van koppeling naar bestemming overslaan](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Geëxporteerde gegevens {#exported-data}

Controleer uw [!DNL Braze]-account om te controleren of gegevens naar de [!DNL Braze]-bestemming zijn geëxporteerd. [!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar  [!DNL Braze] onder het  `AdobeExperiencePlatformSegments` kenmerk.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Zie [Overzicht gegevensbeheer](../../../data-governance/home.md) voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt.
