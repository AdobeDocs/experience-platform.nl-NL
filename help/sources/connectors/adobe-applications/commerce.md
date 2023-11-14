---
title: Adobe Commerce Source Connector
description: Leer hoe u de Adobe Commerce-bron kunt gebruiken om uw handelsgegevens naar het Experience Platform te brengen.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 8249de4c78810a4cee245fa9c48b91c210aeb0a4
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce is een flexibel B2B- en B2C-handelsplatform dat verkopers en merken in staat stelt hun omzet te versnellen via klantgerichte digitale commerciële ervaringen in online en fysieke ruimten.

Adobe Experience Platform Sources biedt ondersteuning voor de integratie van Adobe Commerce zodat handelaren hun gegevens over hun winkel en hun back-office naar het Edge Network van Experience Platforms kunnen verzenden, zodat andere Adobe Experience Cloud-producten zoals Adobe Analytics en Adobe Target ook kunnen gebruiken [!DNL Commerce] gegevens.

* **Gebeurtenissen van Storefront**: Interacties met winkels vastleggen, zoals `View Page`, `View Product`, en `Add to Cart`. Voor B2B-handelaren worden ook storefront-gebeurtenissen vastgelegd [aanvraaglijsten](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Back office evenementen**: Leg informatie vast over de status van een bestelling, bijvoorbeeld of een bestelling is geplaatst, geannuleerd, terugbetaald, verzonden of voltooid.

>[!NOTE]
>
>Vastgelegde gegevens in Adobe Commerce bevatten geen persoonlijk identificeerbare gegevens (PII). Alle gebruikers-id&#39;s, zoals cookie-id&#39;s en IP-adressen, worden strikt geanonimiseerd.

## Vereisten

Als u Adobe Commerce wilt verbinden met Experience Platform, hebt u het volgende nodig:

* Adobe Commerce 2.4.3 of hoger.
* Een geldige Adobe ID- en organisatie-id.
* Toegang tot de [Adobe Clientgegevenslaagextensie](../../../tags/extensions/client/client-data-layer/overview.md). Deze extensie is nodig om gegevens over storefront-gebeurtenissen te verzamelen.
* Rechten op andere Adobe DX-producten.

## Stappen aan boord

Volg de onderstaande stappen en de bijbehorende documentatie om uw Adobe Commerce-bronaccount volledig aan te schaffen.

* [De extensie van de Experience Platform-aansluiting installeren](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html) voor Adobe Commerce. U kunt de verbindingsextensie downloaden van [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Meld u aan bij uw Adobe-account in Experience Cloud nadat u de verbindingsextensie hebt geïnstalleerd en [bevestig uw organisatie-id](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Deze id is gekoppeld aan uw bedrijf voor Experiencen Cloud. De notatie is opgemaakt als een alfanumerieke tekenreeks van 24 tekens en bevat een verplicht teken `@AdobeOrg`.
* Vervolgens maakt of werkt u het XDM-schema (Experience Data Model) bij met uw specifieke veldgroepen voor handel. Voor gedetailleerde stappen op hoe te om Commerce-Specifieke gebiedsgroepen aan uw schema toe te voegen XDM, lees de gids op [veldgroepen toevoegen aan een XDM-schema](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html).
* Zodra uw schema wordt gevormd, moet u een dataset dan creëren die van uw nieuw schema wordt gebaseerd. Deze dataset zal dan bevatten [!DNL Commerce] gegevens die u verzendt. Voor gedetailleerde stappen op hoe te om een dataset tot stand te brengen voor [!DNL Commerce] gegevens, lees de handleiding op [gegevens verzenden naar Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Daarna, creeer een gegevensstroom en selecteer het schema XDM dat uw handel-specifieke gebiedsgroepen bevat. Voor meer informatie over gegevensstromen, lees [datastreams, overzicht](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).
* Vervolgens moet u uw Adobe Commerce-instantie verbinden met de [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Dit staat uw instantie van de Handel toe om als SaaS (Software als Dienst) worden opgesteld.
* Met alle bovengenoemde configuraties volledig, kunt u nu met Experience Platform verbinden door zowel de Schakelaar van de Diensten van de Handel als de Schakelaar van het Experience Platform te vormen gebruikend [!DNL Commerce Admin]. Lees voor meer informatie over deze laatste stap de handleiding op [verbinden van de gegevens van de Handel met Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html).
