---
keywords: streaming, Qualtrict-doel
title: Kwalitatieve automatisering
description: Synchroniseer ervaring en operationele klantgegevens om personalisatie op schaal te ontgrendelen. Gebruik de samenvoeging van meerdere bronnen van operationele gegevens in Adobe Experience Platform als input in de iD van de Ervaring van Qualtrics om uw klanten beter te begrijpen en gerichte outreach toe te laten om de hiaat te sluiten wanneer het aankomt op inzicht in bedoeling, emotie en ervaringsbestuurders.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 3289ed4c-8542-4e22-a574-e49cc6527a24
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
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
>De bestemmingsschakelaar en documentatiepagina worden gecreeerd en door het team van Qualtrics gehandhaafd. Voor om het even welke onderzoeken of updateverzoeken, gelieve hen direct te contacteren door in de [ Hub van het Succes van de Klant ](https://support-portal.qualtrics.com/) te registreren.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de *bestemming van de Automatiseringen van 0} Qualtrics {zou moeten gebruiken, zijn hier de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.*

### Hoofdletters gebruiken #1 {#use-case-1}

**Scenario**: Een bedrijf wil klantentevredenheid over diverse digitale aanraakpunten, zoals hun website en mobiele app meten. Ze gebruiken Adobe Experience Platform om Qualtrics-enquêtes te activeren op basis van gebruikersinteracties, zoals het voltooien van een aankoop of het bezoeken van een specifieke webpagina.

**Resultaat**: Door in real time te verzamelen terugkoppelt, kan het bedrijf gegevens-gedreven verbeteringen aan hun klantenervaring maken, die tot verhoogde tevredenheid en loyaliteit leiden.

### Hoofdletters gebruiken #2 {#use-case-2}

**Scenario**: Een organisatie streeft ernaar om zijn werknemer op het instappen proces te verbeteren. Ze gebruiken Adobe Experience Platform om feedback te verzamelen van nieuwe huren via Qualtrics-enquêtes. Enquêtes worden automatisch geactiveerd na een vooraf gedefinieerde instapperiode.

**Resultaat**: De ononderbroken feedback laat de organisatie toe om het onboarding proces aan te passen en te verbeteren, resulterend in betere overeenkomst en productiviteit onder nieuwe werknemers.

## Vereisten

Voordat u de bestemming Qualtrics in Adobe Experience Platform instelt, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een Qualtrics-account.
* U hebt het vereiste API-token verkregen van Qualtrics.

### Een API-token verkrijgen

Hieronder vindt u de noodzakelijke stappen voor het verkrijgen van een API-token van Qualtrics.

1. Meld u aan bij uw Qualtrics-account.
2. Ga naar **Montages van de Rekening**.
3. Selecteer **Qualtrics IDs**.
4. Op deze pagina, zoek de **API** sectie, bevat het a **Symbolische** gebied. Dit is de API Token, en zal tijdens bestemmingsopstelling worden vereist.

## Ondersteunde identiteiten {#supported-identities}

*de Automatiseringen van Qualtrics* steunen de activering van identiteiten die in de hieronder lijst worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email | E-mailadressen met normale tekst | Alleen e-mailadressen met onbewerkte tekst worden door Qualtrics ondersteund. |
| external_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U voert alle leden van een segment (publiek) met de herkenningstekens (naam, telefoonaantal, of anderen) uit die in de *bestemming van de Automatiseringen 0} worden gebruikt Qualtrics.* |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als deel van authentificatie zult u a **Gebruikersnaam** en **Wachtwoord** moeten verstrekken. De gebruikersnaam is uw Qualtrics-gebruikersnaam en het wachtwoord is de API-token van uw Qualtrics-account. Om het API teken terug te winnen volg de instructies van de **sectie van Eerste vereisten** hierboven.

![Verificatie](/help/destinations/assets/catalog/survey/qualtrics/authentication.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL URL]**: URL die in de [ Gebeurtenis JSON ](https://www.qualtrics.com/support/survey-platform/actions-module/json-events/#About) wordt gevonden die uw [ werkschema in Qualtrics ](https://www.qualtrics.com/support/survey-platform/actions-module/setting-up-actions/#About) teweegbrengt. Zie onderstaande schermafbeelding voor een voorbeeld.

![ URL ](/help/destinations/assets/catalog/survey/qualtrics/json-event-url.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [ activeer profielen en segmenten aan het stromen segment de uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Deze bestemming heeft een open schema zodat kunt u om het even welke eigenschappen naar Qualtrics verzenden.

#### Kenmerken Kaart

Om een attribuut aan uw afbeelding toe te voegen, selecteer eenvoudig **douaneattributen** wanneer het toevoegen van een nieuwe afbeelding. U kunt elke naam voor het kenmerk invoeren. Qualtrics moedigt *camelCase* noemende overeenkomst voor attributennamen (zie onder screenshot voor een voorbeeld) aan.

![ attributen van de Douane ](/help/destinations/assets/catalog/survey/qualtrics/custom-attribute.png)

Zie hieronder screenshot voor een voorbeeld van mogelijke kenmerktoewijzingen.

![ de afbeeldingen van het Voorbeeld ](/help/destinations/assets/catalog/survey/qualtrics/example-mappings.png)

#### Identiteiten toewijzen

Het is verplicht om een naamruimte voor identiteit te selecteren voor deze bestemming. De twee mogelijke brongebieden aan doelgebiedafbeeldingen zijn:

| Source-veld | Doelveld |
|--------------------|-----------------------|
| IdentityMap: E-mail | Identiteit: e-mail |
| IdentityMap: ECID | Identiteit: external_id |

Zie onderstaande schermafbeelding voor een voorbeeld.

![ Identiteitsnaamruimte ](/help/destinations/assets/catalog/survey/qualtrics/identity-namespace.png)

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

Om gegevens te verifiëren is opgenomen in Qualtrics, ga over naar het werkschema dat uw **Gebeurtenis JSON** bevat, van daar, naar **de geschiedenis van de Looppas** waar u de uitvoeringen van uw werkschema zou moeten zien. Elk werkschema heeft een status van of **Succeeded** of **Ontbroken**. Als u een bepaalde uitvoering selecteert, wordt er meer informatie over weergegeven, zodat u problemen kunt oplossen als u problemen hebt.

Als er geen uitvoeringen zichtbaar in **zijn de geschiedenis van de Looppas**, betekent het het werkschema nog niet is teweeggebracht, erop wijzend dat er een kwestie kan zijn. Verzeker het werkschema wordt toegelaten, en dat **URL** in de bestemming in Adobe Experience Platform correct is. De uitvoeringen van het werkschema zijn niet onmiddellijk, zodat kunt u een korte tijd moeten wachten alvorens het voltooit.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).
