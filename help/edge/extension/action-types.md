---
title: Handelingstypen in de Adobe Experience Platform Web SDK-extensie
description: Leer meer over de verschillende actietypen die door de de marktextensie van SDK van het Web van Adobe Experience Platform worden verstrekt.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Typen handelingen

Nadat u de [Adobe Experience Platform Web SDK markeringsuitbreiding ](web-sdk-extension-configuration.md) vormt, vorm uw actietypes.

Op deze pagina worden de beschikbare actietypen beschreven.


## Gebeurtenis verzenden

Verzendt een gebeurtenis naar Adobe [!DNL Experience Platform] zodat Adobe Experience Platform de gegevens kan verzamelen die u verzendt en op die informatie kan handelen. Selecteer een instantie (als u meerdere exemplaren hebt). Alle gegevens die u wilt verzenden, kunnen in het veld **[!UICONTROL XDM Data]** worden verzonden. Gebruik een JSON-object dat voldoet aan de structuur van uw XDM-schema. Dit object kan op uw pagina worden gemaakt of via een **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Er zijn een paar andere gebieden in het Send actietype van de Gebeurtenis die ook afhankelijk van uw implementatie nuttig zouden kunnen zijn. Deze velden zijn allemaal optioneel.

- **Type:** In dit veld kunt u een gebeurtenistype opgeven dat wordt opgenomen in uw XDM-schema. Zie [documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) voor meer informatie over de standaardgebeurtenistypen.
- **Gegevens:** Gegevens die geen XDM-schema aanpassen kunnen worden verzonden gebruikend dit gebied. Dit veld is handig als u probeert een Adobe Target-profiel bij te werken of Recommendations-kenmerken van het doel te verzenden. Bekijk bijvoorbeeld onze [documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).
<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Dataset-id:** Als u gegevens naar een andere gegevensset moet verzenden dan de gegevensset die u in de gegevensstroom hebt opgegeven, kunt u die gegevensset-id hier opgeven.
- **Document wordt verwijderd:** Als u er zeker van wilt zijn dat de gebeurtenissen de server bereiken, zelfs als de gebruiker van de pagina weg navigeert, schakelt u het  **[!UICONTROL Document will unload]** selectievakje in. Hierdoor kunnen gebeurtenissen de server bereiken, maar reacties worden genegeerd.
- **Weergave van visuele beslissingen over personalisatie weergeven:** Als u gepersonaliseerde inhoud op uw pagina wilt renderen, schakelt u het  **[!UICONTROL Render visual personalization decisions]** selectievakje in. Indien nodig kunt u ook het beslissingsbereik opgeven. Zie [verpersoonlijkingsdocumentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) voor meer informatie over het teruggeven van gepersonaliseerde inhoud.

## Goedkeuring instellen

Nadat u toestemming van uw gebruiker hebt ontvangen, moet deze toestemming aan het Web SDK van Adobe Experience Platform worden meegedeeld door het &quot;Vastgestelde type van de Actie van de Toestemming te gebruiken&quot;. Momenteel worden twee typen standaarden ondersteund: &quot;Adobe&quot; en &quot;IAB TCF.&quot; Zie [Voorkeuren voor instemming van de klant](../consent/supporting-consent.md) ondersteunen. Bij gebruik van Adobe versie 2.0 wordt alleen een waarde voor een gegevenselement ondersteund. U moet een gegevenselement maken dat wordt omgezet in het toestemmingsobject.

In deze handeling krijgt u ook een optioneel veld met een identiteitskaarten, zodat identiteiten kunnen worden gesynchroniseerd zodra de toestemming is ontvangen. Het synchroniseren is nuttig wanneer de toestemming als &quot;In behandeling&quot;of &quot;uit&quot;wordt gevormd omdat de toestemmingsvraag waarschijnlijk de eerste vraag aan brand is.

## Samenvoegings-id van gebeurtenis opnieuw instellen

Als u de samenvoegingsidentiteitskaart van de gebeurtenis op uw pagina wilt terugstellen, kunt u dit met deze actie doen. Als u de id opnieuw wilt instellen, selecteert u de samenvoegings-id die u opnieuw wilt instellen en voert u de actie naar wens uit.

## Wat nu

Nadat u uw acties plaatst, [vorm uw types van gegevenselement](data-element-types.md).
