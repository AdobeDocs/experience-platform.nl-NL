---
title: Extensie API voor volgende conversie
description: Leer hoe u de extensie Conversie-API NextDeurogebruikt om conversiegebeurtenissen te verzenden om de prestaties van uw reclamecampagnes te volgen.
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 1%

---


# [!DNL Nextdoor] Conversie API-extensie - Handboek

## Overzicht

[!DNL Nextdoor] is een sociale netwerkservice voor buurten die mensen verbindt met hun lokale gemeenschappen. Het is een platform waar buren kunnen communiceren, informatie delen, bijgewerkt blijven over lokale gebeurtenissen en nieuws, en objecten kopen en verkopen met anderen in hun gebied.

Gebruik de [[!DNL Nextdoor]  Uitbreiding van de Omzetting API &#x200B;](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API) om omzettingsgebeurtenissen naar [!DNL Nextdoor's] Conversie API direct te verzenden. Met deze extensie kunt u de prestaties van uw [!DNL Nextdoor] advertentiecampagnes bijhouden en meten door conversiegegevens op de server te verzenden.

Deze gids toont u hoe te om te installeren, te vormen en, de [!DNL Nextdoor] API uitbreiding van de Omzetting in uw gebeurtenis te gebruiken die [&#x200B; regels &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/tags/ui/rules) door:sturen.

## Vereisten {#prerequisites}

U hebt een geldig account voor [!DNL Nextdoor] Advertentiebeheer nodig om deze extensie te kunnen gebruiken. Als u reeds geen hebt, ga naar de [[!DNL Nextdoor Ads]  registratiepagina &#x200B;](https://ads.nextdoor.com/v2/signup) om uw rekening te registreren en tot stand te brengen.

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u Experience Platform wilt verbinden met [!DNL Nextdoor] , hebt u de volgende informatie nodig:

| Credentials | Beschrijving | Beveiligingsnotities |
| --- | --- | --- |
| Source-id voor gegevens | Uw unieke gegevensbron-id van [!DNL Nextdoor], die u in uw [!DNL Nextdoor Ads Manager] -account kunt vinden via de pagina Assets > Pixels en het genereren van een Volgende pixel. | Het is veilig om dit binnen uw organisatie te delen. |
| Toegangstoken | Het toegangstoken voor API-verificatie voor beveiligde communicatie. U kunt dit token genereren door u aan te melden bij uw [!DNL Nextdoor Ads Manager] -account en de API-instellingen te openen. | Houd dit token veilig, omdat het toegang biedt tot uw account. |

## De extensie [!DNL Nextdoor] installeren en configureren {#install}

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie als u de extensie wilt installeren. Selecteer op het tabblad **[!UICONTROL Catalog]** de **[!UICONTROL Nextdoor Conversion API Extension]** en selecteer vervolgens **[!UICONTROL Install]** .

![&#x200B; de uitbreidingscatalogus die [!DNL Nextdoor] uitbreidingskaart tonen die installeert benadrukt.](../../../images/extensions/server/nextdoor/install-extension.png)

Op het volgende scherm, ga de configuratiewaarden in u van uw [!DNL Nextdoor Ads Manager] produceerde:

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

Selecteer **[!UICONTROL Save]** als u klaar bent.

![[!DNL Nextdoor] configuratiescherm voor de [!DNL Nextdoor] conversie-API-extensie. &#x200B;](../../../images/extensions/server/nextdoor/configure.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis tot stand brengen die regels bepaalt wanneer en hoe uw gebeurtenissen worden verzonden naar [!DNL Nextdoor].

Creeer een nieuwe [&#x200B; regel &#x200B;](../../../ui/managing-resources/rules.md) in uw gebeurtenis door:sturen bezit. Voeg onder **[!UICONTROL Actions]** een nieuwe handeling toe en stel de extensie in op **[!UICONTROL Nextdoor Conversion API Extension]** . Als u Edge Network-gebeurtenissen naar [!DNL Nextdoor] wilt verzenden, stelt u de **[!UICONTROL Action Type]** in op **[!UICONTROL Report Web Conversions]** .

![&#x200B; het [!UICONTROL Report Web Conversions] actietype dat voor een [!DNL Nextdoor] regel in de Inzameling UI van Gegevens wordt geselecteerd.](../../../images/extensions/server/nextdoor/select-action.png)

Nadat u deze selectie hebt gemaakt, worden extra besturingselementen weergegeven waarmee u de gebeurtenis verder kunt configureren, zoals hieronder wordt beschreven. Nadat u de regel hebt voltooid, selecteert u **[!UICONTROL Keep Changes]** om deze op te slaan.

**hoofd-lichaam parameters**

Deze kernparameters definiëren uw conversiegebeurtenis:

| Parameter | Beschrijving | Gegevenstype | Vereist | Opties/Indeling | Voorbeeld |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | Geeft het type conversiegebeurtenis aan dat wordt bijgehouden. | Tekenreeks (vervolgkeuzelijst) | Vereist | <ul><li>Aanschaffen</li><li>Lood</li><li>Aanmelden</li><li>Toevoegen aan winkelwagentje</li><li>Afhandeling starten</li><li>Paginaweergave</li><li>Zoeken</li><li>Inhoud weergeven</li><li>Toevoegen aan Wishlist</li><li>Abonneren</li><li>Aangepast</li></li>Conversie 1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | Unieke id om dubbele gebeurtenisrapportage te voorkomen. Dit wordt automatisch gegenereerd als dit leeg is. | String | Optioneel | Unieke tekenreeks-id | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | Tijdstempel wanneer de conversiegebeurtenis heeft plaatsgevonden. Wordt standaard ingesteld op de huidige tijd als deze leeg wordt gelaten. | Geheel | Optioneel | Unix timestamp in seconden | `1703980800` (30 december 2023) |
| [!UICONTROL Action Source] | Kanaal of platform waar de conversie plaatsvond. | Tekenreeks (vervolgkeuzelijst) | Vereist | <ul><li>website</li><li>email</li><li>app</li><li>phone_call</li><li>chatten</li><li>physical_store</li><li>system_generated</li><li>overige</li></ul> | `website` |
| [!UICONTROL Data Source ID] | Overschrijf de algemene gegevensbron-id voor specifieke gebeurtenissen. Zal van config erven als verlaten leeg. | String | Optioneel | Alphanumeric-tekenreeks | `12345` |
| [!UICONTROL Action Source URL] | De specifieke URL waar de conversie heeft plaatsgevonden. | String | Optioneel | Volledige URL inclusief protocol | https://example.com/checkout/success |

**De parameters van de Privacy en van de naleving**

Gebruik deze parameters om ervoor te zorgen dat de privacy wordt nageleefd:

| Parameter | Beschrijving | Gegevenstype | Vereist | Waarden/indeling | Voorbeeld |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | Markering om gegevensgebruik voor privacynaleving te beperken. | Geheel | Optioneel | <ul><li>0 = Geen beperkingen</li><li>1 = Beperken</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | Landspecifieke beperkingen op gegevensverwerking. | Geheel | Optioneel | 1 = VS (andere codes kunnen worden ondersteund) | `1` |
| [!UICONTROL Restricted Data Usage (State)] | Statusspecifieke beperkingen voor gebruikers in de VS. | Geheel | Optioneel | 1000 = CA, 1001 = CO, enz. | `1000` |
| [!UICONTROL Test Event] | Hiermee markeert u de gebeurtenis als een test voor ontwikkeling/foutopsporing. | String | Optioneel | Een niet-lege tekenreeks | `test` |

**de informatieparameters van de Klant**

>[!IMPORTANT]
>
>U moet minstens één parameter van de klanteninformatie voor juiste gebeurtenisattributie en aanpassing verstrekken.

| Parameter | Beschrijving | Gegevenstype | Vereist | Indeling | Voorbeeld |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | E-mailadres van de klant voor overeenkomende identiteiten. | String | Minimaal één klantveld vereist | Platte tekst of SHA-256-hash | `user@example.com` |
| [!UICONTROL Phone Number] | Telefoonnummer van de klant voor identiteitsvergelijking. | String | Minimaal één klantveld vereist | E.164-indeling (hashed met SHA-256) | `+15551234567` |
| [!UICONTROL First Name] | Voornaam van klant voor verbeterde overeenkomst. | String | Minimaal één klantveld vereist | Platte tekst of SHA-256-hash | `John` |
| [!UICONTROL Last Name] | Achternaam van de klant voor verbeterde overeenkomst. | String | Minimaal één klantveld vereist | Platte tekst of SHA-256-hash | `Smith` |
| [!UICONTROL Date of Birth] | Geboortedatum van de klant voor demografische matching. | String | Optioneel | JJJMMDD (SHA-256 hashed) | `19900115` |
| [!UICONTROL Gender] | geslacht van de klant voor demografische doelwitten. | String | Optioneel | M/F/O (SHA-256 hashed) | `M` |
| [!UICONTROL External ID] | Uw interne klant-id. | String | Optioneel | Elke unieke tekenreeks | `customer_12345` |
| [!UICONTROL Street Address] | Adres van klant. | String | Optioneel | SHA-256 hashed | `123 Main Street` (hashed) |
| [!UICONTROL City] | Plaats van de klant. | String | Optioneel | SHA-256 hashed | `San Francisco` (hashed) |
| [!UICONTROL State] | Staat/provincie van de klant. | String | Optioneel | Code met twee letters (SHA-256 hashed) | `CA` (hashed) |
| [!UICONTROL Zip Code] | Postcode van klant. | String | Optioneel | Eerste 5 cijfers US (SHA-256 hashed) | `94102` (hashed) |
| [!UICONTROL Country] | Land van de klant. | String | Optioneel | ISO-3166-1 alpha-2 (SHA-256 hashed) | `US` (hashed) |
| [!UICONTROL Click ID] | Volgende klikidentificatie voor attributie. | String | Optioneel | Vastgelegd vanaf `ndclid` URL-parameter | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | IP-adres van het apparaat van de gebruiker. | String | Optioneel | IPv4- of IPv6-adres | `192.168.1.1` |
| [!UICONTROL Client User Agent] | De userAgent-tekenreeks van de browser. | String | Optioneel | Onbewerkte browseruser-agent-tekenreeks | `Mozilla/5.0 (Windows...)` |

**de parameters van de Douane**

Deze parameters bieden extra context voor uw conversiegebeurtenis:

| Parameter | Beschrijving | Gegevenstype | Vereist | Indeling | Voorbeeld |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | Totale waarde van de kooptransactie. | String | **VEREIST voor de gebeurtenissen van de Aankoop** | ISO 4217 Valuta + Bedrag (geen spaties) | `USD123.45` |
| [!UICONTROL Order ID] | Unieke transactie- of orderidentificatie. | String | Optioneel | Elke unieke tekenreeks | `order_12345` |
| [!UICONTROL Delivery Category] | Wijze van levering van product/dienst. | String | Optioneel | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | Gedetailleerde informatie over aangekochte producten. | String (JSON-array) | Optioneel | JSON-array van productobjecten | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**Mobiele toepassingsparameters**

U moet deze parameters opnemen wanneer `Action Source = 'APP'` :

| Parameter | Beschrijving | Gegevenstype | Vereist | Indeling | Voorbeeld |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | Id van mobiele toepassing. | String | **VEREIST VOOR APP gebeurtenissen** | <ul><li>Bundel-id (iOS)</li><li>Pakketnaam (Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | iOS App Tracking Transparency toestemmingsstatus. | String | **VEREIST VOOR APP gebeurtenissen** | Booleaanse tekenreeks | `true` |
| [!UICONTROL Platform] | Mobiel besturingssysteem. | String | **VEREIST VOOR APP gebeurtenissen** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | Versie van de mobiele toepassing. | String | **VEREIST VOOR APP gebeurtenissen** | Versietekenreeks zoals gedefinieerd door uw app | `2.0.0-beta` |

## Gebeurtenistypen {#event-types}

De volgende gebeurtenistypen worden ondersteund voor verschillende conversiescenario&#39;s:

| Gebeurtenisnaam | Type gebeurtenis | Beschrijving | Gebruiksscenario | Vereiste velden | Notities |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | Standard | Afgelopen kooptransactie. | E-commerceomzettingen | <ul><li>Gebeurtenisnaam</li><li>Orderwaarde</li><li>Klantgegevens</li></ul> | Het belangrijkste voor optimalisering van ROAS |
| [!UICONTROL Lead] | Standard | Loodgeneratie of onderzoek. | Formulierverzendingen, contactaanvragen | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Omzetting van hoge waarde voor B2B |
| [!UICONTROL Sign Up] | Standard | Gebruikersregistratie of het maken van een account. | Aanmelden voor nieuwsbrief, accountregistratie | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Top-funnel voor conversie |
| [!UICONTROL Add to Cart] | Standard | Product toegevoegd aan winkelwagentje. | E-commerce funnel tracking | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Midden-funnel-betrokkenheidssignaal |
| [!UICONTROL Initiate Checkout] | Standard | Afhandelingsproces gestart. | Inkoopintentie bijhouden | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Sterke indicator voor aankoopintentie |
| [!UICONTROL Page View] | Standard | Belangrijke bezochte pagina. | Inhoudsbetrokkenheid, pagina&#39;s landen | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Alleen gebruiken voor hoogwaardige pagina&#39;s |
| [!UICONTROL Search] | Standard | Zoeken uitgevoerd op de site. | Detectie van product/inhoud | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Geeft een actieve gebruikersbetrokkenheid aan |
| [!UICONTROL View Content] | Standard | Inhoud of product weergegeven. | Weergaven van productpagina&#39;s, betrokkenheid bij inhoud | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Nuttig voor hermarketingpubliek |
| [!UICONTROL Add to Wishlist] | Standard | Product toegevoegd aan wenslijst. | Toekomstige aankoopintentie | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Geeft sterk belang aan product |
| [!UICONTROL Subscribe] | Standard | Abonnement op service/nieuwsbrief. | Terugkerende inkomsten, betrokkenheid | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Waardeindicator voor hoge levenswaarde |
| [!UICONTROL Custom Conversion 1 - 10] | Aangepast | Bedrijfsspecifieke conversiegebeurtenis. | Uw eigen omzettingstype definiëren | <ul><li>Gebeurtenisnaam</li><li>Klantgegevens</li></ul> | Aanpassen voor unieke zakelijke acties |

## Integratie van gegevenselementen {#data-element}

Alle velden ondersteunen Adobe-elementen voor het doorsturen van gegevens. Selecteer het pictogram van het gegevenselement ![&#x200B; gegevenselementen &#x200B;](../../../images/extensions/server/nextdoor/data-element-icon.png) naast om het even welk gebied aan:

* **Uitgezochte Bestaande Elementen van Gegevens**: Uitgezocht van gegevenselementen die reeds zijn gecreeerd.
* **voegt Nieuwe Elementen van Gegevens** toe: Creeer en bepaal nieuwe gegevenselementen zoals nodig.
* **pas Dynamische Waarden** toe: bevolk gebieden met dynamische inhoud die uit uw website wordt voortgebracht.

## Best practices {#best-practices}

Volg de onderstaande aanbevolen procedures om de conversie nauwkeurig te volgen, de gegevenskwaliteit te verbeteren en de privacyregels na te leven. Deze aanbevelingen helpen u de effectiviteit van uw integratie van de conversie-API van [!DNL Nextdoor] te maximaliseren en uw advertentieprestaties te optimaliseren.

### Naleving van gegevenskwaliteit en privacy

Een correcte gegevensverwerking is van essentieel belang voor het maximaliseren van de nauwkeurigheid van conversietoewijzingen, terwijl de privacy van de gebruiker en de naleving van de regelgeving behouden blijven. Deze praktijken helpen ervoor zorgen uw klantengegevens correct worden geformatteerd, veilig worden verwerkt, en volgens privacyverordeningen behandeld.

* **Gebruik verenigbare gegevens die** formatteren: E-mail van het formaat, telefoonaantallen, en andere gegevens constant opmaken:

   * **Normalisatie van de E-mail**: Zet e-mails in kleine letters om, verklein whitespace, en verwijder punten uit [!DNL Gmail] adressen.
   * **het aantalnormalisering van de telefoon**: Het formaat van E.164 van het gebruik (+1234567890) voor internationale verenigbaarheid.
   * **normalisatie van het Adres**: Normaliseer straatafkortingen (St., Ave., Rd.), en verwijder om het even welke extra ruimten.
   * **het formatteren van de Naam**: Zet namen in kleine letters om, verwijder extra ruimten, en handvat constant speciale karakters.

* **Hash gevoelige gegevens**: Overweeg hashing gevoelige klantengegevens alvorens het te verzenden. Normaliseer altijd uw gegevens voordat u hasht om consistente hash-waarden te garanderen:

   * Gebruik SHA-256 hashing voor telefoonaantallen, adressen, en andere PII.
   * De extensie verbergt automatisch e-mails met onbewerkte tekst. U kunt beide indelingen verzenden.
   * De gegevens van de knoeiboel constant over al uw het volgen implementaties.
      * **Voorbeeld**: Normaliseer &quot;John@Example.COM&quot; → &quot;john@example.com&quot;alvorens het hakken.

* **verstrek volledige informatie**: Omvat zoveel klanteninformatie zoals mogelijk voor betere aanpassing:

   * Meerdere id&#39;s opnemen (e-mail + telefoon of e-mail + naam + adres) indien beschikbaar.
   * Gebruik externe klant-id&#39;s om conversiegebeurtenissen te koppelen aan uw CRM-gegevens.
   * Verstrek demografische gegevens (leeftijd, geslacht) indien beschikbaar en in overeenstemming met de privacywetgeving.

* **Beheer van de Toestemming**: Zorg ervoor u juiste toestemming voor gegevensinzameling hebt:

   * Voer juiste toestemmingsmechanismen uit alvorens klantengegevens te verzamelen.
   * De gebruikersvoorkeuren en verzoeken om gegevens te verwijderen worden gerespecteerd.
   * Gebruik de parameters voor beperkt gegevensgebruik voor gebruikers die hebben geweigerd.
   * **Middelen**:
      * [&#x200B; GDPR de Gids van de Naleving &#x200B;](https://gdpr.eu/compliance/)
      * [&#x200B; Vereisten van de Privacy CCPA &#x200B;](https://oag.ca.gov/privacy/ccpa)

* **Minimalisering van Gegevens**: Verzend slechts noodzakelijke gegevens voor omzetting het volgen:

   * Verzamel en verzend slechts gegevens die voor attributie en optimalisering essentieel zijn.
   * Controleer regelmatig de gegevensvelden die u verzendt en controleer deze.
   * Verwijder overbodige klantgegevens om het privacyrisico te beperken.

* **Gebruik nauwkeurige timestamps**: Zorg ervoor gebeurtenistimestamps voor juiste attributie nauwkeurig zijn.
   * Gebruik de werkelijke tijd op het moment dat de conversie heeft plaatsgevonden, niet op het moment dat u de gegevens hebt verwerkt.
   * Zorg ervoor dat tijdstempels de Unix-tijdperkindeling hebben (seconden sinds 1 januari 1970).
   * Zorg voor verschillen in tijdzone in uw tijdstempelberekeningen.

### Gebeurtenis dedupliceren

Voorkom dubbele conversiegebeurtenissen voor een nauwkeurige meting van de campagne en vermijd opgepompte prestatiemetriek. Voer juiste deduplicatie uit, zodat elke conversie maar één keer wordt geteld, zodat u over betrouwbare gegevens beschikt voor uw optimalisatiebeslissingen.

* **verstrek unieke gebeurtenis IDs**: Gebruik altijd unieke gebeurtenis IDs om dubbele omzettingen te verhinderen.
* **Gebruik verenigbare het noemen**: Pas verenigbare gebeurtenis toe die over uw implementatie noemend.

### Snelheidsbeperking

Voor de conversie-API van [!DNL Nextdoor] geldt een snelheidsbeperking. De huidige tariefgrens is **100 verzoeken/minuut** per adverteerder. Als u de snelheidslimiet overschrijdt, retourneert de API een `HTTP 429 Too Many Requests` foutcode.

## Conclusie {#conclusion}

De extensie [!DNL Nextdoor] Conversion API biedt een krachtige manier om conversies te volgen en de effectiviteit van uw [!DNL Nextdoor] -advertentiecampagnes te meten. Door deze handleiding te volgen en de beste werkwijzen te implementeren, kunt u ervoor zorgen dat uw advertenties nauwkeurig worden bijgehouden en geoptimaliseerd.

Voor de meest bijgewerkte informatie en extra middelen, bezoek [[!DNL Nextdoor Ads Manager] &#x200B;](https://ads.nextdoor.com).

## Volgende stappen {#next-steps}

In deze handleiding ziet u hoe u gebeurtenisgegevens aan de serverzijde naar [!DNL Nextdoor] verzendt met de [!DNL Nextdoor] Conversion API-extensie. Meer over gebeurtenis het door:sturen mogelijkheden in [!DNL Adobe Experience Platform] leren, zie de [&#x200B; gebeurtenis het door:sturen overzicht &#x200B;](../../../ui/event-forwarding/overview.md).
