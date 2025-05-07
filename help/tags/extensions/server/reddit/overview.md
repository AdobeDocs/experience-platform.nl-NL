---
title: Conversies-API-extensie bewerken
description: Leer hoe u de API-extensie Reddit Ads Conversions gebruikt om gebruikersinteractiegebeurtenissen te verzenden naar Reddit Ads voor gerichte advertenties.
last-substantial-update: 2025-05-1
source-git-commit: 603cc86892f518852552eaa2fe1bdeaa296137cf
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# [!DNL Reddit] Overzicht van conversie-API

Reddit is een platform voor sociale media met een diverse gebruikersbasis, waardoor het ideaal is voor adverteerders die zich richten op specifieke doelgroepen.

Gebruik de [[!DNL Reddit]  uitbreiding van Conversies API ](https://ads-api.reddit.com/docs/v2/#tag/Conversions-API) om de gebeurtenissen van de gebruikersinteractie te verzenden die in Adobe Experience Platform Edge Network aan [!DNL Reddit Ads] worden gevangen. Gebruik deze extensie om uw merk te helpen een publiek van meer dan 379 miljoen actieve gebruikers per week te bereiken, en om het gedrag van gebruikers beter te begrijpen en gerichte advertenties uit te voeren.

Lees deze gids om te leren hoe te installeren, te vormen en, de [!DNL Reddit] uitbreiding van Conversies API in uw gebeurtenis te gebruiken die [ regels ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules) door:sturen.

## Belangrijkste voordelen {#benefits}

Met de API-extensie Conversies bewerken kunt u:

- **Bereik uw publiek**: Sluit met meer dan 379 miljoen wekelijkse actieve gebruikers op [!DNL Reddit] aan.
- **analyseert gebruikersgedrag**: De gegevens van de gebruikersinteractie van de hefboomwerking om gedrag te begrijpen en campagnes te optimaliseren.
- **lever gerichte advertenties**: Looppas gepersonaliseerde reclame die op gebruikersinteractie wordt gebaseerd in Adobe Experience Platform wordt gevangen.

## Vereisten {#prerequisites}

U moet een geldig Reddit Ads-account hebben om deze extensie te kunnen gebruiken. Ga naar [[!DNL Reddit Ads]  registratiepagina ](https://business.reddithelp.com/s/article/Create-and-manage-your-Reddit-Ads-account) om een rekening te registreren en tot stand te brengen als u reeds geen hebt. Zodra u uw rekeningsopstelling hebt, [ verzoek toegang tot Adds API ](https://www.redditforbusiness.com/api-partnership).

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u de Experience Platform wilt verbinden met [!DNL Reddit] , hebt u de volgende invoeren nodig:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Pixel-id | De pixel-id is een unieke id die is gekoppeld aan uw [!DNL Reddit Ads] -account. Deze wordt gebruikt om gebruikersinteracties en conversiegebeurtenissen op uw website of app bij te houden. U kunt uw identiteitskaart van het Pixel in uw [!DNL Reddit Ads] [ rekening ](https://ads.reddit.com/accounts) vinden. | 123456789012 |
| Token voor toegang tot conversie | Uw token voor conversietoegang van [!DNL Reddit] . Verwijs naar [[!DNL Reddit]  Conversies API ](https://business.reddithelp.com/s/article/conversion-access-token) document voor begeleiding. <br> **u wordt slechts vereist om door dit proces te gaan eens aangezien dit teken niet verloopt.** | {YOUR_REDDIT_BEARER_TOKEN} |

## De extensie [!DNL Reddit] installeren en configureren {#install-configure}

Voer de volgende stappen uit om de API-extensie [!DNL Reddit] Conversies te installeren en te configureren:

1. Selecteer in de gebruikersinterface van de Experience Platform-gegevensverzameling de optie [!UICONTROL Extensions] in de linkernavigatie voor toegang tot de catalogus van [!UICONTROL Extensions] . Dan [ creeer een nieuwe gebeurtenis door:sturen bezit ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview#properties) of selecteer een bestaand bezit.
2. Navigeer naar **[!UICONTROL Extensions]** in het navigatievenster aan de linkerkant. Selecteer **[!UICONTROL Catalog]** en selecteer vervolgens de extensie **[!DNL Reddit]** .
   ![ de catalogus van de Uitbreidingen van Adobe Experience Platform met benadrukte reddit uitbreiding.](../../../images/extensions/server/reddit/reddit-extension.png)
3. Geef de volgende configuratiedetails op:
   - **identiteitskaart van het Pixel**: ga uw [!DNL Reddit Ads] identiteitskaart van het Pixel in.
   - **Token van de Toegang van de Omzetting**: Ga het teken in dat in uw [!DNL Reddit Ads] rekening wordt geproduceerd en selecteer **[!UICONTROL Save]** wanneer gebeëindigd.

     ![ de details van de Configuratie voor de Reddit uitbreiding van Conversies API, met inbegrip van gebieden voor identiteitskaart van het Pixel en Token van de Toegang van de Omzetting.](../../../images/extensions/server/reddit/reddit-capi-details.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Nadat u de gegevenselementen hebt ingesteld, maakt u regels voor het doorsturen van gebeurtenissen om te bepalen wanneer en hoe gebeurtenissen naar [!DNL Reddit Ads] worden verzonden.

1. Navigeer aan **Regels** in uw gebeurtenis door:sturen bezit en creeer een nieuwe [ regel ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules).
2. Onder **Acties**, voeg een nieuwe actie toe en plaats de uitbreiding aan **[!DNL Reddit CAPI]**.
3. Plaats het **Type van Actie** aan **verzendt Gebeurtenis**.
   ![ Gebeurtenis die regelconfiguratieinterface voor Reddit Conversies API uitbreiding door:sturen, met de benadrukte gebieden van het uitbreidings en actietype.](../../../images/extensions/server/reddit/reddit-rule.png)
4. Configureer de aanvullende besturingselementen voor uw gebeurtenis, zoals in de onderstaande tabel wordt getoond:

   | Veldnaam | Beschrijving | Voorbeeld |
   | --- | --- | --- |
   | `Event Name` | Geef de naam van de conversiegebeurtenis op. | `Purchase` |
   | `Event Type` | Bepaal het type van gebeurtenis dat a [ gesteund kan zijn reddit omzettingsgebeurtenis ](https://business.reddithelp.com/s/article/supported-conversion-events#supported-conversion-events) of douane. | `SignUp`, `MyCustomEvent` |
   | `Timestamp` | Geef de tijd van de gebeurtenis op in de ISO-indeling of in de epoche. | `2025-04-15T16:01:00.000Z`, `1744742460000` |
   | `Client Dedupe ID` | Voeg een unieke id toe voor deduplicatie. | `abc123` |
   | `Match Keys` | Inclusief gebruikers- en apparaat-id&#39;s voor attributie. | `{"email":"hashed_email@example.com", "phone":"hashed_phone"}` |
   | `Value` | Geef de monetaire waarde van de gebeurtenis op. | `99.99` |
   | `Currency Code` | Gebruik de ISO-4217-indeling voor de valuta. | `USD` |
   | `Units Sold` | Voer het aantal gekochte objecten in. | `3` |
   | `Country Code` | Geef het land op waar de gebeurtenis heeft plaatsgevonden. | `US` |
   | `Data Processing Options` | Voeg privacymarkeringen toe, zoals LDU (Beperkt gegevensgebruik). | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |
   | `Consent` | Geef de toestemming van de gebruiker voor het gebruik van advertentiegegevens. | `true` |

5. Selecteer **houden Veranderingen** om de regel te bewaren.

## Metagegevens gebeurtenis {#event-metadata}

Lees deze sectie voor een gedetailleerde specificatie van de gebeurtenismeta-gegevens en gebruikersgegevensgebieden, die u verzekeren de vereiste en facultatieve parameters voor het vormen van uw gebeurtenissen begrijpen. De weergegeven velden kunnen variëren, afhankelijk van het geselecteerde gebeurtenistype.

>[!NOTE]
>
>Om de beste resultaten van uw omzettingsgebeurtenissen te krijgen, zorg ervoor om alle gebieden te vullen wanneer vestiging [ dynamische productadvertenties ](https://business.reddithelp.com/s/article/dynamic-product-ads).

### Metagegevensvelden voor gebeurtenissen

![ de details van de Configuratie voor de Reddit uitbreiding van Conversies API, met inbegrip van gebieden voor identiteitskaart van het Pixel en Token van de Toegang van de Omzetting.](../../../images/extensions/server/reddit/reddit-event-metadata.png)

| Veldnaam | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Conversion ID` (vereist) | De unieke id voor de conversiegebeurtenis die wordt gebruikt voor deduplicatie. | `abc123` |
| `Item Count` | Het totale aantal items voor de conversiegebeurtenis. | `6` |
| `Currency` | De munt voor de waarde wordt verstrekt, in [ ISO-4217 ](https://www.iso.org/iso-4217-currency-codes.html) formaat. | `USD` |
| `Value` | De totale monetaire waarde van de conversiegebeurtenis, inclusief decimalen. | `1.23` |
| `Products` | Een JSON-array van objecten met details over de producten die aan de gebeurtenis zijn gekoppeld. Elk object moet minimaal een `id` bevatten. | `[{"id":"SKU123","name":"ProductName","category":"CategoryName"},{"id":"SKU456","name":"ProductName","category":"CategoryName"}]` |

### Gebruikersgegevensvelden

De volgende parameters zijn optioneel, maar worden wel aanbevolen:

| Veldnaam | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Email` (sterk aanbevolen) | Een gehashte of ongehashte e-mail van de gebruiker. | `example@email.com` |
| `External ID` | Een gehashte of ongehashte gebruiker-identiteitskaart van adverteerders | `customer12345` |
| `UUID` (sterk aanbevolen) | De id die door de Reddit Pixel op uw website wordt gegenereerd. | `1677712978045.b8f7eb7d-b357-437b-8bd3-e1c8166c7132` |
| `IP Address` (sterk aanbevolen) | Het apparaat-IP van de gebruiker. | `192.168.0.1` |
| `User Agent` (sterk aanbevolen) | De browser of app die door de gebruiker wordt gebruikt. | `Chrome/98.0.4758.102` |
| `IDFA` | Een hashed of unhashed Apple Identifier voor Advertisers. | `8A2E4F6D-0852-4B2A-B9D5-79334DE14B16` |
| `AAID` | Een hashed of unhashed Android Advertising ID. | `38400000-8cf0-11bd-b23e-10b96e40000d` |
| `Screen Width` | De breedte van de weergave van de gebruiker. | `1920` |
| `Screen Height` | De hoogte van de weergave van de gebruiker. | `1080` |
| `Data Processing Options` (JSON-indeling) | De privacyinstellingen van de gebruiker. Alleen LDU (beperkt gegevensgebruik) wordt ondersteund. | `{"modes":["LDU"],"country":"US","region":"US-NY"}` |

### Belangrijke overwegingen

Voordat gegevens naar [!DNL Reddit Ads] worden verzonden, worden de waarden van de volgende velden door de extensie gehasht en genormaliseerd: `Email` , `External ID` , `IDFA` en `AAID` . Deze waarden worden niet opnieuw ingekapseld in de extensie als deze al zijn gehasht in [!DNL SHA-256] .

## Valideren en implementeren {#validate-deploy}

Na het vormen van de uitbreiding en de regels, bevestig de integratie door gebeurtenisgegevens in de [[!DNL Reddit Ads]  Manager van Gebeurtenissen ](https://business.reddithelp.com/s/article/Events-Manager) te controleren. Gebruik de [ Score van de Kwaliteit van de Gelijke (MQS) ](https://business.reddithelp.com/s/article/match-quality-score) om de nauwkeurigheid en de betrouwbaarheid van uw signaalintegratie te evalueren.

Voor extra details op [!DNL Reddit Ads], bezoek de [ reddit documentatie van Advertenties ](https://ads.reddit.com/).

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, moet u nu weten hoe u de API-extensie [!DNL Reddit] Conversies kunt configureren en gebruiken. Voor meer informatie over gebeurtenis die mogelijkheden in Adobe Experience Platform door:sturen, verwijs naar de [ gebeurtenis die overzicht ](../../../ui/event-forwarding/overview.md) door:sturen of naar de volgende middelen:

- [ Aanpas van het Aandeel sleutels ](https://business.reddithelp.com/s/article/about-attribution-matching-signals) en [ gebeurtenismeta-gegevens ](https://business.reddithelp.com/s/article/about-event-metadata): Begrijp hoe te om sleutels en gebeurtenismeta-gegevens effectief te delen.
- [ Deduplicate gebeurtenissen ](https://business.reddithelp.com/s/article/event-deduplication): Verzeker nauwkeurige gebeurtenis het volgen door gebeurtenissen te dedupliceren.
- [ creeer een teken van de omzettoegang ](https://business.reddithelp.com/helpcenter/s/article/conversion-access-token): Volg de stappen om een token van de omzettoegang voor veilige API authentificatie tot stand te brengen.
