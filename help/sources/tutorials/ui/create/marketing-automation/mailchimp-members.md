---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Een MailChimp-bronverbinding voor leden maken met de gebruikersinterface van het Platform
topic-legacy: tutorial
description: Leer hoe u Adobe Experience Platform met MailChimp-leden verbindt via de gebruikersinterface van het Platform.
source-git-commit: a67f9589346a117eb6f51dc9f908680d661e5d5b
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 0%

---


# Een [!DNL Mailchimp Members] bronverbinding met gebruikersinterface van Platform

Deze zelfstudie bevat stappen voor het maken van een [!DNL Mailchimp] bronaansluiting voor opnemen [!DNL Mailchimp Members] gegevens naar Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze handleiding vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../../../home.md): Met Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met [!DNL Platform] diensten.
* [Sandboxen](../../../../../sandboxes/home.md): Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

## Vereiste referenties verzamelen

Om uw [!DNL Mailchimp Members] gegevens aan Platform, moet u eerst de aangewezen authentificatiegeloofsbrieven verstrekken die met uw beantwoorden [!DNL Mailchimp] account.

De [!DNL Mailchimp Members] De bron steunt zowel OAuth 2 vernieuwt Code als basisauthentificatie. Zie de lijsten hieronder voor meer informatie over deze authentificatietypen.

### Code vernieuwen 2

| Credentials | Beschrijving |
| --- | --- |
| Host | De basis-URL waarmee verbinding wordt gemaakt met de MailChimp-API. De indeling voor de basis-URL is `https://{DC}.api.mailchimp.com`, waarbij `{DC}` vertegenwoordigt het datacenter dat overeenkomt met uw account. |
| Autorisatietest-URL | De autorisatietest-URL wordt gebruikt om referenties te valideren wanneer verbinding wordt gemaakt [!DNL Mailchimp] naar Platform. Als dit niet wordt opgegeven, worden de referenties in plaats daarvan automatisch gecontroleerd tijdens het maken van de bronverbinding. |
| Toegangstoken | Het overeenkomstige toegangstoken dat wordt gebruikt om uw bron voor authentiek te verklaren. Dit is vereist voor verificatie op basis van OAuth. |

Voor meer informatie bij het gebruiken van OAuth 2 om uw voor authentiek te verklaren [!DNL Mailchimp] account aan Platform, zie deze [[!DNL Mailchimp] document over het gebruik van OAuth 2](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### Basisverificatie

| Credentials | Beschrijving |
| --- | --- |
| Host | De basis-URL waarmee verbinding wordt gemaakt met de MailChimp-API. De indeling voor de basis-URL is `https://{DC}.api.mailchimp.com`, waarbij `{DC}` vertegenwoordigt het datacenter dat overeenkomt met uw account. |
| Gebruikersnaam | De gebruikersnaam die overeenkomt met uw MailChimp-account. Dit is vereist voor basisverificatie. |
| Wachtwoord | Het wachtwoord dat overeenkomt met uw MailChimp-account. Dit is vereist voor basisverificatie. |

## Verbind uw [!DNL Mailchimp Members] account aan Platform

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Marketing automation] categorie, selecteert u **[!UICONTROL Mailchimp Campaign]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/mailchimp-members/catalog.png)

De **[!UICONTROL Connect Mailchimp Campaigns account]** wordt weergegeven. Op deze pagina kunt u opgeven of u een bestaande account wilt openen of een nieuwe account wilt maken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Mailchimp Members] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/mailchimp-members/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam en een beschrijving voor uw [!DNL Mailchimp Members] bronverbindingsgegevens.

![new](../../../../images/tutorials/create/mailchimp-members/new.png)


#### Verifiëren met OAuth 2

Als u OAuth 2 wilt gebruiken, selecteert u [!UICONTROL OAuth 2 Refresh Code], geef waarden op voor uw host, test URL voor autorisatie en toegangstoken en selecteer vervolgens **[!UICONTROL Connect to source]**. Laat uw referenties even valideren en selecteer **[!UICONTROL Next]** om verder te gaan.

![oauth](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### Verifiëren met basisverificatie

Selecteer [!UICONTROL Basic authentication], geef waarden op voor uw host, gebruikersnaam en wachtwoord en selecteer **[!UICONTROL Connect to source]**. Laat uw referenties even valideren en selecteer **[!UICONTROL Next]** om verder te gaan.

![basis](../../../../images/tutorials/create/mailchimp-members/basic.png)

### Selecteren [!DNL Mailchimp Members] data

Zodra uw bron voor authentiek wordt verklaard, moet u dan verstrekken `listId` dat overeenkomt met uw [!DNL Mailchimp Members] account.

Op de [!UICONTROL Select data] pagina, voert u uw `listId` en selecteer vervolgens **[!UICONTROL Explore]**.

![verkennen](../../../../images/tutorials/create/mailchimp-members/explore.png)

De pagina wordt bijgewerkt in een interactieve schemastructuur waarmee u de hiërarchie van uw gegevens kunt verkennen en inspecteren. Selecteren **[!UICONTROL Next]** om verder te gaan.

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## Volgende stappen

Met uw [!DNL Mailchimp] account is geverifieerd en uw [!DNL Mailchimp Members] geselecteerde gegevens, kunt u nu beginnen met het maken van een gegevensstroom om uw gegevens naar het Platform te brengen. Raadpleeg de documentatie bij voor gedetailleerde stappen over het maken van een gegevensstroom [het creëren van een gegevensstroom om de gegevens van de marketing automatisering aan Platform te brengen](../../dataflow/marketing-automation.md).
