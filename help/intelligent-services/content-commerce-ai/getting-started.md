---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: Aan de slag met Content and Commerce AI
topic: Getting started
description: De Inhoud en de Handel AI gebruikt Adobe I/O APIs. Om vraag aan Adobe I/O APIs en de Integratie I/O van de Console te maken, moet u het authentificatieleerprogramma eerst voltooien.
translation-type: tm+mt
source-git-commit: 2be04547b96e1a6c293cc63e782fe1b3259619ba
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# Aan de slag met Content and Commerce AI

>[!NOTE]
>
>AI van de Inhoud en van de Handel is in bèta. De documentatie kan worden gewijzigd.

[!DNL Content and Commerce AI] gebruikt Adobe I/O-API&#39;s. Om vraag aan Adobe I/O APIs en de Integratie I/O van de Console te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien.

Wanneer u echter de stap API **** toevoegen uitvoert, bevindt de API zich onder Experience Cloud in plaats van Adobe Experience Platform, zoals in de volgende schermafbeelding wordt getoond:

![AI voor inhoud en handel toevoegen](./images/add-api.png)

Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle I/O API-aanroepen van Adobe, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Een postmanomgeving maken (optioneel)

Nadat u uw project en API hebt ingesteld in de Adobe Developer Console, kunt u een omgevingsbestand voor Postman downloaden. Selecteer onder **[!UICONTROL APIs]** de linkerspoorlijn van uw project, **[!UICONTROL Inhoud en Handel AI]**. Er wordt een nieuw tabblad geopend met een kaart met het label &quot;[!DNL Try it out]&quot;. Selecteer **Download voor Postman** om een JSON-bestand te downloaden dat wordt gebruikt om uw postmanomgeving te configureren.

![download voor postbode](./images/add-to-postman.png)

Nadat u het bestand hebt gedownload, opent u Postman en selecteert u het **tandwielpictogram** rechtsboven om het dialoogvenster **Omgevingen** beheren te openen.

![tandwielpictogram](./images/select-gear-icon.png)

Selecteer vervolgens **Importeren** in het dialoogvenster **Omgevingen** beheren.

![import](./images/import.png)

U wordt omgeleid en gevraagd om een omgevingsbestand van uw computer te selecteren. Selecteer het JSON-bestand dat u eerder hebt gedownload en selecteer vervolgens **Openen** om de omgeving te laden.

![](./images/choose-your-file.png)

![](./images/click-open.png)

U wordt opnieuw omgeleid naar het tabblad *Omgevingen* beheren met een nieuwe omgevingsnaam ingevuld. Selecteer de omgevingsnaam om de variabelen in Postman weer te geven en te bewerken. U moet nog manueel bevolken `JWT_TOKEN` en `ACCESS_TOKEN`. Deze waarden hadden moeten worden verkregen tijdens het voltooien van de [verificatiezelfstudie](../../tutorials/authentication.md).

![](./images/re-direct.png)

Nadat de variabelen zijn voltooid, moeten ze er ongeveer als volgt uitzien: Selecteer **Bijwerken** om het instellen van de omgeving te voltooien.

![](./images/final-environment.png)

U kunt nu de omgeving selecteren in het vervolgkeuzemenu rechtsboven in het scherm en opgeslagen waarden automatisch vullen. U bewerkt gewoon de waarden op elk gewenst moment opnieuw om al uw API-aanroepen bij te werken.

![voorbeeld](./images/select-environment.png)

Voor meer informatie over het werken met Adobe I/O APIs die Postman gebruiken, zie de Middelgrote post over het [gebruiken van Postman voor authentificatie JWT op Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md) in de het oplossen van problemengids van het Experience Platform te lezen.

## Volgende stappen {#next-steps}

Zodra u al uw referenties hebt, kunt u een aangepaste worker instellen voor [!DNL Content and Commerce AI]. De volgende documenten helpen bij het begrijpen van het uitbreidingsframework en de omgeving.

Om meer over het Kader van de Rekbaarheid te leren, begin door de [inleiding aan rekbaarheiddocument](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) te lezen. In dit document worden de voorwaarden en de inrichtingsvereisten beschreven.

Voor meer informatie over het instellen van een omgeving voor [!DNL Content and Commerce AI], begint u met het lezen van de handleiding voor het [instellen van een ontwikkelomgeving](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html). Dit document bevat instellingsinstructies waarmee u de service Asset compute kunt ontwikkelen.