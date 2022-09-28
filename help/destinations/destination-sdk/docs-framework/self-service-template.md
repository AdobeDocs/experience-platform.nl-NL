---
title: Zelfbedieningssjabloon voor documentatie // Vervangen door de naam van uw doel
description: Gebruik deze sjabloon om openbare documentatie voor uw bestemming in de Adobe Experience Platform-catalogus te maken. // Vervang door de alinea in de sectie Overzicht
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 46e8f6cf3e135b31dc508274598f9d76df857c8f
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 0%

---

# YourDestination-verbinding {#your-destination}

*Terwijl u deze sjabloon doorloopt, vervangt of verwijdert u alle cursief gedrukte alinea&#39;s (te beginnen met deze alinea).*

*Begin door de meta-gegevens (titel en beschrijving) bij te werken bij de bovenkant van de pagina. Negeer alle exemplaren van UICONTROL op deze pagina. Dit is een label waarmee de pagina in de verschillende talen die wij ondersteunen correct wordt vertaald in onze computervertaalprocessen. Nadat u de documentatie hebt verzonden, voegen we codes aan de documentatie toe.*

>[!IMPORTANT]
>
>* Vul alle secties in deze sjabloon in in de volgorde waarin ze in de sjabloon worden beschreven.
>* Deze sjabloon wordt niet regelmatig bijgewerkt, op basis van feedback van partners. Voordat u begint met het ontwerpen van documentatie voor uw bestemming, moet u controleren of u het gereedschap [laatste versie van de sjabloon](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).


## Overzicht {#overview}

*Geef een kort overzicht van uw bedrijf, inclusief de waarde die het aan klanten biedt. Voeg een koppeling toe naar de startpagina van de productdocumentatie voor meer informatie.*

>[!IMPORTANT]
>
>Deze documentatiepagina is gemaakt door de *YourDestination* team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *Koppeling of e-mailadres invoegen waar u voor updates kunt komen, bijvoorbeeld `support@YourDestination.com`.*

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het *YourDestination* doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1 {#use-case-1}

*Voor mobiele berichtenplatforms:*

*Een homepage- en verkoopplatform wil mobiele meldingen naar Android- en iOS-apparaten van klanten doorsturen om hen te laten weten dat er 100 bijgewerkte aanbiedingen zijn in het gebied waar ze eerder naar een verhuur hebben gezocht.*

### Hoofdletters gebruiken #2 {#use-case-2}

*Voor sociale netwerkplatforms:*

*Een atletisch merk kledingartikelen wil bestaande klanten bereiken via hun sociale-mediakanalen. Het merk kleding kan e-mailadressen van hun eigen CRM aan Adobe Experience Platform opnemen, segmenten van hun eigen offlinegegevens bouwen, en deze segmenten naar YourDestination verzenden, om advertenties in de sociale media van hun klanten te tonen.*

## Vereisten {#prerequisites}

*Voeg informatie in deze sectie over om het even wat toe dat de klanten zich van bewust moeten zijn alvorens aan opstelling de bestemming in het gebruikersinterface van Adobe Experience Platform te beginnen. Dit kan over zijn:*

* *moet aan een lijst van gewenste personen worden toegevoegd*
* *vereisten voor e-mailhashing*
* *accountdetails aan je kant*
* *hoe u een API-sleutel kunt verkrijgen voor verbinding met uw platform*

*U kunt een koppeling maken naar uw relevante documentatie als dat nuttig zou zijn voor klanten.*

## Ondersteunde identiteiten {#supported-identities}

*Voeg in deze sectie informatie toe over de identiteiten die door uw bestemming worden gesteund. We hebben de tabel vooraf gevuld met enkele standaardwaarden. Verwijder de waarden die niet van toepassing zijn op de bestemming en alle waarden die niet zijn voorgevuld.*

*YourDestination* ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Naar deze naamruimte kan ook worden verwezen door de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Lees het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie . |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style=&quot;table-layout:auto&quot;}

## Type en frequentie exporteren {#export-type-frequency}

*In de lijst, houd slechts de lijnen die aan uw bestemming beantwoorden. U moet één regel voor het type Exporteren en één regel voor de frequentie Exporteren hebben. Verwijder de waarden die niet van toepassing zijn op de bestemming.*

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster *YourDestination* bestemming. |
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |
| Uitvoerfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

*Voeg de velden toe die klanten moeten invullen wanneer ze verificatie uitvoeren op uw bestemming. Deze gebieden zijn bestemming-specifiek en hangen van uw configuratie in Destination SDK af. De velden van uw bestemming zijn mogelijk niet gelijk aan de onderstaande velden. Neem ook een schermafbeelding op, vergelijkbaar met de onderstaande voorbeeldschermafbeelding.*

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![Voorbeeldscreenshot waarin wordt getoond hoe u verificatie uitvoert voor de bestemming](/help/destinations/destination-sdk/docs-framework/assets/authenticate-destination.png)

* **[!UICONTROL Bearer token]**: Vul de token van de drager in om te verifiëren bij de bestemming.

### Doelgegevens invullen {#destination-details}

*Voeg de gebieden toe die de klanten moeten invullen wanneer het vormen van een nieuwe bestemming. Deze gebieden zijn bestemming-specifiek en hangen van uw configuratie in Destination SDK af. De velden van uw bestemming zijn mogelijk niet gelijk aan de onderstaande velden. Neem ook een schermafbeelding op, vergelijkbaar met de onderstaande voorbeeldschermafbeelding.*

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Voorbeeldschermafbeelding met informatie over het invullen van details voor uw bestemming](/help/destinations/destination-sdk/docs-framework/assets/configure-destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw *YourDestination* account-id.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Lees voor meer informatie over waarschuwingen de handleiding op [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

*Doorhalen wat niet van toepassing is - Als u een nieuwe streamingbestemming documenteert, blijft de eerste alinea onder. Als u een nieuw op een bestand gebaseerd doel documenteert, houd de tweede paragraaf.*

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

Lezen [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

*Voeg informatie over ondersteunde toewijzingen tussen bron- en doelvelden toe in de stap Toewijzing van de activeringsworkflow. Uw doel biedt mogelijk ondersteuning voor het exporteren van profielkenmerken, naamruimten of beide. Sommige velden zijn mogelijk verplicht. Doelkenmerken kunnen vooraf gedefinieerd of aangepast zijn. Roep de belangrijke waarschuwingen uit en gebruik voorbeelden, bij voorkeur met screenshots. Twee voorbeelden van doelpagina&#39;s die u ter referentie kunt gebruiken zijn:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

*Voeg een alinea toe over de manier waarop gegevens naar uw doel worden geëxporteerd. Dit zou de klant helpen ervoor zorgen dat zij correct met uw bestemming geïntegreerd hebben. U kunt bijvoorbeeld een voorbeeld-JSON opgeven, zoals hieronder. Of, kon u screenshots en informatie van de interface van uw bestemming verstrekken die tonen hoe de klanten segmenten zouden moeten verwachten om in het bestemmingsplatform te bevolken.*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

*U kunt verdere verbindingen aan uw productdocumentatie of om het even welke andere middelen verstrekken die u voor de klant belangrijk om vindt succesvol te zijn.*