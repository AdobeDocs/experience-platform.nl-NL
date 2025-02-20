---
keywords: reclame; criteria;
title: Criteverbinding
description: Criteo biedt vertrouwde en ondoordachte reclame de mogelijkheid om meer ervaring op te doen voor elke consument op het open internet. Met 's werelds grootste set handelsgegevens en de best-in-class AI zorgt Criteo ervoor dat elk touchpoint over de winkelreis gepersonaliseerd is om klanten met de juiste en juiste advertentie op het juiste moment te bereiken.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: e594e473ac78663203c9254623fe8e324985fa39
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 1%

---

# Criteverbinding

## Overzicht {#overview}

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en door Criteo gehandhaafd. Voor om het even welke onderzoeken of updateverzoeken, gelieve direct contactCiteo [ ](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo biedt vertrouwde en ondoordachte reclame de mogelijkheid om meer ervaring op te doen voor elke consument op het open internet. Met &#39;s werelds grootste set handelsgegevens en de best-in-class AI zorgt Criteo ervoor dat elk touchpoint over de winkelreis gepersonaliseerd is om klanten met de juiste en juiste advertentie op het juiste moment te bereiken.

## Vereisten {#prerequisites}

* U moet een beheerdergebruikersrekening op [ Centrum van het Beheer van de Nota ](https://marketing.criteo.com) hebben.
* U hebt uw advertentie-id voor de website nodig (vraag uw contactpersoon voor de website als u deze id niet hebt).
* U moet [!DNL GUM caller ID] opgeven voor het geval u [!DNL GUM ID] als id wilt gebruiken.

## Beperkingen {#limitations}

* Crite accepteert alleen e-mails met [!DNL SHA-256] hashes en normale tekst (om te worden omgezet in [!DNL SHA-256] voordat ze worden verzonden). Stuur geen PII (Persoonlijke identificeerbare gegevens, zoals namen van personen of telefoonnummers).
* De criteo heeft minstens één id nodig die door de cliënt moet worden verstrekt. [!DNL GUM ID] krijgt de prioriteit als id boven gehashte e-mail, omdat dit bijdraagt aan een betere corresponderende snelheid.

![Vereisten](../../assets/catalog/advertising/criteo/prerequisites.png)

## Ondersteunde identiteiten {#supported-identities}

Criteo ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Doelidentiteit | Beschrijving | Overwegingen |
| --- | --- | --- |
| `email_sha256` | E-mailadressen die met het algoritme SHA-256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA-256-gehashte e-mailadressen. Wanneer het bronveld niet-gehashte kenmerken bevat, schakelt u de optie [!UICONTROL Apply transformation] in om ervoor te zorgen dat Platform de gegevens bij activering automatisch verbergt. |
| `gum_id` | Criteo [!DNL GUM] cookie-id | [!DNL GUM IDs] staat cliënten toe om een correspondentie tussen hun systeem van de gebruikersidentificatie en de gebruikersidentificatie van het Comité te handhaven ([!DNL UID]). Als het id-type `gum_id` is, moet ook een extra parameter, de [!DNL GUM Caller ID] , worden opgenomen. Neem indien nodig contact op met het accountteam van uw website voor de juiste [!DNL GUM Caller ID] of voor meer informatie over deze [!DNL GUM ID] -synchronisatie. |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
| --- | --- | --- |
| Exporttype | Publiek exporteren | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die in de [!DNL Criteo] -bestemming worden gebruikt. |
| Exportfrequentie | Streaming | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](../../destination-types.md#streaming-destinations). |

## Gebruiksscenario’s {#use-cases}

Voor een beter inzicht in het gebruik van de [!DNL Criteo] -bestemming zijn er enkele doelstellingen die Adobe Experience Platform-klanten kunnen bereiken met [!DNL Criteo] :

### Gebruik geval 1: Krijg verkeer

Laat uw bedrijf zien met relevante productaanbiedingen en flexibele creatieve producten. Met intelligente productaanbevelingen zullen uw advertenties automatisch de producten bevatten die het meest waarschijnlijk bezoeken en betrokkenheid zullen veroorzaken. Dankzij de flexibele manier van toewijzen kunt u een publiek maken op basis van de gegevensset Handelsgegevens van Criteo of op basis van uw eigen perspectieflijsten en Adobe CDP-segmenten.

### Hoofdlettergebruik 2: website-conversies verhogen

Wanneer bezoekers uw website verlaten, herinner hen wat zij met het herrichten van advertenties missen die omzettingen door speciale overeenkomsten en hyper-relevante aanbiedingen te tonen verhogen, waar zij ook gaan. Sluit uw Adobe CDP-publiek aan om bestaande klanten opnieuw aan te trekken of richt zich op klanten die vergelijkbaar zijn met uw meest loyale klanten.

## Verbinding maken met website {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven.

### Verifiëren voor commissie

De stappen om te verbinden zijn als volgt:

1. Meld u aan bij Adobe Experience Platform en maak verbinding met het doel Computer.

   ![ Login ](../../assets/catalog/advertising/criteo/connect-destination.png)

1. U wordt omgeleid naar de website om de verbinding te autoriseren. Mogelijk moet u zich eerst aanmelden met uw verificatiegegevens:

   ![ login van de citaat ](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![ login van de citaat ](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![ login van de citaat ](../../assets/catalog/advertising/criteo/log-in-3.png)


### Verbindingsparameters {#connection-parameters}

Vul de volgende verbindingsparameters in nadat u de bestemming hebt geverifieerd.

![ de parameters van de Verbinding ](../../assets/catalog/advertising/criteo/connection-parameters.png)

| Veld | Beschrijving | Vereist |
| --- | --- | --- |
| Naam | Een naam waarmee u deze bestemming in de toekomst kunt herkennen. De naam die u hier kiest, wordt de [!DNL Audience] -naam in het Centro Management Center en kan in een later stadium niet worden gewijzigd. | Ja |
| Beschrijving | Een beschrijving waarmee u deze bestemming in de toekomst kunt identificeren. | Nee |
| Adverteerder-id | Identiteitskaart van Adverteerder van de website van uw organisatie. Neem contact op met uw accountmanager van de website voor deze informatie. | Ja |
| Criteo [!DNL GUM caller ID] | [!DNL GUM Caller ID] van uw organisatie. Neem indien nodig contact op met het accountteam van uw website voor de juiste [!DNL GUM Caller ID] of voor meer informatie over deze [!DNL GUM] -synchronisatie. | Ja, telkens wanneer [!DNL GUM ID] wordt opgegeven als id |

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate-segments}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](../../ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

U kunt het uitgevoerde publiek in het [ centrum van het Beheer van de Nota zien ](https://marketing.criteo.com/audience-manager/dashboard).

De aanvraagtekst voor het toevoegen van een gebruikersprofiel dat door de [!DNL Criteo] -verbinding wordt ontvangen, ziet er ongeveer als volgt uit:

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

De aanvraagtekst voor het verwijderen van gebruikersprofielen die door de [!DNL Criteo] -verbinding worden ontvangen, ziet er ongeveer als volgt uit:

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

Alle Adobe Experience Platform-doelen zijn bij het verwerken van uw gegevens compatibel met het beleid voor gegevensgebruik. Voor gedetailleerde informatie over hoe Adobe Experience Platform gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Aanvullende bronnen

* [ het Centrum van de Hulp van de Nota ](https://help.criteo.com/kb/en)
* [ Portaal van de Ontwikkelaar van de Nota van de Nota van de Nota ](https://developers.criteo.com)
