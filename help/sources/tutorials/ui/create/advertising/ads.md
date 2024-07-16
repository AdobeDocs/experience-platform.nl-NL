---
title: Een Google Ads Source Connection maken in de gebruikersinterface
description: Leer hoe u een Google Ads-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Een Google Ads-bronverbinding maken in de gebruikersinterface

>[!WARNING]
>
>De [!DNL Google Ads] -bron is tijdelijk niet beschikbaar. Adobe werkt aan het oplossen van problemen met deze bron.

>[!NOTE]
>
>De Google Ads-bron is bèta. Zie het [ Overzicht van Bronnen ](../../../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Deze zelfstudie bevat stappen voor het maken van een Google Ads-bronverbinding via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige verbinding van Google Ads hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/advertising.md)

### Vereiste referenties verzamelen

U moet de volgende waarden opgeven om toegang te krijgen tot uw Google Ads-accountplatform:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Client-id | De client-id is het accountnummer dat overeenkomt met de Google Ads-clientaccount die u wilt beheren met de Google Ads-API. Deze id volgt de sjabloon van `123-456-7890` . |
| Gebruikersnaam klant aanmelden | De inlogklant-id is het accountnummer dat overeenkomt met uw Google Ads Manager-account en wordt gebruikt om rapportgegevens van een specifieke operationele klant op te halen. Voor meer informatie over login identiteitskaart van de klantenklant, lees de [ API documentatie van Google Ads ](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| Developer token | Met de ontwikkelaarstoken hebt u toegang tot de API voor Google Ads. U kunt dezelfde ontwikkelaarstoken gebruiken om aanvragen in te dienen voor al uw Google Ads-accounts. Haal uw ontwikkelaarstoken door [ het programma openen aan uw managerrekening ](https://ads.google.com/home/tools/manager-accounts/) op en navigeert dan aan de pagina van het Centrum API. |
| Token vernieuwen | Het token Vernieuwen maakt deel uit van [!DNL OAuth2] -verificatie. Dit teken staat u toe om uw toegangstokens na het verlopen opnieuw te produceren. |
| Client-id | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van [!DNL OAuth2] -verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |
| Clientgeheim | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van [!DNL OAuth2] -verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |

Lees het API overzichtsdocument voor [ meer informatie over het worden begonnen met Ads van Google ](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Een Google Ads-account verbinden

Selecteer in de gebruikersinterface van het platform **[!UICONTROL Sources]** in de linkernavigatiebalk voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie **[!UICONTROL Advertising]** de optie **[!UICONTROL Google Ads]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ de broncatalogus in het Experience Platform UI.](../../../../images/tutorials/create/ads/catalog.png).

De pagina **[!UICONTROL Connect to Google Ads]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt verbinden, selecteert u het Google Ads-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om door te gaan.

![ de selectiepagina voor bestaande rekeningen in het bronwerkschema.](../../../../images/tutorials/create/ads/existing.png)

### Nieuwe account

Selecteer **[!UICONTROL New account]** als u nieuwe referenties gebruikt. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties voor Google Ads op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ de nieuwe rekeningsinterface in het bronwerkschema.](../../../../images/tutorials/create/ads/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Google Ads-account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om reclamegegevens in Platform ](../../dataflow/advertising.md) te brengen.
