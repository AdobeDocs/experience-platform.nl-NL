---
keywords: reclame; criteria;
title: Criteverbinding
description: Criteo biedt vertrouwde en ondoordachte reclame de mogelijkheid om meer ervaring op te doen voor elke consument op het open internet. Met 's werelds grootste set handelsgegevens en de best-in-class AI zorgt Criteo ervoor dat elk touchpoint over de winkelreis gepersonaliseerd is om klanten met de juiste en juiste advertentie op het juiste moment te bereiken.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 1%

---

# (bèta) Criteo-verbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en door Criteo gehandhaafd. Dit is momenteel een bètaproduct en de functionaliteit kan worden gewijzigd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de Commissie [hier](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo biedt vertrouwde en ondoordachte reclame de mogelijkheid om meer ervaring op te doen voor elke consument op het open internet. Met &#39;s werelds grootste set handelsgegevens en de best-in-class AI zorgt Criteo ervoor dat elk touchpoint over de winkelreis gepersonaliseerd is om klanten met de juiste en juiste advertentie op het juiste moment te bereiken.

## Vereisten {#prerequisites}

* U moet een beheerdersgebruikersaccount hebben op [Centrum voor systeembeheer](https://marketing.criteo.com).
* U hebt uw advertentie-id voor de website nodig (vraag uw contactpersoon voor de website als u deze id niet hebt).
* U moet [!DNL GUM caller ID], voor het geval u wilt gebruiken [!DNL GUM ID] als id.

## Beperkingen {#limitations}

* Criteuse accepteert alleen [!DNL SHA-256]-hashed en onbewerkte e-mails (om te zetten in [!DNL SHA-256] vóór verzending). Stuur geen PII (Persoonlijke identificeerbare gegevens, zoals namen van personen of telefoonnummers).
* De criteo heeft minstens één id nodig die door de cliënt moet worden verstrekt. Prioriteiten [!DNL GUM ID] als id over gehashte e-mail aangezien dit bijdraagt aan een betere matching rate.

![Vereisten](../../assets/catalog/advertising/criteo/prerequisites.png)

## Ondersteunde identiteiten {#supported-identities}

Criteo ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
| --- | --- | --- |
| `email_sha256` | E-mailadressen die met het algoritme SHA-256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA-256-gehashte e-mailadressen. Wanneer het bronveld hashkenmerken bevat, controleert u de [!UICONTROL Apply transformation] als u wilt dat Platform de gegevens bij activering automatisch verbergt. |
| `gum_id` | Criteo [!DNL GUM] cookie-id | [!DNL GUM IDs] cliënten toestaan een correspondentie aan te houden tussen hun systeem voor gebruikersidentificatie en de gebruikersidentificatie van de Commissie ([!DNL UID]). Als het id-type `gum_id`, een aanvullende parameter, [!DNL GUM Caller ID], moet ook worden opgenomen. Neem contact op met het accountteam van uw website voor de juiste [!DNL GUM Caller ID] of om meer informatie hierover te krijgen [!DNL GUM ID] synchroniseren, indien nodig. |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| --- | --- | --- |
| Exporttype | Publiek exporteren | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster [!DNL Criteo] bestemming. |
| Exportfrequentie | Streaming | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](../../destination-types.md#streaming-destinations). |

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe te gebruiken [!DNL Criteo] doel, hier zijn sommige doelstellingen die de klanten van Adobe Experience Platform kunnen bereiken met [!DNL Criteo]:

### Gebruik geval 1: Krijg verkeer

Laat uw bedrijf zien met relevante productaanbiedingen en flexibele creatieve producten. Met intelligente productaanbevelingen zullen uw advertenties automatisch de producten bevatten die het meest waarschijnlijk bezoeken en betrokkenheid zullen veroorzaken. Flexibele het richten staat u toe om publiek van de handelgegevens van Criteo of van uw eigen perspectieflijsten en Adobe CDP segmenten te bouwen.

### Hoofdlettergebruik 2: website-conversies verhogen

Wanneer bezoekers uw website verlaten, herinner hen wat zij met het herrichten van advertenties missen die omzettingen door speciale overeenkomsten en hyper-relevante aanbiedingen te tonen verhogen, waar zij ook gaan. Verbind uw Adobe CDP publiek om bestaande klanten opnieuw in dienst te nemen of consumenten te richten gelijkend op uw meest loyale kopers.

## Verbinding maken met website {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

### Verifiëren voor commissie

De stappen om te verbinden zijn als volgt:

1. Meld u aan bij Adobe Experience Platform en maak verbinding met het doel Computer.

   ![Aanmelden](../../assets/catalog/advertising/criteo/connect-destination.png)

1. U wordt omgeleid naar de website om de verbinding te autoriseren. Mogelijk moet u zich eerst aanmelden met uw verificatiegegevens:

   ![Aanmelden bij website](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![Aanmelden bij website](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![Aanmelden bij website](../../assets/catalog/advertising/criteo/log-in-3.png)


### Verbindingsparameters {#connection-parameters}

Vul de volgende verbindingsparameters in nadat u de bestemming hebt geverifieerd.

![Verbindingsparameters](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Veld | Beschrijving | Vereist |
| --- | --- | --- |
| Naam | Een naam waarmee u deze bestemming in de toekomst kunt herkennen. De naam die u hier kiest, is [!DNL Audience] naam in het Centrum van het Beheer van de Nota en kan niet in later stadium worden gewijzigd. | Ja |
| Beschrijving | Een beschrijving waarmee u deze bestemming in de toekomst kunt identificeren. | Nee |
| Adverteerder-id | Identiteitskaart van Adverteerder van de website van uw organisatie. Neem contact op met uw accountmanager van de website voor deze informatie. | Ja |
| Criteo [!DNL GUM caller ID] | [!DNL GUM Caller ID] van uw organisatie. Neem contact op met het accountteam van uw website voor de juiste [!DNL GUM Caller ID] of om meer informatie hierover te krijgen [!DNL GUM] synchroniseren, indien nodig. | Ja, telkens [!DNL GUM ID] wordt opgegeven als een id |

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate-segments}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](../../ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Geëxporteerde gegevens {#exported-data}

U kunt het geëxporteerde publiek bekijken in het dialoogvenster [Centrum voor systeembeheer](https://marketing.criteo.com/audience-manager/dashboard).

De aanvraaginstantie voor het toevoegen van een gebruikersprofiel dat door de [!DNL Criteo] De verbinding ziet er ongeveer als volgt uit:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

De aanvraaginstantie voor het verwijderen van gebruikersprofielen die door de [!DNL Criteo] De verbinding ziet er ongeveer als volgt uit:

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## Gegevensgebruik en -beheer {#data-usage}

Alle Adobe Experience Platform-doelen zijn bij het verwerken van uw gegevens compatibel met het beleid voor gegevensgebruik. Lees voor meer informatie over hoe Adobe Experience Platform gegevensbeheer afdwingt de [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## Aanvullende bronnen

* [Criteo Help Center](https://help.criteo.com/kb/en)
* [Criteo Developer Portal](https://developers.criteo.com)
