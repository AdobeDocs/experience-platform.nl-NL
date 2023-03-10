---
keywords: Experience Platform;aan de slag;content ai;commerce ai;content tagging
solution: Experience Platform
title: Aan de slag met tags van inhoud
description: Tags voor inhoud maken gebruik van Adobe I/O-API's. Om vraag aan Adobe I/O APIs en de I/O Integratie van de Console te maken, moet u het authentificatieleerprogramma eerst voltooien.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a98639851e7245b9cbd6fe42b35b4730dd19c3f8
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Aan de slag met Inhoud taggen

[!DNL Content tagging] gebruikt Adobe I/O API&#39;s. Als u aanroepen wilt uitvoeren naar Adobe I/O API&#39;s en de I/O-consolesupintegratie, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en).

Wanneer u echter de **API toevoegen** De API bevindt zich stap voor stap onder Experience Cloud in plaats van Adobe Experience Platform, zoals in de volgende schermafbeelding wordt getoond:

![toevoegen van inhoudscodes](./images/add-api-updated.png)

Het voltooien van het authentificatieleerprogramma verstrekt de waarden voor elk van de vereiste kopballen in alle Adobe I/O API vraag, zoals hieronder getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Een Postman-omgeving maken (optioneel)

Als u uw project en API hebt ingesteld in Adobe Developer Console, kunt u een omgevingsbestand voor Postman downloaden. Onder **[!UICONTROL APIs]** het linkerspoor van uw project, selecteer **[!UICONTROL Content tagging]**. Er wordt een nieuw tabblad geopend met een kaart met het label &quot;[!DNL Try it out]&quot;. Selecteren **Downloaden naar Postman** om een JSON-bestand te downloaden dat wordt gebruikt om uw postmanomgeving te configureren.

![download voor postbode](./images/add-to-postman-updated.png)

Als u het bestand hebt gedownload, opent u Postman en selecteert u de **tandwielpictogram** in de rechterbovenhoek **omgevingen beheren** .

![tandwielpictogram](./images/select-gear-icon.png)

Selecteer vervolgens **Importeren** van binnen **Omgevingen beheren** .

![import](./images/import-updated.png)

U wordt omgeleid en gevraagd om een omgevingsbestand van uw computer te selecteren. Selecteer het JSON-bestand dat u eerder hebt gedownload en selecteer **Openen** om de omgeving te laden.

![](./images/choose-your-file.png)

![](./images/click-open.png)

U wordt omgeleid naar de *Omgevingen beheren* met een nieuwe omgevingsnaam ingevuld. Selecteer de omgevingsnaam om de variabelen in Postman weer te geven en te bewerken. U moet nog steeds handmatig de `JWT_TOKEN` en `ACCESS_TOKEN`. Deze waarden hadden moeten worden verkregen tijdens het voltooien van de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct-updated.png)

Nadat de variabelen zijn voltooid, moeten ze er ongeveer als volgt uitzien: Selecteren **Bijwerken** om uw omgeving te voltooien.

![](./images/final-environment-updated.png)

U kunt nu de omgeving selecteren in het vervolgkeuzemenu rechtsboven in het scherm en opgeslagen waarden automatisch vullen. U bewerkt gewoon de waarden op elk gewenst moment opnieuw om al uw API-aanroepen bij te werken.

![voorbeeld](./images/select-environment-updated.png)

Voor meer informatie over het werken met Adobe I/O API&#39;s die Postman gebruiken, raadpleegt u het artikel Medium op [Postman gebruiken voor JWT-verificatie op Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md) in de gids voor het oplossen van problemen met Experience Platforms.

## Volgende stappen {#next-steps}

Zodra u al uw referenties hebt, kunt u een aangepaste worker instellen voor [!DNL Content tagging]. De volgende documenten helpen bij het begrijpen van het uitbreidingsframework en de omgeving.

Om meer over het Kader van de Rekbaarheid te leren, begin door te lezen [inleiding tot uitbreidbaarheid](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html) document. In dit document worden de voorwaarden en de inrichtingsvereisten beschreven.

Meer informatie over het instellen van een omgeving voor [!DNL Content tagging], te beginnen met het lezen van de handleiding voor [een ontwikkelomgeving instellen](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Dit document bevat instellingsinstructies waarmee u de service Asset compute kunt ontwikkelen.
