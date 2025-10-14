---
keywords: Experience Platform;home;populaire onderwerpen;Algemene REST API
title: Een algemene REST API Source-verbinding maken in de gebruikersinterface
type: Tutorial
description: Leer hoe u een algemene REST API-bronverbinding maakt met de gebruikersinterface van Adobe Experience Platform.
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Een [!DNL Generic REST API] bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
> De bron [!DNL Generic REST API] is in bèta. Zie het [&#x200B; Bronoverzicht &#x200B;](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Generic REST API] bronaansluiting met behulp van de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [&#x200B; Bronnen &#x200B;](../../../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Sandboxes &#x200B;](../../../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Vereiste referenties verzamelen

Als u toegang wilt tot uw [!DNL Generic REST API] -account op Experience Platform, moet u geldige gegevens opgeven voor het type verificatie dat u kiest. Generieke REST API ondersteunt zowel OAuth 2-vernieuwingscode als basisverificatie. Zie de volgende lijsten voor informatie over de geloofsbrieven voor de twee gesteunde authentificatietypen.

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

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekbalk.

Selecteer onder de categorie [!UICONTROL Protocols] de optie **[!UICONTROL Generic REST API]** en selecteer vervolgens **[!UICONTROL Add data]** .

![&#x200B; catalogus &#x200B;](../../../../images/tutorials/create/generic-rest/catalog.png)

De pagina **[!UICONTROL Connect to Generic REST API]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u de algemene REST API-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![&#x200B; bestaand &#x200B;](../../../../images/tutorials/create/generic-rest/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam en een optiebeschrijving voor uw nieuwe [!DNL Generic REST API] -account.

![&#x200B; nieuw &#x200B;](../../../../images/tutorials/create/generic-rest/new.png)

#### Verifiëren met OAuth 2-vernieuwingscode

[!DNL Generic REST API] ondersteunt zowel OAuth 2 om code te vernieuwen als basisverificatie. Als u wilt verifiëren met een OAuth2-verificatie, selecteert u **[!UICONTROL OAuth2RefreshCode]**, geeft u uw OAuth 2-referenties op en selecteert u vervolgens **[!UICONTROL Connect to source]** .

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### Verifiëren met gebruik van basisverificatie

Als u standaardverificatie wilt gebruiken, selecteert u **[!UICONTROL Basic authentication]** , geeft u uw host, gebruikersnaam en wachtwoord op en selecteert u vervolgens **[!UICONTROL Connect to source]** .

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw algemene REST API-account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens in Experience Platform &#x200B;](../../dataflow/protocols.md) te brengen.
