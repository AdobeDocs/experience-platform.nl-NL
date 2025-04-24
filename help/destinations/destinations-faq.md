---
keywords: bestemmingen; vragen; veelgestelde vragen; vk; bestemmingen vk
title: Veelgestelde vragen
description: Antwoorden op de meest gestelde vragen over Adobe Experience Platform-bestemmingen
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 0%

---

# Veelgestelde vragen {#faq}

## Overzicht {#overview}

In dit document worden antwoorden gegeven op veelgestelde vragen over Adobe Experience Platform-doelen. Voor vragen en het oplossen van problemen met betrekking tot andere [!DNL Experience Platform] diensten, met inbegrip van die over alle [!DNL Experience Platform] APIs worden ontmoet, gelieve te verwijzen naar de [ het oplossen van problemengids van Experience Platform ](../landing/troubleshooting.md).

## Algemene vragen over bestemmingen {#general}

### Waarom zie ik verschillende profieltellingen in Experience Platform UI en in de uitgevoerde Csv- dossiers?

+++Antwoord
Dit is een normaal gedrag vanwege de manier waarop Experience Platform segmentatie uitvoert.

Streaming segmentatie werkt het aantal profielen voor streaming publiek gedurende de dag bij, terwijl batchsegmentatie het aantal profielen voor batchgebruikers eenmaal om de 24 uur bijwerkt.

Wanneer het schema voor het exporteren van publiek afwijkt van het segmentatieschema, telt het profiel tussen de gebruikersinterface en het geëxporteerde [!DNL CSV] -bestand anders, vooral wanneer het gaat om streaming publiek.

Zie de [ documentatie van de Dienst van de Segmentatie ](../segmentation/home.md) voor meer details.
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

Nee, er is geen afhankelijkheid tussen de bestemming van Experience Platform en de klanteninstantie van het doelsysteem. Aan de ontvangende kant, is de enige aanwijzing dat het doelsysteem zou zien dat het ophield die publieksgegevens te ontvangen.

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

### Wat moet ik doen voordat ik het publiek in [!DNL Facebook Custom Audiences] kan activeren?

+++Antwoord
Voordat u uw publiek naar [!DNL Facebook] kunt sturen, moet u controleren of aan de volgende vereisten is voldaan:

* Voor uw [!DNL Facebook] -gebruikersaccount moet de **[!DNL Manage campaigns]** -machtiging zijn ingeschakeld voor de advertentieaccount die u wilt gebruiken.
* De **Adobe Experience Cloud** bedrijfsrekening moet als advertentiepartner in uw [!DNL Facebook Ad Account] worden toegevoegd. Gebruik `business ID=206617933627973` . Zie [ Partners aan Uw BedrijfsManager ](https://www.facebook.com/business/help/1717412048538897) in de documentatie Facebook voor details toevoegen.

  >[!IMPORTANT]
  >
  > Wanneer het vormen van de toestemmingen voor Adobe Experience Cloud, moet u **toelaten leidt campagnes** toestemming. Dit is vereist voor de [!DNL Adobe Experience Platform] -integratie.
* Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga hiertoe naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` , waar `accountID` uw [!DNL Facebook Ad Account ID] is.
+++

### Moet ik apps of pixels toevoegen aan mijn [!DNL Facebook] adverteerderaccount?

+++Antwoord
Nee. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.
+++

### Hoe lang duurt het voordat Facebook informatie uit Adobe Experience Platform verwerkt?

+++Antwoord
Vanaf maart 2021 heeft [!DNL Facebook Custom Audiences] een uur nodig om de gegevens te verwerken die zijn ontvangen van [!DNL Experience Platform] .
+++

### Kan ik [!DNL Facebook Custom Audiences] gebruiken voor doelgroepen in andere [!DNL Facebook] apps, zoals [!DNL Instagram] ?

+++Minder
U kunt de bestemming [!DNL Facebook Custom Audiences] gebruiken voor doelgroepen in de Facebook-reeks met apps die worden ondersteund door [!DNL Facebook Custom Audiences] , inclusief [!DNL Facebook] , [!DNL Instagram] , [!DNL Audience Network] en [!DNL Messenger] . De selectie van de app waarop adverteerders campagnes willen uitvoeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager] .
+++

### Wat is het verschil tussen de extensie [!DNL Facebook Custom Audiences] en [!DNL Facebook Pixel] ?

+++Antwoord
De [!DNL Facebook Custom Audiences] verbinding gebruikt [!DNL Experience Platform] identiteiten wanneer het verzenden van publiek naar [!DNL Facebook], terwijl de [[!DNL Facebook Pixel]  verbinding ](../destinations/catalog/advertising/facebook-pixel.md) [!DNL Facebook] pixel gebruikt die in een website wordt geïntegreerd.

Deze twee integraties zijn complementair; u kunt beide gebruiken om betere publieksdekking te verzekeren. U kunt bijvoorbeeld de extensie [!DNL Facebook Pixel] gebruiken voor het zoeken naar websitebezoekers die geen account hebben gemaakt, terwijl [!DNL Facebook Custom Audiences] u kan helpen bestaande klanten als doel in te stellen op basis van [!DNL Experience Platform] -identiteiten.
+++

### Biedt de integratie van Adobe Experience Platform met [!DNL Facebook Custom Audiences] ondersteuning voor het uitschakelen van gebruikers die niet langer in aanmerking komen voor deze toepassing?**

+++Antwoord
Ja, de integratie ondersteunt het verwijderen van gebruikers uit [!DNL Facebook Custom Audiences] wanneer ze niet langer in aanmerking komen.
+++

### Hoe moet ik de publieksgegevens hashen voordat ik deze naar [!DNL Facebook] verstuurt?

+++Antwoord
[!DNL Facebook] vereist dat er geen PII&#39;s (Personal Identified Information) worden verzonden. Daarom kan het publiek dat aan [!DNL Facebook] wordt geactiveerd van *gehakt* herkenningstekens, zoals e-mailadressen of telefoonaantallen worden afgevinkt.

Voor gedetailleerde verklaringen over identiteitskaart passende vereisten, zie [ identiteitskaart passende vereisten ](catalog/social/facebook.md#id-matching-requirements).
+++

### Welk type identiteiten kan ik activeren in [!DNL Facebook Custom Audiences]?

+++Antwoord
[!DNL Facebook Custom Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, gehashte telefoonnummers, [!DNL GAID] , [!DNL IDFA] en aangepaste externe id&#39;s.
+++

### Kan ik meerdere Facebook-doelen maken in de gebruikersinterface van Experience Platform voor afzonderlijke Facebook-accounts?

+++Antwoord
Ja. Een Facebook-bestemming in Experience Platform is 1:1 voor een advertentieaccount op Facebook. U kunt een aparte Facebook-bestemming maken voor elk Facebook-advertentieaccount in uw bedrijf. Volg het [ leerprogramma van de bestemmingsverbinding ](/help/destinations/ui/connect-destination.md) en verbind met een afzonderlijke rekening Facebook voor elke nieuwe bestemming Facebook in Experience Platform UI. Er is geen limiet voor het aantal Facebook-advertentieaccounts waarmee u verbinding kunt maken.
+++

## Google Customer Match {#google-customer-match}

### Waarom zie ik extra nummers toevoegen aan het einde van de publieksnamen in de Google-interface wanneer ik publiek exporteer naar Google Customer Match?

+++Antwoord
Google vereist dat publieksnamen uniek zijn. De aantallen die u ziet zijn [ tijdstempels van UNIX ](https://www.unixtimestamp.com/) en zij worden toegevoegd om de publieksnamen uniek te houden, als u het zelfde publiek aan veelvoudige bestemmingen van Google in kaart bracht.
+++

## Gekoppeld publiek gekoppeld aan {#linkedin}

### Moet ik apps of pixels toevoegen aan mijn [!DNL LinkedIn] adverteerderaccount?

+++Antwoord
Nee. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.
+++

### Wat moet ik doen voordat ik het publiek in [!DNL LinkedIn Matched Audiences] kan activeren?

+++Antwoord
Voordat u het doel van [!UICONTROL LinkedIn Matched Audience] kunt gebruiken, moet u ervoor zorgen dat uw [!DNL LinkedIn Campaign Manager] -account het machtigingsniveau [!DNL Creative Manager] of hoger heeft.

Leren hoe te om uw [!DNL LinkedIn Campaign Manager] gebruikerstoestemmingen uit te geven, zie [ toevoegen, uitgeven, en verwijderen de Toestemmingen van de Gebruiker op de Rekeningen van Advertising ](https://www.linkedin.com/help/lms/answer/5753) in de documentatie LinkedIn.
+++

### Hoe moet ik de publieksgegevens hashen voordat ik deze naar [!DNL LinkedIn] verstuurt?

+++Antwoord
[!DNL LinkedIn] vereist dat er geen PII&#39;s (Personal Identified Information) worden verzonden. Daarom kan het publiek dat aan [!DNL LinkedIn] wordt geactiveerd van *gehakt* herkenningstekens, zoals e-mailadressen of telefoonaantallen worden afgevinkt.

Voor gedetailleerde verklaringen over identiteitskaart passende vereisten, zie [ identiteitskaart passende vereisten ](catalog/social/linkedin.md#id-matching-requirements).
+++

### Welk type identiteiten kan ik activeren in [!DNL LinkedIn]?

+++Antwoord
[!DNL LinkedIn Matched Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, [!DNL GAID] en [!DNL IDFA] .

+++

## Zelfde pagina en volgende pagina personalisatie door de bestemmingen van Adobe Target en van de Douane Personalization {#same-next-page-personalization}

### Moet ik Experience Platform Web SDK gebruiken om publiek en attributen naar Adobe Target te verzenden?

+++Antwoord
Nr, [ SDK van het Web ](../web-sdk/home.md) wordt niet vereist om publiek aan [ Adobe Target ](catalog/personalization/adobe-target-connection.md) te activeren.

Nochtans, als [[!DNL at.js] ](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) in plaats van Web SDK wordt gebruikt, slechts wordt de volgende-zittingsverpersoonlijking gesteund.

Voor [ zelfde-pagina en volgende-pagina verpersoonlijking ](ui/activate-edge-personalization-destinations.md) gebruiksgevallen, moet u of [ SDK van het Web ](../web-sdk/home.md) of [ Edge Network API ](https://developer.adobe.com/data-collection-apis/docs/api/) gebruiken. Zie de documentatie bij [ activerend publiek aan randbestemmingen ](ui/activate-edge-personalization-destinations.md) voor meer implementatiedetails.
+++

### Is er een grens op het aantal attributen die ik van het Platform van de Gegevens van de Klant in real time naar Adobe Target of een bestemming van de Douane Personalization kan verzenden?

+++Antwoord
Ja, de gebruiksgevallen van dezelfde pagina en van de volgende pagina personalisatie ondersteunen maximaal 30 kenmerken per sandbox bij het activeren van het publiek naar Adobe Target- of Custom Personalization-doelen. Zie meer informatie over activeringsbegeleiding in de [ begeleidende documentatie ](guardrails.md#edge-destinations-activation).
+++

### Welke typen kenmerken worden ondersteund voor activering (bijvoorbeeld arrays, kaarten, enz.)?

+++Antwoord
Momenteel worden alleen statische kenmerken met één waarde ondersteund, zoals `person.name.firstName` . Arraykenmerken worden momenteel niet ondersteund.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Nadat ik een publiek in Experience Platform creeer, hoe lang zal het voor dat publiek om voor randsegmentatie gebruiksgevallen ter beschikking te stellen nemen?

+++Antwoord
De definities van het publiek worden verspreid aan [ Edge Network ](../web-sdk/home.md) in tot één uur. Als een publiek echter binnen dit eerste uur wordt geactiveerd, kunnen sommige bezoekers die voor het publiek in aanmerking zouden zijn gekomen, worden overgeslagen.
+++

### Waar zie ik de geactiveerde kenmerken in Adobe Target?

+++Antwoord
De attributen zullen beschikbaar in Doel in [ JSON ](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) en [ HTML ](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html) aanbiedingen zijn te gebruiken.
+++

### Kan ik een bestemming zonder een gegevensstroom tot stand brengen en dan een gegevensstroom aan de zelfde bestemming op een recentere punt toevoegen?

+++Antwoord
Dit wordt momenteel niet gesteund door de Doelen UI. Neem contact op met uw Adobe-vertegenwoordiger als u in dit geval hulp nodig hebt.
+++

### Wat gebeurt er als ik een Adobe Target-bestemming verwijder?

+++Antwoord
Wanneer u een doel verwijdert, worden alle soorten publiek en kenmerken die onder het doel zijn toegewezen, uit Adobe Target verwijderd en uit de Edge Network verwijderd.
+++

### Werkt de integratie met de Edge Network API?

+++Antwoord
Ja, de Edge Network API werkt met de Custom Personalization-bestemming. Aangezien profielkenmerken gevoelige gegevens kunnen bevatten, vereist de aangepaste Personalization-bestemming dat u de Edge Network API voor gegevensverzameling gebruikt om deze gegevens te beveiligen. Voorts moeten alle API vraag in een [ voor authentiek verklaarde context ](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/) worden gemaakt.
+++

### Ik kan slechts één samenvoegbeleid hebben dat actief-op-rand is. Kan ik een publiek opbouwen dat een ander samenvoegbeleid gebruikt en ze nog steeds naar Adobe Target sturen als streaming publiek?

+++Antwoord
Nee. Al publiek dat u aan Adobe Target wilt activeren moet een actief-op-rand [ samenvoegbeleid ](../profile/merge-policies/ui-guide.md) gebruiken.
+++

### Worden de Etikettering en de Handhaving van het Gebruik van Gegevens (DULE) en het Beleid van de Toestemming afgedwongen?

+++Antwoord
Ja. Het [ Beheers en Toestemmingsbeleid van Gegevens ](../data-governance/home.md) creeerde en verbonden aan de geselecteerde marketing acties zullen de activering van de geselecteerde attributen bepalen.
+++

### Zijn de [!DNL Adobe Target] en [!DNL Custom Personalization] bestemmingen [!DNL HIPAA] compatibel?

+++Antwoord
[!DNL Adobe Target] is niet [!DNL HIPPA] - volgzaam met [[!DNL Adobe Healthcare Shield] ](https://business.adobe.com/solutions/industries/healthcare.html). Klanten dienen met hun eigen juridische teams na te gaan of [!DNL HIPPA] gereed is voor aangepaste optimalisatiekanalen voordat ze de randaanpassing via [!DNL Adobe Target] of de [!DNL Custom Personalization] -doelen gebruiken.

Wanneer het beheer van het toestemmingsbeleid op schaal moet worden toegepast, moeten klanten [!DNL Adobe Privacy & Security Shield] kopen. [!DNL Adobe Privacy & Security Shield] -functies worden verkocht als een geavanceerde suite van mogelijkheden en worden mogelijk niet afzonderlijk aangeschaft.

Deze dienst omvat klant-beheerde sleutels en verhoogde drempels om de levenscyclus van klantengegevens te beheren.

De [!DNL Adobe Target] en [!DNL Custom Personalization] bestemmingen zijn geïntegreerd met de [ Etiketten van het Gebruik van de Gegevens van Experience Platform ](../data-governance/labels/overview.md) en de [ Dienst van de Handhaving van het Beleid van de Toestemming ](../data-governance/enforcement/overview.md). Deze functies zijn beschikbaar voor alle klanten.




+++

