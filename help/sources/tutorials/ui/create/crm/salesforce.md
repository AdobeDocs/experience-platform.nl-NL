---
title: Uw Salesforce-account aansluiten via de gebruikersinterface van het Experience Platform
description: Leer hoe u uw Salesforce-account koppelt en uw CRM-gegevens via de gebruikersinterface naar het Experience Platform brengt.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 8d62cf4ca0071e84baa9399e0a25f7ebfb096c1a
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Verbind uw [!DNL Salesforce] account aan Experience Platform met behulp van de gebruikersinterface

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL Salesforce] en breng uw gegevens van CRM naar Adobe Experience Platform gebruikend het gebruikersinterface van het Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geverifieerde [!DNL Salesforce] account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het vormen van een gegevensstroom voor de gegevens van CRM](../../dataflow/crm.md).

### Vereiste referenties verzamelen {#gather-required-credentials}

De [!DNL Salesforce] De bron steunt basisauthentificatie en de Credentials van de Cliënt OAuth2.

>[!BEGINTABS]

>[!TAB Basisverificatie]

U moet waarden opgeven voor de volgende referenties om verbinding te maken met uw [!DNL Salesforce] account met basisverificatie.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de [!DNL Salesforce] broninstantie. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Salesforce] gebruikersaccount. |
| Wachtwoord | Het wachtwoord voor de [!DNL Salesforce] gebruikersaccount. |
| Beveiligingstoken | De beveiligingstoken voor de [!DNL Salesforce] gebruikersaccount. |
| API-versie | (Optioneel) De REST API-versie van de [!DNL Salesforce] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |

Raadpleeg voor meer informatie over verificatie de [dit [!DNL Salesforce] verificatiehandleiding](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 Client Credential]

U moet waarden opgeven voor de volgende referenties om verbinding te maken met uw [!DNL Salesforce] account met OAuth2 Client Credential.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de [!DNL Salesforce] broninstantie. |
| Client-id | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce]. |
| Clientgeheim | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce]. |
| API-versie | De REST API-versie van de [!DNL Salesforce] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |

Voor meer informatie over het gebruik van OAuth voor [!DNL Salesforce], lees de [[!DNL Salesforce] handleiding over OAuth Authorization Flows](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om verbinding te maken met uw [!DNL Salesforce] aan Experience Platform.

## Verbind uw [!DNL Salesforce] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *CRM* categorie, selecteert u **[!DNL Salesforce]** en selecteer vervolgens **[!UICONTROL Add data]**.

>[!TIP]
>
>De bronnen in de broncatalogus geven de **[!UICONTROL Set up]** als een bepaalde bron nog geen geverifieerde account heeft. Als er eenmaal een geverifieerd account is, wordt deze optie gewijzigd in **[!UICONTROL Add data]**.

![De broncatalogus op het Experience Platform UI met de Salesforce-bronkaart geselecteerd.](../../../../images/tutorials/create/salesforce/catalog.png)

De **[!UICONTROL Connect to Salesforce]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven. Selecteer **[!UICONTROL Next]** om verder te gaan.

![Een lijst met geverifieerde Salesforce-accounts die al in uw organisatie bestaan.](../../../../images/tutorials/create/salesforce/existing.png)

### Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef een naam en een beschrijving voor uw nieuwe [!DNL Salesforce] account.

![De interface waarin u een nieuwe rekening kunt tot stand brengen Salesforce door de aangewezen authentificatiegeloofsbrieven te verstrekken.](../../../../images/tutorials/create/salesforce/new.png)

Selecteer vervolgens het verificatietype dat u voor uw nieuwe account wilt gebruiken.

>[!BEGINTABS]

>[!TAB Basisverificatie]

Selecteer voor basisverificatie de optie **[!UICONTROL Basic authentication]** en geef vervolgens waarden op voor de volgende referenties:

* URL van omgeving
* Gebruikersnaam
* Wachtwoord
* API-versie (optioneel)

Selecteer **[!UICONTROL Connect to source]**.

![De basisauthentificatieinterface voor Salesforce rekeningsverwezenlijking.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB OAuth2 Client Credential]

Voor OAuth 2 Client Credential selecteert u **[!UICONTROL OAuth2 Client Credential]** en geef vervolgens waarden op voor de volgende referenties:

* URL van omgeving
* Client-id
* Clientgeheim
* API-versie

Selecteer **[!UICONTROL Connect to source]**.

![De OAuth interface voor Salesforce account creation.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Salesforce] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens over te brengen naar [!DNL Platform]](../../dataflow/crm.md).
