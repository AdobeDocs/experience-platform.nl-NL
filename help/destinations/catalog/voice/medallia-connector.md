---
title: verbinding met Medallia
description: Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 0%

---

# verbinding met Medallia

## Overzicht {#overview}

Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen.

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en door het team van Medallia gehandhaafd. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de afdeling adobe-integrations@medallia.com.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van Medallia zou moeten gebruiken, zijn hier de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### Hoofdletters gebruiken #1

Een B2B-merk wil zijn instapprogramma evalueren en stroomlijnen. Ze willen persoonlijke enquêtes in real-time verzenden naar klanten die net het instapproces hebben voltooid.

### Hoofdletters gebruiken #2

Een detailhandelaar zoekt naar een beter begrip van de voorkeur van de klant voor ordervervulling. Ze willen een korte SMS-enquête met één vraag verzenden naar klanten die de afgelopen maand online en in-store aankopen hebben gedaan.

## Vereisten {#prerequisites}

Voor de verbinding met Medallia is de volgende informatie vereist:
* **URL OAuth Token Endpoint**
* **Client-id**
* **Clientgeheim**
* **API Gateway-URL**
* **API-naam importeren**

Werk samen met uw Media-leveringsteam om deze gegevens te verkrijgen.

## Ondersteunde identiteiten {#supported-identities}

Medallia ondersteunt de activering van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| email | E-mailadres | Selecteer de identiteit van het e-maildoel wanneer u enquêtes wilt verzenden naar een e-mailuitnodiging. Als een profiel is gekoppeld aan meerdere e-mailadressen, wordt de uitnodiging alleen voor de eerste e-mail geactiveerd. |
| telefoon | Telefoonnummers in E.164-indeling | Selecteer de identiteit van het telefoondoel wanneer u op SMS-Gebaseerde onderzoeken wilt verzenden. Het telefoonnummer moet de E.164-indeling hebben, die een plusteken (+), een internationale aanroepcode van het land, een lokale netcode en een telefoonnummer bevat. Bijvoorbeeld: (+)(landcode)(netnummer)(telefoonnummer). Wanneer een profiel met veelvoudige telefoonaantallen wordt geassocieerd, zal Medallia de uitnodiging aan het eerste slechts telefoonaantal teweegbrengen. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle zojuist gekwalificeerde leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL OAuth Token Endpoint URL]**: Doorgaans heeft dit de vorm van https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client ID]**: Vraag het aan bij uw Media-leveringsteam.
* **[!UICONTROL Client Secret]**: Vraag het aan bij uw Media-leveringsteam.

![Afbeelding die het verificatiescherm voor deze bestemming weergeeft.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL API Gateway URL]**: Vraag het aan bij uw Media-leveringsteam. De notatie https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Vraag het aan bij uw Media-leveringsteam. Naam van de Media Import API (ook wel Web Feed genoemd) die in deze verbinding moet worden gebruikt. U kunt verschillende soorten publiek activeren voor verschillende API&#39;s voor importeren om verschillende enquêteprogramma&#39;s te activeren.

![Afbeelding die het scherm met doeldetails voor deze bestemming weergeeft.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De volgende naamruimte(s) voor de doelidentiteit moeten worden toegewezen, afhankelijk van het gebruiksgeval:
* Voor e-mailenquêtes: **email** moet worden toegewezen als een doelveld met **Doelveld** > **Naamruimte selecteren** > **email**
* Voor SMS-enquêtes: **telefoon** moet worden toegewezen als een doelveld met **Doelveld** > **Naamruimte selecteren** > **telefoon**. Telefoonnummers moeten de E.164-indeling hebben, waaronder een plusteken (+), een internationale aanroepcode van het land, een lokale netcode en een telefoonnummer.

Het wordt sterk geadviseerd dat u ook extra attributen van de doeldouane in kaart brengt om gepersonaliseerde onderzoeken tot stand te brengen en extra informatie over de klant aan het onderzoeksverslag toe te voegen:

* De gepersonaliseerde onderzoeken richten typisch de klant door naam
   * De voornaam van de klant toewijzen aan **Doelveld** > **Aangepaste kenmerken selecteren** > **Kenmerknaam** > **firstname**
   * De achternaam van de klant toewijzen aan **Doelveld** > **Aangepaste kenmerken selecteren** > **Kenmerknaam** > **lastname**
* Toewijzingen toevoegen voor andere aangepaste doelkenmerken naar wens

![Afbeelding die een voorbeeldtoewijzing voor identiteiten en kenmerken weergeeft.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Deel uw Media-leveringsteam exact **Kenmerknamen** voor elk doelattribuut van de douane u toewijst gebruikend **Doelveld** > **Aangepaste kenmerken selecteren** > **Kenmerknaam**. Mogelijk wilt u een schermafbeelding maken van de toewijzingspagina om deze rechtstreeks te delen.

## Geëxporteerde gegevens {#exported-data}

Zodra u uw segment(en) hebt geactiveerd naar de bestemming, informeert u het leveringsteam van Medallia, dat de geëxporteerde gegevens van Adobe Experience Platform naar Medallia zal kunnen valideren. Let op: enquêtes kunnen alleen in Medallia worden geactiveerd nadat de gegevens zijn geverifieerd; voorafgaand aan deze verificatie worden de gegevens naar Medallia geëxporteerd, maar worden geen enquêtes naar de klanten gestart.

Hieronder ziet u een voorbeeld van JSON van de geëxporteerde gegevens, waarin de voorbeeldtoewijzing uit de bovenstaande schermafbeelding in het dialoogvenster **Kenmerken en identiteiten toewijzen** sectie:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).
