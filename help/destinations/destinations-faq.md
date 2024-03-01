---
keywords: bestemmingen; vragen; veelgestelde vragen; vk; bestemmingen vk
title: Veelgestelde vragen
description: Antwoorden op de meest gestelde vragen over Adobe Experience Platform-bestemmingen
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: dff460f0b0d365d3d643744544642d9f9488e18a
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 2%

---

# Veelgestelde vragen {#faq}

## Overzicht {#overview}

In dit document worden antwoorden gegeven op veelgestelde vragen over Adobe Experience Platform-doelen. Voor vragen en problemen met betrekking tot andere [!DNL Platform] services, inclusief de services die in alle [!DNL Platform] API&#39;s, raadpleeg de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

## Algemene vragen over bestemmingen {#general}

### Waarom zie ik verschillende profieltellingen in het Experience Platform UI en in de uitgevoerde Csv- dossiers?

+++Antwoord Dit is een normaal gedrag toe te schrijven aan de manier waarop het Experience Platform segmentatie uitvoert.

Streaming segmentatie werkt het aantal profielen voor streaming publiek gedurende de dag bij, terwijl batchsegmentatie het aantal profielen voor batchgebruikers eenmaal om de 24 uur bijwerkt.

Wanneer het programma voor publieksexport afwijkt van het segmentatieschema, telt het profiel tussen de gebruikersinterface en het geëxporteerde bestand [!DNL CSV] Het bestand zal anders zijn, vooral wanneer het gaat om streaming publiek.

Zie de [Documentatie voor segmentatieservice](../segmentation/home.md) voor meer informatie .
+++

### Waarom zie ik lage gelijke tarieven na het deactiveren en het opnieuw activeren van een bijgewerkt publiek aan de zelfde bestemming?

+++Antwoord

De deactivering en van een publiek van een het stromen bestemming teweegbrengen geen backfill op publieksheractivering aan de zelfde het stromen bestemming teweeg.

**Voorbeeld**

U activeerde een publiek dat uit 10 profielen bestaat aan een het stromen bestemming.

Nadat u het publiek hebt geactiveerd, realiseert u zich dat u de publieksconfiguratie wilt wijzigen, zodat u het publiek deactiveert en de bevolkingscriteria wijzigt, wat leidt tot een populatie van 100 profielen.

U activeert het bijgewerkte publiek opnieuw naar dezelfde bestemming, maar aangezien er geen backfill geactiveerd is, ontvangt uw bestemming niet de aanvullende 90 profielen.

**Oplossing**

Om ervoor te zorgen dat alle profielen naar uw bestemming worden verzonden, moet u een nieuw publiek met de nieuwe configuratie tot stand brengen, en dan het activeren aan uw bestemming.

+++

### Wanneer een publiek van een bestemming wordt verwijderd, is er om het even welk signaal dat naar de bestemming wordt verzonden erop wijst die dat het publiek wordt verwijderd?

+++Antwoord

Nr, is er geen gebiedsdeel tussen de bestemming van het Experience Platform en de klanteninstantie van het doelsysteem. Aan de ontvangende kant, is de enige aanwijzing dat het doelsysteem zou zien dat het ophield die publieksgegevens te ontvangen.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Wat moet ik doen voordat ik publiek kan activeren [!DNL Facebook Custom Audiences]?

+++Antwoord Voordat u uw publiek naar kunt sturen [!DNL Facebook]voldoet aan de volgende vereisten:

* Uw [!DNL Facebook] gebruikersaccount moet de **[!DNL Manage campaigns]** Toestemming ingeschakeld voor de advertentie-account die u wilt gebruiken.
* De **Adobe Experience Cloud** bedrijfsaccount moet worden toegevoegd als advertentiepartner in uw [!DNL Facebook Ad Account]. Gebruik `business ID=206617933627973`. Zie [Partners toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) in de documentatie van Facebook voor meer informatie.

  >[!IMPORTANT]
  >
  > Wanneer u de machtigingen voor Adobe Experience Cloud configureert, moet u de optie **Campagnes beheren** toestemming. Dit is nodig voor de [!DNL Adobe Experience Platform]-integratie.
* Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga daarvoor naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waarbij `accountID` uw [!DNL Facebook Ad Account ID] is.
+++

### Moet ik apps of pixels toevoegen aan mijn [!DNL Facebook] adverteerderaccount?

+++Antwoord nr. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.
+++

### Hoe lang duurt het voor Facebook informatie uit Adobe Experience Platform verwerkt?

+++Antwoord per maart 2021, [!DNL Facebook Custom Audiences] heeft tot een uur nodig om informatie te verwerken die is ontvangen van [!DNL Platform].
+++

### Kan ik gebruiken [!DNL Facebook Custom Audiences] voor doelgroepen in andere [!DNL Facebook] apps, zoals [!DNL Instagram]?

+++Minder stroom U kunt de opdracht [!DNL Facebook Custom Audiences] doel voor doelgroepen in Facebook-apps die worden ondersteund door [!DNL Facebook Custom Audiences], inclusief [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], en [!DNL Messenger]. De selectie van de app waarop adverteerders campagnes willen uitvoeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager].
+++

### Wat is het verschil tussen [!DNL Facebook Custom Audiences] verbinding en [!DNL Facebook Pixel] uitbreiding?

++ beantwoord [!DNL Facebook Custom Audiences] verbinding gebruikt [!DNL Platform] identiteiten bij het versturen van publiek naar [!DNL Facebook], terwijl de [[!DNL Facebook Pixel] verbinding](../destinations/catalog/advertising/facebook-pixel.md) gebruikt de [!DNL Facebook] pixel geïntegreerd in een website.

Deze twee integraties zijn complementair; u kunt beide gebruiken om te zorgen voor een betere doelgroepdekking. U kunt bijvoorbeeld de opdracht [!DNL Facebook Pixel] uitbreiding voor potentiële websitebezoekers die geen account hebben gemaakt, terwijl [!DNL Facebook Custom Audiences] kan u helpen bestaande klanten richten, gebaseerd op [!DNL Platform] identiteiten.
+++

### Wordt Adobe Experience Platform geïntegreerd met [!DNL Facebook Custom Audiences] gebruikers die niet langer in aanmerking komen voor de kwalificatie van een publiek ondersteunen?**

++ + Ja beantwoorden, de integratie ondersteunt het verwijderen van gebruikers uit [!DNL Facebook Custom Audiences] wanneer zij niet langer in aanmerking komen.
+++

### Hoe moet ik de publieksgegevens hashen voordat ik ze naar [!DNL Facebook]?

+++Antwoord
[!DNL Facebook] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL Facebook] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Zie voor gedetailleerde uitleg over de vereisten voor ID-matching [Vereisten voor id-afstemming](catalog/social/facebook.md#id-matching-requirements).
+++

### Welk type identiteiten kan ik activeren? [!DNL Facebook Custom Audiences]?

+++Antwoord
[!DNL Facebook Custom Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, gehashte telefoonnummers, [!DNL GAID], [!DNL IDFA]en aangepaste externe id&#39;s.
+++

### Kan ik meerdere Facebook-doelen maken in de interface van het platform voor afzonderlijke Facebook-accounts?

++ + Antwoord Ja. Een Facebook-bestemming in Experience Platform is 1:1 voor een advertentieaccount in Facebook. U kunt een aparte Facebook-bestemming maken voor elke Facebook-advertentieaccount in uw bedrijf. Volg de [zelfstudie over doelverbinding](/help/destinations/ui/connect-destination.md) en maak verbinding met een aparte Facebook-account voor elke nieuwe Facebook-bestemming in de interface van het platform. Er is geen limiet voor het aantal Facebook-advertentieaccounts waarmee u verbinding kunt maken.
+++

## Google Customer Match {#google-customer-match}

### Waarom zie ik extra nummers toevoegen aan het einde van de publieksnamen in de Google-interface wanneer ik publiek exporteer naar Google Customer Match?

+++Antwoord Google vereist dat publieksnamen uniek zijn. De getallen die u ziet [UNIX-tijdstempels](https://www.unixtimestamp.com/) en worden toegevoegd om de publieksnamen uniek te houden, als u het zelfde publiek aan veelvoudige bestemmingen van Google in kaart bracht.
+++

## LinkedIn-publiek met overeenkomst {#linkedin}

### Moet ik apps of pixels toevoegen aan mijn [!DNL LinkedIn] adverteerderaccount?

+++Antwoord nr. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.
+++

### Wat moet ik doen voordat ik publiek kan activeren [!DNL LinkedIn Matched Audiences]?

+++Antwoord Voordat u de [!UICONTROL LinkedIn Matched Audience] doel, zorg ervoor uw [!DNL LinkedIn Campaign Manager] account bevat [!DNL Creative Manager] machtigingsniveau of hoger.

Leren hoe u uw [!DNL LinkedIn Campaign Manager] gebruikersmachtigingen, zie [Gebruikersmachtigingen toevoegen, bewerken en verwijderen voor advertentieaccounts](https://www.linkedin.com/help/lms/answer/5753) in de documentatie van LinkedIn.
+++

### Hoe moet ik de publieksgegevens hashen voordat ik ze naar [!DNL LinkedIn]?

+++Antwoord
[!DNL LinkedIn] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL LinkedIn] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Zie voor gedetailleerde uitleg over de vereisten voor ID-matching [Vereisten voor id-afstemming](catalog/social/linkedin.md#id-matching-requirements).
+++

### Welk type identiteiten kan ik activeren? [!DNL LinkedIn]?

+++Antwoord
[!DNL LinkedIn Matched Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails; [!DNL GAID], en [!DNL IDFA].

+++

## Zelfde pagina en volgende-paginagrootte door de bestemmingen van de Aanpassing van Adobe Target en van de Aanpassing {#same-next-page-personalization}

### Moet ik het Web SDK van het Experience Platform gebruiken om publiek en attributen naar Adobe Target te verzenden?

++ + antwoordnr., [Web SDK](../edge/home.md) is niet vereist om het publiek te activeren op [Adobe Target](catalog/personalization/adobe-target-connection.md).

Als echter [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) wordt gebruikt in plaats van Web SDK, slechts wordt de volgende-zittingsverpersoonlijking gesteund.

Voor [personalisatie op dezelfde pagina en op de volgende pagina](ui/activate-edge-personalization-destinations.md) gebruik gevallen, moet u of gebruiken [Web SDK](../edge/home.md) of de [Edge Network Server-API](../server-api/overview.md). Zie de documentatie op [activeren van publiek naar randbestemmingen](ui/activate-edge-personalization-destinations.md) voor meer details over de implementatie.
+++

### Is er een limiet voor het aantal kenmerken dat ik kan verzenden van Real-time Customer Data Platform naar Adobe Target of een aangepaste persoonlijke bestemming?

++ Antwoord ja, zelfde-pagina en volgende-pagina verpersoonlijkingsgebruiksgevallen steunen een maximum van 30 attributen per zandbak, wanneer het activeren van publiek aan Adobe Target of de bestemmingen van de Aanpassing van de Aanpassing. Meer informatie over activeringsinstructies vindt u in de [begeleidende documentatie](guardrails.md#edge-destinations-activation).
+++

### Welke typen kenmerken worden ondersteund voor activering (bijvoorbeeld arrays, kaarten, enz.)?

+++Antwoord Momenteel worden alleen statische kenmerken met één waarde ondersteund, zoals `person.name.firstName`. Arraykenmerken worden momenteel niet ondersteund.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Nadat ik een publiek in Experience Platform creeer, hoe lang zal het voor dat publiek beschikbaar zijn om van de randsegmentatie te gebruiken gevallen?

+++De definities van het Publiek van het Antwoord worden verspreid aan [Edge Network](../edge/home.md) binnen een uur. Als een publiek echter binnen dit eerste uur wordt geactiveerd, kunnen sommige bezoekers die voor het publiek in aanmerking zouden zijn gekomen, worden overgeslagen.
+++

### Waar zie ik de geactiveerde kenmerken in Adobe Target?

+++Antwoordkenmerken zijn beschikbaar voor gebruik in Doel [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) en [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html) voorstellen.
+++

### Kan ik een bestemming zonder een gegevensstroom tot stand brengen en dan een gegevensstroom aan de zelfde bestemming op een recentere punt toevoegen?

+++Antwoord Dit wordt momenteel niet gesteund door de Doelen UI. Neem contact op met uw Adobe als u in dit geval hulp nodig hebt.
+++

### Wat gebeurt er als ik een Adobe Target-bestemming verwijder?

+++Antwoord Wanneer u een bestemming schrapt, worden alle publiek en attributen die onder de bestemming in kaart worden gebracht geschrapt van Adobe Target en zij worden ook verwijderd uit het Netwerk van de Rand.
+++

### Werkt de integratie met de Edge Network Server-API?

++ Antwoord ja, de Server API van het Netwerk van Edge werkt met de bestemming van de Aangepaste Personalisatie. Aangezien profielattributen gevoelige gegevens kunnen bevatten, vereist de bestemming van de Aangepaste Aanpassing u om de Server API van het Netwerk van de Rand voor gegevensinzameling te gebruiken. Bovendien moeten alle API-aanroepen worden uitgevoerd in een [geverifieerde context](../server-api/authentication.md).
+++

### Ik kan slechts één samenvoegbeleid hebben dat actief-op-rand is. Kan ik een publiek opbouwen dat een ander samenvoegbeleid gebruikt en ze nog steeds naar Adobe Target sturen als streaming publiek?

+++Antwoord nr. Alle soorten publiek die u naar Adobe Target wilt activeren, moeten een &#39;active-on-edge&#39; gebruiken [samenvoegingsbeleid](../profile/merge-policies/ui-guide.md).
+++

### Worden de Etikettering en de Handhaving van het Gebruik van Gegevens (DULE) en het Beleid van de Toestemming afgedwongen?

++ + Antwoord Ja. De [Beleid inzake gegevensbeheer en instemming](../data-governance/home.md) die zijn gemaakt en gekoppeld aan de geselecteerde marketingacties, worden toegepast op de activering van de geselecteerde kenmerken.
+++

### zijn [!DNL Adobe Target] en [!DNL Custom Personalization] bestemmingen [!DNL HIPAA]-compatibel?

+++Antwoord
[!DNL Adobe Target] is niet [!DNL HIPPA]-compatibel met [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). Klanten moeten met hun eigen juristen controleren of [!DNL HIPPA]-gereedheid voor aangepaste optimalisatiekanalen voordat randvervorming wordt gebruikt via [!DNL Adobe Target] of de [!DNL Custom Personalization] bestemmingen.

Voor gebruiksgevallen waarbij het beheer van het toestemmingsbeleid op schaal moet worden toegepast, moeten klanten [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] worden verkocht als een geavanceerde suite van mogelijkheden en worden mogelijk niet afzonderlijk aangeschaft.

Deze dienst omvat klant-beheerde sleutels en verhoogde drempels om de levenscyclus van klantengegevens te beheren.

De [!DNL Adobe Target] en [!DNL Custom Personalization] de bestemmingen zijn geïntegreerd met de [Labels voor gegevensgebruik van Experience Platforms](../data-governance/labels/overview.md) en de [Toegestane beleidshandhavingsdienst](../data-governance/enforcement/overview.md). Deze functies zijn beschikbaar voor alle klanten.




+++

