---
keywords: Experience Platform;home;populaire onderwerpen;onetrust;OneTrust
solution: Experience Platform
title: (Beta) Creeer een OneTrust Source Connection in UI
topic-legacy: overview
type: Tutorial
description: Leer hoe u een OneTrust-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: cfc6e7cb3877f3b5f716b7f82e7c2d308ef5ed10
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# (Beta) Maak een [!DNL OneTrust Integration] bronverbinding in de gebruikersinterface

>[!NOTE]
>
>De [!DNL OneTrust Integration] De bron is in bèta. De kenmerken en documentatie van het programma kunnen worden gewijzigd. Voor informatie over het gebruik van bèta-gelabelde bronnen raadpleegt u de [overzicht van bronnen](../../../../home.md#terms-and-conditions).

Deze zelfstudie bevat stappen voor het maken van een [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) De bronverbinding om zowel historische als geplande toestemmingsgegevens in Adobe Experience Platform op te nemen gebruikend het gebruikersinterface van het Platform.

## Vereisten

>[!IMPORTANT]
>
>De [!DNL OneTrust Integration] bronaansluiting en documentatie gemaakt door de [!DNL OneTrust Integration] team. Voor vragen of verzoeken om updates kunt u contact opnemen met de [[!DNL OneTrust] team](https://my.onetrust.com/s/contactsupport?language=en_US) rechtstreeks.

Voordat u verbinding maakt [!DNL OneTrust Integration] aan Platform, moet u uw toegangstoken eerst terugwinnen. Voor gedetailleerde instructies bij het vinden van uw toegangstoken, zie [[!DNL OneTrust Integration] Handleiding OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Het toegangstoken verfrist zich niet automatisch na het verloopt omdat het systeem-aan-systeem tokens verfrist niet door wordt gesteund [!DNL OneTrust]. Daarom is het noodzakelijk om ervoor te zorgen dat uw toegangstoken in de verbinding wordt bijgewerkt alvorens het verloopt. De maximum configureerbare levensduur voor een toegangstoken is één jaar. Voor meer informatie over het bijwerken van uw toegangstoken, zie [[!DNL OneTrust] document over het beheren van uw OAuth 2.0-clientreferenties](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Vereiste referenties verzamelen

Om verbinding te maken [!DNL OneTrust Integration] aan Platform, moet u waarden voor de volgende authentificatiegeloofsbrieven verstrekken:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Hostnaam | Het milieu waarvan [!DNL OneTrust Integration] gegevens moeten worden opgehaald. | `https://uat.onetrust.com/` |
| Autorisatietest-URL | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |  |
| Toegangstoken | Het toegangstoken dat met uw [!DNL OneTrust Integration] account. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Voor meer informatie over deze geloofsbrieven, zie [[!DNL OneTrust Integration] verificatiedocumentatie](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Verbind uw [!DNL OneTrust Integration] account

>[!NOTE]
>
>De [!DNL OneTrust Integration] API-specificaties worden gedeeld met Adobe voor gegevensinvoer.

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *[!UICONTROL Consent & Preferences]* categorie, selecteert u [!DNL OneTrust Integration]en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/onetrust/catalog.png)

De **[!UICONTROL Connect OneTrust Integration account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL OneTrust Integration] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/onetrust/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam, een optionele beschrijving en uw referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/onetrust/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL OneTrust Integration] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over toestemming in Platform te brengen](../../dataflow/consent-and-preferences.md).
