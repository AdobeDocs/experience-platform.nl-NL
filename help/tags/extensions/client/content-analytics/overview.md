---
title: Overzicht Adobe Content Analytics-extensie
description: Meer informatie over de Adobe Content Analytics-tagextensie in Adobe Experience Platform.
exl-id: fcc46c86-e765-4bc7-bfdf-b8b10e8afacc
source-git-commit: 34f50c6e92cb1bde4e5f27a4378058615fb0cdff
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Overzicht Adobe Content Analytics-extensie

Met de tagextensie [!DNL Adobe Content Analytics] kunt u gebeurtenissen met betrekking tot inhoud op een website bijhouden. De extensie verzendt inhoudsgegevens (ervaringen en elementen) vanuit wegeigenschappen naar een gegevensstroom in Adobe Experience Cloud via de Experience Platform Edge Network.

Met de extensie kunt u specifieke gebeurtenisgegevens die door de inhoud worden vrijgegeven, streamen naar Experience Platform, zodat u die gegevens kunt gebruiken in rapporten voor inhoudsanalyse in Customer Journey Analytics.

In dit document wordt uitgelegd hoe u de tagextensie configureert in de gebruikersinterface voor tags.

## De Adobe Content Analytics-tagextensie installeren {#install}

De de markeringsuitbreiding van Adobe Content Analytics wordt automatisch geïnstalleerd als deel van het markeringsbezit dat automatisch wordt gecreeerd wanneer het gebruiken van de [ Content Analytics geleide configuratietovenaar ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided).

<!--
### Manual installation

In case of a manual configuration, the Adobe Content Analytics tag extension needs a property to be installed on. If you have not done so already, see the documentation on [creating a tag property](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/create-a-property).

After you have created a property or when you select the property created using the [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided), open the property and select the **[!UICONTROL Extensions]** tab on the left side bar.

Select the **[!UICONTROL Catalog]** tab. From the list of available extensions, find the **[!DNL Adobe Content Analytics]** extension and select **[!UICONTROL Install]**.

![Image showing the Tags UI with the Web SDK extension selected](assets/aca-tag-install.png)

After selecting **[!UICONTROL Install]**, you must configure the Adobe Content Analytics tag extension and save the configuration.
-->

<!--
## Configure schema

The [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) automatically populates the proper value for the **[!UICONTROL Tenant Schema Name]**. 

![Image that shows the Schema configuration of the Adobe Content Analytics tag extension in the Tags UI](assets/aca-tag-schema.png)

>[!WARNING]
>
>Do not modify the value for **[!UICONTROL Tenant Schema Name]**.

-->

## Gegevensstromen configureren

De [ Content Analytics geleide configuratietovenaar ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) selecteert automatisch de juiste waarde voor **[!UICONTROL Sandbox]** en **[!UICONTROL Production Datastream]**. U kunt desgewenst een extra **[!UICONTROL Staging Datastream]** en **[!UICONTROL Development Datastream]** configureren.

![ Beeld dat de configuratie van Datastreams van de de markeringsuitbreiding van Adobe Content Analytics in de Markeringen UI ](assets/aca-tag-datastreams.png) toont

U kunt de automatische geselecteerde waarden voor **[!UICONTROL Sandbox]** en **[!UICONTROL Production Datastream]** overschrijven voor het geval u Content Analytics wilt gebruiken voor een andere sandbox en voor verschillende gegevensstreams. Als u dit doet, kunt u een sandbox en gegevensstreams selecteren in de beschikbare vervolgkeuzemenu&#39;s of **[!UICONTROL Enter values]** selecteren en een aangepaste gegevensstroom-id invoeren voor elke omgeving.

>[!IMPORTANT]
>
>Wanneer u een andere zandbak en gegevensstromen vormt, zorg ervoor dat
>
>* de geselecteerde sandbox is nog niet gekoppeld aan een andere Content Analytics-configuratie, en
>* Voor elke geselecteerde gegevensstroom is de Experience Platform-service geconfigureerd met een ingeschakelde Content Analytics Experience-gebeurtenisgegevensset.

Zie de gids op [ gegevensstromen ](../../../../datastreams/overview.md) leren hoe te om een gegevensstroom te vormen.

## Vastleggen en definiëren van ervaring configureren

In de sectie **[!UICONTROL Experience Capture & Definition]** kunt u **[!UICONTROL Include Experiences]** de mogelijkheid bieden ervaringen op te nemen bij het verzamelen van gegevens voor Content Analytics.

![ Beeld dat de sectie van de Vangst en van de Definitie van de Ervaring in uitbreiding toont ](assets/aca-tag-experiencecapture.png)

1. Schakel **[!UICONTROL Include experiences]** in.
1. Optioneel. Geef de parameters op voor de weergave van inhoud op uw website. De parameters zijn nul of meer combinaties van a **[!UICONTROL Domain regular expression]** en **[!UICONTROL Query parameters]**.
   1. Voer een **[!UICONTROL Domain regular expression]** in, bijvoorbeeld `^(?!.*\b(store|help|admin)\b)` .
   1. Geef bijvoorbeeld een door komma&#39;s gescheiden lijst op van **[!UICONTROL Query parameters]** . `outdoors, patio, kitchen`
Gebruik ![ dicht ](./assets/CrossSize300.svg) om individuele parameters te schrappen, of **[!UICONTROL Clear all]** om alle parameters te schrappen.
1. Selecteer **[!UICONTROL Remove]** als u een combinatie van de reguliere expressie van het domein en queryparameters wilt verwijderen.
1. Selecteer **[!UICONTROL Add Regex]** als u een andere combinatie van een reguliere expressie en queryparameters wilt toevoegen.

## Gebeurtenisfiltering configureren

In de sectie **[!UICONTROL Event Filtering]** kunt u de reguliere expressies wijzigen om te filteren **[!UICONTROL Page URLs]** en **[!UICONTROL Assets URLs]** wanneer u gegevens voor Content Analytics verzamelt. De regelmatige uitdrukkingen die u in de [ Content Analytics geleide configuratietovenaar ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) hebt bepaald worden automatisch bevolkt.

![ Beeld dat de gebeurtenis het filtreren montages van de de markeringsuitbreiding van Adobe Content Analytics in de markeringen UI toont ](assets/aca-tag-eventfiltering.png)


### Voorbeelden

* U wilt alle documentatiepagina&#39;s uitsluiten van Content Analytics.<br/> Gebruik de volgende reguliere expressie: `^(?!.*documentation).*`
* U wilt alle JPEG- en SVG-afbeeldingen met logo&#39;s uitsluiten van Content Analytics.<br/> Gebruik de volgende reguliere expressie: `^(?!.*(logo\.jpg|)).*$`

Met **[!UICONTROL Test Regex]** kunt u de reguliere expressie testen in de **[!UICONTROL Regular Expression Tester]** .

![ Beeld die het regelmatige uitdrukkingsmeetapparaat van de de markeringsuitbreiding van Adobe Content Analytics in Tags UI tonen ](assets/aca-tag-regextester.png)

