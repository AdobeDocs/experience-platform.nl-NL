---
title: Uw Salesforce Service Cloud-account aansluiten via de gebruikersinterface van het Experience Platform
description: Leer hoe u uw Salesforce Service Cloud-account kunt aansluiten en uw gegevens over klantresultaten naar het Experience Platform kunt brengen via de gebruikersinterface.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: 7930a869627130a5db34780e64b809cda0c1e5f4
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---

# Verbind uw [!DNL Salesforce Service Cloud] account aan Experience Platform met behulp van de gebruikersinterface

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL Salesforce Service Cloud] en breng uw gegevens over klantsucces naar Adobe Experience Platform via de gebruikersinterface van het Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige [!DNL Salesforce Service Cloud] verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het vormen van een gegevensstroom voor een klantensucces](../../dataflow/customer-success.md)

### Vereiste referenties verzamelen

De [!DNL Salesforce Service Cloud] De bron steunt basisauthentificatie en de Credentials van de Cliënt OAuth2.

>[!BEGINTABS]

>[!TAB Basisverificatie]

U moet waarden opgeven voor de volgende referenties om verbinding te maken met uw [!DNL Salesforce Service Cloud] account met basisverificatie.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de [!DNL Salesforce Service Cloud] broninstantie. |
| Gebruikersnaam | De gebruikersnaam voor de [!DNL Salesforce Service Cloud] gebruikersaccount. |
| Wachtwoord | Het wachtwoord voor de [!DNL Salesforce Service Cloud] gebruikersaccount. |
| Beveiligingstoken | De beveiligingstoken voor de [!DNL Salesforce Service Cloud] gebruikersaccount. |
| API-versie | (Optioneel) De REST API-versie van de [!DNL Salesforce Service Cloud] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |

Raadpleeg voor meer informatie over verificatie de [dit [!DNL Salesforce Service Cloud] verificatiehandleiding](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 Client Credential]

U moet waarden opgeven voor de volgende referenties om verbinding te maken met uw [!DNL Salesforce Service Cloud] account met OAuth2 Client Credential.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de [!DNL Salesforce Service Cloud] broninstantie. |
| Client-id | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce Service Cloud]. |
| Clientgeheim | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen voor uw account werken door uw toepassing te identificeren voor [!DNL Salesforce Service Cloud]. |
| API-versie | De REST API-versie van de [!DNL Salesforce Service Cloud] -instantie die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie gebruikt `52`vervolgens moet u de waarde invoeren als `52.0`. Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |

Voor meer informatie over het gebruik van OAuth voor [!DNL Salesforce Service Cloud], lees de [[!DNL Salesforce Service Cloud] handleiding over OAuth Authorization Flows](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om verbinding te maken met uw [!DNL Salesforce Service Cloud] aan Experience Platform.

## Verbind uw [!DNL Salesforce Service Cloud] account

Selecteer in de interface Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteren **[!DNL Salesforce Service Cloud]** onder de *[!UICONTROL Customer success]* categorie en selecteer vervolgens **[!UICONTROL Add data]**.

>[!TIP]
>
>De bronnen in de broncatalogus geven de **[!UICONTROL Set up]** als een bepaalde bron nog geen geverifieerde account heeft. Als er eenmaal een geverifieerd account is, wordt deze optie gewijzigd in **[!UICONTROL Add data]**.

![De broncatalogus op de gebruikersinterface van het Experience Platform met de bronkaart van de Salesforce-service Cloud geselecteerd.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

De **[!UICONTROL Connect to Salesforce Service Cloud]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens het gewenste account in de lijst die wordt weergegeven. Selecteer **[!UICONTROL Next]** om verder te gaan.

![Een lijst met geautoriseerde Salesforce Service Cloud-accounts die al in uw organisatie bestaan.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef een naam en een beschrijving voor uw nieuwe [!DNL Salesforce Service Cloud] account.

![De interface waarin u een nieuwe account voor de cloud van de Salesforce-service kunt maken door de juiste verificatiereferenties op te geven.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Selecteer vervolgens het verificatietype dat u voor uw nieuwe account wilt gebruiken.

>[!BEGINTABS]

>[!TAB Basisverificatie]

Selecteer voor basisverificatie de optie **[!UICONTROL Basic authentication]** en geef vervolgens waarden op voor de volgende referenties:

* URL van omgeving
* Gebruikersnaam
* Wachtwoord
* API-versie (optioneel)

Selecteer **[!UICONTROL Connect to source]**.

![De basisauthentificatieinterface voor Salesforce rekeningsverwezenlijking.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB OAuth2 Client Credential]

Voor OAuth 2 Client Credential selecteert u **[!UICONTROL OAuth2 Client Credential]** en geef vervolgens waarden op voor de volgende referenties:

* URL van omgeving
* Client-id
* Clientgeheim
* API-versie

Selecteer **[!UICONTROL Connect to source]**.

![De OAuth interface voor Salesforce account creation.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Salesforce Service Cloud] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens van Klantsucces in Experience Platform te brengen](../../dataflow/customer-success.md).
