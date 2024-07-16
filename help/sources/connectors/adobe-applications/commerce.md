---
title: Adobe Commerce Source Connector
description: Leer hoe u de Adobe Commerce-bron kunt gebruiken om uw handelsgegevens naar het Experience Platform te brengen.
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 506f33e03dea5d5879808bccb82948209714926a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce is een flexibel B2B- en B2C-handelsplatform dat verkopers en merken in staat stelt hun omzet te versnellen via klantgerichte digitale commerciële ervaringen in online en fysieke ruimten.

Adobe Experience Platform Sources biedt ondersteuning voor de integratie van Adobe Commerce zodat handelaren hun gegevens over hun winkel en hun back-office naar de Edge Network van het Experience Platform kunnen verzenden. Andere Adobe Experience Cloud-producten zoals Adobe Analytics en Adobe Target kunnen dus [!DNL Commerce] -gegevens gebruiken.

* **gebeurtenissen Storefront**: De interactie van de vangstverkoopaar zoals `View Page`, `View Product`, en `Add to Cart`. Voor kooplieden B2B, vangen de storefront gebeurtenissen ook [ verzoeklijsten ](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **de gebeurtenissen van het achterkantoor**: Vang informatie over het statuut van een orde, zoals of een orde werd geplaatst, geannuleerd, terugbetaald, verscheept, of voltooid.

>[!NOTE]
>
>Vastgelegde gegevens in Adobe Commerce bevatten geen persoonlijk identificeerbare gegevens (PII). Alle gebruikers-id&#39;s, zoals cookie-id&#39;s en IP-adressen, worden strikt geanonimiseerd.

## Vereisten

Als u Adobe Commerce wilt verbinden met Experience Platform, hebt u het volgende nodig:

* Adobe Commerce 2.4.3 of hoger.
* Een geldige Adobe ID- en organisatie-id.
* Toegang tot de [ uitbreiding van de Laag van de Gegevens van de Cliënt van de Adobe ](../../../tags/extensions/client/client-data-layer/overview.md). Deze extensie is nodig om gegevens over storefront-gebeurtenissen te verzamelen.
* Rechten op andere Adobe DX-producten.

## Stappen aan boord

Volg de onderstaande stappen en de bijbehorende documentatie om uw Adobe Commerce-bronaccount volledig aan te schaffen.

* [ installeer de  [!DNL Data Connection]  uitbreiding ](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) voor Adobe Commerce. U kunt de schakelaaruitbreiding van [ Adobe Marketplace ](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html) downloaden.
* Zodra u met succes de schakelaaruitbreiding hebt geïnstalleerd, teken binnen aan uw rekening van de Adobe in Experience Cloud en [ bevestig uw organisatieidentiteitskaart ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Deze id is gekoppeld aan uw bedrijf voor Experiencen Cloud. De notatie is opgemaakt als een alfanumerieke tekenreeks van 24 tekens en bevat een verplichte `@AdobeOrg` .
* Maak vervolgens een XDM-schema (Experience Data Model) of werk dit bij met uw Commerce-specifieke veldgroepen. Voor gedetailleerde stappen op hoe te om Commerce-Specifieke gebiedsgroepen aan uw schema toe te voegen XDM, lees de gids op [ toevoegend gebiedsgroepen aan een XDM schema ](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
* Zodra uw schema wordt gevormd, moet u een dataset dan creëren die van uw nieuw schema wordt gebaseerd. Deze gegevensset bevat vervolgens de [!DNL Commerce] -gegevens die u verzendt. Voor gedetailleerde stappen op hoe te om een dataset voor [!DNL Commerce] gegevens tot stand te brengen, lees de gids over [ verzendend gegevens naar Experience Platform ](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Maak vervolgens een gegevensstroom en selecteer het XDM-schema dat uw Commerce-specifieke veldgroepen bevat. Voor meer informatie over gegevensstromen, lees het [ overzicht van gegevensstromen ](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).
* Dan, moet u uw instantie van Adobe Commerce met de [ Schakelaar van de Diensten van Commerce verbinden ](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Hierdoor kan uw Commerce-instantie worden geïmplementeerd als SaaS (Software as a Service).
* Als alle bovenstaande configuraties zijn voltooid, kunt u nu verbinding maken met Experience Platform door zowel de Commerce Services Connector als de [!DNL Data Connection] extensie te configureren met [!DNL Commerce Admin] . Voor meer informatie over deze definitieve stap, leest de gids op [ verbindend de gegevens van Commerce met Experience Platform ](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).
