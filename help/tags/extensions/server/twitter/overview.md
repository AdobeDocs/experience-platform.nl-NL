---
keywords: extensie voor verzenden van gebeurtenissen;twitter;twitter-gebeurtenis voor verzenden van extensie
title: Twitter-gebeurtenis, extensie doorsturen
description: Met deze Adobe Experience Platform-extensie voor het doorsturen van gebeurtenissen kunt u gebeurtenissen opnemen in Twitter voor uw zakelijke vereisten.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 374c140a5db678adfa2e038b69478ad8c7f8dc95
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# [!DNL Twitter] -gebeurtenis, extensie doorsturen

[[!DNL Twitter] &#x200B;](https://twitter.com/i/flow/login) is een online sociale media en de sociale voorzien van een netwerkdienst, waarop de gebruikers posten en met 280 karakter-lange berichten in wisselwerking staan die als tweets worden bekend. De gebruikers kunnen met Twitter in wisselwerking staan gebruikend browser, mobiele frontend software, of programmatically door zijn [&#x200B; APIs &#x200B;](https://developer.twitter.com/en/docs/twitter-api)

De [!DNL Twitter] gebeurtenis die van de Conversies API van het Web [&#128279;](../../../ui/event-forwarding/overview.md) uitbreiding door:sturen staat u toe aan hefboomwerkingsgegevens in Adobe Experience Platform Edge Network worden gevangen en het verzenden naar [!DNL Twitter]. Dit document behandelt de gebruiksgevallen van de uitbreiding, hoe te om het te installeren, en hoe te om zijn mogelijkheden in uw gebeurtenis te integreren die [&#x200B; regels &#x200B;](../../../ui/managing-resources/rules.md) door:sturen.

[!DNL Twitter] vereist [&#x200B; OAuth 1.0 &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) voor authentificatie met [!DNL Twitter] [!DNL Web Conversions] API.

## Gebruiksscenario’s

Deze extensie moet worden gebruikt als u gegevens van de Edge Network in [!DNL Twitter] wilt gebruiken om te profiteren van de analysemogelijkheden van de klant en de doelmogelijkheden.

Neem bijvoorbeeld een marketingteam in een organisatie. Het team legt gebruikersinteractiegebeurtenisgegevens van zijn website vast als gebeurtenisgegevens van zijn website en laadt deze in [!DNL Twitter] met deze door:sturen-extensie van gebeurtenis.

De marketing- en analyseteams kunnen vervolgens gebruikmaken van [!DNL Twitter's] -mogelijkheden om aanvullende analyses uit te voeren en deze gebruikers te richten op gerichte advertentiecampagnes.

Voor meer informatie over gebruiksgevallen specifiek voor [!DNL Twitter], verwijs naar de [[!DNL Twitter]  gebruiksgevallen &#x200B;](https://developer.twitter.com/en/use-cases/build-for-businesses) documentatie.

## [!DNL Twitter] voorwaarden en instructies {#prerequisites}

U moet een geldige [!DNL Twitter] -account hebben om deze extensie te kunnen gebruiken. Ga naar de [[!DNL Twitter]  registratiepagina &#x200B;](https://help.twitter.com/en/using-twitter/create-twitter-account) om een rekening te registreren en tot stand te brengen als u niet reeds hebt.

U moet uw account instellen als een [!DNL Twitter] -ontwikkelaarsaccount. Om te weten te komen hoe te om omhoog als ontwikkelaar te ondertekenen, verwijs naar de [[!DNL Twitter]  ontwikkelaarsrekening &#x200B;](https://developer.twitter.com/en/support/twitter-api/developer-account1).

### API-handleidingen {#guardrails}

De [!DNL Twitter] Web Conversions API heeft een tariefgrens van 60.000 verzoeken per 15 minieme interval, waar elke aanvraag 500 gebeurtenissen toestaat.

### Verzamel vereiste configuratiedetails {#configuration-details}

Als u de Experience Platform wilt verbinden met [!DNL Twitter] , hebt u de volgende invoeren nodig:

| Type toets | Beschrijving |
| --- | --- |
| Consumentencode | &#x200B; de API-sleutel van de app voor toegang tot de [!DNL Twitter] -API. Verwijs naar de [!DNL Twitter] documentatie over [&#x200B; api sleutels en geheimen &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) voor begeleiding. |
| Consumentengeheim | Met het API-geheim heeft uw toepassing toegang tot de [!DNL Twitter] API. Verwijs naar de [!DNL Twitter] documentatie over [&#x200B; api sleutels en geheimen &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) voor begeleiding. |
| Token Secret | Het niet-vervalsende token-geheim van uw app, dat wordt gebruikt voor verificatie naar de [!DNL Twitter] -API via OAuth. Verwijs naar de [!DNL Twitter] documentatie op [&#x200B; het verkrijgen van de tokens van de gebruikstoegang &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) voor begeleiding. |
| Toegangstoken | Het niet-verouderde toegangstoken van uw app, die wordt gebruikt voor verificatie met de [!DNL Twitter] -API via OAuth. Verwijs naar de [!DNL Twitter] documentatie op [&#x200B; het verkrijgen van de tokens van de gebruikstoegang &#x200B;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) voor begeleiding. |
| Pixel-id | De pixel van [!DNL Twitter] is een websitemarkering die op uw website wordt uitgevoerd om plaatsacties of omzettingen te volgen. Verwijs naar de [!DNL Twitter] documentatie over [&#x200B; omzetting het volgen voor websites &#x200B;](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) voor begeleiding. |

## De extensie [!DNL Twitter] installeren en configureren {#install}

Om de uitbreiding te installeren, [&#x200B; creeer een gebeurtenis door:sturen bezit &#x200B;](../../../ui/event-forwarding/overview.md#properties) of kies een bestaand bezit in plaats daarvan uit te geven.

Selecteer **[!UICONTROL Extensions]** in de linkernavigatie. Selecteer op het tabblad **[!UICONTROL Catalog]** **[!UICONTROL Install]** op de kaart voor de extensie [!DNL Twitter] .

![&#x200B; Catalogus die de [!DNL Twitter] uitbreiding toont die installeert benadrukt.](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>Afhankelijk van uw implementatiebehoeften, kunt u een schema, gegevenselementen, en een dataset moeten tot stand brengen alvorens de uitbreiding te vormen. Controleer alle configuratiestappen voordat u begint om te bepalen welke entiteiten u moet instellen voor uw geval van gebruik.

Op het volgende scherm, input de volgende [&#x200B; configuratiewaarden &#x200B;](#configuration-details) die u eerder van [!DNL Twitter] verzamelde:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL Consumer Key]**
* **[!UICONTROL Consumer Secret]**
* **[!UICONTROL Token]**
* **[!UICONTROL Token Secret]**

Selecteer **[!UICONTROL Save]** als u klaar bent.

![[!DNL Twitter] configuratiescherm voor de [!DNL Twitter] extensie. &#x200B;](../../../images/extensions/server/twitter/configure.png)

## Vorm een gebeurtenis door:sturen regel {#config-rule}

Zodra al uw gegevenselementen opstelling zijn, kunt u gebeurtenis beginnen tot stand te brengen die regels bepaalt wanneer en hoe uw gebeurtenissen naar [!DNL Twitter] zullen worden verzonden.

Creeer een nieuwe [&#x200B; regel &#x200B;](../../../ui/managing-resources/rules.md) in uw gebeurtenis door:sturen bezit. Voeg onder **[!UICONTROL Actions]** een nieuwe handeling toe en stel de extensie in op **[!UICONTROL Twitter]** . Als u Edge Network-gebeurtenissen naar [!DNL Twitter] wilt verzenden, stelt u de eigenschap **[!UICONTROL Action Type]** to **[!UICONTROL Send Web Conversion]in.**

Na selectie, schijnen de extra controles om de gebeurtenis verder te vormen. U moet de eigenschappen van de gebeurtenis [!DNL Twitter] toewijzen aan de gegevenselementen die u eerder hebt gemaakt. Voor meer informatie, verwijs naar de [[!DNL Twitter]  Conversies API van het Web &#x200B;](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions).

![&#x200B; [!DNL Twitter] creërend een regel van de omzettingsgebeurtenis.](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL User Identification]**

| Veldnaam | Beschrijving | Voorbeeld | Vereist |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] Click ID] | [!DNL Twitter] Klik op Id als geparseerd via de URL waarop u klikt. | 26l6412g5p4iyj65a2oic2ayg2 | Vereist als er geen andere id is toegevoegd. |
| [!UICONTROL Email] | Een e-mailadres dat is hashed met SHA256. De tekst moet in kleine letters worden geschreven en eventuele afsluitende of voorloopspaties moeten worden verwijderd voordat de tekst wordt gehasht. | eventforwarding@example.com | Vereist als er geen andere id is toegevoegd. |
| [!UICONTROL Phone] | Telefoon fungeert als id die overeenkomt met de conversiegebeurtenis. Het telefoonaantal moet in formaat E164 zijn [+] [landcode] [ gebiedscode ][local phone number] alvorens het hakken. | +911234567875 | Vereist als er geen andere id is toegevoegd. |

**[!UICONTROL Conversion Data]**

| Veldnaam | Beschrijving | Voorbeeld | Vereist |
| --- | --- | --- | --- |
| [!UICONTROL Conversion Time] | Datum en tijd als tekenreeks in ISO 8601 of in `yyyy-MM-dd'T'HH:mm:ss:SSSZ` indeling. | 2022-02-18T01 :14: 00.603Z | Ja |
| [!UICONTROL Event Id] | De basis-36-id van een specifieke gebeurtenis. Deze id moet overeenkomen met een vooraf geconfigureerde gebeurtenis in uw [!DNL Twitter] ad-account. Dit wordt de id voor de bijbehorende gebeurtenis in Events Manager genoemd. | o87ne of tw-o8z6j-o87ne (tw-pixel_id-event-id) | Ja |
| [!UICONTROL Number of Items] | Het aantal items dat in de gebeurtenis wordt aangeschaft. Dit moet een positief getal zijn dat groter is dan 0. | 4 | Nee |
| [!UICONTROL Currency] | De valuta van de items die in de gebeurtenis worden gekocht. Dit wordt uitgedrukt in ISO-4217 en indien niet verstrekt, zal de standaardwaarde USD zijn. | USD | Nee |
| [!UICONTROL Value] | De prijswaarde van de items die in het geval worden aangeschaft. | 100,00 | Nee |
| [!UICONTROL Conversion ID] | Een id voor een conversiegebeurtenis die kan worden gebruikt voor deduplicatie tussen webpixels en conversie-API-conversies in dezelfde gebeurtenistag. | 23294827 | Nee |
| [!UICONTROL Description] | Een beschrijving met aanvullende informatie over de omzettingen. | Conversie testen | Nee |

## Gegevens valideren binnen [!DNL Twitter]

Nadat de regel voor het doorsturen van gebeurtenissen is gemaakt en uitgevoerd, controleert u of de gebeurtenis die naar de [!DNL Twitter] API is verzonden, wordt weergegeven zoals u had verwacht in de [!DNL Twitter] -gebruikersinterface.

Als de gebeurtenisverzameling en [!DNL Experience Platform] -integratie zijn gelukt, ziet u gebeurtenissen in de [!DNL Twitter] [!UICONTROL Events manager] .

![&#x200B; de [!DNL Twitter] gebeurtenismanager &#x200B;](../../../images/extensions/server/twitter/event-manager.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe conversiegebeurtenissen naar [!DNL Twitter] kunnen worden verzonden via het doorsturen van gebeurtenissen. Raadpleeg de officiële documentatie voor meer informatie over deze onderliggende technologieën:

* [[!DNL Twitter]  APIs &#x200B;](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter]  de omzetting API van het Web &#x200B;](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [&#128279;](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) Token van de Toegang van 0&rbrace; Gebruiker[!DNL Twitter] 
* [&#x200B; identiteitskaart van het Pixel en omzetting die &#x200B;](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) volgen
