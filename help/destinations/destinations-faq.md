---
keywords: bestemmingen; vragen; veelgestelde vragen; faq; bestemmingen - vk
title: Veelgestelde vragen over doelen
seo-title: Veelgestelde vragen over doelen
description: Antwoorden op de vaakst gestelde vragen over de Doelen van Adobe Experience Platform
seo-description: Antwoorden op de vaakst gestelde vragen over de Doelen van Adobe Experience Platform
source-git-commit: 61678c5a62980cdb81714420016b7c4b2093f5c6
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 5%

---


# Veelgestelde vragen over doelen {#faq}

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Wat moet ik doen voordat ik publiek kan activeren  [!DNL Facebook Custom Audiences]?**

Voordat u publiekssegmenten kunt verzenden naar [!DNL Facebook], moet u controleren of aan de volgende vereisten is voldaan:

* Voor uw [!DNL Facebook]-gebruikersaccount moet de **[!DNL Manage campaigns]**-machtiging zijn ingeschakeld voor de advertentiaccount die u wilt gebruiken.
* De **Adobe Experience Cloud** bedrijfsrekening moet als advertentiepartner in uw [!DNL Facebook Ad Account] worden toegevoegd. Gebruik `business ID=206617933627973`. Zie [Partners toevoegen aan uw Business Manager](https://www.facebook.com/business/help/1717412048538897) in de documentatie van Facebook voor meer informatie.
   >[!IMPORTANT]
   >
   > Wanneer het vormen van de toestemmingen voor Adobe Experience Cloud, moet u **Manage campagnes** toestemming toelaten. Dit is nodig voor de [!DNL Adobe Experience Platform]-integratie.
* Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga daarvoor naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waarbij `accountID` uw [!DNL Facebook Ad Account ID] is.

**Moet ik apps of pixels toevoegen aan mijn  [!DNL Facebook] adverteerderaccount?**

Nee. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.

**Hoe lang duurt het voor Facebook informatie uit Adobe Experience Platform verwerkt?**

Vanaf maart 2021 heeft [!DNL Facebook Custom Audiences] een uur nodig om informatie te verwerken die van [!DNL Platform] is ontvangen.

**Kan ik gebruiken  [!DNL Facebook Custom Audiences] voor doelgroepen in andere  [!DNL Facebook] apps, zoals  [!DNL Instagram]?**

U kunt de [!DNL Facebook Custom Audiences] bestemming voor publiek gebruiken richtend over de familie van Facebook van apps die door [!DNL Facebook Custom Audiences], met inbegrip van [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], en [!DNL Messenger] worden gesteund. De selectie van de app waarop adverteerders campagnes willen uitvoeren, wordt aangegeven op het plaatsingsniveau in [!DNL Facebook Ads Manager].

**Wat is het verschil tussen de  [!DNL Facebook Custom Audiences] verbinding en de  [!DNL Facebook Pixel] uitbreiding?**

Bij de [!DNL Facebook Custom Audiences]-verbinding worden [!DNL Platform]-identiteiten gebruikt bij het verzenden van soorten publiek naar [!DNL Facebook], terwijl bij de [[!DNL Facebook Pixel] verbinding](../destinations/catalog/advertising/facebook-pixel.md) de pixel [!DNL Facebook] in een website wordt geïntegreerd.

Deze twee integraties zijn complementair; u kunt beide gebruiken om te zorgen voor een betere doelgroepdekking. Als voorbeeld kunt u de extensie [!DNL Facebook Pixel] gebruiken om websitebezoekers te verkennen die geen account hebben gemaakt, terwijl [!DNL Facebook Custom Audiences] u kan helpen bestaande klanten als doel in te stellen op basis van [!DNL Platform]-identiteiten.

**Is de integratie van Adobe Experience Platform met de  [!DNL Facebook Custom Audiences] ondersteuning die gebruikers van een publiek onderscheidt wanneer ze niet langer voor het publiek in aanmerking komen?**

Ja, de integratie ondersteunt het verwijderen van gebruikers van [!DNL Facebook Custom Audiences] wanneer ze niet langer in aanmerking komen.

**Hoe moet ik de publieksgegevens hashen voordat ik ze naar  [!DNL Facebook]sturen?**

[!DNL Facebook] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom kan het publiek dat aan [!DNL Facebook] wordt geactiveerd *hashed* herkenningstekens, zoals e-mailadressen of telefoonaantallen worden afgevinkt.

Zie [ID-overeenstemmingsvereisten](catalog/social/facebook.md#id-matching-requirements) voor gedetailleerde uitleg over de vereisten voor id-overeenkomsten.

**In welk soort identiteiten activeer ik  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, gehashte telefoonnummers  [!DNL GAID],  [!DNL IDFA]en aangepaste externe id&#39;s.

## linkedIn-doelgroepen {#linkedin}

**Moet ik apps of pixels toevoegen aan mijn  [!DNL LinkedIn] adverteerderaccount?**

Nee. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.

**Wat moet ik doen voordat ik publiek kan activeren  [!DNL LinkedIn Matched Audiences]?**

Voordat u de bestemming [!UICONTROL LinkedIn Matched Audience] kunt gebruiken, moet u ervoor zorgen dat uw [!DNL LinkedIn Campaign Manager]-account het machtigingsniveau [!DNL Creative Manager] of hoger heeft.

Zie [Gebruikersmachtigingen toevoegen, bewerken en verwijderen voor meer informatie over het bewerken van uw [!DNL LinkedIn Campaign Manager]-gebruikersmachtigingen in de documentatie van LinkedIn.](https://www.linkedin.com/help/lms/answer/5753)

**Hoe moet ik de publieksgegevens hashen voordat ik ze naar  [!DNL LinkedIn]sturen?**

[!DNL LinkedIn] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Daarom kan het publiek dat aan [!DNL LinkedIn] wordt geactiveerd *hashed* herkenningstekens, zoals e-mailadressen of telefoonaantallen worden afgevinkt.

Zie [ID-overeenstemmingsvereisten](catalog/social/linkedin.md#id-matching-requirements) voor gedetailleerde uitleg over de vereisten voor id-overeenkomsten.

**In welk soort identiteiten activeer ik  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] ondersteunt de activering van de volgende identiteiten: e-mails met hashing  [!DNL GAID], en  [!DNL IDFA].
