---
title: Verbinding maken met uw Salesforce Service Cloud-account via de Experience Platform-gebruikersinterface
description: Leer hoe u uw Salesforce Service Cloud-account kunt aansluiten en uw gegevens over klantresultaten naar Experience Platform kunt brengen via de gebruikersinterface.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Sluit uw [!DNL Salesforce Service Cloud] -account aan op Experience Platform via de gebruikersinterface

Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding tussen uw [!DNL Salesforce Service Cloud] -account en voor het tot stand brengen van gegevens voor klanten naar Adobe Experience Platform via de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Salesforce Service Cloud] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [&#x200B; vormend een dataflow voor een klantensucces &#x200B;](../../dataflow/customer-success.md)

### Vereiste referenties verzamelen

>[!WARNING]
>
>Basisverificatie voor de [!DNL Salesforce Service Cloud] -bron wordt in januari 2026 afgekeurd. U moet naar OAuth 2 Client Credential-verificatie gaan om de bron te kunnen blijven gebruiken en gegevens van uw [!DNL Salesforce Service Cloud] -account te kunnen invoeren naar Experience Platform.

De [!DNL Salesforce Service Cloud] -bron ondersteunt basisverificatie en OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

U moet waarden opgeven voor de volgende referenties om uw [!DNL Salesforce Service Cloud] -account te verbinden met behulp van basisverificatie.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de broninstantie [!DNL Salesforce Service Cloud] . |
| Gebruikersnaam | De gebruikersnaam voor de gebruikersaccount van [!DNL Salesforce Service Cloud] . |
| Wachtwoord | Het wachtwoord voor de [!DNL Salesforce Service Cloud] -gebruikersaccount. |
| Beveiligingstoken | Het beveiligingstoken voor de gebruikersaccount van [!DNL Salesforce Service Cloud] . |
| API-versie | (Optioneel) De REST API-versie van de instantie [!DNL Salesforce Service Cloud] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt Experience Platform automatisch de meest recente beschikbare versie. |

Voor meer informatie over authentificatie, verwijs naar [&#x200B; deze  [!DNL Salesforce Service Cloud]  authentificatiegids &#x200B;](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB  OAuth2 Client Credential ]

U moet waarden opgeven voor de volgende referenties om uw [!DNL Salesforce Service Cloud] -account aan te sluiten met OAuth2 Client Credential.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de broninstantie [!DNL Salesforce Service Cloud] . |
| Client-id | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce Service Cloud] . |
| Clientgeheim | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce Service Cloud] . |
| API-versie | De REST API-versie van de instantie [!DNL Salesforce Service Cloud] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt Experience Platform automatisch de meest recente beschikbare versie. |

Voor meer informatie bij het gebruiken van OAuth voor [!DNL Salesforce Service Cloud], lees de [[!DNL Salesforce Service Cloud]  gids over de Stroom van de Vergunning OAuth &#x200B;](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

>[!ENDTABS]

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Salesforce Service Cloud] -account te verbinden met Experience Platform.

## Sluit uw [!DNL Salesforce Service Cloud] -account aan

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!DNL Salesforce Service Cloud]** onder de categorie *[!UICONTROL Customer success]* en selecteer vervolgens **[!UICONTROL Add data]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![&#x200B; de broncatalogus op UI van Experience Platform met de geselecteerde Bron van de Wolk van de Dienst van Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

De pagina **[!UICONTROL Connect to Salesforce Service Cloud]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens het gewenste account in de lijst die wordt weergegeven. Als u klaar bent, selecteert u **[!UICONTROL Next]** om door te gaan.

![&#x200B; een lijst van voor authentiek verklaarde rekeningen van de Wolk van de Dienst van Salesforce die reeds in uw organisatie bestaan.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en een beschrijving voor uw nieuwe [!DNL Salesforce Service Cloud] -account.

![&#x200B; de interface waarin u een nieuwe rekening van de Wolk van de Dienst van Salesforce kunt tot stand brengen door de aangewezen authentificatiegeloofsbrieven te verstrekken.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

Selecteer vervolgens het verificatietype dat u voor uw nieuwe account wilt gebruiken.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Selecteer **[!UICONTROL Basic authentication]** voor basisverificatie en geef waarden op voor de volgende referenties:

* URL van omgeving
* Gebruikersnaam
* Wachtwoord
* API-versie (optioneel)

Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![&#x200B; de basisauthentificatieinterface voor de rekeningsverwezenlijking van Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB  OAuth2 Client Credential ]

Selecteer **[!UICONTROL OAuth2 Client Credential]** voor OAuth 2 Client Credential en geef waarden op voor de volgende referenties:

* URL van omgeving
* Client-id
* Clientgeheim
* API-versie

Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![&#x200B; de interface OAuth voor de rekeningsverwezenlijking van Salesforce.](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Salesforce Service Cloud] -account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om de gegevens van het Succes van de Klant in Experience Platform &#x200B;](../../dataflow/customer-success.md) te brengen.
