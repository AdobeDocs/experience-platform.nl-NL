---
title: Handelingstypen in de Adobe Experience Platform Web SDK-extensie
description: Leer meer over de verschillende actietypen die door de de marktextensie van SDK van het Web van Adobe Experience Platform worden verstrekt.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# Typen handelingen

Nadat u vormt [Adobe Experience Platform Web SDK-tagextensie](web-sdk-extension-configuration.md)configureert u de actietypen.

Op deze pagina worden de beschikbare actietypen beschreven.


## Gebeurtenis verzenden

Verzendt een gebeurtenis naar Adobe [!DNL Experience Platform] zodat Adobe Experience Platform de gegevens die u verzendt kan verzamelen en op die gegevens kan reageren. Selecteer een instantie (als u meerdere exemplaren hebt). Alle gegevens die u wilt verzenden, kunnen worden verzonden in het dialoogvenster **[!UICONTROL XDM Data]** veld. Gebruik een JSON-object dat voldoet aan de structuur van uw XDM-schema. Dit object kan op uw pagina worden gemaakt of via een **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Er zijn een paar andere gebieden in het Send actietype van de Gebeurtenis die ook afhankelijk van uw implementatie nuttig zouden kunnen zijn. Deze velden zijn allemaal optioneel.

- **Type:** In dit veld kunt u een gebeurtenistype opgeven dat in uw XDM-schema wordt opgenomen. Zie de [documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) voor meer informatie over de standaardgebeurtenistypen.
- **Gegevens:** Gegevens die niet overeenkomen met een XDM-schema kunnen met dit veld worden verzonden. Dit veld is handig als u probeert een Adobe Target-profiel bij te werken of Recommendations-kenmerken van het doel te verzenden. Voor voorbeelden bekijk onze [documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Gegevensset-id:** Als u gegevens naar een dataset buiten moet verzenden u in uw gegevensstroom specificeerde, kunt u die dataset identiteitskaart hier specificeren.
- **Document wordt verwijderd:** Als u er zeker van wilt zijn dat de gebeurtenissen de server bereiken, zelfs als de gebruiker weg van de pagina navigeert, controleert u **[!UICONTROL Document will unload]** selectievakje. Hierdoor kunnen gebeurtenissen de server bereiken, maar reacties worden genegeerd.
- **Render visuele verpersoonlijkingsbesluiten:** Als u gepersonaliseerde inhoud op uw pagina wilt teruggeven, controleer **[!UICONTROL Render visual personalization decisions]** selectievakje. Indien nodig kunt u ook het beslissingsbereik en/of de oppervlakken opgeven. Zie de [verpersoonlijkingsdocumentatie](../personalization/rendering-personalization-content.md#automatically-rendering-content) voor meer informatie over het renderen van gepersonaliseerde inhoud.

## Goedkeuring instellen

Nadat u toestemming van uw gebruiker hebt ontvangen, moet deze toestemming aan het Web SDK van Adobe Experience Platform worden meegedeeld door het &quot;Vastgestelde type van de Actie van de Toestemming te gebruiken&quot;. Momenteel worden twee typen standaarden ondersteund: &quot;Adobe&quot; en &quot;IAB TCF.&quot; Zie [Voorkeuren voor goedkeuring door klant ondersteunen](../consent/supporting-consent.md). Bij gebruik van Adobe versie 2.0 wordt alleen een waarde voor een gegevenselement ondersteund. U moet een gegevenselement maken dat wordt omgezet in het toestemmingsobject.

In deze handeling krijgt u ook een optioneel veld met een identiteitskaarten, zodat identiteiten kunnen worden gesynchroniseerd zodra de toestemming is ontvangen. Het synchroniseren is nuttig wanneer de toestemming als &quot;In behandeling&quot;of &quot;uit&quot;wordt gevormd omdat de toestemmingsvraag waarschijnlijk de eerste vraag aan brand is.

## Samenvoegings-id van gebeurtenis opnieuw instellen

Als u de samenvoegingsidentiteitskaart van de gebeurtenis op uw pagina wilt terugstellen, kunt u dit met deze actie doen. Als u de id opnieuw wilt instellen, selecteert u de samenvoegings-id die u opnieuw wilt instellen en voert u de actie naar wens uit.

## Wat nu

Nadat u de handelingen hebt ingesteld, [configureren, gegevenselementen](data-element-types.md).
