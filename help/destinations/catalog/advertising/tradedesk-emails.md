---
title: De Trade Desk - CRM-verbinding
description: Activeer profielen aan uw rekening van het Bureau van de Handel voor publiek gericht en onderdrukking die op de gegevens van CRM wordt gebaseerd.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 0%

---

# De [!DNL Trade Desk] - CRM-verbinding

>[!IMPORTANT]
>
>Er zijn twee de Commerciële Desk - bestemmingen CRM in de [&#x200B; bestemmingscatalogus &#x200B;](/help/destinations/catalog/overview.md).
>
>* Als u gegevens in de EU bront, gebruikt u de **[!DNL The Trade Desk - CRM (EU)]** bestemming.
>* Als u gegevens in de APAC- of NAMER-gebieden bront, gebruikt u de bestemming **[!DNL The Trade Desk - CRM (NAMER & APAC)]** .
>
>Deze doelconnector en documentatiepagina worden gemaakt en onderhouden door het team van *[!DNL Trade Desk]* . Neem contact op met uw [!DNL Trade Desk] vertegenwoordiger voor meer informatie of verzoeken om updates.

## Overzicht {#overview}

Begrijp hoe u profielen aan uw [!DNL Trade Desk] rekening voor publiek activeert richt en onderdrukking die op de gegevens van CRM wordt gebaseerd.

Deze schakelaar verzendt gegevens naar [!DNL The Trade Desk] voor de activering van Gegevens van eerste partij. [!DNL The Trade Desk] sla uw onbewerkte e-mails en telefoonnummers op.

>[!TIP]
>
>Gebruik [!DNL The Trade Desk - CRM] -bestemming om CRM-gegevens (zoals e-mails en telefoonnummers) en andere id&#39;s voor gegevens van de eerste partij, zoals cookies en apparaat-id&#39;s, te verzenden. U kunt de [&#x200B; bestemming van het Bureau van de Handel &#x200B;](/help/destinations/catalog/advertising/tradedesk.md) in de catalogus van Experience Platform voor koekjes en apparatenidentiteitskaart in kaart brengen blijven gebruiken.

## Vereisten {#prerequisites}

>[!IMPORTANT]
>
>Voordat u het publiek naar de handelsdesk kunt activeren, moet u contact opnemen met uw accountmanager van [!DNL Trade Desk] om de functie in te schakelen. Als u e-mails, telefoonnummers en UID2/EUID verzendt, moet u de ondertekende UID2/EUID-overeenkomst delen met [!DNL The Trade Desk] .

## Vereisten voor ID-afstemming {#id-matching-requirements}

Afhankelijk van het type id&#39;s dat u in Adobe Experience Platform invoert, moet u aan de desbetreffende vereisten voldoen. Gelieve te lezen het [&#x200B; overzicht van Namespace van de Identiteit &#x200B;](/help/identity-service/features/namespaces.md) voor meer informatie.

## Ondersteunde identiteiten {#supported-identities}

[!DNL The Trade Desk] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

Adobe Experience Platform ondersteunt zowel e-mailadressen zonder hashing als telefoonnummers. Volg de instructies in de sectie met vereisten voor id-afstemming en gebruik de juiste naamruimten voor normale tekst en gehashte e-mailadressen.

| Doelidentiteit | Beschrijving |
|---|---|
| Email | E-mailadressen (tekst wissen) |
| Email_LC_SHA256 | E-mailadressen moeten worden gehasht met behulp van SHA256 en verlaagd. U kunt deze instelling later niet wijzigen. |
| Telefoon (E.164) | Telefoonnummers die genormaliseerd moeten worden in E.164-indeling. De E.164-indeling bevat een plusteken (+), een internationale aanroepcode van het land, een lokale netcode en een telefoonnummer. Bijvoorbeeld: (+)(landcode)(netnummer)(telefoonnummer). Deze identificatiecode is niet beschikbaar voor The Trade Desk - First-Party Data (EU). |
| Telefoon (SHA256_E.164) | De aantallen van de telefoon die reeds aan formaat E.164 zijn genormaliseerd en dan gehakt gebruikend SHA-256, met de resulterende hash Base64-Gecodeerd. Deze identificatiecode is niet beschikbaar voor The Trade Desk - First-Party Data (EU). |
| TDID | Cookie-id in de handelsbank |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | Apple-id voor adverteerders |
| UID2 | De onbewerkte UID2-waarde |
| UID2Token | De gecodeerde UID2-token, ook wel reclametoken genoemd. |
| EUID | Onbewerkte id-waarde van Europese Unie |
| EUIDToken | De gecodeerde EUID-token, ook wel reclametoken genoemd. |
| RampID | De RampID van 49 tekens of 70 tekens (voorheen IdentityLink of IDL genoemd). Dit moet een RampID van LiveRamp zijn die specifiek voor de Commerciële Desk in kaart wordt gebracht. |
| netID | De netID van de gebruiker als 70 karakter base64-gecodeerde koord. Deze id wordt alleen in Europa ondersteund. |
| FirstID | De First-id van de gebruiker, een eerstepartijcookie die doorgaans door uitgevers in Frankrijk wordt ingesteld. Deze id wordt alleen in Europa ondersteund. |

{style="table-layout:auto"}

## E-mailhashingvereisten {#email-hashing}

U kunt e-mailadressen hashen alvorens hen in Adobe Experience Platform op te nemen of onbewerkte e-mailadressen gebruiken.

Om over het opnemen van e-mailadressen in Experience Platform te leren, lees het [&#x200B; overzicht van de partijingestitie &#x200B;](/help/ingestion/batch-ingestion/overview.md).

Als u ervoor kiest om de e-mailadressen zelf te hashen, moet u aan de volgende vereisten voldoen:

* Voorloopspaties en volgspaties verwijderen.
* Zet alle ASCII-tekens om in kleine letters.
* Verwijder in het gedeelte Gebruikersnaam van het e-mailadres van `gmail.com` de volgende tekens uit het e-mailadres:

      * De periode (`.`) teken (ASCII-code 46). U kunt bijvoorbeeld &quot;jane.doe@gmail.com&quot; normaliseren naar &quot;janedoe@gmail.com&quot;.
     * Het plusteken (`+&#39;) (ASCII-code 43) en alle daaropvolgende tekens. Bijvoorbeeld, normaliseer ` janedoe+home@gmail.com ` aan ` janedoe@gmail.com &grave;.
  

## De het aantalnormalisatie en hashing van de telefoon vereisten {#phone-hashing}

Dit is wat u moet weten over het uploaden van telefoonaantallen:

* U moet telefoonaantallen normaliseren alvorens hen in een verzoek te verzenden, ongeacht of u hen hashed of unhashed in een verzoek verzendt.
* Om genormaliseerde, gehakt, en gecodeerde gegevens te uploaden, moet u telefoonaantallen als Base64-Gecodeerde hashes SHA-256 van de genormaliseerde telefoonaantallen verzenden.

Of u ruwe of gehakt telefoonaantallen wilt uploaden, moet u hen normaliseren.

>[!IMPORTANT]
>
>Normalisatie vóór hashing zorgt ervoor dat de gegenereerde id-waarde altijd hetzelfde is en dat de gegevens op de juiste wijze kunnen worden aangepast.

Hier is wat u over de normalisatievereisten van het telefoonaantal moet weten:

* De UID2-operator accepteert telefoonnummers in de E.164-indeling. Dit is de internationale notatie voor telefoonnummers die garant staat voor wereldwijde uniciteit.
* E.164 telefoonaantallen kunnen een maximum van 15 cijfers hebben.
* Voor genormaliseerde E.164-telefoonnummers wordt de volgende syntaxis gebruikt: `[+][country code][subscriber number including area code]` zonder spaties, afbreekstreepjes, haakjes of andere speciale tekens. Hier volgen enkele voorbeelden:

      * VS: 1 (234) 567-8901 is genormaliseerd naar +12345678901.
     * Singapore: 65 1243 5678 is genormaliseerd naar +6512345678.
     * Australië: mobiel telefoonnummer 0491 570 006 is genormaliseerd om de landcode toe te voegen en de voorloopnul te laten vallen: +61491570006.
     * VK: mobiel telefoonnummer 07812 345678 is genormaliseerd om de landcode toe te voegen en de voorloopnul te laten vallen: +447812345678.
  
Controleer of het genormaliseerde telefoonnummer UTF-8 is en geen ander coderingssysteem zoals UTF-16.

Een hash van het telefoonaantal is een Base64-Gecodeerde hash SHA-256 van een genormaliseerd telefoonaantal. Het telefoonaantal wordt eerst genormaliseerd, dan gehakt gebruikend het shashing algoritme SHA-256, en dan worden de resulterende bytes van de knoeiboelwaarde gecodeerd gebruikend het coderen Base64. Merk op dat Base64 het coderen wordt toegepast op de bytes van de knoeiboelwaarde, niet de hexadecimale gecodeerde koordvertegenwoordiging.
In de volgende tabel ziet u een voorbeeld van een eenvoudig invoertelefoonnummer en het resultaat van elke stap om tot een veilige, ondoorzichtige waarde te komen.

| Type | Voorbeeld | Opmerkingen en gebruik |
|---|---|---|
| Onbewerkt telefoonnummer | 1 (234) 567-8901 | Dit is het uitgangspunt. |
| Genormaliseerd telefoonnummer | +12345678901 | Normalisatie is altijd de eerste stap. |
| SHA-256 hash van genormaliseerd telefoonnummer | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee9ee | Deze 64-tekenreeks is een hexadecimale gecodeerde representatie van de 32-byte SHA-256. |
| Hex aan Base64 SHA-256 codering van genormaliseerd en gehakt telefoonaantal | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | Deze 44-tekenreeks is een Base64-gecodeerde representatie van de 32-byte SHA-256. De SHA-256-hash is een hexadecimale waarde. U moet een codeermodule Base64 gebruiken die een hexadecimale waarde als input neemt. Gebruik deze codering voor phone_hash-waarden die worden verzonden in de hoofdtekst van de aanvraag. |

>[!IMPORTANT]
>
>Wanneer u Base64-codering toepast, moet u een functie gebruiken die een hexadecimale waarde als invoer gebruikt. Als u een functie gebruikt die tekst als invoer gebruikt, is het resultaat een langere tekenreeks die ongeldig is in UID2.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail of gehashte e-mail) die worden gebruikt in de bestemming Handelsbureau. |
| Exportfrequentie | **[!UICONTROL Daily Batch]** | Aangezien een profiel in Experience Platform wordt bijgewerkt op basis van publieksevaluatie, wordt het profiel (de identiteiten) eenmaal per dag bijgewerkt naar het doelplatform. Lees meer over [&#x200B; partijuitvoer &#x200B;](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

### Verifiëren voor doel {#authenticate}

[!DNL The Trade Desk] CRM-bestemming is een dagelijkse bestandsupload waarvoor geen verificatie door de gebruiker is vereist.

### Bestemmingsdetails invullen {#fill-in-details}

Voordat u publieksgegevens naar een doel kunt verzenden of activeren, moet u een verbinding met uw eigen doelplatform instellen. Terwijl [&#x200B; vestiging &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) deze bestemming, u de volgende informatie moet verstrekken:

* **[!UICONTROL Account Type]**: Kies de optie **[!UICONTROL Existing Account]** .
* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Advertiser ID]**: uw [!DNL Trade Desk Advertiser ID] , die kan worden gedeeld door uw [!DNL Trade Desk] accountmanager of kan worden gevonden onder [!DNL Advertiser Preferences] in de gebruikersinterface van [!DNL Trade Desk] .

{het schermschot van 0} Experience Platform UI die tonen hoe te om bestemmingsdetails in te vullen.![](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Wanneer u verbinding maakt met de bestemming, is het instellen van een beleid voor gegevensbeheer volledig optioneel. Gelieve te herzien Experience Platform [&#x200B; overzicht van het gegevensbeheer &#x200B;](/help/data-governance/policies/overview.md) voor meer details.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer publieksgegevens aan de uitvoerbestemmingen van het partijprofiel &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) voor instructies bij het activeren van publiek aan een bestemming.

Op de pagina **[!UICONTROL Scheduling]** kunt u het schema en de bestandsnamen configureren voor elk publiek dat u exporteert. Het is verplicht het schema te configureren, maar het configureren van de bestandsnaam is optioneel.

{het schermschot van 0} Experience Platform UI aan de activering van het programmapubliek.![](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Alle soorten publiek die op [!DNL The Trade Desk] CRM-bestemming worden geactiveerd, worden automatisch ingesteld op een dagelijkse frequentie en het volledige bestand wordt geëxporteerd.

{het schermschot van 0} Experience Platform UI aan de activering van het programmapubliek.![](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Op de pagina **[!UICONTROL Mapping]** moet u kenmerken of naamruimten selecteren in de bronkolom en toewijzen aan de doelkolom.

{het schermschot van 0} Experience Platform UI aan de activering van het kaartpubliek.![](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Hieronder ziet u een voorbeeld van correcte identiteitstoewijzing bij het activeren van soorten publiek naar [!DNL The Trade Desk] CRM-bestemming.

Bron- en doelvelden selecteren:

| Source-veld | Doelveld |
|---|---|
| Email | email |
| Email_LC_SHA256 | hashed_email |
| Telefoon (E.164) | telefoon |
| Telefoon (SHA256_E.164) | hashed_phone |
| TDID | tdid |
| GAID | droid |
| IDFA | idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | euïsch |
| EUIDToken | euid_token |
| RampID | idl |
| ID5 | id5 |
| netID | net_id |
| FirstID | first_id |


## Gegevens exporteren valideren {#validate}

Als u wilt controleren of gegevens correct vanuit Experience Platform en naar [!DNL The Trade Desk] worden geëxporteerd, zoekt u het publiek onder het tabblad Adobe 1PD in de bibliotheek [!DNL The Trade Desk] Gegevens en identiteit van adverteerders. Hier volgen de stappen voor het zoeken van de bijbehorende id in de gebruikersinterface van [!DNL Trade Desk] :

1. Selecteer eerst de tab **[!UICONTROL Libraries]** en bekijk de sectie **[!UICONTROL Advertiser data and identity]** .
2. Klik op **[!UICONTROL Adobe 1PD]** en geef alle soorten publiek weer dat op [!DNL The Trade Desk] is geactiveerd.
3. De segmentnaam of segment-id uit Experience Platform wordt weergegeven als de segmentnaam in de gebruikersinterface van [!DNL Trade Desk] .

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).
