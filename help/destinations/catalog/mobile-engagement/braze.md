---
keywords: mobiel; schil; berichten;
title: Braze verbinding
description: Braze is een uitgebreid platform voor klantbetrokkenheid dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 0%

---


# (Bèta) [!DNL Braze] verbinding

>[!IMPORTANT]
>
>Het doel Braze in Adobe Experience Platform is momenteel in Bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

Met de bestemming [!DNL Braze] kunt u profielgegevens naar [!DNL Braze] verzenden.

[!DNL Braze] is een uitgebreid platform voor klantenservice dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die zij leuk vinden, mogelijk maakt.

Als u profielgegevens naar [!DNL Braze] wilt verzenden, moet u eerst verbinding maken met het doel.

## Doelspecificaties {#destination-specs}

Let op de volgende details die specifiek zijn voor het doel [!DNL Braze]:

* [!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar  [!DNL Braze] onder het  `AdobeExperiencePlatformSegments` kenmerk.

>[!NOTE]
>
>Onthoud dat het verzenden van extra aangepaste kenmerken naar [!DNL Braze] kan leiden tot een toename van het verbruik van [!DNL Braze] gegevenspunten. Neem contact op met uw [!DNL Braze]-accountmanager voordat u aanvullende aangepaste kenmerken verzendt.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik gebruikers in een mobiele betrokkenheidsbestemming richten, met segmenten die in [!DNL Adobe Experience Platform] worden gebouwd. Daarnaast wil ik persoonlijke ervaringen aan hen aanbieden op basis van kenmerken uit hun [!DNL Adobe Experience Platform]-profielen, zodra segmenten en profielen worden bijgewerkt in [!DNL Adobe Experience Platform].

## Ondersteunde identiteiten {#supported-identities}

[!DNL Google Ad Manager] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| external_id | Aangepaste [!DNL Braze]-id die het toewijzen van elke identiteit ondersteunt. | U kunt elke [identity](../../../identity-service/namespaces.md) naar de [!DNL Braze] bestemming verzenden, zolang u het aan [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation) in kaart brengt. |

## Type exporteren {#export-type}

**[!DNL Profile-based]** - u exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam) en/of identiteiten, afhankelijk van uw veldtoewijzing.
[!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar  [!DNL Braze] onder het  `AdobeExperiencePlatformSegments` kenmerk.

## Verbinden met doel {#connect-destination}

Selecteer [!DNL Braze] in **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer **[!UICONTROL Configure]**.

![Braze bestemming configureren](../../assets/catalog/mobile-engagement/braze/configure.png)

>[!NOTE]
>
>Als er al een verbinding met dit doel bestaat, kunt u een **[!UICONTROL Activate]** knop op de doelkaart zien. Raadpleeg voor meer informatie over het verschil tussen **[!UICONTROL Activate]** en **[!UICONTROL Configure]** de sectie [Catalog](../../ui/destinations-workspace.md#catalog) van de documentatie van de doelwerkruimte.
>
>![Braze doel activeren](../../assets/catalog/mobile-engagement/braze/activate.png)

In de stap [!UICONTROL Account] moet u uw [!DNL Braze] accounttoken opgeven. Dit is uw [!DNL Braze] [!DNL API] sleutel. Hier vindt u gedetailleerde instructies voor het verkrijgen van uw [!DNL API]-toets: [REST API Key Overview](https://www.braze.com/docs/api/api_key/). Voer het token in en klik op **[!UICONTROL Connect to destination]**.

![Stap Braze-doelaccount](../../assets/catalog/mobile-engagement/braze/account.png)

Klik op **[!UICONTROL Next]**. In de stap [!UICONTROL Authentication] moet u de verbindingsgegevens [!DNL Braze] invoeren:
* **[!UICONTROL Name]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Endpoint Instance]**: Vraag uw  [!DNL Braze] vertegenwoordiger welke eindpuntinstantie u zou moeten gebruiken.
* **[!UICONTROL Marketing action]**: marketingacties geven de intentie aan waarvoor gegevens naar de bestemming worden geëxporteerd. U kunt kiezen uit door Adobe gedefinieerde marketingacties of u kunt uw eigen marketingactie maken. Zie de pagina [Gegevensbeheer in Adobe Experience Platform](../../../data-governance/policies/overview.md) voor meer informatie over marketingacties. Zie [Overzicht van beleidsregels voor gegevensgebruik](../../../data-governance/policies/overview.md) voor informatie over de afzonderlijke door Adobe gedefinieerde marketingacties.

![Verificatiestap Braze](../../assets/catalog/mobile-engagement/braze/authentication.png)

Klik op **[!UICONTROL Create destination]**. Uw doel is nu gemaakt. U kunt **[!UICONTROL Save & Exit]** klikken als u segmenten later wilt activeren, of u kunt **[!UICONTROL Next]** selecteren om de werkstroom voort te zetten en segmenten te selecteren om te activeren. In beide gevallen raadpleegt u de volgende sectie [Segmenten activeren](#activate-segments) voor de rest van de workflow.

## Segmenten {#activate-segments} activeren

Zie [Profielen en segmenten activeren naar een doel](../../ui/activate-destinations.md#select-attributes) voor informatie over de workflow voor segmentactivering.

## Veld toewijzen {#field-mapping}

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

