---
keywords: Experience Platform;home;populaire onderwerpen;Google-advertenties;Google Ads-bronaansluiting;Google-advertentiesconnector
title: Een Google Ads Source Connection maken in de gebruikersinterface
description: Leer hoe u een Google Ads-bronverbinding maakt met de Adobe Experience Platform-interface.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 56419f41188c9bfdbeda7dde680f269b980a37f0
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 0%

---

# Een Google Ads-bronverbinding maken in de gebruikersinterface

>[!NOTE]
>
>De Google Ads-bron is bèta. Zie de [Overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Deze zelfstudie bevat stappen voor het maken van een Google Ads-bronconnector via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een geldige Google Ads-verbinding hebt, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/advertising.md)

### Vereiste referenties verzamelen

Geef de volgende waarden op om toegang te krijgen tot het Platform voor Google Ads-accounts:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Client-id | De client-id is het accountnummer dat overeenkomt met de Google Ads-clientaccount die u wilt beheren met de Google Ads-API. Deze id volgt de sjabloon van `123-456-7890`. |
| Developer token | Met de ontwikkelaarstoken hebt u toegang tot de API voor Google Ads. U kunt dezelfde ontwikkelaarstoken gebruiken om aanvragen in te dienen voor al uw Google Ads-accounts. Haal de ontwikkelaarstoken op door [aanmelden bij uw beheerdersaccount](https://ads.google.com/home/tools/manager-accounts/) en navigeer naar de pagina API Center. |
| Token vernieuwen | Het token Vernieuwen maakt deel uit van [!DNL OAuth2] verificatie. Dit teken staat u toe om uw toegangstokens na het verlopen opnieuw te produceren. |
| Client-id | De client-id wordt gebruikt in combinatie met het clientgeheim als onderdeel van [!DNL OAuth2] verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |
| Clientgeheim | Het clientgeheim wordt gebruikt in combinatie met de client-id als onderdeel van [!DNL OAuth2] verificatie. Met de client-id en het clientgeheim kan uw toepassing samen namens uw account werken door uw toepassing te identificeren bij Google. |

Het API-overzichtsdocument lezen voor [meer informatie over hoe je aan de slag gaat met Google Ads](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Een Google Ads-account verbinden

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de **[!UICONTROL Advertising]** categorie, selecteert u **[!UICONTROL Google Ads]** en selecteer vervolgens **[!UICONTROL Add data]**.

![Een afbeelding van de Google Ads-bron in de Experience Platform UI-broncatalogus](../../../../images/tutorials/create/ads/catalog.png).

De **[!UICONTROL Connect to Google Ads]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u verbinding wilt maken met een bestaande account, selecteert u het Google Ads-account waarmee u verbinding wilt maken en selecteert u **[!UICONTROL Next]** om verder te gaan.

![Een afbeelding van een lijst met bestaande accounts waarmee u een Google Ads-gegevensstroom kunt maken met](../../../../images/tutorials/create/ads/existing.png).

### Nieuwe account

Als u nieuwe referenties gebruikt, selecteert u **[!UICONTROL New account]**. Geef in het invoerformulier dat wordt weergegeven een naam, een optionele beschrijving en uw referenties voor Google Ads op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![Een afbeelding van het nieuwe scherm voor accountverbinding op de gebruikersinterface van het Experience Platform](../../../../images/tutorials/create/ads/connect.png).

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw Google Ads-account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om advertentiegegevens in Platform te brengen](../../dataflow/advertising.md).
