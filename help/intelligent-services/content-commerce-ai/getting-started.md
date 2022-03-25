---
keywords: Experience Platform;aan de slag;content ai;commerce ai;content en commerce ai
solution: Intelligent Services
title: Aan de slag met AI voor Inhoud en Handel
topic-legacy: Getting started
description: De Inhoud en de Handel AI gebruikt Adobe I/O APIs. In order to make calls to Adobe I/O APIs and the I/O Console Integration, you must first complete the authentication tutorial.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 0%

---

# Getting started with Content and Commerce AI

>[!NOTE]
>
>Content and Commerce AI is in beta. The documentation is subject to change.

[!DNL Content and Commerce AI] gebruikt Adobe I/O API&#39;s. In order to make calls to Adobe I/O APIs and the I/O Console Integration, you must first complete the [authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en).

Wanneer u echter de **API toevoegen** De API bevindt zich stap voor stap onder Experience Cloud in plaats van Adobe Experience Platform, zoals in de volgende schermafbeelding wordt getoond:

![adding Content and Commerce AI](./images/add-api.png)

Het voltooien van het authentificatieleerprogramma verstrekt de waarden voor elk van de vereiste kopballen in alle Adobe I/O API vraag, zoals hieronder getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Een Postman-omgeving maken (optioneel)

Once you have set up your project and API within Adobe Developer Console, you have the option to download an environment file for Postman. Under **[!UICONTROL APIs]** the left rail of your project, select **[!UICONTROL Content and Commerce AI]**. A new tab opens, containing a card labeled &quot;[!DNL Try it out]&quot;. Select **Download for Postman** to download a JSON file used to configure your postman environment.

![download for postman](./images/add-to-postman.png)

Once you have downloaded the file, open Postman and select the **gear icon** in the top right to open up the **manage environments** dialog.

![tandwielpictogram](./images/select-gear-icon.png)

Selecteer vervolgens **Importeren** van binnen **Omgevingen beheren** .

![import](./images/import.png)

You are redirected and asked to select an environment file from your computer. Selecteer het JSON-bestand dat u eerder hebt gedownload en selecteer **Openen** om de omgeving te laden.

![](./images/choose-your-file.png)

![](./images/click-open.png)

You are redirected back to the *Manage environments* tab with a new environment name populated. Selecteer de omgevingsnaam om de variabelen in Postman weer te geven en te bewerken. U moet nog steeds handmatig de `JWT_TOKEN` en `ACCESS_TOKEN`. Deze waarden hadden moeten worden verkregen tijdens het voltooien van de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

Nadat de variabelen zijn voltooid, moeten ze er ongeveer als volgt uitzien: Selecteren **Bijwerken** om uw omgeving te voltooien.

![](./images/final-environment.png)

U kunt nu de omgeving selecteren in het vervolgkeuzemenu rechtsboven in het scherm en opgeslagen waarden automatisch vullen. U bewerkt gewoon de waarden op elk gewenst moment opnieuw om al uw API-aanroepen bij te werken.

![voorbeeld](./images/select-environment.png)

Voor meer informatie over het werken met Adobe I/O API&#39;s die Postman gebruiken, raadpleegt u het artikel Medium op [Postman gebruiken voor JWT-verificatie op Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. These include paths, required headers, and properly formatted request payloads. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md) in the Experience Platform troubleshooting guide.

## Volgende stappen {#next-steps}

Once you have all your credentials, you are ready to set up a custom worker for [!DNL Content and Commerce AI]. De volgende documenten helpen bij het begrijpen van het uitbreidingsframework en de omgeving.

Om meer over het Kader van de Rekbaarheid te leren, begin door te lezen [inleiding tot uitbreidbaarheid](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) document. In dit document worden de voorwaarden en de inrichtingsvereisten beschreven.

To learn more about setting up an environment for [!DNL Content and Commerce AI], start by reading the guide for [setting up a developer environment](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Dit document bevat instellingsinstructies waarmee u de service Asset compute kunt ontwikkelen.
