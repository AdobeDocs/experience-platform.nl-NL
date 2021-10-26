---
keywords: Experience Platform;home;populaire onderwerpen;Algemene REST API
title: Een algemene REST API-bronverbinding maken in de gebruikersinterface
topic-legacy: overview
type: Tutorial
description: Leer hoe u een algemene REST API-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
exl-id: fb2038b9-7f27-4818-b5de-cc8072122127
source-git-commit: 1a9c4d5ba3ba9201378e78c0e92dea5101668a24
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Een [!DNL Generic REST API] bronverbinding in de gebruikersinterface

>[!NOTE]
>
> De [!DNL Generic REST API] De bron is in bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Generic REST API] bronaansluiting die gebruikmaakt van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Platform:

* [Bronnen](../../../../home.md): Met Experience Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Experience Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Generic REST API] op Platform, moet u geldige geloofsbrieven voor het authentificatietype van uw keus verstrekken. Generieke REST API ondersteunt zowel OAuth 2-vernieuwingscode als basisverificatie. Zie de volgende lijsten voor informatie over de geloofsbrieven voor de twee gesteunde authentificatietypen.

#### Code voor 2 vernieuwen

| Credentials | Beschrijving |
| --- | --- |
| Host | De host-URL van de bron waarnaar u een verzoek indient. Deze waarde is vereist en kan niet worden omzeild door de parameter override van de aanvraag te gebruiken. |
| Autorisatietest-URL | (Optioneel) De autorisatietest-URL wordt gebruikt om referenties te valideren bij het maken van een basisverbinding. Als deze optie niet is opgegeven, worden de referenties automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| Client-id | (Optioneel) De client-id die aan uw gebruikersaccount is gekoppeld. |
| Clientgeheim | (Optioneel) Het clientgeheim dat aan uw gebruikersaccount is gekoppeld. |
| Toegangstoken | De primaire verificatiereferentie die wordt gebruikt voor toegang tot uw toepassing. Het toegangstoken vertegenwoordigt de toestemming van uw toepassing, om tot bepaalde aspecten van de gegevens van een gebruiker toegang te hebben. Deze waarde is vereist en kan niet worden omzeild door de parameter override van de aanvraag te gebruiken. |
| Token vernieuwen | (Optioneel) Een token dat wordt gebruikt om een nieuw toegangstoken te genereren wanneer het toegangstoken is verlopen. |
| Toegang token-URL | (Optioneel) Het URL-eindpunt dat wordt gebruikt om uw toegangstoken op te halen. |
| Verzoek om parameteroverschrijving | (Optioneel) Een eigenschap waarmee u kunt opgeven welke referentie-parameters moeten worden overschreven. |


#### Basisverificatie

| Credentials | Beschrijving |
| --- | --- |
| Host | De host-URL van de bron waarnaar u een verzoek indient. |
| Gebruikersnaam | De gebruikersnaam die overeenkomt met uw gebruikersaccount. |
| Wachtwoord | Het wachtwoord dat overeenkomt met uw gebruikersaccount. |

## Maak verbinding met uw Generic REST API-account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Onder de [!UICONTROL Protocols] categorie, selecteert u **[!UICONTROL Generic REST API]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/generic-rest/catalog.png)

De **[!UICONTROL Connect to Generic REST API]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de algemene REST API-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/generic-rest/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een beschrijving van de optie voor uw nieuwe [!DNL Generic REST API] account.

![new](../../../../images/tutorials/create/generic-rest/new.png)

#### Verifiëren met OAuth 2-vernieuwingscode

[!DNL Generic REST API] steunt zowel OAuth 2 vernieuwt code en basisauthentificatie. Om het gebruiken van een authentificatie te verifiëren OAuth2, selecteer **[!UICONTROL OAuth2RefreshCode]**, geef uw OAuth 2-referenties op en selecteer **[!UICONTROL Connect to source]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Verifiëren met basisverificatie

Selecteer **[!UICONTROL Basic authentication]**, geef uw host, gebruikersnaam en wachtwoord op en selecteer vervolgens **[!UICONTROL Connect to source]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw algemene REST API-account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens naar het Platform te brengen](../../dataflow/protocols.md).
