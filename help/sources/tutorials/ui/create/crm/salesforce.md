---
title: Verbinding maken met uw Salesforce-account via de gebruikersinterface van het Experience Platform
description: Leer hoe u uw Salesforce-account koppelt en uw CRM-gegevens via de gebruikersinterface naar het Experience Platform brengt.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: ae322ee421edd73cd5a3fb8499267cd417491318
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 0%

---

# Sluit uw [!DNL Salesforce] -account aan op het Experience Platform via de gebruikersinterface

Deze zelfstudie bevat stappen voor het verbinden van uw [!DNL Salesforce] -account en het doorgeven van uw CRM-gegevens aan Adobe Experience Platform via de gebruikersinterface van het Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een voor authentiek verklaarde [!DNL Salesforce] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow voor de gegevens van CRM ](../../dataflow/crm.md).

### Vereiste referenties verzamelen {#gather-required-credentials}

De [!DNL Salesforce] -bron ondersteunt basisverificatie en OAuth2 Client Credential.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

U moet waarden opgeven voor de volgende referenties om uw [!DNL Salesforce] -account te verbinden met behulp van basisverificatie.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de broninstantie [!DNL Salesforce] . De indeling voor omgeving-URL is `https://[domain].my.salesforce.com` . |
| Gebruikersnaam | De gebruikersnaam voor de gebruikersaccount van [!DNL Salesforce] . |
| Wachtwoord | Het wachtwoord voor de [!DNL Salesforce] -gebruikersaccount. |
| Beveiligingstoken | Het beveiligingstoken voor de gebruikersaccount van [!DNL Salesforce] . |
| API-versie | (Optioneel) De REST API-versie van de instantie [!DNL Salesforce] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |

Voor meer informatie over authentificatie, verwijs naar [ deze  [!DNL Salesforce]  authentificatiegids ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB  OAuth2 Client Credential ]

U moet waarden opgeven voor de volgende referenties om uw [!DNL Salesforce] -account aan te sluiten met OAuth2 Client Credential.

| Credentials | Beschrijving |
| --- | --- |
| URL van omgeving | De URL van de broninstantie [!DNL Salesforce] . De indeling voor omgeving-URL is `https://[domain].my.salesforce.com` . |
| Client-id | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce] . |
| Clientgeheim | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van OAuth2-verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing aan te duiden op [!DNL Salesforce] . |
| API-versie | De REST API-versie van de instantie [!DNL Salesforce] die u gebruikt. De waarde voor de API-versie moet met een decimaal worden opgemaakt. Als u bijvoorbeeld API-versie `52` gebruikt, moet u de waarde invoeren als `52.0` . Als dit veld niet wordt ingevuld, gebruikt het Experience Platform automatisch de meest recente beschikbare versie. |

Voor meer informatie bij het gebruiken van OAuth voor [!DNL Salesforce], lees de [[!DNL Salesforce]  gids over de Stroom van de Vergunning OAuth ](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Salesforce] -account te verbinden met het Experience Platform.

## Sluit uw [!DNL Salesforce] -account aan

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer **[!DNL Salesforce]** onder de categorie *[!UICONTROL CRM]* en selecteer vervolgens **[!UICONTROL Add data]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account bestaat, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus op het Experience Platform UI met geselecteerde de bronkaart van Salesforce.](../../../../images/tutorials/create/salesforce/catalog.png)

De pagina **[!UICONTROL Connect to Salesforce]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven. Als u klaar bent, selecteert u **[!UICONTROL Next]** om door te gaan.

![ een lijst van voor authentiek verklaarde rekeningen van Salesforce die reeds in uw organisatie bestaan.](../../../../images/tutorials/create/salesforce/existing.png)

### Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam en een beschrijving voor uw nieuwe [!DNL Salesforce] -account.

![ de interface waarin u een nieuwe rekening van Salesforce kunt tot stand brengen door de aangewezen authentificatiegeloofsbrieven te verstrekken.](../../../../images/tutorials/create/salesforce/new.png)

Selecteer vervolgens het verificatietype dat u voor uw nieuwe account wilt gebruiken.

>[!BEGINTABS]

>[!TAB  Basisauthentificatie ]

Selecteer **[!UICONTROL Basic authentication]** voor basisverificatie en geef waarden op voor de volgende referenties:

* URL van omgeving
* Gebruikersnaam
* Wachtwoord
* API-versie (optioneel)

Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![ de basisauthentificatieinterface voor de rekeningsverwezenlijking van Salesforce.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB  OAuth2 Client Credential ]

Selecteer **[!UICONTROL OAuth2 Client Credential]** voor OAuth 2 Client Credential en geef waarden op voor de volgende referenties:

* URL van omgeving
* Client-id
* Clientgeheim
* API-versie

Selecteer **[!UICONTROL Connect to source]** als u klaar bent.

![ de interface OAuth voor de rekeningsverwezenlijking van Salesforce.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

### Voorvertoning van voorbeeldgegevens overslaan {#skip-preview-of-sample-data}

Tijdens de stap voor gegevensselectie kan er een time-out optreden wanneer u grote tabellen of bestanden met gegevens opgeeft. U kunt gegevensvoorvertoning overslaan om de time-out te omzeilen en toch uw schema weer te geven, zij het zonder voorbeeldgegevens. Als u de gegevensvoorvertoning wilt overslaan, schakelt u de schakeloptie **[!UICONTROL Skip previewing sample data]** in.

De rest van de workflow blijft ongewijzigd. Het enige voorbehoud is dat bij het overslaan van de gegevensvoorvertoning berekende en vereiste velden mogelijk niet automatisch worden gevalideerd tijdens de toewijzingsstap. Vervolgens moet u deze velden handmatig valideren tijdens de toewijzing.

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Salesforce] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in  [!DNL Platform]](../../dataflow/crm.md) te brengen.
