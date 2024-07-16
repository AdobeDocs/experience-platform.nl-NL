---
title: Opmerkingen bij de release voor tags en doorsturen van gebeurtenissen
description: De nieuwste aanvullende informatie voor tags en het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 2%

---

# Opmerkingen bij de release voor tags en gebeurtenissen doorsturen

>[!IMPORTANT]
>
>Het vooruit bewegen van de markeringen en de gebeurtenis door:sturen versienota&#39;s zullen niet meer op deze pagina worden verstrekt. Gelieve te verwijzen naar de recentste [ de versienota&#39;s van Adobe Experience Platform ](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) voor gedetailleerde markeringen en gebeurtenis door:sturen updates.

## donderdag 26 april 2023

* **OAuth JWT Geheim**: [ Geheime JWT ](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) staat klanten toe om Adobe en de tokens van de Dienst van Google te gebruiken om server-aan-server interactie in Gebeurtenis te steunen die door:sturen.

De volgende nieuwe extensie is vrijgegeven:

* **[!DNL Pinterest Conversions API]extension**: De [[!DNL Pinterest Conversions API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) gebeurtenis die uitbreiding door:sturen staat u toe om gegevens te gebruiken die in de Edge Network van Adobe Experience Platform worden gevangen en het te verzenden naar [!DNL Pinterest] in de vorm van server-zijgebeurtenissen gebruikend [!DNL Pinterest Conversions API].

## donderdag 29 maart 2023

**Snelle Stark Workflows (Beta)**

Toegang tot nieuwe snelstartworkflows onder &quot;Aan de slag&quot; vanuit het startscherm van de gegevensverzameling. De volgende workflows zijn nu beschikbaar voor klanten als openbare Beta.
* **[de Conversies van Meta API ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: De gebeurtenis die klanten door:sturen kan gebeurtenisgegevens, server-kant aan Meta voor advertentieconversies in enkel een paar eenvoudige stappen snel verzamelen en door:sturen.
* **[Mobiele SDK ](https://developer.adobe.com/client-sdks/documentation/)**: De klanten kunnen mobiele SDK snel uitvoeren en fundamentele mobiele gebeurtenissen in enkel een paar eenvoudige stappen bevestigen.

Nieuwe extensies zijn vrijgegeven:

* **[!DNL Braze]event Forwarding extension**: Met de [[!DNL Braze Track Events API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) event forward extension kunt u gegevens die in de Adobe Experience Platform Edge Network zijn vastgelegd, benutten en verzenden naar [!DNL Braze] in de vorm van server-side gebeurtenissen met behulp van de [!DNL Braze] User Track API&#39;s.
* **[Epsilon Gebeurtenissen API ] gebeurtenis door:sturen uitbreiding**: De [[!DNL Epsilon Events API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) uitbreiding staat u toe aan hefboomgebeurtenis het door:sturen om gebeurtenisinformatie in de Edge Network van Adobe Experience Platform te vangen en het te verzenden naar [!DNL Epsilon] gebruikend [!DNL Epsilon] Gebeurtenis API.
* **[!DNL Mixpanel]gebeurtenis die uitbreiding** door:sturen: De [[!DNL Mixpanel Track Events API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) uitbreiding staat u toe om gebeurtenis te hefboomwerking door:sturen om gebeurtenisinformatie in de Edge Network van Adobe Experience Platform te vangen en het te verzenden naar [!DNL Mixpanel] gebruikend de Gebeurtenissen API van het Spoor.

## donderdag 25 januari 2023

* **Nieuw homescherm**: De homepage voor UI van de Inzameling van Gegevens is bijgewerkt om nuttige onboarding informatie en verbindingen te omvatten om productiviteit te stroomlijnen. Dit omvat:
   1. Documentatie en aanbevolen workflows om aan de slag te gaan
   1. Recente eigenschappen, regels en gegevenselementen
   1. Populaire extensies
   1. Nieuwe extensies worden bijgewerkt met een functie voor snelle installatie
* **verzendt gegevens naar [!DNL Google Ads] gebruikend gebeurtenis het door:sturen**: U kunt de [[!DNL Google Ads Enhanced Conversions]  API uitbreiding ](../extensions/server/google-ads-enhanced-conversions/overview.md) voor gebeurtenis nu gebruiken door:sturen, gecombineerd met [ Google Oauth 2 geheimen ](../ui/event-forwarding/secrets.md#google-oauth2), om server-zijgegevens aan [!DNL Google Ads] in real time veilig te verzenden.

## 23 november 2022

* **[!DNL AWS]uitbreiding voor gebeurtenis door:sturen**: U kunt gegevens [!DNL Amazon Web Services] ([!DNL AWS]) nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL AWS]  uitbreidingsoverzicht ](../../tags/extensions/server/aws/overview.md) voor meer informatie.
* **[!DNL Google Ads Enhanced Conversions]uitbreiding voor gebeurtenis door:sturen**: U kunt omzettingsgegevens naar [!DNL Google Ads] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Google Ads Enhanced Conversions]  uitbreidingsoverzicht ](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor meer informatie.
* **[!DNL Microsoft Azure]uitbreiding voor gebeurtenis die** door:sturen: U kunt gegevens [!DNL Microsoft Azure] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Microsoft Azure]  uitbreidingsoverzicht ](../../tags/extensions/server/azure/overview.md) voor meer informatie.

## donderdag 26 oktober 2022

* **Gevoelige gegevens behandeling voor gegevensstromen**: De stromen van gegevensstromen hefboomwerking nu verscheidene technologieën van het Platform om gevoelige gegevens geschikt te behandelen zoals die door verordeningen zoals de Wet van de Portabiliteit en van de Verantwoording van de Ziekteverzekering (HIPAA) worden afgedwongen. Zie de sectie over [ behandelend gevoelige gegevens in datstromen ](../../datastreams/overview.md#sensitive) voor meer informatie.
* **[!DNL Splunk]uitbreiding voor gebeurtenis die** door:sturen: U kunt gegevens [!DNL Splunk] nu verzenden gebruikend een [ gebeurtenis die ](../ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Splunk]  uitbreidingsoverzicht ](../extensions/server/splunk/overview.md) voor meer informatie.
* **[!DNL Zendesk]uitbreiding voor gebeurtenis die** door:sturen: U kunt gegevens [!DNL Zendesk] nu verzenden gebruikend een [ gebeurtenis die ](../ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Zendesk]  uitbreidingsoverzicht ](../extensions/server/zendesk/overview.md) voor meer informatie.

## 28 september 2022

* **Adobe Experience Platform verlaten nav integratie**: Alle mogelijkheden die eerder exclusief aan de Inzameling van Gegevens UI (met inbegrip van markeringen en gebeurtenis het door:sturen) waren zijn nu ook beschikbaar door de linkernavigatie in Experience Platform UI, onder de categorie **[!UICONTROL Data Collection]**. Dit elimineert de behoefte om tussen UIs te schakelen wanneer het werken met de mogelijkheden van de gegevensinzameling in Platform.
* **de attributie van de Gebruiker in markeringen en gebeurtenis door:sturen**: Wanneer de lijst van beschikbare eigenschappen in markeringen en gebeurtenis door:sturen, toont elk vermeld bezit nu wanneer het het laatst werd bijgewerkt en door wie.
* **[[!DNL Snap Conversions API] uitbreiding ](https://exchange.adobe.com/apps/ec/108550) voor gebeurtenis door:sturen**: U kunt gegevens naar [!DNL Snapchat Conversions API] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Voor meer informatie over hoe te voor authentiek te verklaren en API te gebruiken, verwijs naar de [[!DNL Snapchat Marketing API]  documentatie ](https://marketingapi.snapchat.com/docs/conversion.html).

## donderdag 27 juli 2022

* De toegang tot labels en mogelijkheden voor het doorsturen van gebeurtenissen wordt nu beheerd via Adobe Admin Console onder de kaart voor Adobe Experience Platform-gegevensverzameling. Zie de gids op [ toestemmingen van de gegevensinzameling ](../../collection/permissions.md) voor meer informatie.
* De steun voor Internet Explorer 10 en 11 is afgekeurd [ ](../ie-deprecation.md).

## donderdag 22 juni 2022

Nieuwe extensies zijn vrijgegeven:

* [ de markeringsuitbreiding van de Laag van Gegevens van Google ](../extensions/client/google-data-layer/overview.md): Staat u toe om een de gegevenslaag van Google in uw markeringsimplementatie te gebruiken.
* [ Google voegt Verbeterde gebeurtenis van Conversies toe die uitbreiding ](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html) door:sturen: Staat u toe om uw omzettingen van de Advertenties van Google in real time te verbeteren.
* [ gebeurtenis Mailchimp die uitbreiding ](../extensions/server/mailchimp/overview.md) door:sturen: verzendt gebeurtenissen naar de Marketing API van Mailchimp die e-mails voor de marketing van Mailchimp campagnes, reizen, of transacties kan teweegbrengen.