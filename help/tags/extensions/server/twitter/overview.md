---
keywords: event forward extension;twitter;twitter event forward extension
title: Twitter-gebeurtenis door:sturen, extensie
description: Deze Adobe Experience Platform-gebeurtenis die extensie doorstuurt, stelt u in staat om gebeurtenissen in te voeren in Twitter voor uw zakelijke vereisten.
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 2%

---

# [!DNL Twitter] extensie voor doorsturen van gebeurtenissen

[[!DNL Twitter]](https://twitter.com/i/flow/login) is een online sociale media en sociale netwerkdienst, waarop gebruikers post en met 280 karakter-lange berichten die als tweets worden bekend in wisselwerking staan. Gebruikers kunnen met Twitter communiceren via een browser, mobiele frontend software of via programmacode [API&#39;s](https://developer.twitter.com/en/docs/twitter-api)

De [!DNL Twitter] Web Conversions API [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge Network gebruiken en verzenden naar [!DNL Twitter]. Dit document behandelt de gebruiksgevallen van de extensie, de manier waarop de extensie moet worden geïnstalleerd en de manier waarop de mogelijkheden van de extensie moeten worden geïntegreerd in het doorsturen van de gebeurtenis [regels](../../../ui/managing-resources/rules.md).

[!DNL Twitter] vereist [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) voor verificatie met de [!DNL Twitter] [!DNL Web Conversions] API.

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van het Edge-netwerk wilt gebruiken in [!DNL Twitter] om voordeel te halen uit zijn klantenanalyses en gerichte mogelijkheden.

Neem bijvoorbeeld een marketingteam in een organisatie. Het team legt gebruikersinteractiegebeurtenisgegevens van zijn website vast als gebeurtenisgegevens van zijn website en laadt deze in [!DNL Twitter] gebruiken van deze gebeurtenis die uitbreiding door:sturen.

De marketing- en analyseteams kunnen vervolgens gebruikmaken van [!DNL Twitter's] mogelijkheden om extra analyses uit te voeren en deze gebruikers voor gerichte reclamecampagnes te richten.

Voor meer informatie over gebruiksgevallen die specifiek zijn voor [!DNL Twitter], verwijst u naar de [[!DNL Twitter] use cases](https://developer.twitter.com/en/use-cases/build-for-businesses) documentatie.

## [!DNL Twitter] voorwaarden en waarborgen {#prerequisites}

U moet een geldige [!DNL Twitter] om deze extensie te gebruiken. Ga naar de [[!DNL Twitter] registratiepagina](https://help.twitter.com/en/using-twitter/create-twitter-account) als u nog geen account hebt, kunt u zich registreren en een account maken.

U moet uw account instellen als een [!DNL Twitter] ontwikkelaarsaccount. Als u wilt weten hoe u zich aanmeldt als ontwikkelaar, raadpleegt u de [[!DNL Twitter] ontwikkelaarsaccount](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API-handleidingen {#guardrails}

De [!DNL Twitter] De Conversies API van het Web heeft een tariefgrens van 60.000 verzoeken per 15 minieme interval, waar elk verzoek 500 gebeurtenissen toestaat.

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u het Experience Platform wilt verbinden met [!DNL Twitter]zijn de volgende gegevens vereist:

| Type toets | Beschrijving |
| --- | --- |
| Consumentencode | De API-sleutel van de app &#x200B; voor toegang tot de [!DNL Twitter] API. Zie de [!DNL Twitter] documentatie over [api-sleutels en geheimen](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) ter begeleiding. | |
| Consumentengeheim | Met het API-geheim heeft uw toepassing toegang tot [!DNL Twitter] API. Zie de [!DNL Twitter] documentatie over [api-sleutels en geheimen](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) ter begeleiding. |
| Token Secret | Het niet-vervalsende token-geheim van uw app, dat wordt gebruikt voor verificatie bij de [!DNL Twitter] API via OAuth. Zie de [!DNL Twitter] documentatie over [gebruikstoegangstokens verkrijgen](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) ter begeleiding. |
| Toegangstoken | Het niet-verouderde toegangstoken van uw app, dat wordt gebruikt voor verificatie bij de [!DNL Twitter] API via OAuth. Zie de [!DNL Twitter] documentatie over [gebruikstoegangstokens verkrijgen](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) ter begeleiding. |
| Pixel-id | De [!DNL Twitter] Pixel is een website-tag die op uw website wordt geïmplementeerd om sitehandelingen of -conversies bij te houden. Zie de [!DNL Twitter] documentatie over [bijhouden van conversies voor websites](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) ter begeleiding. |

## Installeer en configureer de [!DNL Twitter] extension {#install}

Als u de extensie wilt installeren, [een eigenschap voor het doorsturen van gebeurtenissen maken](../../../ui/event-forwarding/overview.md#properties) of kies een bestaande eigenschap die u wilt bewerken.

Selecteren **[!UICONTROL Extensions]** in de linkernavigatie. In de **[!UICONTROL Catalog]** tab, selecteert u **[!UICONTROL Install]** op de kaart voor de [!DNL Twitter] extensie.

![Catalogus met de [!DNL Twitter] installatie van markering voor extensie.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Afhankelijk van uw implementatiebehoeften, kunt u een schema, gegevenselementen, en een dataset moeten tot stand brengen alvorens de uitbreiding te vormen. Controleer alle configuratiestappen voordat u begint om te bepalen welke entiteiten u moet instellen voor uw geval van gebruik.

Voer in het volgende scherm het volgende in [configuratiewaarden](#configuration-details) dat u eerder hebt verzameld van [!DNL Twitter]:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Consumer Secret]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token Secret]**

Als u klaar bent, selecteert u **[!UICONTROL Save]**.

![[!DNL Twitter] configuratiescherm voor de [!DNL Twitter] extensie.](../../../images/extensions/server/twitter/configure.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen door:sturen regels die bepalen wanneer en hoe uw gebeurtenissen zullen worden verzonden naar [!DNL Twitter].

Een nieuwe [regel](../../../ui/managing-resources/rules.md) in uw gebeurtenis die bezit door:sturen. Onder **[!UICONTROL Actions]** voegt u een nieuwe handeling toe en stelt u de extensie in op **[!UICONTROL Twitter]**. Adobe Experience Edge Network-gebeurtenissen naar [!DNL Twitter]stelt u de **[!UICONTROL Action Type]** tot **[!UICONTROL Send Web Conversion].**

Na selectie, schijnen de extra controles om de gebeurtenis verder te vormen. U moet de [!DNL Twitter] gebeurteniseigenschappen voor de gegevenselementen die u eerder hebt gemaakt. Raadpleeg voor meer informatie de [[!DNL Twitter] Web Conversions API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![De [!DNL Twitter] een regel voor conversiegebeurtenissen maken.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL User Identification]**

| Veldnaam | Beschrijving | Voorbeeld | Vereist |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Click ID] | [!DNL Twitter] Klik op Id als geparseerd via de URL waarop u klikt. | 26l6412g5p4iyj65a2oic2ayg2 | Vereist als er geen andere id is toegevoegd. |
| [!UICONTROL Email] | Een e-mailadres dat is hashed met SHA256. De tekst moet in kleine letters worden geschreven en eventuele afsluitende of voorloopspaties moeten worden verwijderd voordat de tekst wordt gehasht. | eventforwarding@example.com | Vereist als er geen andere id is toegevoegd. |
| [!UICONTROL Phone] | Telefoon fungeert als id die overeenkomt met de conversiegebeurtenis. Het telefoonnummer moet de E164-notatie [+][landcode] hebben[netnummer][local phone number] voordat u gaat hashen. | +911234567875 | Vereist als er geen andere id is toegevoegd. |

**[!UICONTROL Conversion Data]**

| Veldnaam | Beschrijving | Voorbeeld | Vereist |
| --- | --- | --- | --- |
| [!UICONTROL Conversion Time] | Datum-tijd als tekenreeks in ISO 8601 of in jjjj-MM-dd&#39;T&#39;HH:mm:ss:SSSZ-indeling. | 2022-02-18T01:14:00,603Z | Ja |
| [!UICONTROL Event Id] | De basis-36-id van een specifieke gebeurtenis. Deze id moet overeenkomen met een vooraf geconfigureerde gebeurtenis in uw [!DNL Twitter] advertentieaccount. Dit wordt de id voor de bijbehorende gebeurtenis in Events Manager genoemd. | o87ne of tw-o8z6j-o87ne (tw-pixel_id-event-id) | Ja |
| [!UICONTROL Number of Items] | Het aantal items dat in de gebeurtenis wordt aangeschaft. Dit moet een positief getal zijn dat groter is dan 0. | 4 | Nee |
| [!UICONTROL Currency] | De valuta van de items die in de gebeurtenis worden gekocht. Dit wordt uitgedrukt in ISO-4217 en indien niet verstrekt, zal de standaardwaarde USD zijn. | USD | Nee |
| [!UICONTROL Value] | De prijswaarde van de items die in het geval worden aangeschaft. | 100.00 | Nee |
| [!UICONTROL Conversion ID] | Een id voor een conversiegebeurtenis die kan worden gebruikt voor deduplicatie tussen webpixels en conversie-API-conversies in dezelfde gebeurtenistag. | 23294827 | Nee |
| [!UICONTROL Description] | Een beschrijving met aanvullende informatie over de omzettingen. | Conversie testen | Nee |

## Gegevens valideren binnen [!DNL Twitter]

Zodra de gebeurtenis door:sturen regel is gecreeerd en uitgevoerd, bevestig of de gebeurtenis die werd verzonden naar [!DNL Twitter] API wordt weergegeven zoals wordt verwacht in het dialoogvenster [!DNL Twitter] UI.

Als de gebeurtenisinzameling en [!DNL Experience Platform] de integratie is voltooid, u ziet de gebeurtenissen in het [!DNL Twitter] [!UICONTROL Events manager].

![De [!DNL Twitter] gebeurtenismanager](../../../images/extensions/server/twitter/event-manager.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen naar [!DNL Twitter] het gebruiken van gebeurtenis door:sturen. Raadpleeg de officiële documentatie voor meer informatie over deze onderliggende technologieën:

* [[!DNL Twitter] API&#39;s](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] API voor webconversie](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] Toegangstoken gebruiker](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [Pixel-id en conversie bijhouden](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
