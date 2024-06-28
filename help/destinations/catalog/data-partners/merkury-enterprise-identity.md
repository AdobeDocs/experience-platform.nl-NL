---
title: Merkury Enterprise Identity Destination
description: Leer hoe u een Merkury Enterprise Identity-doelverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 66a0a085e696dbe13d0368da395f655c7ca01a97
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 0%

---


# Merkury Enterprise Identity Destination

>[!NOTE]
>
>De bestemmingsschakelaar en documentatiepagina worden gecreeerd en door het team van de Merkury gehandhaafd. Neem voor vragen of verzoeken om updates contact op met uw vertegenwoordiger van de Merkury-account.

## Overzicht

Gebruik de Merkury Enterprise Identity-bestemming om nauwkeurigere, uitgebreide en inzichtelijkere consumentenprofielen samen te stellen. Met verbeterde profielgegevens kunnen marketers betere inzichten, segmenten en modellen genereren, wat resulteert in een nauwkeurigere gerichtheid en voorspellende modellering.

![Een diagram met de koppeling tussen Merkury en Experience Platform, inclusief inslikken en activering](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Voer de stappen in deze documentatiepagina uit om een Merkury Identity-bestemmingsverbinding te maken en een publiek voor identificatie en verrijking te activeren via de Adobe Experience Platform-gebruikersinterface.

>[!NOTE]
>
>Als u het publiek naar mediadoelen wilt activeren met uw Merkury Connect-account, gebruikt u in plaats daarvan onze Merkury Connections-bestemming.

![De Merkury Enterprise Identity-doelkaart wordt gemarkeerd in de catalogus met Experience Platforms doelen.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Gebruiksscenario’s

De Bestemming van de Identiteit van de Onderneming van de Merkury verstrekt de capaciteit om consument PII voor de volgende Merkury mogelijkheden veilig over te brengen:

* **Gegevenskwaliteit**: Verbetering van de gegevenskwaliteit van het consumentenprofiel met behulp van gegevenshygiëne en -standaardisering. Merkury omvat de Amerikaanse posthygiëne en verplaatst identificatie om de meest geavanceerde gevallen van direct mailmarketing te ondersteunen.
* **Identiteitsresolutie**: Bouw een nauwkeurige en uitgebreide, uniforme weergave van de klant, op de hoogte gebracht door Merkury Individual en Household IDs. Merkury-id&#39;s bieden een diepe profielkoppeling die wordt aangedreven door de uitgebreide Amerikaanse identiteitsgrafiek voor volwassen consumenten van Merkury van 268+ miljoen mensen.
* **Verrijking**: Creëer betere inzichten en personalisatie met Merkury Data. Merkury Data omvat meer dan 10.000 beschikbare gegevensattributen variërend van demografische, levensstijl, financiële, levensgebeurtenissen en aankoopgegevens van de Merkury Data Suite.

>[!NOTE]
>
>Deze gebruiksgevallen worden uitgevoerd door een combinatie van zowel bestemmings als bronschakelaars. De klant zou beginnen door hun bestaande klantenverslagen voor verrijking uit te voeren gebruikend deze bestemmingsschakelaar. De service van Merkury zou het bestand zoeken, ophalen, verrijken met de gegevens van Merkury en een bestand genereren. De klant zou dan de overeenkomstige Merkury Source-connectorbronkaart gebruiken om de gehydrateerde klantprofielen weer in Adobe Real-Time CDP in te voeren.

## Vereisten

>[!IMPORTANT]
>
>* Om met de bestemming te verbinden, hebt u nodig **Doelen weergeven** en **Doelen beheren**, **Doelen activeren**, **Profielen weergeven**, en **Segmenten weergeven** [[toegangsbeheermachtigingen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lees de [[overzicht van toegangsbeheer]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **Identiteitsgrafiek weergeven** [[toegangsbeheermachtiging]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| GAID | Google-advertentie-id | Selecteer de GAID doelidentiteit wanneer uw bronidentiteit een GAID-naamruimte is. |
| IDFA | Apple-id voor adverteerders | Selecteer de IDFA doelidentiteit wanneer uw bronidentiteit een IDFA namespace is. |
| ECID | Experience Cloud-id | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/features/ecid.md) voor meer informatie . |
| phone_sha256 | Telefoonnummers die zijn hashed met het SHA256-algoritme | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-telefoonnummers. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| email_lc_sha256 | E-mailadressen die met het algoritme SHA256 worden gehasht | Adobe Experience Platform biedt ondersteuning voor zowel platte tekst- als SHA256-e-mailadressen met hashing. Wanneer het bronveld hashkenmerken bevat, controleert u de **[!UICONTROL Apply transformation]** optie, om [!DNL Platform] de gegevens bij activering automatisch hashen. |
| extern_id | Aangepaste gebruikers-id&#39;s | Selecteer deze doelidentiteit wanneer uw bronidentiteit een aangepaste naamruimte is. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen

In deze sectie wordt beschreven welk type publiek u naar dit doel kunt exporteren.

| **Doelgroep** | **Ondersteund** | **Beschrijving** | **oorsprong** |
|---|---|---|---|
| Segmenteringsservice | ✓ | Door het Experience Platform gegenereerde soorten publiek [[Segmentatieservice]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| Aangepaste uploads | x | Soorten publiek [[geïmporteerd]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

|**Publiek**|**Ondersteund**|**Oorsprong van beschrijving**|
|---|---|---|
|Segmenteringsdienst|✓|Soorten publiek gegenereerd door het Experience Platform [[Segmentatieservice]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home).|
|Aangepaste uploads|X|Soorten publiek [[geïmporteerd]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform van CSV-bestanden.|

{style="table-layout:auto"}

## Verbinden met de bestemming

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **Doelen weergeven** en **Dataset-doelen beheren en activeren** [[toegangsbeheermachtigingen]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Lees de [[overzicht van toegangsbeheer]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [[zelfstudie over doelconfiguratie]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). Vul in de workflow voor doelconfiguratie de velden in die in de twee onderstaande secties worden vermeld.

### Verifiëren voor bestemming

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **Verbinden met doel**.

Om tot uw emmer op Experience Platform toegang te hebben, moet u geldige waarden voor de volgende geloofsbrieven verstrekken:

| **Credentials** | **Beschrijving** |
|---|---|
| Toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen van het Merkury-team. |
| Geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen van het Merkury-team. |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen van het Merkury-team. |

{style="table-layout:auto"}

![nieuw scherm voor het maken van de bestemming](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Doelgegevens invullen

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Screenshot van bestemmingsdetails](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Naam (vereist)** - De naam waaronder het doel wordt opgeslagen
* **Beschrijving** - Korte toelichting van het doel van de bestemming
* **Emmernaam (vereist)** - Naam van het Amazon S3-emmertje dat is ingesteld op S3
* **Pad naar map (vereist)** - Als submappen in een emmertje worden gebruikt, moet een pad worden gedefinieerd of moet &#39;/&#39; worden gedefinieerd om naar het hoofdpad te verwijzen.
* **Bestandstype** - Selecteer de indeling die het Experience Platform moet gebruiken voor de geëxporteerde bestanden. Raadpleeg uw Merkury-team voor het verwachte bestandstype voor uw account.

>[!NOTE]
>
>Wanneer u de optie CSV, Scheidingsteken, Citateken, Escape-teken, Lege waarde, Null-waarde, Compressie-indeling en Inclusief manifestbestandsopties selecteert, neemt u contact op met uw Merkury-team voor de juiste instellingen voor uw account.

![afbeelding van de csv-optie](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Bestaande account

Accounts die al zijn gedefinieerd met de Merkury Enterprise Identity-bestemming, worden weergegeven in een pop-up lijst. Als u deze optie selecteert, kunt u details van de account bekijken in de rechtertrack. Bekijk het voorbeeld van UI, wanneer u navigeert aan **Doelen** > **Accounts**;

![Een screenshot van bestemmingsaccount op pagina met bestemmingsaccounts](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Waarschuwingen inschakelen

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **Volgende**.

## Soorten publiek naar dit doel activeren

>[!IMPORTANT]
>
>* Als u gegevens wilt activeren, hebt u de toegangsbeheermachtigingen voor Bestemmingen weergeven, Doelen activeren, Profielen weergeven en Segmenten weergeven nodig. Lees het toegangsbeheeroverzicht of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om identiteiten uit te voeren, hebt u de de toegangsbeheertoestemming van de Grafiek van de Identiteit van de Mening nodig.

Lezen [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) voor instructies voor het activeren van het publiek naar deze bestemming.

## Toewijzingssuggesties

Voor een correcte verwerking van bestanden aan de zijde van Merkury zijn naam- en adreselementen vereist. Hoewel niet alle elementen vereist zijn, zal het zo veel mogelijk helpen om tot een succesvolle overeenkomst te komen.

Toewijzingssuggesties worden gegeven in de onderstaande tabel met lijstkenmerken aan uw bestemmingszijde die worden gebruikt door Merkury-verwerking waaraan klanten profielkenmerken kunnen toewijzen. Behandel deze elementen als suggesties aangezien niet alle elementen worden vereist, en de bronwaarden zullen van de behoeften van de rekening afhangen.

| Doelveld | Bronbeschrijving |
|---|---|
| id | Identiteitsveld dat moet worden gebruikt om merkury-gegevens aan Experience Platform toe te wijzen via de Merkury Enterprise Identity Resolution Source-connector |
| Input_First_Name | De `person.name.firstName` waarde in Experience Platform. |
| Input_Last_Name | De `person.name.lastName` waarde in Experience Platform. |
| Input_Address_Line_1 | De `mailingAddress.street` waarde in Experience Platform. |
| Input_City | De `mailingAddress.city` waarde in Experience Platform. |
| Input_State_Province_Code | De `mailingAddress.state` waarde in Experience Platform. Wordt gebruikt als de status in de vorm van een code van twee tekens staat. |
| Input_State_Province_Name | De `mailingAddress.state` waarde in Experience Platform. Gebruiken als de staat de volledige staatsnaam is |
| Input_Postal_Code | De `mailingAddress.postalCode` waarde in Experience Platform. |
| Input_Email_Address | De waarde die u wilt toewijzen als het e-mailadres voor profielen. |
| Invoer_Telefoon | De waarde u als aantal van de profielentelefoon wilt in kaart brengen. |

{style="table-layout:auto"}

## Gegevens exporteren valideren

Om te controleren of gegevens zijn geëxporteerd, controleert u het Amazon S3 Storage bucket en controleert u of de geëxporteerde bestanden de verwachte profielpopulaties bevatten.

## Gegevensgebruik en -beheer

Alle Adobe Experience Platform-doelen zijn bij het verwerken van uw gegevens compatibel met het beleid voor gegevensgebruik. Lees voor meer informatie over hoe Adobe Experience Platform gegevensbeheer afdwingt de [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een dataflow gecreeerd om profielgegevens van Experience Platform naar uw Merkury beheerde S3 plaats uit te voeren. Vervolgens moet u contact opnemen met uw vertegenwoordiger van Merkury met de naam van de account, bestandsnamen en het emmerpad, zodat de verwerking kan worden ingesteld.
