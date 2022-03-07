---
keywords: bestemmingen; vragen; veelgestelde vragen; faq; bestemmingen - vk
title: Veelgestelde vragen
seo-title: Frequently asked questions
description: Antwoorden op de meest gestelde vragen over Adobe Experience Platform-bestemmingen
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: b2636377eda6740dceb9bc07fbcc082b85ff3c94
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 4%

---

# Veelgestelde vragen {#faq}

## Overzicht {#overview}

Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform-doelen. For questions and troubleshooting related to other [!DNL Platform] services, including those encountered across all [!DNL Platform] APIs, please refer to the [Experience Platform troubleshooting guide](../landing/troubleshooting.md).

## General destinations questions {#general}

**Why am I seeing different profile counts in the Experience Platform UI and in the exported CSV files?**

Dit is een normaal gedrag als gevolg van de manier waarop Experience Platform segmentatie uitvoert.

De het stromen segmentatie werkt het profielaantal voor het stromen segmenten door de dag bij, terwijl de partijsegmentatie de profieltelling voor partijsegmenten eens om de 24 uur bijwerkt.

When the segment export schedule differs from the segmentation schedule, the profile counts between the UI and the exported [!DNL CSV] file will be different, especially when it comes to streaming segments.

See the [Segmentation Service documentation](../segmentation/home.md) for more details.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**What do I need to do before I can activate audiences in [!DNL Facebook Custom Audiences]?**

Before you can send your audience segments to [!DNL Facebook], make sure you meet the following requirements:

* Uw [!DNL Facebook] gebruikersaccount moet de **[!DNL Manage campaigns]** Toestemming ingeschakeld voor de advertentie-account die u wilt gebruiken.
* De **Adobe Experience Cloud** bedrijfsaccount moet worden toegevoegd als advertentiepartner in uw [!DNL Facebook Ad Account]. Gebruik `business ID=206617933627973`. See [Add Partners to Your Business Manager](https://www.facebook.com/business/help/1717412048538897) in the Facebook documentation for details.
   >[!IMPORTANT]
   >
   > When configuring the permissions for Adobe Experience Cloud, you must enable the **Manage campaigns** permission. Dit is nodig voor de [!DNL Adobe Experience Platform]-integratie.
* Lees en onderteken de [!DNL Facebook Custom Audiences] Servicevoorwaarden. Ga daarvoor naar `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, waarbij `accountID` uw [!DNL Facebook Ad Account ID] is.

**Moet ik apps of pixels toevoegen aan mijn [!DNL Facebook] adverteerderaccount?**

Nee. Aangezien dit geen op pixels gebaseerde integratie is, is het niet nodig om pixels toe te voegen aan uw adverteerderaccount.

**How long does Facebook take to process information from Adobe Experience Platform?**

Vanaf maart 2021 [!DNL Facebook Custom Audiences] heeft tot een uur nodig om informatie te verwerken die is ontvangen van [!DNL Platform].

**Kan ik gebruiken [!DNL Facebook Custom Audiences] voor doelgroepen in andere [!DNL Facebook] apps, zoals [!DNL Instagram]?**

U kunt de [!DNL Facebook Custom Audiences] doel voor doelgroepen in Facebook-apps die worden ondersteund door [!DNL Facebook Custom Audiences], met inbegrip van [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], en [!DNL Messenger]. Selection of the app which advertisers want to run campaigns on is indicated at the placement level in [!DNL Facebook Ads Manager].

**Wat is het verschil tussen [!DNL Facebook Custom Audiences] verbinding en [!DNL Facebook Pixel] uitbreiding?**

De [!DNL Facebook Custom Audiences] verbinding gebruikt [!DNL Platform] identiteiten bij het versturen van publiek naar [!DNL Facebook], terwijl de [[!DNL Facebook Pixel] verbinding](../destinations/catalog/advertising/facebook-pixel.md) gebruikt de [!DNL Facebook] pixel geïntegreerd in een website.

Deze twee integraties zijn complementair; u kunt beide gebruiken om te zorgen voor een betere doelgroepdekking. U kunt bijvoorbeeld de opdracht [!DNL Facebook Pixel] uitbreiding voor potentiële websitebezoekers die geen account hebben gemaakt, terwijl [!DNL Facebook Custom Audiences] kan u helpen bestaande klanten richten, die op [!DNL Platform] identiteiten.

**Wordt Adobe Experience Platform geïntegreerd met [!DNL Facebook Custom Audiences] gebruikers die niet meer in aanmerking komen voor de kwalificatie , ondersteunen van een publiek dat ze niet meer in aanmerking komt voor de kwalificatie ?**

Yes, the integration supports removing users from [!DNL Facebook Custom Audiences] when they no longer qualify.

**How should I hash the audience data before sending it to [!DNL Facebook]?**

[!DNL Facebook] requires that no personally identifiable information (PII) is sent in clear. Therefore, the audiences activated to [!DNL Facebook] can be keyed off *hashed* identifiers, such as email addresses or phone numbers.

For detailed explanations on the ID matching requirements, see [ID matching requirements](catalog/social/facebook.md#id-matching-requirements).

**What kind of identities can I activate in [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] ondersteunt de activering van de volgende identiteiten: gehashte e-mails, gehashte telefoonnummers, [!DNL GAID], [!DNL IDFA]en aangepaste externe id&#39;s.

**Kan ik veelvoudige bestemmingen van Facebook in Platform UI voor afzonderlijke rekeningen van Facebook tot stand brengen?**

Ja. A Facebook destination in Experience Platform is 1:1 to an ad account in Facebook. U kunt een aparte Facebook-bestemming maken voor elke Facebook-advertentieaccount in uw bedrijf. Volg de [zelfstudie over doelverbinding](/help/destinations/ui/connect-destination.md) en maak verbinding met een aparte Facebook-account voor elke nieuwe Facebook-bestemming in de gebruikersinterface van het Platform. Er is geen limiet voor het aantal Facebook-advertentieaccounts waarmee u verbinding kunt maken.

## Google Customer Match {#google-customer-match}

**Wanneer het uitvoeren van segmenten aan de Gelijke van de Klant van Google, waarom zie ik extra aantallen aan het eind van de segmentnamen in de interface van Google worden toegevoegd?**

Google requires segment names to be unique. De getallen die u ziet [UNIX-tijdstempels](https://www.unixtimestamp.com/) en ze worden toegevoegd om de segmentnamen uniek te houden, als u hetzelfde segment toewees aan meerdere Google-doelen.

## LinkedIn Matched Audiences {#linkedin}

**Do I need to add any apps or pixels to my [!DNL LinkedIn] advertiser account?**

Nee. As this is not a pixel-based integration, there is no need to add any pixels to your advertiser account.

**Wat moet ik doen voordat ik publiek kan activeren [!DNL LinkedIn Matched Audiences]?**

Voordat u de [!UICONTROL LinkedIn Matched Audience] doel, zorg ervoor uw [!DNL LinkedIn Campaign Manager] account bevat [!DNL Creative Manager] machtigingsniveau of hoger.

To learn how to edit your [!DNL LinkedIn Campaign Manager] user permissions, see [Add, Edit, and Remove User Permissions on Advertising Accounts](https://www.linkedin.com/help/lms/answer/5753) in the LinkedIn documentation.

**Hoe moet ik de publieksgegevens hashen voordat ik ze naar [!DNL LinkedIn]?**

[!DNL LinkedIn] vereist dat er geen duidelijk identificeerbare informatie (PII) wordt verstrekt. Therefore, the audiences activated to [!DNL LinkedIn] can be keyed off *hashed* identifiers, such as email addresses or phone numbers.

Voor gedetailleerde uitleg over de vereisten voor ID-matching raadpleegt u [Vereisten voor id-afstemming](catalog/social/linkedin.md#id-matching-requirements).

**What kind of identities can I activate in [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] supports the activation of the following identities: hashed emails, [!DNL GAID], and [!DNL IDFA].
