---
title: SDK-configuratie-instellingen
description: Configureer algemene instellingen voor de Web SDK-instantie.
exl-id: cc22b8b3-88c6-4030-91b4-60e14a3b0f42
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# SDK-configuratie-instellingen {#sdk-instance}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_sdkinstance"
>title="SDK-instanties"
>abstract="Hiermee stelt u de SDK-instantienaam, de IMS-org waartoe het behoort en het Edge-domein in."

Deze configuratiesectie regelt de Web SDK instantienaam, de IMS org waarop het van toepassing is, en de plaats waarnaar u gegevens wilt verzenden. Een instantie krijgt standaard de naam `alloy` .

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Zoek de instantienaam net onder de uitgevouwen accordeon [!UICONTROL SDK instances] .

![ Beeld dat de algemene montages van de de markeringsuitbreiding van SDK van het Web in de markeringen UI toont ](../assets/web-sdk-ext-general.png)

De volgende opties zijn beschikbaar:

## [!UICONTROL Name]

De Adobe Experience Platform Web SDK-tagextensie ondersteunt meerdere exemplaren op de pagina. De naam wordt gebruikt om gegevens naar veelvoudige organisaties te verzenden zonder dubbele de markeringsbibliotheken van SDK van het Web te vereisen. U kunt de instantienaam wijzigen in elke geldige JavaScript-objectnaam.

## [!UICONTROL IMS organization ID]

De id van de organisatie waarnaar u de gegevens op Adobe wilt verzenden. Meestal gebruikt u de standaardwaarde die automatisch wordt ingevuld. Wanneer u meerdere exemplaren op de pagina hebt, vult u dit veld met de waarde van de tweede organisatie waarnaar u gegevens wilt verzenden.

## [!UICONTROL Edge domain]

Het domein waarvan de extensie gegevens verzendt en ontvangt. Het veld bevat standaard `<COMPANYID>.data.adobedc.net` . Oudere implementaties kunnen de standaardwaarde `edge.adobedc.net` bevatten. Deze waarde is ook geldig.

Adobe raadt in de meeste gevallen aan een domein van de eerste partij te gebruiken. Zie [ Adobe-Beheerde certificaatprogramma ](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) voor instructies op hoe te opstelling een eerste-partijdomein geschikt voor gegevensinzameling. Zie ook [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) in de documentatie van de JavaScript-bibliotheek voor hulp bij het instellen van deze waarde.
