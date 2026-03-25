---
title: Merkury Enterprise Identity Destination
description: Leer hoe u een Merkury Enterprise Identity-doelverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
last-substantial-update: 2024-07-20T00:00:00Z
exl-id: a5452183-289c-49c3-9574-e09b0153dc00
source-git-commit: 20427c4c8826905a77fac04d055d523b12a6f739
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 1%

---

# Merkury Enterprise Identity Destination

>[!NOTE]
>
>De doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van [!DNL Merkury] . Neem voor vragen of verzoeken om updates contact op met uw [!DNL Merkury] -accountvertegenwoordiger.

## Overzicht {#overview}

Gebruik de bestemming [!DNL Merkury Enterprise Identity] om nauwkeurigere, uitgebreidere en inzichtelijkere consumentenprofielen te maken. Met verbeterde profielgegevens kunnen marketers betere inzichten, segmenten en modellen genereren, wat resulteert in een nauwkeurigere gerichtheid en voorspellende modellering.

![&#x200B; een diagram dat van A de interconnectie tussen Merkury en Experience Platform toont, met inbegrip van opname en activering &#x200B;](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Voer de stappen in deze documentatiepagina uit om een [!DNL Merkury Identity] doelverbinding te maken en een publiek voor identificatie en verrijking te activeren via de gebruikersinterface van [!DNL Adobe Experience Platform] .

>[!NOTE]
>
>Als u het publiek wilt activeren naar mediadoelen met uw [!DNL Merkury Connect] -account, gebruikt u in plaats daarvan het doel van [!DNL Merkury Connections] .

![&#x200B; de de bestemmingskaart van de Identiteit van de Onderneming van de Merkury die in de de bestemmingscatalogus van Experience Platform wordt benadrukt.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Gebruiksscenario’s {#use-cases}

De [!DNL Merkury Enterprise Identity] -bestemming biedt de mogelijkheid om consumentengepompel veilig over te brengen voor de volgende [!DNL Merkury] -mogelijkheden:

* **Kwaliteit van Gegevens**: Verbeter de kwaliteit van de het profielgegevens van de consument met gegevenshygiëne en normalisatie. [!DNL Merkury] bevat Amerikaanse posthygiëne en verplaatsingsidentificatie ter ondersteuning van de meest geavanceerde gevallen van direct mailmarketing.
* **Resolutie van de Identiteit**: Bouw een nauwkeurige en uitvoerige enige mening van de klant, die door [!DNL Merkury] Individuele en Huishoudelijke IDs wordt geïnformeerd. Merkury-id&#39;s bieden een diepe profielkoppeling, aangedreven door de uitgebreide identiteitsgrafiek van 268+ miljoen mensen in de VS van [!DNL Merkury] voor volwassenen.
* **Verrijking**: De betere Inzichten en verpersoonlijking van de aandrijving met [!DNL Merkury Data]. [!DNL Merkury Data] bevat meer dan 10.000 beschikbare gegevenskenmerken, variërend van demografische kenmerken, levensstijl, financiën, levensgebeurtenissen en aankoopgegevens van de [!DNL Merkury Data Suite] .

>[!NOTE]
>
>Deze gebruiksgevallen worden uitgevoerd door een combinatie van zowel bestemmings als bronschakelaars. De klant zou beginnen door hun bestaande klantenverslagen voor verrijking uit te voeren gebruikend deze bestemmingsschakelaar. De service van [!DNL Merkury] zoekt naar het bestand, haalt het op, verrijkt het met de gegevens van [!DNL Merkury] en genereert een bestand. De klant zou dan de bijbehorende [!DNL Merkury] Source-connectorbronkaart gebruiken om de gehydrateerde klantprofielen weer in Adobe op te nemen [!DNL Real-Time CDP] .

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>* Om met de bestemming te verbinden, hebt u de **Doelen van de Mening** nodig en **leidt Doelen**, **Doelen**, **Profielen van de Mening**, en **Segmenten van de Mening** [&#x200B; [toegangsbeheertoestemmingen] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/home#permissions). Lees [&#x200B; [toegangsbeheeroverzicht] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/ui/overview) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **Grafiek van de Identiteit van de Mening** [&#x200B; [toegangsbeheertoestemming] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/home#permissions) nodig.\![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze namespace kan ook door de volgende aliassen worden bedoeld: &quot;identiteitskaart van Adobe Marketing Cloud&quot;, &quot;[!DNL Adobe Experience Cloud] identiteitskaart&quot;, &quot;[!DNL Adobe Experience Platform] identiteitskaart&quot;. Zie het volgende document op [&#x200B; ECID &#x200B;](/help/identity-service/features/ecid.md) voor meer informatie. |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Onbewerkte tekst en via SHA256 gehashte telefoonnummers worden ondersteund door [!DNL Adobe Experience Platform] . Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Zowel platte tekst als gehashte e-mailadressen van SHA256 worden ondersteund door [!DNL Adobe Experience Platform]. Wanneer het bronveld hashingkenmerken bevat, schakelt u de optie **[!UICONTROL Apply transformation]** in om de gegevens automatisch te laten hashen bij activering door [!DNL Experience Platform] . |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Nee | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| **Doelgroep** | **Gesteund** | **Oorsprong van de Beschrijving** |
|---|---|---|      
| Segmentatieservice | Ja | Soorten publiek dat door Experience Platform [&#x200B; [de Dienst van de Segmentatie] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/segmentation/home) wordt geproduceerd. |
| Aangepaste uploads | Nee | Soorten publiek [&#x200B; [ingevoerd] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u de **Doelen van de Mening** nodig en **leidt en activeert de Doelen van de Dataset** [&#x200B; [toegangsbeheertoestemmingen] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/home#permissions). Lees [&#x200B; [toegangsbeheeroverzicht] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/ui/overview) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in [&#x200B; worden beschreven [de zelfstudie van de bestemmingsconfiguratie] &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/ui/connect-destination). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming {#authenticate}

Om aan de bestemming voor authentiek te verklaren, vul de vereiste gebieden in en selecteer **verbinden met bestemming**.

Als u toegang wilt tot uw emmertje op Experience Platform, moet u geldige waarden opgeven voor de volgende referenties:

| **Referentie** | **Beschrijving** |
|---|---|
| Toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen van het Merkury-team. |
| Geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen van het Merkury-team. |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen van het Merkury-team. |

{style="table-layout:auto"}

![&#x200B; het nieuwe scherm van de bestemmingsverwezenlijking &#x200B;](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![&#x200B; het schermschot van bestemmingsdetails &#x200B;](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Naam (Vereist)** - de naam de bestemming onder zal worden bewaard
* **Beschrijving** - Korte verklaring van het doel van de bestemming
* **Naam van het Emmertje (Vereist)** - Naam van de Amazon S3 emmer opstelling op S3
* **Weg van de Omslag (Vereist)** - als subdirectories in een emmertje worden gebruikt moet een weg worden bepaald, of &quot;/&quot;om de wortelweg van verwijzingen te voorzien.
* **Type van Dossier** - selecteer het formaat Experience Platform voor de uitgevoerde dossiers zou moeten gebruiken. Raadpleeg uw Merkury-team voor het verwachte bestandstype voor uw account.

>[!NOTE]
>
>Als u de optie CSV, Scheidingsteken, Citaat, Escape-teken, Lege waarde, Null-waarde, Compressie-indeling en Inclusief manifestbestandsopties selecteert, neemt u contact op met uw Merkury-team voor de juiste instellingen voor uw account.

![&#x200B; beeld van csv optie &#x200B;](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Bestaande account {#existing-account}

Accounts die al zijn gedefinieerd met de Merkury Enterprise Identity-bestemming, worden weergegeven in een pop-up lijst. Als u deze optie selecteert, kunt u details van de account bekijken in de rechtertrack. Bekijk het voorbeeld van UI, wanneer u aan **Doelen** navigeert > **Rekeningen**;

![&#x200B; het screenshot van A van bestemmingsrekening in pagina van bestemmingsrekeningen &#x200B;](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/ui/alerts).

Wanneer u klaar bent met het verstrekken van details voor uw bestemmingsverbinding, selecteer **daarna**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>* Om gegevens te activeren, hebt u de **Doelen van de Mening** nodig, **activeert Doelen**, **Profielen van de Mening**, en **de toegangsbeheertoestemmingen van de Segmenten van de Mening**. Lees het toegangsbeheeroverzicht of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om identiteiten uit te voeren, hebt u de **toestemming van de de toegangscontrole van de Grafiek van de Identiteit van de Mening** nodig.

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) voor instructies bij het activeren van publiek aan deze bestemming.

## Toewijzingssuggesties {#mapping-suggestions}

Voor een correcte verwerking van bestanden aan de zijde van [!DNL Merkury] zijn naam- en adreselementen vereist. Hoewel niet alle elementen vereist zijn, zal het zo veel mogelijk helpen om tot een succesvolle overeenkomst te komen.

Toewijzingssuggesties worden gegeven in de onderstaande tabel met de kenmerken aan uw doelzijde die worden gebruikt door [!DNL Merkury] -verwerking waaraan klanten profielkenmerken kunnen toewijzen. Behandel deze elementen als suggesties aangezien niet alle elementen worden vereist, en de bronwaarden zullen van de behoeften van de rekening afhangen.

| Doelveld | Source-beschrijving |
|---|---|
| id | Identiteitsveld dat moet worden gebruikt om [!DNL Merkury] -gegevens via de [!DNL Merkury Enterprise Identity] Source-connector toe te wijzen aan Experience Platform |
| Input_First_Name | De `person.name.firstName` -waarde in Experience Platform. |
| Input_Last_Name | De `person.name.lastName` -waarde in Experience Platform. |
| Input_Address_Line_1 | De `mailingAddress.street` -waarde in Experience Platform. |
| Input_City | De `mailingAddress.city` -waarde in Experience Platform. |
| Input_State_Province_Code | De `mailingAddress.state` -waarde in Experience Platform. Wordt gebruikt als de status in de vorm van een code van twee tekens staat. |
| Input_State_Province_Name | De `mailingAddress.state` -waarde in Experience Platform. Gebruiken als de staat de volledige staatsnaam is |
| Input_Postal_Code | De `mailingAddress.postalCode` -waarde in Experience Platform. |
| Input_Email_Address | De waarde die u wilt toewijzen als het e-mailadres voor profielen. |
| Invoer_Telefoon | De waarde u als aantal van de profielentelefoon wilt in kaart brengen. |

{style="table-layout:auto"}

## Gegevens exporteren valideren {#validate-data-export}

Om te controleren of gegevens zijn geëxporteerd, controleert u het Amazon S3 Storage bucket en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, lees het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/data-governance/home).

## Volgende stappen {#next-steps}

U hebt een gegevensstroom gemaakt om profielgegevens van Experience Platform naar uw [!DNL Merkury] beheerde S3-locatie te exporteren. Vervolgens moet u contact opnemen met uw [!DNL Merkury] -vertegenwoordiger met de naam van de account, de bestandsnamen en het emmerpad, zodat de verwerking kan worden ingesteld.
