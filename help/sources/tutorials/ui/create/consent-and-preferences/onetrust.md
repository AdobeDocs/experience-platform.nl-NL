---
keywords: Experience Platform;home;populaire onderwerpen;onetrust;OneTrust
solution: Experience Platform
title: Een OneTrust Source-verbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een OneTrust-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Een [!DNL OneTrust Integration] bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De bron [!DNL OneTrust Integration] ondersteunt alleen het opnemen van toestemmings- en voorkeursgegevens en geen cookies.

Deze zelfstudie biedt stappen voor het maken van een [[!DNL OneTrust Integration] &#x200B;](https://my.onetrust.com/s/contactsupport?language=en_US) -bronverbinding om zowel historische als geplande toestemmingsgegevens in Adobe Experience Platform in te voeren via de Experience Platform-gebruikersinterface.

## Vereisten

>[!IMPORTANT]
>
>De [!DNL OneTrust Integration] bronconnector en documentatie zijn gemaakt door het [!DNL OneTrust Integration] -team. Voor om het even welke onderzoeken of updateverzoeken, gelieve het [[!DNL OneTrust]  team &#x200B;](https://my.onetrust.com/s/contactsupport?language=en_US) direct te contacteren.

Voordat u [!DNL OneTrust Integration] kunt verbinden met Experience Platform, moet u eerst uw toegangstoken ophalen. Voor gedetailleerde instructies bij het vinden van uw toegangstoken, zie [[!DNL OneTrust Integration]  OAuth 2 gids &#x200B;](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Het toegangstoken wordt niet automatisch vernieuwd nadat het verloopt omdat de systeem-aan-systeem vernieuwingstokens niet door [!DNL OneTrust] worden gesteund. Daarom is het noodzakelijk om ervoor te zorgen dat uw toegangstoken in de verbinding wordt bijgewerkt alvorens het verloopt. De maximum configureerbare levensduur voor een toegangstoken is één jaar. Meer leren over het bijwerken van uw toegangstoken, zie het [[!DNL OneTrust]  document bij het beheren van uw OAuth 2.0 cliëntgeloofsbrieven &#x200B;](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Vereiste referenties verzamelen

Als u [!DNL OneTrust Integration] wilt verbinden met Experience Platform, moet u waarden opgeven voor de volgende verificatiereferenties:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Hostnaam | De omgeving waaruit de [!DNL OneTrust Integration] -gegevens moeten worden opgehaald. | `app.onetrust.com` |
| Autorisatietest-URL | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. | |
| Toegangstoken | Het toegangstoken dat overeenkomt met uw [!DNL OneTrust Integration] -account. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Voor meer informatie over deze geloofsbrieven, zie de [[!DNL OneTrust Integration]  authentificatiedocumentatie &#x200B;](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Sluit uw [!DNL OneTrust Integration] -account aan

>[!NOTE]
>
>De API-specificaties van [!DNL OneTrust Integration] worden gedeeld met Adobe voor gegevensinvoer.

In de gebruikersinterface van Experience Platform selecteert u **[!UICONTROL Sources]** in de linkernavigatie om de werkruimte van [!UICONTROL Sources] te openen voor een catalogus met bronnen die beschikbaar zijn in Experience Platform.

Gebruik het menu *[!UICONTROL Categories]* om bronnen op categorie te filteren. U kunt ook een bronnaam invoeren in de zoekbalk om een specifieke bron uit de catalogus te zoeken.

Ga naar de categorie [!UICONTROL Consent & Preferences] voor de [!DNL OneTrust Integration] -bronkaart. Selecteer eerst **[!UICONTROL Add data]** .

![&#x200B; de de broncatalogus van Experience Platform UI.](../../../../images/tutorials/create/onetrust/catalog.png)

De pagina **[!UICONTROL Connect OneTrust Integration account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL OneTrust Integration] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![&#x200B; de bestaande stap van de rekeningsauthentificatie in het bronwerkschema.](../../../../images/tutorials/create/onetrust/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u een naam, een optionele beschrijving en uw referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![&#x200B; de nieuwe stap van de rekeningsauthentificatie in het bronwerkschema.](../../../../images/tutorials/create/onetrust/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL OneTrust Integration] -account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om toestemmingsgegevens in Experience Platform &#x200B;](../../dataflow/consent-and-preferences.md) te brengen.
