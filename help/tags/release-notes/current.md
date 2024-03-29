---
title: Opmerkingen bij de release voor tags en doorsturen van gebeurtenissen
description: De nieuwste aanvullende informatie voor tags en het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---

# Opmerkingen bij de release voor tags en gebeurtenissen doorsturen

>[!IMPORTANT]
>
>Het vooruit bewegen van de markeringen en de gebeurtenis door:sturen versienota&#39;s zullen niet meer op deze pagina worden verstrekt. Raadpleeg de meest recente [Opmerkingen bij de release van Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) voor gedetailleerde tags en updates voor het doorsturen van gebeurtenissen.

## 26 april 2023

* **OAuth JWT Secret**: De [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) Hiermee kunnen klanten Adobe- en Google Service-tokens gebruiken ter ondersteuning van server-naar-server interacties bij het doorsturen van gebeurtenissen.

De volgende nieuwe extensie is vrijgegeven:

* **[!DNL Pinterest Conversions API]extension**: De [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) Met de extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in Adobe Experience Platform Edge Network, benutten en verzenden naar [!DNL Pinterest] in de vorm van server-side-gebeurtenissen die de [!DNL Pinterest Conversions API].

## 29 maart 2023

**Quick Stark Workflows (bèta)**

Toegang tot nieuwe snelstartworkflows onder &quot;Aan de slag&quot; vanuit het startscherm van de gegevensverzameling. De volgende workflows zijn nu beschikbaar voor klanten als openbare bètaversie.
* **[API voor metaconversie](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: Gebruikers die gebeurtenissen doorsturen kunnen snel gebeurtenisgegevens, servergegevens naar Meta voor advertentieconversies in een paar eenvoudige stappen verzamelen en doorsturen.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: Klanten kunnen de Mobile SDK snel implementeren en mobiele basisgebeurtenissen in slechts een paar eenvoudige stappen valideren.

Nieuwe extensies zijn vrijgegeven:

* **[!DNL Braze]extensie voor doorsturen van gebeurtenissen**: De [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Met de extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge-netwerk, benutten en verzenden naar [!DNL Braze] in de vorm van server-side-gebeurtenissen die de [!DNL Braze] Gebruikerstrack-API&#39;s.
* **[Epsilon Events API] extensie voor doorsturen van gebeurtenissen**: De [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Met de extensie kunt u gebeurtenissen doorsturen om gebeurtenisinformatie vast te leggen in het Adobe Experience Platform Edge-netwerk en deze naar [!DNL Epsilon] met de [!DNL Epsilon] Gebeurtenis-API.
* **[!DNL Mixpanel]extensie voor doorsturen van gebeurtenissen**: De [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Met de extensie kunt u gebeurtenissen doorsturen om gebeurtenisinformatie vast te leggen in het Adobe Experience Platform Edge-netwerk en deze naar [!DNL Mixpanel] met de API voor gebeurtenissen bijhouden.

## 25 januari 2023

* **Nieuw beginscherm**: De homepage voor de UI van de Inzameling van Gegevens is bijgewerkt om nuttige onboarding informatie en verbindingen te omvatten om productiviteit te stroomlijnen. Dit omvat:
   1. Documentatie en aanbevolen workflows om aan de slag te gaan
   1. Recente eigenschappen, regels en gegevenselementen
   1. Populaire extensies
   1. Nieuwe extensies worden bijgewerkt met een functie voor snelle installatie
* **Gegevens verzenden naar [!DNL Google Ads] gebruiken, gebeurtenis doorsturen**: U kunt nu de opdracht [[!DNL Google Ads Enhanced Conversions] API-extensie](../extensions/server/google-ads-enhanced-conversions/overview.md) voor gebeurtenis door:sturen, gecombineerd met [Google Oauth 2 geheimen](../ui/event-forwarding/secrets.md#google-oauth2), om servergegevens veilig te verzenden naar [!DNL Google Ads] in real time.

## 23 november 2022

* **[!DNL AWS]extensie voor het doorsturen van gebeurtenissen**: U kunt nu gegevens verzenden naar [!DNL Amazon Web Services] ([!DNL AWS]) met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL AWS] extensieoverzicht](../../tags/extensions/server/aws/overview.md) voor meer informatie .
* **[!DNL Google Ads Enhanced Conversions]extensie voor het doorsturen van gebeurtenissen**: U kunt nu conversiegegevens verzenden naar [!DNL Google Ads] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Google Ads Enhanced Conversions] extensieoverzicht](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor meer informatie .
* **[!DNL Microsoft Azure]extensie voor het doorsturen van gebeurtenissen**: U kunt nu gegevens verzenden naar [!DNL Microsoft Azure] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Microsoft Azure] extensieoverzicht](../../tags/extensions/server/azure/overview.md) voor meer informatie .

## 26 oktober 2022

* **Gevoelige gegevensverwerking voor gegevensstromen**: Data streams maken nu gebruik van verschillende platformtechnologieën om gevoelige gegevens op de juiste manier te verwerken, zoals wordt voorgeschreven door verordeningen zoals de Health Insurance Portability and Accountability Act (HIPAA). Zie de sectie over [verwerking van gevoelige gegevens in gegevensstreams](../../datastreams/overview.md#sensitive) voor meer informatie .
* **[!DNL Splunk]extensie voor het doorsturen van gebeurtenissen**: U kunt nu gegevens verzenden naar [!DNL Splunk] met een [gebeurtenis doorsturen](../ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Splunk] extensieoverzicht](../extensions/server/splunk/overview.md) voor meer informatie .
* **[!DNL Zendesk]extensie voor het doorsturen van gebeurtenissen**: U kunt nu gegevens verzenden naar [!DNL Zendesk] met een [gebeurtenis doorsturen](../ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Zendesk] extensieoverzicht](../extensions/server/zendesk/overview.md) voor meer informatie .

## 28 september 2022

* **Adobe Experience Platform-integratie linker-nav**: Alle mogelijkheden die voorheen exclusief waren voor de gebruikersinterface voor gegevensverzameling (inclusief tags en het doorsturen van gebeurtenissen) zijn nu ook beschikbaar via de linkernavigatie in de gebruikersinterface van het Experience Platform, onder de categorie **[!UICONTROL Data Collection]**. Dit elimineert de behoefte om tussen UIs te schakelen wanneer het werken met de mogelijkheden van de gegevensinzameling in Platform.
* **Toewijzing door gebruiker in tags en gebeurtenis doorsturen**: Wanneer een lijst van beschikbare eigenschappen in markeringen en gebeurtenis het door:sturen, toont elk vermeld bezit nu wanneer het het laatst werd bijgewerkt en door wie.
* **[[!DNL Snap Conversions API] extension](https://exchange.adobe.com/apps/ec/108550) voor gebeurtenis doorsturen**: U kunt nu gegevens verzenden naar de [!DNL Snapchat Conversions API] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Voor meer informatie over het verifiëren en gebruiken van API, verwijs naar [[!DNL Snapchat Marketing API] documentatie](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 juli 2022

* De toegang tot labels en mogelijkheden voor het doorsturen van gebeurtenissen wordt nu beheerd via Adobe Admin Console onder de kaart voor Adobe Experience Platform-gegevensverzameling. Zie de handleiding op [gegevensverzamelingsmachtigingen](../../collection/permissions.md) voor meer informatie .
* Ondersteuning voor Internet Explorer 10 en 11 is [verouderd](../ie-deprecation.md).

## 22 juni 2022

Nieuwe extensies zijn vrijgegeven:

* [Google Data Layer-tagextensie](../extensions/client/google-data-layer/overview.md): Hiermee kunt u een Google-gegevenslaag gebruiken in de implementatie van tags.
* [Google Ads Enhanced Conversions-gebeurtenis door:sturen extensie](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Hiermee kunt u uw Google Ads-conversies in real-time verbeteren.
* [Mailchimp-gebeurtenis door:sturen, extensie](../extensions/server/mailchimp/overview.md): Verstuurt gebeurtenissen naar de Mailchimp Marketing API die e-mails kan activeren voor marketingcampagnes, reizen of transacties in Mailchimp.