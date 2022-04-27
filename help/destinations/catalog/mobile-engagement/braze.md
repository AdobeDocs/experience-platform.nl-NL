---
keywords: mobiel; schil; berichten;
title: Braze verbinding
description: Braze is een uitgebreid platform voor klantbetrokkenheid dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die ze leuk vinden, mogelijk maakt.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 1%

---

# [!DNL Braze] verbinding

## Overzicht {#overview}

De [!DNL Braze] doel helpt u profielgegevens te verzenden naar [!DNL Braze].

[!DNL Braze] is een uitgebreid platform voor klantenservice dat relevante en gedenkwaardige ervaringen tussen klanten en de merken die zij leuk vinden, mogelijk maakt.

Profielgegevens verzenden naar [!DNL Braze], moet u eerst verbinding maken met het doel.

## Doelspecificaties {#specifics}

Let op de volgende details die specifiek zijn voor de [!DNL Braze] bestemming:

* [!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar [!DNL Braze] onder de `AdobeExperiencePlatformSegments` kenmerk.

>[!NOTE]
>
>Houd er rekening mee dat extra aangepaste kenmerken worden verzonden naar [!DNL Braze] kan een toename van uw [!DNL Braze] verbruik van gegevenspunten. Neem contact op met uw [!DNL Braze] accountmanager voordat aanvullende aangepaste kenmerken worden verzonden.

## Gebruiksscenario’s {#use-cases}

Als markator, wil ik gebruikers in een mobiele betrokkenheidsbestemming richten, met ingebouwde segmenten [!DNL Adobe Experience Platform]. Daarnaast wil ik hen persoonlijke ervaringen bieden op basis van hun kenmerken [!DNL Adobe Experience Platform] profielen, zodra segmenten en profielen in [!DNL Adobe Experience Platform].

## Ondersteunde identiteiten {#supported-identities}

[!DNL Braze] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven.

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| external_id | Aangepast [!DNL Braze] id die het toewijzen van om het even welke identiteit steunt. | U kunt elke [identiteit](../../../identity-service/namespaces.md) aan de [!DNL Braze] doel, zolang u deze toewijst aan de [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam) en/of identiteiten, afhankelijk van uw veldtoewijzing.[!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar [!DNL Braze] onder de `AdobeExperiencePlatformSegments` kenmerk. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **[!UICONTROL Braze account token]**: Dit is uw [!DNL Braze] [!DNL API] toets. U kunt gedetailleerde instructies vinden over hoe u uw [!DNL API] sleutel hier: [Overzicht van REST API-sleutel](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL Name]**: Voer een naam in waarmee u deze bestemming in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Voer een beschrijving in die u helpt deze bestemming in de toekomst te identificeren.
* **[!UICONTROL Endpoint Instance]**: vragen [!DNL Braze] representatief welke eindpuntinstantie u zou moeten gebruiken.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Zie [De publieksgegevens van de activering aan het stromen segment de uitvoerbestemmingen](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Toewijzingsoverwegingen {#mapping-considerations}

Om uw publieksgegevens correct te verzenden van [!DNL Adobe Experience Platform] aan de [!DNL Braze] doel, moet u door de stap van de gebiedstoewijzing gaan.

Toewijzing bestaat uit het maken van een koppeling tussen uw [!DNL Experience Data Model] (XDM) schemavelden in uw [!DNL Platform] en de overeenkomstige equivalenten van de doelbestemming.

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL Braze] doelvelden, voer de volgende stappen uit:

In de [!UICONTROL Mapping] stap, klik op **[!UICONTROL Add new mapping]**.

![Braze bestemming Toewijzing toevoegen](../../assets/catalog/mobile-engagement/braze/mapping.png)

In de [!UICONTROL Source Field] klikt u op de pijlknop naast het lege veld.

![Bronttoewijzing op doel onderbreken](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

In de [!UICONTROL Select source field] kunt u kiezen uit twee categorieën XDM-velden:
* [!UICONTROL Select attributes]: gebruik deze optie om een specifiek veld van uw XDM-schema toe te wijzen aan een [!DNL Braze] kenmerk.

![Brontekeningskenmerk Braze-bestemming](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Select identity namespace]: Gebruik deze optie om een [!DNL Platform] naamruimte identiteit [!DNL Braze] naamruimte.

![Bronnaamruimte voor Braze-doeltoewijzing](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Kies uw bronveld en klik op **[!UICONTROL Select]**.

In de [!UICONTROL Target Field] klikt u op het koppelingspictogram rechts van het veld.

![Doel-toewijzing op lichtsterkte](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

In de [!UICONTROL Select target field] kunt u kiezen uit twee categorieën doelvelden:
* [!UICONTROL Select identity namespace]: Deze optie gebruiken om toe te wijzen [!DNL Platform] naamruimten naar [!DNL Braze] naamruimten.
* [!UICONTROL Select custom attributes]: Met deze optie kunt u XDM-kenmerken toewijzen aan aangepaste kenmerken [!DNL Braze] kenmerken die u in uw [!DNL Braze] account. <br> U kunt deze optie ook gebruiken om bestaande XDM-kenmerken te hernoemen in [!DNL Braze]. Bijvoorbeeld het toewijzen van een `lastName` XDM-kenmerk aan een aangepast element `Last_Name` kenmerk in [!DNL Braze], worden de `Last_Name` kenmerk in [!DNL Braze], als het nog niet bestaat, en kaart de `lastName` XDM-kenmerk eraan gekoppeld.

![Doeltoewijzingsvelden van doel dempen](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Kies uw doelveld en klik op **[!UICONTROL Select]**.

Nu wordt de veldtoewijzing weergegeven in de lijst.

![Toewijzing bestemming wijzigen voltooid](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Herhaal de vorige stappen om meer toewijzingen toe te voegen.

## Voorbeeld van toewijzing {#mapping-example}

Laat ons uw XDM profielschema en uw [!DNL Braze] -instantie bevat de volgende kenmerken en identiteiten:

|  | XDM-profielschema | [!DNL Braze] Instantie |
|---|---|---|
| Attributen | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| Identiteiten | <ul><li>E-mail</code></li><li>Google-advertentie-ID (GAID)</code></li><li>Apple-id voor adverteerders (IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

De juiste toewijzing zou er als volgt uitzien:

![Voorbeeld van koppeling naar bestemming overslaan](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Geëxporteerde gegevens {#exported-data}

Controleren of gegevens zijn geëxporteerd naar de [!DNL Braze] doel, controleer uw [!DNL Braze] account. [!DNL Adobe Experience Platform] segmenten worden geëxporteerd naar [!DNL Braze] onder de `AdobeExperiencePlatformSegments` kenmerk.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](../../../data-governance/home.md).
