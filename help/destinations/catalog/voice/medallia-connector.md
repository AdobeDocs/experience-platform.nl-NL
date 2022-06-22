---
title: verbinding met Medallia
description: Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen.
source-git-commit: be2d4e5d1f204feefc7acb7cb4518044ab3f153a
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---


# verbinding met Medallia

## Overzicht {#overview}

Activeer profielen voor gerichte Media enquêtes en koppel inzameling terug om klantenbehoeften en verwachtingen beter te begrijpen.

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door het Medallia-team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen met de afdeling adobe-integrations@medallia.com.

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

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle zojuist gekwalificeerde leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

* **[!UICONTROL OAuth Token Endpoint URL]**: De notatie https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL Client ID]**: Haal het op van je Media-leveringsteam.
* **[!UICONTROL Client Secret]**: Haal het op van je Media-leveringsteam.

![Afbeelding die het verificatiescherm voor deze bestemming weergeeft.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Doelgegevens invullen {#destination-details}

Om details voor de bestemming te vormen, vul de vereiste gebieden in en selecteer **[!UICONTROL Next]**.

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL API Gateway URL]**: Haal het op van je Media-leveringsteam. De notatie https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Import API Name]**: Haal het op van je Media-leveringsteam. Naam van de Media Import API (ook wel Web Feed genoemd) die in deze verbinding moet worden gebruikt. U kunt verschillende segmenten activeren voor verschillende import-API&#39;s om verschillende enquêteprogramma&#39;s te activeren.

![Afbeelding die het scherm met doeldetails voor deze bestemming weergeeft.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

De volgende naamruimte(s) voor de doelidentiteit moeten worden toegewezen, afhankelijk van het gebruiksgeval:
* Voor e-mailenquêtes: **email** moet als doelveld worden toegewezen met **Doelveld** > **Naamruimte selecteren** > **email**
* Voor SMS-enquêtes: **telefoon** moet als doelveld worden toegewezen met **Doelveld** > **Naamruimte selecteren** > **telefoon**. Telefoonnummers moeten de E.164-indeling hebben, waaronder een plusteken (+), een internationale aanroepcode van het land, een lokale netcode en een telefoonnummer.

Het wordt sterk geadviseerd dat u ook extra attributen van de doeldouane in kaart brengt om gepersonaliseerde onderzoeken tot stand te brengen en extra informatie over de klant aan het onderzoeksverslag toe te voegen:

* De gepersonaliseerde onderzoeken richten typisch de klant door naam
   * De voornaam van de klant toewijzen aan **Doelveld** > **Aangepaste kenmerken selecteren** > **Kenmerknaam** > **firstname**
   * De achternaam van de klant toewijzen aan **Doelveld** > **Aangepaste kenmerken selecteren** > **Kenmerknaam** > **lastname**
* Toewijzingen toevoegen voor andere aangepaste doelkenmerken naar wens

![Afbeelding die een voorbeeldtoewijzing voor identiteiten en kenmerken weergeeft.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Deel de exacte gegevens met uw Media-leveringsteam **Kenmerknamen** voor elk doelattribuut van de douane u toewijst gebruikend **Doelveld** > **Aangepaste kenmerken selecteren** > **Kenmerknaam**. Mogelijk wilt u een schermafbeelding maken van de toewijzingspagina om deze rechtstreeks te delen.

## Geëxporteerde gegevens {#exported-data}

Zodra u uw segment(en) hebt geactiveerd naar de bestemming, informeert u het leveringsteam van Medallia, dat de geëxporteerde gegevens van Adobe Experience Platform naar Medallia zal kunnen valideren. Merk op dat enquêtes alleen binnen Medallia kunnen worden geactiveerd na succesvolle verificatie van de gegevens; voordien zullen de gegevens naar Medallia worden geëxporteerd, maar zullen er geen enquêtes naar de klanten worden gehouden.

Hieronder ziet u een voorbeeld van JSON van de geëxporteerde gegevens, waarin de voorbeeldtoewijzing uit de bovenstaande schermafbeelding in het dialoogvenster **Kenmerken en identiteiten toewijzen** sectie:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).
