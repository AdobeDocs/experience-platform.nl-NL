---
title: Aanvullende informatie voor tags en het doorsturen van gebeurtenissen
description: De nieuwste aanvullende informatie voor tags en het doorsturen van gebeurtenissen in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 92%

---

# Aanvullende informatie voor tags en het doorsturen van gebeurtenissen

>[!IMPORTANT]
>
>In de toekomst zijn aanvullende informatie voor tags en het doorsturen van gebeurtenissen niet meer op deze pagina te vinden. Raadpleeg de recentste [Aanvullende informatie voor Adobe Experience Platform](/help/release-notes/latest/latest.md) voor gedetailleerde tags en updates voor het doorsturen van gebeurtenissen.

## 26 april 2023

* **OAuth JWT Secret**: met het [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=nl-NL) kunnen klanten Adobe- en Google Service-tokens gebruiken om server-naar-server-interacties bij het doorsturen van gebeurtenissen te ondersteunen.

De volgende nieuwe extensie is uitgebracht:

* **[!DNL Pinterest Conversions API]-extensie**: met de [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html?lang=nl-NL)-extensie voor het doorsturen van gebeurtenissen kunt u gebruikmaken van gegevens die zijn vastgelegd in het Adobe Experience Platform Edge Network en deze naar [!DNL Pinterest] verzenden als gebeurtenissen aan de serverzijde met behulp van de [!DNL Pinterest Conversions API].

## 29 maart 2023

**Snelstartworkflows (beta)**

Krijg toegang tot nieuwe snelstartworkflows onder Aan de slag vanuit het startscherm voor gegevensverzameling. De volgende workflows zijn nu beschikbaar voor klanten als openbare beta.

* **[API voor metaconversies](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=nl-NL#quick-start)**: klanten met toegang tot de functie Gebeurtenis doorsturen kunnen snel gebeurtenisgegevens verzamelen en aan serverzijde doorsturen naar Meta voor advertentieconversies in slechts een paar eenvoudige stappen.
* **[Mobiele SDK](https://developer.adobe.com/client-sdks/documentation/)**: klanten kunnen de mobiele SDK snel implementeren en fundamentele mobiele gebeurtenissen in een paar eenvoudige stappen bevestigen.

Er zijn nieuwe extensies uitgebracht:

* **[!DNL Braze]-extensie voor het doorsturen van gebeurtenissen**: met de [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=nl-NL)-extensie voor het doorsturen van gebeurtenissen kunt u gebruikmaken van gegevens die zijn vastgelegd in het Adobe Experience Platform Edge Network en deze naar [!DNL Braze] verzenden als gebeurtenissen aan de serverzijde met behulp van de [!DNL Braze] User Track API&#39;s.
* **[Epsilon Events-API]-extensie voor het doorsturen van gebeurtenissen**: met de extensie [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=nl-NL) kunt u gebruikmaken van het doorsturen van gebeurtenissen om gebeurtenisgegevens vast te leggen in het Adobe Experience Platform Edge Network en deze naar [!DNL Epsilon] te verzenden met behulp van de [!DNL Epsilon] Event-API.
* **[!DNL Mixpanel]-extensie voor het doorsturen van gebeurtenissen**: met de extensie [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=nl-NL) kunt u gebruikmaken van het doorsturen van gebeurtenissen om gebeurtenisgegevens vast te leggen in het Adobe Experience Platform Edge Network en deze naar [!DNL Mixpanel] te verzenden met behulp van de API voor het bijhouden van gebeurtenissen.

## 25 januari 2023

* **Nieuw startscherm**: de startpagina van de gebruikersinterface voor dataverzameling is bijgewerkt met nuttige informatie over onboarding en koppelingen om de productiviteit te stroomlijnen. Dit omvat het volgende:
   1. Documentatie en aanbevolen workflows om aan de slag te gaan
   1. Recente eigenschappen, regels en gegevenselementen
   1. Populaire extensies
   1. Nieuwe extensies zijn bijgewerkt met een functie voor snelle installatie
* **Gegevens verzenden naar [!DNL Google Ads] met de functie Gebeurtenis doorsturen**: u kunt nu de [[!DNL Google Ads Enhanced Conversions] API-extensie](../extensions/server/google-ads-enhanced-conversions/overview.md) gebruiken voor het doorsturen van gebeurtenissen, gecombineerd met [Google Oauth 2-geheimen](../ui/event-forwarding/secrets.md#google-oauth2), om gegevens aan de serverzijde veilig en in real time naar [!DNL Google Ads] te verzenden.

## 23 november 2022

* **[!DNL AWS]-extensie voor het doorsturen van gebeurtenissen**: u kunt nu gegevens verzenden naar [!DNL Amazon Web Services] ([!DNL AWS]) met behulp van een [extensie voor het doorsturen van gebeurtenissen](../../tags/ui/event-forwarding/overview.md). Zie het [[!DNL AWS] extensieoverzicht](../../tags/extensions/server/aws/overview.md) voor meer informatie.
* **[!DNL Google Ads Enhanced Conversions]-extensie voor het doorsturen van gebeurtenissen**: u kunt nu conversiegegevens verzenden naar [!DNL Google Ads] met behulp van een [extensie voor het doorsturen van gebeurtenissen](../../tags/ui/event-forwarding/overview.md). Zie het [[!DNL Google Ads Enhanced Conversions] extensieoverzicht](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor meer informatie.
* **[!DNL Microsoft Azure]-extensie voor het doorsturen van gebeurtenissen**: u kunt nu gegevens verzenden naar [!DNL Microsoft Azure] met behulp van een extensie voor het [doorsturen van gebeurtenissen](../../tags/ui/event-forwarding/overview.md). Zie het [[!DNL Microsoft Azure] extensieoverzicht](../../tags/extensions/server/azure/overview.md) voor meer informatie.

## 26 oktober 2022

* **Gevoelige gegevens behandeling voor gegevensstromen**: De stromen van gegevensstromen hefboomwerking nu verscheidene technologieën van Experience Platform om gevoelige gegevens geschikt te behandelen zoals die door verordeningen zoals de Wet van de Portabiliteit en van de Verantwoording van de Ziekteverzekering (HIPAA) worden afgedwongen. Zie de sectie over [omgaan met gevoelige gegevens in datastreams](../../datastreams/overview.md#sensitive) voor meer informatie.
* **[!DNL Splunk]-extensie voor het doorsturen van gebeurtenissen**: u kunt nu gegevens verzenden naar [!DNL Splunk] met behulp van een extensie voor het [doorsturen van gebeurtenissen](../ui/event-forwarding/overview.md). Zie het [[!DNL Splunk] extensieoverzicht](../extensions/server/splunk/overview.md) voor meer informatie.
* **[!DNL Zendesk]-extensie voor het doorsturen van gebeurtenissen**: u kunt nu gegevens verzenden naar [!DNL Zendesk] met behulp van een extensie voor het [doorsturen van gebeurtenissen](../ui/event-forwarding/overview.md). Zie het [[!DNL Zendesk] extensieoverzicht](../extensions/server/zendesk/overview.md) voor meer informatie.

## 28 september 2022

* **Integratie van het linkernavigatiedeelvenster in Adobe Experience Platform**: alle mogelijkheden die voorheen exclusief waren voor de gebruikersinterface voor dataverzameling (inclusief tags en het doorsturen van gebeurtenissen), zijn nu ook beschikbaar via het linkernavigatiedeelvenster in de gebruikersinterface van Experience Platform, onder de categorie **[!UICONTROL Data Collection]**. Dit elimineert de behoefte om tussen UIs te schakelen wanneer het werken met de mogelijkheden van de gegevensinzameling in Experience Platform.
* **Gebruikersattributie in tags en gebeurtenissen doorsturen**: bij het weergeven van beschikbare eigenschappen in tags en gebeurtenissen doorsturen wordt nu voor elke vermelde eigenschap weergegeven wanneer deze voor het laatst is bijgewerkt, en door wie.
* **[[!DNL Snap Conversions API] -extensie](https://exchange.adobe.com/apps/ec/108550) voor gebeurtenissen doorsturen**: u kunt nu gegevens naar de [!DNL Snapchat Conversions API] verzenden met behulp van de extensie [Gebeurtenissen doorsturen](../../tags/ui/event-forwarding/overview.md). Raadpleeg de [[!DNL Snapchat Marketing API] documentatie](https://marketingapi.snapchat.com/docs/conversion.html) voor meer informatie over het verifiëren en gebruiken van de API.

## 27 juli 2022

* Toegang tot tags en mogelijkheden voor het doorsturen van gebeurtenissen wordt nu beheerd via de Adobe Admin Console onder de kaart voor Adobe Experience Platform Data Collection. Zie de gids over [machtigingen voor dataverzameling](../../collection/permissions.md) voor meer informatie.
* Ondersteuning voor Internet Explorer 10 en 11 is afgekeurd.

## 22 juni 2022

Er zijn nieuwe extensies uitgebracht:

* [Google Data Layer-tagextensie](../extensions/client/google-data-layer/overview.md): Hiermee kunt u een Google-gegevenslaag gebruiken in uw tagimplementatie.
* [Google Ads Enhanced Conversions-extensie voor gebeurtenissen doorsturen](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): hiermee kunt u uw Google Ads-conversies in real time verbeteren.
* [Mailchimp-extensie voor gebeurtenissen doorsturen](../extensions/server/mailchimp/overview.md): stuurt gebeurtenissen naar de Mailchimp Marketing API, die e-mails kunnen activeren voor Mailchimp-marketingcampagnes, -journeys of -transacties.