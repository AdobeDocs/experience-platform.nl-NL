---
keywords: streaming, Qualtrict-doel
title: Kwalitatieve automatisering
description: Synchroniseer ervaring en operationele klantgegevens om personalisatie op schaal te ontgrendelen. Gebruik de samenvoeging van meerdere bronnen van operationele gegevens in Adobe Experience Platform als input in de iD van de Ervaring van Qualtrics om uw klanten beter te begrijpen en gerichte outreach toe te laten om de hiaat te sluiten wanneer het aankomt op inzicht in bedoeling, emotie en ervaringsbestuurders.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Kwalitatieve automatisering

## Overzicht {#overview}

Synchroniseer ervaring en operationele klantgegevens om personalisatie op schaal te ontgrendelen.

Gebruik de samenvoeging van meerdere bronnen van operationele gegevens in Adobe Experience Platform als input in de iD van de Ervaring van Qualtrics om uw klanten beter te begrijpen en gerichte outreach toe te laten om de hiaat te sluiten wanneer het aankomt op inzicht in bedoeling, emotie en ervaringsbestuurders.

>[!IMPORTANT]
>
>De bestemmingsschakelaar en documentatiepagina worden gecreeerd en door het team van Qualtrics gehandhaafd. Voor vragen of updateverzoeken kunt u rechtstreeks contact opnemen met de aanvrager door u aan te melden bij de [Klantsucceshub](https://support-portal.qualtrics.com/).

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het *Kwalitatieve automatisering* doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1 {#use-case-1}

**Scenario**: Een bedrijf wil klanttevredenheid meten voor verschillende digitale aanraakpunten, zoals de website en mobiele app. Ze gebruiken Adobe Experience Platform om Qualtrics-enquêtes te activeren op basis van gebruikersinteracties, zoals het voltooien van een aankoop of het bezoeken van een specifieke webpagina.

**Resultaat**: Door real-time feedback te verzamelen, kan het bedrijf gegevensgestuurde verbeteringen aanbrengen in de klantervaring. Dit leidt tot meer tevredenheid en loyaliteit.

### Hoofdletters gebruiken #2 {#use-case-2}

**Scenario**: Een organisatie streeft ernaar het instapproces van haar werknemers te verbeteren. Ze gebruiken Adobe Experience Platform om feedback te verzamelen van nieuwe huren via Qualtrics-enquêtes. Enquêtes worden automatisch geactiveerd na een vooraf gedefinieerde instapperiode.

**Resultaat**: Dankzij continue feedback kan de organisatie het instapproces aanpassen en verbeteren, wat resulteert in een betere betrokkenheid en productiviteit bij nieuwe werknemers.

## Vereisten

Voordat u de bestemming Qualtrics in Adobe Experience Platform instelt, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een Qualtrics-account.
* U hebt het vereiste API-token verkregen van Qualtrics.

### Een API-token verkrijgen

Hieronder vindt u de noodzakelijke stappen voor het verkrijgen van een API-token van Qualtrics.

1. Meld u aan bij uw Qualtrics-account.
2. Ga naar **Accountinstellingen**.
3. Selecteren **Qualtrics-id&#39;s**.
4. Op deze pagina zoekt u naar de **API** bevat een **Token** veld. Dit is de API Token, en zal tijdens bestemmingsopstelling worden vereist.

## Ondersteunde identiteiten {#supported-identities}

*Kwalitatieve automatisering* ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email | E-mailadressen met normale tekst | Alleen e-mailadressen met onbewerkte tekst worden door Qualtrics ondersteund. |
| external_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster *Kwalitatieve automatisering* bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als deel van authentificatie zult u moeten verstrekken **Gebruikersnaam** en **Wachtwoord**. De gebruikersnaam is uw Qualtrics-gebruikersnaam en het wachtwoord is de API-token van uw Qualtrics-account. Volg de instructies van het dialoogvenster om het API-token op te halen **Vereisten** hierboven.

![Verificatie](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL URL]**: De URL gevonden in het dialoogvenster [JSON-gebeurtenis](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) dat uw [workflow in Qualtrics](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About). Zie onderstaande schermafbeelding voor een voorbeeld.

![URL](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Deze bestemming heeft een open schema zodat kunt u om het even welke eigenschappen naar Qualtrics verzenden.

#### Kenmerken Kaart

Als u een kenmerk aan uw toewijzing wilt toevoegen, selecteert u **aangepaste kenmerken** wanneer u een nieuwe toewijzing toevoegt. U kunt elke naam voor het kenmerk invoeren. Qualtrics moedigt de *camelCase* naamgevingsconventie voor kenmerknamen (zie onder schermafbeelding voor een voorbeeld).

![Aangepast, kenmerk](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Zie hieronder screenshot voor een voorbeeld van mogelijke kenmerktoewijzingen.

![Voorbeeldtoewijzingen](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Identiteiten toewijzen

Het is verplicht om een naamruimte voor identiteit te selecteren voor deze bestemming. De twee mogelijke brongebieden aan doelgebiedafbeeldingen zijn:

| Bronveld | Doelveld |
|--------------------|-----------------------|
| IdentityMap: E-mail | Identiteit: e-mail |
| IdentityMap: ECID | Identiteit: external_id |

Zie onderstaande schermafbeelding voor een voorbeeld.

![Naamruimte identiteit](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

Zoals eerder vermeld, gebruikt deze bestemming een open schema, zodat kunnen om het even welke eigenschappen naar Qualtrics worden verzonden. Niettemin zullen de gegevens die aan Qualtrics worden verzonden de volgende structuur volgen:

```json
{
  "person": {
    "name": {
      "firstName": "Dave"
    }
  },
  "mobilePhone": {
    "number": "0123456789"
  },
  "identityMap": {
    "Email": [
      {
        "id": "Email-2Sf6C"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "046456e3b-18e1-48a6-9bda-d68547861283": {
        "lastQualificationTime": "2023-09-05T10:43:55.602687Z",
        "status": "realized"
      },
      "007844dd1-9e5d-4531-a4ee-05470doe759dd": {
        "lastQualificationTime": "2023-09-05T10:43:55.602689Z",
        "status": "realized"
      }
    }
  }
}
```

Als u wilt controleren of gegevens in Qualtrics zijn opgenomen, gaat u naar de workflow met uw **JSON-gebeurtenis**, van daaruit, ga naar **Geschiedenis uitvoeren** waar u de uitvoeringen van uw werkschema zou moeten zien. Elke werkstroom heeft een van de **Geslaagd** of **Mislukt**. Als u een bepaalde uitvoering selecteert, wordt er meer informatie over weergegeven, zodat u problemen kunt oplossen als u problemen hebt.

Als er geen uitvoeringen zichtbaar zijn in **Geschiedenis uitvoeren**, betekent het dat de workflow nog niet is geactiveerd om aan te geven dat er een probleem kan zijn. Zorg ervoor dat de workflow is ingeschakeld en dat de **URL** op de bestemming in Adobe Experience Platform juist is. De uitvoeringen van het werkschema zijn niet onmiddellijk, zodat kunt u een korte tijd moeten wachten alvorens het voltooit.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).
