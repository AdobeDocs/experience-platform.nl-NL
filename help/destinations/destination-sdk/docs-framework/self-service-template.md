---
title: Zelfbedieningssjabloon voor documentatie // Vervangen door de naam van uw doel
description: Gebruik deze sjabloon om openbare documentatie voor uw bestemming in de Adobe Experience Platform-catalogus te maken. // Vervang door de alinea in de sectie Overzicht
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Uw doelverbinding {#your-destination}

*Terwijl u deze sjabloon doorloopt, vervangt of verwijdert u alle cursief gedrukte alinea&#39;s (te beginnen met deze alinea).*

*Begin door de meta-gegevens (titel en beschrijving) bij te werken bij de bovenkant van de pagina. Negeer alle exemplaren van UICONTROL op deze pagina. Dit is een label waarmee de pagina in de verschillende talen die wij ondersteunen correct wordt vertaald in onze computervertaalprocessen. Nadat u de documentatie hebt verzonden, voegen we codes aan de documentatie toe.*

>[!IMPORTANT]
>
>* Vul alle secties in deze sjabloon in in de volgorde waarin ze in de sjabloon worden beschreven.
>* Deze sjabloon wordt niet regelmatig bijgewerkt, op basis van feedback van partners. Voordat u begint met het ontwerpen van documentatie voor uw bestemming, moet u controleren of u het gereedschap [laatste versie van de sjabloon](../assets/docs-framework/yourdestination-template.zip).

## Overzicht {#overview}

*Geef een kort overzicht van uw bedrijf, inclusief de waarde die het aan klanten biedt. Voeg een koppeling toe naar de startpagina van de productdocumentatie voor meer informatie.*

>[!IMPORTANT]
>
>Deze bestemmingsschakelaar en documentatiepagina worden gecreeerd en gehandhaafd door *YourDestination* team. Voor vragen of verzoeken om updates kunt u rechtstreeks contact opnemen via *Koppeling of e-mailadres invoegen waar u voor updates kunt komen, bijvoorbeeld `support@YourDestination.com`.*

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het *YourDestination* doel, hier zijn de gevallen van het steekproefgebruik die de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### Hoofdletters gebruiken #1 {#use-case-1}

*Voor mobiele berichtenplatforms:*

*Een homepage- en verkoopplatform wil mobiele meldingen naar Android- en iOS-apparaten van klanten sturen om hen te laten weten dat er 100 bijgewerkte aanbiedingen zijn in het gebied waar ze eerder naar een verhuur hebben gezocht.*

### Hoofdletters gebruiken #2 {#use-case-2}

*Voor sociale netwerkplatforms:*

*Een atletisch merk kledingartikelen wil bestaande klanten bereiken via hun sociale-mediakanalen. Het merk kleding kan e-mailadressen van hun eigen CRM aan Adobe Experience Platform opnemen, publiek van hun eigen offline gegevens bouwen, en deze soorten publiek naar YourDestination sturen, om advertenties in de sociale media van hun klanten te tonen.*

## Vereisten {#prerequisites}

*Voeg informatie in deze sectie over om het even wat toe dat de klanten zich van bewust moeten zijn alvorens aan opstelling de bestemming in het gebruikersinterface van Adobe Experience Platform te beginnen. Dit kan over zijn:*

* *moet aan een lijst van gewenste personen worden toegevoegd*
* *vereisten voor e-mailhashing*
* *accountdetails aan je kant*
* *hoe u een API-sleutel kunt verkrijgen om verbinding te maken met uw platform*

*U kunt een koppeling maken naar uw relevante documentatie als dat nuttig zou zijn voor klanten.*

## Ondersteunde identiteiten {#supported-identities}

*Voeg in deze sectie informatie toe over de identiteiten die door uw bestemming worden gesteund. We hebben de tabel vooraf gevuld met enkele standaardwaarden. Verwijder de waarden die niet van toepassing zijn op de bestemming en/of voeg waarden toe die niet zijn voorgevuld.*

*YourDestination* ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Lees het volgende document op [ECID](/help/identity-service/features/ecid.md) voor meer informatie . |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

*Voeg in deze sectie informatie toe over het publiek dat door uw bestemming wordt gesteund. We hebben de tabel vooraf gevuld met enkele standaardwaarden. Gebruik de `✓` en `X` tekens die aangeven of het type publiek door dit doel wordt ondersteund.*

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | X | Soorten publiek [geïmporteerd](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

*In de lijst, houd slechts de lijnen die aan uw bestemming beantwoorden. U moet één regel voor het type Exporteren en één regel voor de frequentie Exporteren hebben. Verwijder de waarden die niet van toepassing zijn op de bestemming.*

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (naam, telefoonnummer of andere) die worden gebruikt in het dialoogvenster *YourDestination* bestemming. |
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een publiek samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals u hebt gekozen in het scherm met de kenmerken voor het geselecteerde profiel van het dialoogvenster [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporttype | **[!UICONTROL Dataset export]** | U exporteert onbewerkte gegevenssets, die niet zijn gegroepeerd of gestructureerd op basis van belangen of kwalificaties van het publiek. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |
| Exportfrequentie | **[!UICONTROL Batch]** | De bestemmingen van de partij voeren dossiers naar stroomafwaartse platforms in toename van drie, zes, acht, twaalf, of 24 uren uit. Meer informatie over [batchbestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

*Voeg de velden toe die klanten moeten invullen wanneer ze verificatie uitvoeren op uw bestemming. Deze gebieden zijn bestemming-specifiek en hangen van uw configuratie in Destination SDK af. De velden van uw bestemming zijn mogelijk niet gelijk aan de onderstaande velden. Neem ook een schermafbeelding op, vergelijkbaar met de onderstaande voorbeeldschermafbeelding.*

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![Voorbeeldscreenshot waarin wordt getoond hoe u verificatie uitvoert voor de bestemming](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL Bearer token]**: Vul het token van de gebruiker in om te verifiëren bij de bestemming.

### Doelgegevens invullen {#destination-details}

*Voeg de gebieden toe die de klanten moeten invullen wanneer het vormen van een nieuwe bestemming. Deze gebieden zijn bestemming-specifiek en hangen van uw configuratie in Destination SDK af. De velden van uw bestemming zijn mogelijk niet gelijk aan de onderstaande velden. Neem ook een schermafbeelding op, vergelijkbaar met de onderstaande voorbeeldschermafbeelding.*

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Voorbeeldschermafbeelding met informatie over het invullen van details voor uw bestemming](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Account ID]**: Uw *YourDestination* account-id.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Lees voor meer informatie over waarschuwingen de handleiding op [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

*Doorhalen wat niet van toepassing is - Als u een nieuwe streamingbestemming documenteert, blijft de eerste alinea onder. Als u een nieuw op een bestand gebaseerd doel documenteert, houd de tweede paragraaf. Als u een bestemming documenteert die datasets uitvoert, houd de derde paragraaf.*

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

Lezen [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

Lezen [(Beta) Gegevensbestanden voor export](/help/destinations/ui/export-datasets.md) voor uitgebreide instructies over het uitvoeren van datasets naar deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

*Voeg informatie over ondersteunde toewijzingen tussen bron- en doelvelden toe in de stap Toewijzing van de activeringsworkflow. Uw doel biedt mogelijk ondersteuning voor het exporteren van profielkenmerken, naamruimten of beide. Sommige velden zijn mogelijk verplicht. Doelkenmerken kunnen vooraf gedefinieerd of aangepast zijn. Roep de belangrijke waarschuwingen uit en gebruik voorbeelden, bij voorkeur met screenshots. Twee voorbeelden van doelpagina&#39;s die u ter referentie kunt gebruiken zijn:*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## Geëxporteerde gegevens/Gegevens valideren bij exporteren {#exported-data}

*Voeg een alinea toe over de manier waarop gegevens naar uw doel worden geëxporteerd. Dit zou de klant helpen ervoor zorgen dat zij correct met uw bestemming geïntegreerd hebben. U kunt bijvoorbeeld een voorbeeld-JSON opgeven, zoals hieronder. Of, kon u screenshots en informatie van de interface van uw bestemming verstrekken die tonen hoe de klanten zouden moeten verwachten dat het publiek in het bestemmingsplatform bevolkt is.*

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
        "status": "realized"
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