---
keywords: extensie voor doorsturen van gebeurtenis;pinterest;pinterest-gebeurtenis voor extensie doorsturen
title: Pinterest-gebeurtenis door:sturen, extensie
description: Deze Adobe Experience Platform-gebeurtenis die extensie doorstuurt, stelt u in staat om gebeurtenissen in te voeren in Pinterest voor uw zakelijke vereisten.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 0%

---

# [!DNL Pinterest] -gebeurtenis, extensie doorsturen

[!DNL Pinterest] is een visuele zoekfunctie waarmee u ideeën kunt vinden zoals recepten, thuisdecor, stijlinspiratie en nog veel meer. Er zijn miljarden punten op [!DNL Pinterest] die ook met anderen kunnen worden gedeeld op [!DNL Pinterest] . U kunt de gebruikersinteractiegebeurtenissen en hefboomwerking [!DNL Pinterest Analytics] sorteren om gebruikersgedrag te begrijpen en gerichte reclame in werking te stellen.

De [[!DNL Pinterest]  gebeurtenis van Conversies ](https://developers.pinterest.com/docs/conversions/conversion-management/) API [ die ](../../../ui/event-forwarding/overview.md) uitbreiding door:sturen staat u toe aan hefboomwerkingsgegevens in de Edge Network van Adobe Experience Platform worden gevangen en het verzenden naar [!DNL Pinterest]. Dit document behandelt de gebruiksgevallen van de uitbreiding, hoe te om het te installeren, en hoe te om zijn mogelijkheden in uw gebeurtenis te integreren die [ regels ](../../../ui/managing-resources/rules.md) door:sturen.

Conversies van toegangstokens zijn de verificatiemethode die [!DNL Pinterest] gebruikt bij interactie met de [!DNL Pinterest] API.

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van de Edge Network in [!DNL Pinterest] wilt gebruiken om te profiteren van de analysemogelijkheden van de klant.

Neem bijvoorbeeld een marketingteam in een organisatie. Het team legt gebruikersinteractiegebeurtenisgegevens van zijn website vast en laadt deze in [!DNL Pinterest] met deze door:sturen-extensie van gebeurtenis.

De marketing- en analyseteams kunnen vervolgens gebruikmaken van [!DNL Pinterest] Analysemogelijkheden om belangrijke gebruikersinteracties en -gedrag te begrijpen, zodat u gebruikers beter kunt begrijpen en beter kunt richten op doelgerichte advertentiecampagnes.

Voor meer informatie over gebruiksgevallen specifiek voor [!DNL Pinterest], verwijs naar de [[!DNL Pinterest]  gebruiksgevallen ](https://business.pinterest.com/en/success-stories) documentatie.

## [!DNL Pinterest] voorwaarden {#prerequisites}

U moet een geldige [!DNL Pinterest] [ bedrijfsrekening ](https://help.pinterest.com/en/business/article/get-a-business-account) hebben om deze uitbreiding te gebruiken. Ga naar de [[!DNL Pinterest]  registratiepagina ](https://www.pinterest.com/business/create/) om een rekening te registreren en tot stand te brengen als u niet reeds hebt.

U hebt ook een [!DNL Pinterest] -ontwikkelaarsaccount nodig, die aan uw [!DNL Pinterest] -zakelijke account moet worden gekoppeld. Om uw ontwikkelaarrekening met uw bedrijfsrekening te associëren, verwijs naar de [[!DNL Pinterest &#x200B;]  ontwikkelaarrekening ](https://developers.pinterest.com/account-setup/).

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u het Experience Platform wilt verbinden met [!DNL Pinterest] , hebt u de volgende invoeren nodig:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Adds-account-id | Je account-id voor [!DNL Pinterest] Adds. Verwijs naar de [[!DNL Pinterest]  documentatie ](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) voor begeleiding. | 123456789012 |
| Token voor toegang tot conversie | Uw token voor conversietoegang van [!DNL Pinterest] . Verwijs naar [[!DNL Pinterest]  Conversies API ](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) document voor begeleiding. <br> **u zal slechts worden vereist dit één keer te doen aangezien dit teken niet verloopt.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## De extensie [!DNL Pinterest] installeren en configureren {#install}

Om de uitbreiding te installeren, [ creeer een gebeurtenis door:sturen bezit ](../../../ui/event-forwarding/overview.md#properties) of kies een bestaand bezit in plaats daarvan uit te geven.

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. Selecteer **[!UICONTROL Install]** op de kaart voor de extensie [!DNL Pinterest] op het tabblad **[!UICONTROL Catalog]** .

![ Catalogus die de [!DNL Pinterest] uitbreiding met [!UICONTROL Install] benadrukte tonen.](../../../images/extensions/server/pinterest/install.png)

### De extensie [!DNL Pinterest] configureren

>[!IMPORTANT]
>
>Afhankelijk van uw implementatiebehoeften, kunt u een schema, gegevenselementen, en een dataset moeten tot stand brengen alvorens de uitbreiding te vormen. Controleer alle configuratiestappen voordat u begint om te bepalen welke entiteiten u moet instellen voor uw geval van gebruik.

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. Selecteer **[!UICONTROL Configure]** op de kaart voor de [!DNL Pinterest] -extensie op het tabblad [!UICONTROL Installed] **.

![[!DNL Pinterest] die wordt weergegeven op de [!UICONTROL Install] tab met [!UICONTROL Configure] gemarkeerde extensie. ](../../../images/extensions/server/pinterest/configure.png)

Op het volgende scherm, input [!UICONTROL Ads Account Id] en [!UICONTROL Conversion Access Token] die u eerder in de [ sectie van configuratiedetails ](#configuration-details) verzamelde. Selecteer **[!UICONTROL Save]** als u klaar bent.

![ het [!DNL Pinterest] [!UICONTROL Configure] scherm dat de [!UICONTROL Ads Account Id] en [!UICONTROL Conversion Access Token] inputgebieden benadrukt.](../../../images/extensions/server/pinterest/input.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen die regels bepaalt wanneer en hoe uw gebeurtenissen naar [!DNL Pinterest] zullen worden verzonden.

Creeer een nieuwe [ regel ](../../../ui/managing-resources/rules.md) in uw gebeurtenis door:sturen bezit. Voeg onder **[!UICONTROL Actions]** een nieuwe handeling toe en stel de extensie in op **[!UICONTROL Pinterest]** . Als u Edge Network-gebeurtenissen naar [!DNL Pinterest] wilt verzenden, stelt u de waarde **[!UICONTROL Action Type]** in op **[!UICONTROL Send Event].**

![ de [!DNL Pinterest] [!UICONTROL Send Event] regelverwezenlijking.](../../../images/extensions/server/pinterest/rule.png)

Na selectie, schijnen de extra controles om de gebeurtenis verder te vormen. U moet de eigenschappen van de gebeurtenis [!DNL Pinterest] toewijzen aan de gegevenselementen die u eerder hebt gemaakt.

### [!UICONTROL Event Data]

De volgende gebeurtenisgegevens worden vereist om de nieuwe regel te maken:

| Veldnaam | Beschrijving | Voorbeeld |
| --- | --- | --- | 
| [!UICONTROL Event Name] | Het type van de gebruikersgebeurtenis. Dit kan om het even welk gebeurtenistype echter zijn, aan hefboomwerking [!DNL Pinterest Analytics] wordt het geadviseerd om [[!DNL Pinterest]  gebeurteniscodes ](https://help.pinterest.com/en/business/article/add-event-codes) te gebruiken | * checkout <br> * add_to_cart <br> * page_visit <br> * signup <br> * [ user-defined gebeurtenis ] |
| [!UICONTROL Action Source] | De bron die aangeeft waar de conversiegebeurtenis heeft plaatsgevonden. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Event Time] | Dit verwijst naar de tijd van de gebeurtenis. De standaardtijdnotatie die wordt gebruikt, is UNIX, in de notatie `<seconds>.<miliseconds>` , afhankelijk van uw lokale tijdzone. Voor meer informatie, verwijs naar [[!DNL Pinterest]  API ](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 wijst op 1433188255 seconden en 500 milliseconden na epoch, of maandag, 1 Juni, 2015, bij 7 :50: 55 PM GMT. |
| [!UICONTROL Event ID] | Een unieke id-tekenreeks die deze gebeurtenis identificeert en kan worden gebruikt voor het verwijderen tussen gebeurtenissen die via de API voor conversie en Pinterest-tracking worden opgenomen. Zonder dit zullen de gegevens van de gebeurtenis waarschijnlijk dubbel worden geteld en zal de inflatie in metrische termen worden gerapporteerd. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | Een JSON-object dat aangepaste eigenschappen van de gebeurtenis bevat. Maak een keuze uit het opgeven van onbewerkte JSON of uit het gebruik van een vereenvoudigde set toetsinvoer. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![ [!DNL Pinterest] [!UICONTROL Event Data] benadrukt in de regelactie.](../../../images/extensions/server/pinterest/event-data.png)

De volgende gebeurteniseigenschappen kunnen worden geconfigureerd:

| Veldnaam | Beschrijving |
| --- | --- |
| Source-URL voor gebeurtenis | URL van de webconversiegebeurtenis. |
| Toepassingsarchief-id | De toepassings-id van de App Store. |
| Toepassingsnaam | De naam van de toepassing. |
| Toepassingsversie | De versie van de toepassing. |
| Merk apparaat | Merk apparaat dat door de gebruiker wordt gebruikt. |
| Apparaatdrager | De mobiele provider van de gebruiker voor het apparaat. |
| Apparaatmodel | Model van het apparaat van de gebruiker |
| Apparaattype | Type apparaat dat door de gebruiker wordt gebruikt. |
| Versie besturingssysteem | Versie van het besturingssysteem van het apparaat. |
| Taal van gebruiker | ISO-639-1-taalcode van twee tekens die de taal van de gebruiker aangeeft. |

### [!UICONTROL User Data]

De volgende gebruikersgegevens kunnen worden ingevoerd door zijn geen vereiste velden:

| Veldnaam | Beschrijving | Voorbeeld |
| --- | --- | --- | 
| [!UICONTROL Email] | E-mailadres van gebruiker of een SHA256-hash van het e-mailadres van de gebruiker. | ebd543592.f2b7e1 |
| [!UICONTROL Mobile Adverstising IDs] | Sha256 hashes van &quot;Google Advertising IDs&quot; (GAIDs) van de gebruiker of &quot;Apple Identifier for Advertisers&quot; (IDFAs) | ebd543592.f2b7e1 |
| [!UICONTROL Client IP Address] | Het IP-adres van de gebruiker. Dit kan de IPv4- of IPv6-indeling hebben. Wordt gebruikt voor overeenkomsten. | 192 168 0,1 |
| [!UICONTROL Client User Agent] | De userAgent-tekenreeks van de webbrowser van de gebruiker. | Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | Een JSON-object dat andere klantgegevens bevat. Maak een keuze uit het opgeven van onbewerkte JSON of uit het gebruik van een vereenvoudigde set toetsinvoer. | { &quot;ph&quot;: &quot;122333445&quot; } |

![ [!DNL Pinterest] [!UICONTROL User Data] benadrukt in de regelactie.](../../../images/extensions/server/pinterest/user-data.png)

De eigenschappen van de klanteninformatie die kunnen worden gevormd zijn:

| Veldnaam | Beschrijving |
| --- | --- |
| Telefoon | Contactnummer gebruiker. Alleen cijfers worden geaccepteerd en moeten worden ingevoerd met de landcode, de gebiedscode en het nummer. |
| Geslacht | Geslacht kan worden ingevoerd als &quot;f&quot; voor vrouwelijk, &quot;m&quot; voor mannelijk en &quot;n&quot; voor niet-binair. |
| Geboortedatum | Geboortedatum, ingevoerd als jaar, maand, en dag. |
| Achternaam | Achternaam van de gebruiker. |
| Voornaam | Voornaam van gebruiker. |
| Plaats | De woonplaats van de gebruiker. Dit wordt meestal gebruikt voor factureringsdoeleinden. |
| Staat | De staat van de gebruiker, die als twee-lettercode in kleine letters wordt verstrekt. |
| Postcode | De postcode van de gebruiker, die hoofdzakelijk voor factureringsdoeleinden wordt gebruikt. |
| Land | ISO-3166-landcode van twee tekens die het land van de gebruiker aangeeft. |
| Externe id | Unieke id van de adverteerder die een gebruiker in zijn ruimte identificeert. Bijvoorbeeld gebruikers-id, loyaliteit-id enzovoort. |
| Klik op ID | De unieke id die is opgeslagen in _epik cookie op uw domein of de query-parameter &amp;epik= in de URL. |

>[!IMPORTANT]
>
>Voordat de gegevens naar het API-eindpunt van [!DNL Pinterest] worden verzonden, wordt de waarde van de volgende velden door de extensie gewijzigd en genormaliseerd: E-mail, Telefoonnummer, Voornaam, Achternaam, Genderinstelling, Geboortedatum, Plaats, Staat, Postcode, Land en Externe id. De extensie verbergt de waarde van deze velden niet als er al een SHA256-tekenreeks aanwezig is.

### [!UICONTROL Custom Data]

De volgende aangepaste gegevens kunnen voor de regel worden ingevoerd:

| Veldnaam | Beschrijving |
| --- | --- |
| Valuta | De ISO-4217-valutacode. Als dit niet wordt opgegeven, wordt in [!DNL Pinterest] de valuta van de adverteerder gebruikt die tijdens het maken van de account is ingesteld. |
| Waarde | Totale waarde van de gebeurtenis. Wordt geaccepteerd als een tekenreeks in de aanvraag. Dit wordt in een dubbel cijfer geparseerd. |
| Zoektekenreeks | De zoektekenreeks die betrekking heeft op de conversiegebeurtenis van de gebruiker. |
| Order-id | De bestellings-id. Door `order_id` te verzenden, kunt u [!DNL Pinterest] gebeurtenissen indien nodig dedupliceren. |
| Aantal producten | Het totale aantal producten van de gebeurtenis. Bijvoorbeeld het totale aantal objecten dat is aangeschaft tijdens een uitcheckgebeurtenis. |
| Inhoud-id&#39;s | Lijst (array) met product-id&#39;s. |
| Inhoud | Een lijst (array) met objecten die informatie over producten bevatten, zoals prijs en hoeveelheid. |

![ [!DNL Pinterest] [!UICONTROL Custom Data] benadrukt in de regelactie.](../../../images/extensions/server/pinterest/custom-data.png)

## Gegevens valideren binnen [!DNL Pinterest]

Nadat de regel voor het doorsturen van gebeurtenissen is gemaakt en uitgevoerd, controleert u of de gebeurtenis die naar de [!DNL Pinterest] API is verzonden, wordt weergegeven zoals u had verwacht in de [!DNL Pinterest] -gebruikersinterface.

Als de gebeurtenisverzameling en [!DNL Experience Platform] -integratie zijn gelukt, ziet u gebeurtenissen in de gebruikersinterface van [!DNL Pinterest] .

![ de [!DNL Pinterest] gebeurtenismanager ](../../../images/extensions/server/pinterest/event-history.png)

U kunt de [!DNL Pinterest] -gebeurtenisgegevensdistributie verder doorlopen en bekijken.

![ de [!DNL Pinterest] gegevensdistributie ](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Volgende stappen

Deze handleiding besprak het installeren en configureren van de [!DNL Pinterest] -gebeurtenis voor het doorsturen van extensies in de gebruikersinterface. Raadpleeg de officiële documentatie voor meer informatie:

* [[!DNL Pinterest]  API ](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest]  Conversies API Overzicht ](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
