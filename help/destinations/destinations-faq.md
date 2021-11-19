---
keywords: bestemmingen; vragen; veelgestelde vragen; faq; bestemmingen - vk
title: Veelgestelde vragen
seo-title: Frequently asked questions
description: Antwoorden op de meest gestelde vragen over Adobe Experience Platform-bestemmingen
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 69fc8e8ec3211495056be73c2e49c6aecfc569ea
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 4%

---

# Veelgestelde vragen {#faq}

## Overzicht {#overview}

Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform-doelen. Voor vragen en problemen met betrekking tot andere problemen [!DNL Platform] services, inclusief de services die in alle [!DNL Platform] API&#39;s, raadpleeg de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

## Algemene vragen over bestemmingen {#general}

**Waarom zie ik verschillende profieltellingen in het Experience Platform UI en in de uitgevoerde Csv- dossiers?**

Dit is een normaal gedrag als gevolg van de manier waarop Experience Platform segmentatie uitvoert.

De het stromen segmentatie werkt het profielaantal voor het stromen segmenten door de dag bij, terwijl de partijsegmentatie de profieltelling voor partijsegmenten eens om de 24 uur bijwerkt.

Wanneer het segment uitvoerschema van het segmenteringsprogramma verschilt, telt het profiel tussen UI en geëxporteerde [!DNL CSV] Het bestand is anders, vooral wanneer het gaat om streaming segmenten.

Zie de [Documentatie voor segmentatieservice](../segmentation/home.md) voor meer informatie .

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Wat moet ik doen voordat ik publiek kan activeren [!DNL Facebook Custom Audiences]?**

Voordat u publiekssegmenten kunt verzenden naar [!DNL Facebook]voldoet aan de volgende vereisten:

* Uw [!DNL Facebook] gebruikersaccount moet de **[!DNL Manage campaigns]** Toestemming ingeschakeld voor de advertentie-account die u wilt gebruiken.
* De **Adobe Experience Cloud** bedrijfsaccount moet worden toegevoegd als advertentiepartner in uw [!DNL Facebook Ad Account]. Gebruik `business ID=206617933627973`. Zie [Partners toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) in de documentatie van Facebook voor meer informatie.
   >[!IMPORTANT]
   >
   > Wanneer u de machtigingen voor Adobe Experience Cloud configureert, moet u de optie **Campagnes beheren** toestemming. Dit is nodig voor de [!DNL Adobe Experience Platform]-integratie.
* Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga daarvoor naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waarbij `accountID` uw [!DNL Facebook Ad Account ID] is.

**Moet ik apps of pixels toevoegen aan mijn [!DNL Facebook] adverteerderaccount?**

Nee. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.

**Hoe lang duurt het voor Facebook informatie uit Adobe Experience Platform verwerkt?**

Vanaf maart 2021 [!DNL Facebook Custom Audiences] heeft tot een uur nodig om informatie te verwerken die is ontvangen van [!DNL Platform].

**Kan ik gebruiken [!DNL Facebook Custom Audiences] voor doelgroepen in andere [!DNL Facebook] apps, zoals [!DNL Instagram]?**

U kunt de [!DNL Facebook Custom Audiences] doel voor doelgroepen in Facebook-apps die worden ondersteund door [!DNL Facebook Custom Audiences], met inbegrip van [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], en [!DNL Messenger]. De selectie van de app waarop adverteerders campagnes willen uitvoeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager].

**Wat is het verschil tussen [!DNL Facebook Custom Audiences] verbinding en [!DNL Facebook Pixel] uitbreiding?**

De [!DNL Facebook Custom Audiences] verbinding gebruikt [!DNL Platform] identiteiten bij het versturen van publiek naar [!DNL Facebook], terwijl de [[!DNL Facebook Pixel] verbinding](../destinations/catalog/advertising/facebook-pixel.md) gebruikt de [!DNL Facebook] pixel geïntegreerd in een website.

Deze twee integraties zijn complementair; u kunt beide gebruiken om te zorgen voor een betere doelgroepdekking. U kunt bijvoorbeeld de opdracht [!DNL Facebook Pixel] uitbreiding voor potentiële websitebezoekers die geen account hebben gemaakt, terwijl [!DNL Facebook Custom Audiences] kan u helpen bestaande klanten richten, die op [!DNL Platform] identiteiten.

**Wordt Adobe Experience Platform geïntegreerd met [!DNL Facebook Custom Audiences] gebruikers die niet meer in aanmerking komen voor de kwalificatie , ondersteunen van een publiek dat ze niet meer in aanmerking komt voor de kwalificatie ?**

Ja, de integratie ondersteunt het verwijderen van gebruikers uit [!DNL Facebook Custom Audiences] wanneer zij niet langer in aanmerking komen.

**Hoe moet ik de publieksgegevens hashen voordat ik ze naar [!DNL Facebook]?**

[!DNL Facebook] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL Facebook] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Voor gedetailleerde uitleg over de vereisten voor ID-matching raadpleegt u [Vereisten voor id-afstemming](catalog/social/facebook.md#id-matching-requirements).

**Welk type identiteiten kan ik activeren? [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, gehashte telefoonnummers, [!DNL GAID], [!DNL IDFA]en aangepaste externe id&#39;s.

**Kan ik veelvoudige bestemmingen van Facebook in Platform UI voor afzonderlijke rekeningen van Facebook tot stand brengen?**

Ja. Een Facebook-bestemming in Experience Platform is 1:1 voor een advertentieaccount in Facebook. U kunt een aparte Facebook-bestemming maken voor elke Facebook-advertentieaccount in uw bedrijf. Volg de [zelfstudie over doelverbinding](/help/destinations/ui/connect-destination.md) en maak verbinding met een aparte Facebook-account voor elke nieuwe Facebook-bestemming in de gebruikersinterface van het Platform. Er is geen limiet voor het aantal Facebook-advertentieaccounts waarmee u verbinding kunt maken.

## linkedIn-doelgroepen {#linkedin}

**Moet ik apps of pixels toevoegen aan mijn [!DNL LinkedIn] adverteerderaccount?**

Nee. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.

**Wat moet ik doen voordat ik publiek kan activeren [!DNL LinkedIn Matched Audiences]?**

Voordat u de [!UICONTROL LinkedIn Matched Audience] doel, zorg ervoor uw [!DNL LinkedIn Campaign Manager] account bevat [!DNL Creative Manager] machtigingsniveau of hoger.

Meer informatie over het bewerken van uw [!DNL LinkedIn Campaign Manager] gebruikersmachtigingen, zie [Gebruikersmachtigingen toevoegen, bewerken en verwijderen voor advertentieaccounts](https://www.linkedin.com/help/lms/answer/5753) in de documentatie van LinkedIn.

**Hoe moet ik de publieksgegevens hashen voordat ik ze naar [!DNL LinkedIn]?**

[!DNL LinkedIn] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom wordt het publiek geactiveerd tot [!DNL LinkedIn] kan worden uitgeschakeld *hashed* id&#39;s, zoals e-mailadressen of telefoonnummers.

Voor gedetailleerde uitleg over de vereisten voor ID-matching raadpleegt u [Vereisten voor id-afstemming](catalog/social/linkedin.md#id-matching-requirements).

**Welk type identiteiten kan ik activeren? [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, [!DNL GAID], en [!DNL IDFA].
