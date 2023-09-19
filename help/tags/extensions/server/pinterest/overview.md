---
keywords: extensie voor doorsturen van gebeurtenis;pinterest;pinterest-gebeurtenis voor extensie doorsturen
title: Pinterest-gebeurtenis door:sturen, extensie
description: Deze Adobe Experience Platform-gebeurtenis die extensie doorstuurt, stelt u in staat om gebeurtenissen in te voeren in Pinterest voor uw zakelijke vereisten.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 2%

---

# [!DNL Pinterest] extensie voor doorsturen van gebeurtenissen

[!DNL Pinterest] is een visuele zoekmachine om ideeën zoals recepten, thuisdecor, stijlinspiratie en nog veel meer te vinden. Er zijn miljarden spelden op [!DNL Pinterest], die ook met anderen kunnen worden gedeeld over [!DNL Pinterest]. U kunt de gebeurtenissen van de gebruikersinteractie en hefboomwerking sorteren [!DNL Pinterest Analytics] om gebruikersgedrag te begrijpen en gerichte reclame in werking te stellen.

De [[!DNL Pinterest] Conversies](https://developers.pinterest.com/docs/conversions/conversion-management/) API [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge Network gebruiken en verzenden naar [!DNL Pinterest]. Dit document behandelt de gebruiksgevallen van de extensie, de manier waarop de extensie moet worden geïnstalleerd en de manier waarop de mogelijkheden van de extensie moeten worden geïntegreerd in het doorsturen van de gebeurtenis [regels](../../../ui/managing-resources/rules.md).

De tokens van de toegang van omzettingen zijn de authentificatiemethode die door wordt gebruikt [!DNL Pinterest] bij interactie met de [!DNL Pinterest] API.

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van het Edge-netwerk wilt gebruiken in [!DNL Pinterest] om gebruik te maken van de mogelijkheden voor klantanalyse.

Neem bijvoorbeeld een marketingteam in een organisatie. Het team legt gebruikersinteractiegebeurtenisgegevens van zijn website vast en laadt deze in [!DNL Pinterest] gebruiken van deze gebeurtenis die uitbreiding door:sturen.

De marketing- en analyseteams kunnen vervolgens gebruikmaken van [!DNL Pinterest] Analysemogelijkheden om belangrijke gebruikersinteractie en gedrag te begrijpen, die u toestaan om gebruikers beter te begrijpen en hen voor gerichte advertentiecampagnes te richten.

Voor meer informatie over gebruiksgevallen die specifiek zijn voor [!DNL Pinterest], verwijst u naar de [[!DNL Pinterest] use cases](https://business.pinterest.com/en/success-stories) documentatie.

## [!DNL Pinterest] voorwaarden {#prerequisites}

U moet een geldige [!DNL Pinterest] [zakelijke account](https://help.pinterest.com/en/business/article/get-a-business-account) om deze extensie te gebruiken. Ga naar de [[!DNL Pinterest] registratiepagina](https://www.pinterest.com/business/create/) als u nog geen account hebt, kunt u zich registreren en een account maken.

U hebt ook een [!DNL Pinterest] ontwikkelaarsaccount, dat moet worden gekoppeld aan uw [!DNL Pinterest] zakelijke account. Als u uw ontwikkelaarsaccount wilt koppelen aan uw zakelijke account, raadpleegt u de [[!DNL Pinterest ] ontwikkelingsaccount](https://developers.pinterest.com/account-setup/).

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u het Experience Platform wilt verbinden met [!DNL Pinterest], zijn de volgende invoeren vereist:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Adds-account-id | Uw [!DNL Pinterest] Account-ID toevoegen. Zie de [[!DNL Pinterest] documentatie](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) ter begeleiding. | 123456789012 |
| Token voor toegang tot conversie | Uw [!DNL Pinterest] Token voor conversietoegang. Zie de [[!DNL Pinterest] Conversies-API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) document ter begeleiding. <br> **U hoeft dit slechts één keer te doen, aangezien deze token niet verloopt.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Installeer en configureer de [!DNL Pinterest] extension {#install}

Als u de extensie wilt installeren, [een eigenschap voor het doorsturen van gebeurtenissen maken](../../../ui/event-forwarding/overview.md#properties) of kies een bestaande eigenschap die u wilt bewerken.

Selecteer in de linkernavigatie de optie **[!UICONTROL Extensions]**. Selecteren **[!UICONTROL Install]** op de kaart voor de [!DNL Pinterest] in de **[!UICONTROL Catalog]** tab.

![Catalogus met de [!DNL Pinterest] extensie [!UICONTROL Install] gemarkeerd.](../../../images/extensions/server/pinterest/install.png)

### Vorm [!DNL Pinterest] extension

>[!IMPORTANT]
>
>Afhankelijk van uw implementatiebehoeften, kunt u een schema, gegevenselementen, en een dataset moeten tot stand brengen alvorens de uitbreiding te vormen. Controleer alle configuratiestappen voordat u begint om te bepalen welke entiteiten u moet instellen voor uw geval van gebruik.

Selecteer in de linkernavigatie de optie **[!UICONTROL Extensions]**. Selecteren **[!UICONTROL Configure]** op de kaart voor de [!DNL Pinterest] in de [!UICONTROL Installed]** tab.

![[!DNL Pinterest] extensie die wordt weergegeven in het dialoogvenster [!UICONTROL Install] tab met [!UICONTROL Configure] gemarkeerd.](../../../images/extensions/server/pinterest/configure.png)

Voer in het volgende scherm de [!UICONTROL Ads Account Id] en [!UICONTROL Conversion Access Token] die u eerder in [configuratiedetails](#configuration-details) sectie. Als u klaar bent, selecteert u **[!UICONTROL Save]**.

![De [!DNL Pinterest] [!UICONTROL Configure] scherm markeren [!UICONTROL Ads Account Id] en [!UICONTROL Conversion Access Token] invoervelden.](../../../images/extensions/server/pinterest/input.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen door:sturen regels die bepalen wanneer en hoe uw gebeurtenissen zullen worden verzonden naar [!DNL Pinterest].

Een nieuwe [regel](../../../ui/managing-resources/rules.md) in uw gebeurtenis die bezit door:sturen. Onder **[!UICONTROL Actions]** voegt u een nieuwe handeling toe en stelt u de extensie in op **[!UICONTROL Pinterest]**. Edge Network-gebeurtenissen verzenden naar [!DNL Pinterest], stelt u de **[!UICONTROL Action Type]** tot **[!UICONTROL Send Event].**

![De [!DNL Pinterest] [!UICONTROL Send Event] regel maken.](../../../images/extensions/server/pinterest/rule.png)

Na selectie, schijnen de extra controles om de gebeurtenis verder te vormen. U moet de [!DNL Pinterest] gebeurteniseigenschappen voor de gegevenselementen die u eerder hebt gemaakt.

### [!UICONTROL Event Data]

De volgende gebeurtenisgegevens worden vereist om de nieuwe regel te maken:

| Veldnaam | Beschrijving | Voorbeeld |
| --- | --- | --- | 
| [!UICONTROL Event Name] | Het type van de gebruikersgebeurtenis. Dit kan echter elk gebeurtenistype zijn, zodat u de [!DNL Pinterest Analytics] aanbevolen wordt [[!DNL Pinterest] gebeurteniscodes](https://help.pinterest.com/en/business/article/add-event-codes) | * uitchecken <br> * add_to_cart <br> * pagina_bezoek <br> * inschrijving <br> * [Door gebruiker gedefinieerde gebeurtenis] |
| [!UICONTROL Action Source] | De bron die aangeeft waar de conversiegebeurtenis heeft plaatsgevonden. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Event Time] | Dit verwijst naar de tijd van de gebeurtenis. De standaardtijdnotatie die wordt gebruikt, is UNIX, in de notatie `<seconds>.<miliseconds>` afhankelijk van uw lokale tijdzone. Raadpleeg voor meer informatie de [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 geeft 1433188255 seconden en 500 milliseconden na het tijdperk aan, of maandag 1 juni 2015, 7 juni:50:17:00 GMT. |
| [!UICONTROL Event ID] | Een unieke id-tekenreeks die deze gebeurtenis identificeert en kan worden gebruikt voor het verwijderen tussen gebeurtenissen die via de API voor conversie en Pinterest-tracking worden opgenomen. Zonder dit zullen de gegevens van de gebeurtenis waarschijnlijk dubbel worden geteld en zal de inflatie in metrische termen worden gerapporteerd. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | Een JSON-object dat aangepaste eigenschappen van de gebeurtenis bevat. Maak een keuze uit het opgeven van onbewerkte JSON of uit het gebruik van een vereenvoudigde set toetsinvoer. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![De [!DNL Pinterest] [!UICONTROL Event Data] gemarkeerd in de regelactie.](../../../images/extensions/server/pinterest/event-data.png)

De volgende gebeurteniseigenschappen kunnen worden geconfigureerd:

| Veldnaam | Beschrijving |
| --- | --- |
| URL van gebeurtenisbron | URL van de webconversiegebeurtenis. |
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
| [!UICONTROL Mobile Adverstising IDs] | Sha256 hashes of &quot;Google Advertising IDs&quot; (GAIDs) of &quot;Apple Identifier for Advertisers&quot; (IDFAs) van gebruikers | ebd543592.f2b7e1 |
| [!UICONTROL Client IP Address] | Het IP-adres van de gebruiker. Dit kan de IPv4- of IPv6-indeling hebben. Wordt gebruikt voor overeenkomsten. | 192.168.0.1 |
| [!UICONTROL Client User Agent] | De userAgent-tekenreeks van de webbrowser van de gebruiker. | Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | Een JSON-object dat andere klantgegevens bevat. Maak een keuze uit het opgeven van onbewerkte JSON of uit het gebruik van een vereenvoudigde set toetsinvoer. | { &quot;ph&quot;: &quot;122333445&quot; } |

![De [!DNL Pinterest] [!UICONTROL User Data] gemarkeerd in de regelactie.](../../../images/extensions/server/pinterest/user-data.png)

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
>Voordat u de gegevens naar de [!DNL Pinterest] API eindpunt, zal de uitbreiding de waarden van de volgende gebieden hakken en normaliseren: E-mail, Telefoonaantal, Voornaam, Achternaam, Geslacht, Geboortedatum, Stad, Staat, Postcode, Land, en Externe identiteitskaart De extensie verbergt de waarde van deze velden niet als er al een SHA256-tekenreeks aanwezig is.

### [!UICONTROL Custom Data]

De volgende aangepaste gegevens kunnen voor de regel worden ingevoerd:

| Veldnaam | Beschrijving |
| --- | --- |
| Valuta | De ISO-4217-valutacode. Indien dit niet wordt vermeld, [!DNL Pinterest] wordt standaard ingesteld op de valuta van de adverteerder die is ingesteld tijdens het maken van de account. |
| Waarde | Totale waarde van de gebeurtenis. Wordt geaccepteerd als een tekenreeks in de aanvraag. Dit wordt in een dubbel cijfer geparseerd. |
| Zoektekenreeks | De zoektekenreeks die betrekking heeft op de conversiegebeurtenis van de gebruiker. |
| Order-id | De bestellings-id. Verzenden `order_id` helpt [!DNL Pinterest] dedupliceer gebeurtenissen indien nodig. |
| Aantal producten | Het totale aantal producten van de gebeurtenis. Bijvoorbeeld het totale aantal objecten dat is aangeschaft tijdens een uitcheckgebeurtenis. |
| Inhoud-id&#39;s | Lijst (array) met product-id&#39;s. |
| Inhoud | Een lijst (array) met objecten die informatie over producten bevatten, zoals prijs en hoeveelheid. |

![De [!DNL Pinterest] [!UICONTROL Custom Data] gemarkeerd in de regelactie.](../../../images/extensions/server/pinterest/custom-data.png)

## Gegevens valideren binnen [!DNL Pinterest]

Zodra de gebeurtenis door:sturen regel is gecreeerd en uitgevoerd, bevestig of de gebeurtenis die werd verzonden naar [!DNL Pinterest] API wordt weergegeven zoals wordt verwacht in het dialoogvenster [!DNL Pinterest] UI.

Als de gebeurtenisinzameling en [!DNL Experience Platform] de integratie is voltooid, u ziet de gebeurtenissen in het [!DNL Pinterest] UI.

![De [!DNL Pinterest] gebeurtenismanager](../../../images/extensions/server/pinterest/event-history.png)

U kunt de [!DNL Pinterest] distributie van gebeurtenisgegevens.

![De [!DNL Pinterest] gegevensdistributie](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u de [!DNL Pinterest] gebeurtenis die uitbreiding in UI door:sturen. Raadpleeg de officiële documentatie voor meer informatie:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Overzicht van conversie-API](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
