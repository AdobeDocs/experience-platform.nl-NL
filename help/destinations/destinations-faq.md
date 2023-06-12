---
keywords: bestemmingen; vragen; veelgestelde vragen; faq; bestemmingen - vk
title: Veelgestelde vragen
description: Antwoorden op de meest gestelde vragen over Adobe Experience Platform-bestemmingen
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 784c529691f2f550176080474f5091bfb1b84279
workflow-type: tm+mt
source-wordcount: '1393'
ht-degree: 2%

---

# Veelgestelde vragen {#faq}

## Overzicht {#overview}

Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform-doelen. Voor vragen en problemen met betrekking tot andere problemen [!DNL Platform] services, inclusief de services die in alle [!DNL Platform] API&#39;s, raadpleeg de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

## Algemene vragen over bestemmingen {#general}

### Waarom zie ik verschillende profieltellingen in het Experience Platform UI en in de uitgevoerde Csv- dossiers?

+++Antwoord Dit is een normaal gedrag toe te schrijven aan de manier waarop het Experience Platform segmentatie uitvoert.

De het stromen segmentatie werkt het profielaantal voor het stromen segmenten door de dag bij, terwijl de partijsegmentatie de profieltelling voor partijsegmenten eens om de 24 uur bijwerkt.

Wanneer het segment uitvoerschema van het segmenteringsprogramma verschilt, telt het profiel tussen UI en geëxporteerde [!DNL CSV] Het bestand is anders, vooral wanneer het gaat om streaming segmenten.

Zie de [Documentatie voor segmentatieservice](../segmentation/home.md) voor meer informatie .
+++

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Wat moet ik doen voordat ik publiek kan activeren [!DNL Facebook Custom Audiences]?

+++Antwoord alvorens u uw publiekssegmenten kunt verzenden naar [!DNL Facebook]voldoet aan de volgende vereisten:

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

+++Minder stroom U kunt de opdracht [!DNL Facebook Custom Audiences] doel voor doelgroepen in Facebook-apps die worden ondersteund door [!DNL Facebook Custom Audiences], met inbegrip van [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], en [!DNL Messenger]. De selectie van de app waarop adverteerders campagnes willen uitvoeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager].
+++

### Wat is het verschil tussen [!DNL Facebook Custom Audiences] verbinding en [!DNL Facebook Pixel] uitbreiding?

++ beantwoord [!DNL Facebook Custom Audiences] verbinding gebruikt [!DNL Platform] identiteiten bij het versturen van publiek naar [!DNL Facebook], terwijl de [[!DNL Facebook Pixel] verbinding](../destinations/catalog/advertising/facebook-pixel.md) gebruikt de [!DNL Facebook] pixel geïntegreerd in een website.

Deze twee integraties zijn complementair; u kunt beide gebruiken om te zorgen voor een betere doelgroepdekking. U kunt bijvoorbeeld de opdracht [!DNL Facebook Pixel] uitbreiding voor potentiële websitebezoekers die geen account hebben gemaakt, terwijl [!DNL Facebook Custom Audiences] kan u helpen bestaande klanten richten, die op [!DNL Platform] identiteiten.
+++

### Wordt Adobe Experience Platform geïntegreerd met [!DNL Facebook Custom Audiences] gebruikers die niet langer in aanmerking komen voor de kwalificatie van een publiek ondersteunen?**

++ + Ja beantwoorden, de integratie ondersteunt het verwijderen van gebruikers uit [!DNL Facebook Custom Audiences] wanneer zij niet langer in aanmerking komen.
+++

### Hoe moet ik de publieksgegevens hashen voordat ik ze naar [!DNL Facebook]?

+++Antwoord
[!DNL Facebook] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL Facebook] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Voor gedetailleerde uitleg over de vereisten voor ID-matching raadpleegt u [Vereisten voor id-afstemming](catalog/social/facebook.md#id-matching-requirements).
+++

### Welk type identiteiten kan ik activeren? [!DNL Facebook Custom Audiences]?

+++Antwoord
[!DNL Facebook Custom Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, gehashte telefoonnummers, [!DNL GAID], [!DNL IDFA]en aangepaste externe id&#39;s.
+++

### Kan ik veelvoudige bestemmingen van Facebook in Platform UI voor afzonderlijke rekeningen van Facebook tot stand brengen?

++ + Antwoord Ja. Een Facebook-bestemming in Experience Platform is 1:1 voor een advertentieaccount in Facebook. U kunt een aparte Facebook-bestemming maken voor elke Facebook-advertentieaccount in uw bedrijf. Volg de [zelfstudie over doelverbinding](/help/destinations/ui/connect-destination.md) en maak verbinding met een aparte Facebook-account voor elke nieuwe Facebook-bestemming in de gebruikersinterface van het Platform. Er is geen limiet voor het aantal Facebook-advertentieaccounts waarmee u verbinding kunt maken.
+++

## Google Customer Match {#google-customer-match}

### Wanneer het uitvoeren van segmenten aan de Gelijke van de Klant van Google, waarom zie ik extra aantallen aan het eind van de segmentnamen in de interface van Google worden toegevoegd?

+++Antwoord Google vereist dat segmentnamen uniek zijn. De getallen die u ziet [UNIX-tijdstempels](https://www.unixtimestamp.com/) en ze worden toegevoegd om de segmentnamen uniek te houden, als u hetzelfde segment toewees aan meerdere Google-doelen.
+++

## linkedIn-doelgroepen {#linkedin}

### Moet ik apps of pixels toevoegen aan mijn [!DNL LinkedIn] adverteerderaccount?

+++Antwoord nr. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.
+++

### Wat moet ik doen voordat ik publiek kan activeren [!DNL LinkedIn Matched Audiences]?

+++Antwoord Voordat u de [!UICONTROL LinkedIn Matched Audience] doel, zorg ervoor uw [!DNL LinkedIn Campaign Manager] account bevat [!DNL Creative Manager] machtigingsniveau of hoger.

Meer informatie over het bewerken van uw [!DNL LinkedIn Campaign Manager] gebruikersmachtigingen, zie [Gebruikersmachtigingen toevoegen, bewerken en verwijderen voor advertentieaccounts](https://www.linkedin.com/help/lms/answer/5753) in de documentatie van LinkedIn.
+++

### Hoe moet ik de publieksgegevens hashen voordat ik ze naar [!DNL LinkedIn]?

+++Antwoord
[!DNL LinkedIn] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL LinkedIn] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Voor gedetailleerde uitleg over de vereisten voor ID-matching raadpleegt u [Vereisten voor id-afstemming](catalog/social/linkedin.md#id-matching-requirements).
+++

### Welk type identiteiten kan ik activeren? [!DNL LinkedIn]?

+++Antwoord
[!DNL LinkedIn Matched Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, [!DNL GAID], en [!DNL IDFA].
+++

## Zelfde pagina en volgende-paginagrootte door de bestemmingen van de Aanpassing van Adobe Target en van de Aanpassing {#same-next-page-personalization}

### Moet ik het Web SDK van het Experience Platform gebruiken om publiek en attributen naar Adobe Target te verzenden?

++ + antwoordnr., [Web SDK](../edge/home.md) is niet vereist om het publiek te activeren op [Adobe Target](catalog/personalization/adobe-target-connection.md).

Als [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=en) wordt gebruikt in plaats van Web SDK, slechts wordt de volgende-zittingsverpersoonlijking gesteund.

Voor [personalisatie op dezelfde pagina en op de volgende pagina](ui/activate-edge-personalization-destinations.md) gebruik gevallen, moet u of [Web SDK](../edge/home.md) of de [Edge Network Server-API](../server-api/overview.md). Zie de documentatie op [activeren van publiek naar randbestemmingen](ui/activate-edge-personalization-destinations.md) voor meer details over de implementatie.
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

+++Antwoordkenmerken zijn beschikbaar voor gebruik in Doel in [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) en [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=en) voorstellen.
+++

### Kan ik een bestemming zonder een gegevensstroom tot stand brengen en dan een gegevensstroom aan de zelfde bestemming op een recentere punt toevoegen?

+++Antwoord Dit wordt momenteel niet gesteund door de Doelen UI. Neem contact op met uw Adobe-vertegenwoordiger als u in dit geval hulp nodig hebt.
+++

### Wat gebeurt er als ik een Adobe Target-bestemming verwijder?

+++Antwoord Wanneer u een bestemming schrapt, worden alle publiek en attributen die onder de bestemming in kaart worden gebracht geschrapt van Adobe Target en zij worden ook verwijderd uit het Netwerk van de Rand.
+++

### Werkt de integratie met de Edge Network Server-API?

++ Antwoord ja, de Server API van het Netwerk van Edge werkt met de bestemming van de Aangepaste Personalisatie. Aangezien profielattributen gevoelige gegevens kunnen bevatten, vereist de bestemming van de Aangepaste Aanpassing u om de Server API van het Netwerk van de Rand voor gegevensinzameling te gebruiken. Bovendien moeten alle API-aanroepen worden uitgevoerd in een [geverifieerde context](../server-api/authentication.md).
+++

### Ik kan slechts één samenvoegbeleid hebben dat actief-op-rand is. Kan ik publiek bouwen dat een verschillend fusiebeleid gebruikt en hen nog naar Adobe Target als het stromen segmenten verzendt?

+++Antwoord nr. Alle soorten publiek die u naar Adobe Target wilt activeren, moeten een &#39;active-on-edge&#39; gebruiken [samenvoegingsbeleid](../profile/merge-policies/ui-guide.md).
+++

### Worden de Etikettering en de Handhaving van het Gebruik van Gegevens (DULE) en het Beleid van de Toestemming afgedwongen?

++ + Antwoord Ja. De [Beleid inzake gegevensbeheer en instemming](../data-governance/home.md) die zijn gemaakt en gekoppeld aan de geselecteerde marketingacties, worden toegepast op de activering van de geselecteerde kenmerken.
+++
