---
title: Handelingstypen in de Adobe Experience Platform Web SDK-extensie
description: Leer meer over de verschillende actietypen die door de uitbreiding van SDK van het Web van Adobe Experience Platform in Adobe Experience Platform Launch worden verstrekt.
solution: Experience Platform
feature: Web SDK
translation-type: tm+mt
source-git-commit: 9ce6dd5a290b55da04f4ae185cab96c120777775
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Typen handelingen

Nadat u de [uitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension.md) voor [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) vormt, vorm uw actietypes.

Op deze pagina worden de beschikbare actietypen beschreven.

## Gebeurtenis verzenden

Verzendt een gebeurtenis naar Adobe [!DNL Experience Platform] zodat Adobe Experience Platform de gegevens kan verzamelen die u verzendt en op die informatie kan handelen. Selecteer een instantie (als u meerdere exemplaren hebt). Alle gegevens die u wilt verzenden, kunnen worden verzonden in het veld **[!UICONTROL XDM Data]**. Gebruik een JSON-object dat voldoet aan de structuur van uw XDM-schema. Dit object kan op uw pagina worden gemaakt of via een **[!UICONTROL Aangepaste code]** **[!UICONTROL Gegevenselement]**.

Er zijn een paar andere gebieden in het Send actietype van de Gebeurtenis die ook afhankelijk van uw implementatie nuttig zouden kunnen zijn. Deze velden zijn allemaal optioneel.

- **Type:** In dit veld kunt u een gebeurtenistype opgeven dat wordt opgenomen in uw XDM-schema. Zie [documentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) voor meer informatie over de standaardgebeurtenistypen.
- **Id samenvoegen:** Als u een  [samenvoegings-](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) id wilt opgeven voor de gebeurtenis, kunt u dit in dit veld doen. Houd er rekening mee dat de oplossingen verderop uw gebeurtenisgegevens momenteel niet kunnen samenvoegen.
- **Dataset-id:** Als u gegevens naar een andere gegevensset moet verzenden dan de gegevensset die u in de randconfiguratie hebt opgegeven, kunt u die gegevensset-id hier opgeven.
- **Document wordt verwijderd:** Als u er zeker van wilt zijn dat de gebeurtenissen de server bereiken, zelfs als de gebruiker van de pagina weg navigeert, schakelt u het selectievakje  **[!UICONTROL Document]** uit. Hierdoor kunnen gebeurtenissen de server bereiken, maar reacties worden genegeerd.
- **Render visuele verpersoonlijkingsbesluiten:** Als u gepersonaliseerde inhoud op uw pagina wilt teruggeven, controleer het  **[!UICONTROL Render visuele verpersoonlijkingsbepalende]** vakje. Indien nodig kunt u ook het beslissingsbereik opgeven. Zie [verpersoonlijkingsdocumentatie](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) voor meer informatie over het teruggeven van gepersonaliseerde inhoud.

## Goedkeuring instellen

Nadat u toestemming van uw gebruiker hebt ontvangen, moet deze toestemming aan het Web SDK van Adobe Experience Platform worden meegedeeld door het &quot;Vastgestelde type van de Actie van de Toestemming te gebruiken&quot;. Momenteel worden twee typen standaarden ondersteund: &quot;Adobe&quot; en &quot;IAB TCF.&quot; Zie [Voorkeuren voor instemming van de klant](../consent/supporting-consent.md) ondersteunen. Bij gebruik van Adobe versie 2.0 wordt alleen een waarde voor een gegevenselement ondersteund. U moet een gegevenselement maken dat wordt omgezet in het toestemmingsobject.

In deze handeling krijgt u ook een optioneel veld met een identiteitskaarten, zodat identiteiten kunnen worden gesynchroniseerd zodra de toestemming is ontvangen. Het synchroniseren is nuttig wanneer de toestemming als &quot;In behandeling&quot;of &quot;uit&quot;wordt gevormd omdat de toestemmingsvraag waarschijnlijk de eerste vraag aan brand is.

## Samenvoegings-id van gebeurtenis opnieuw instellen

Als u de samenvoegingsidentiteitskaart van de gebeurtenis op uw pagina wilt terugstellen, kunt u dit met deze actie doen. Als u de id opnieuw wilt instellen, selecteert u de samenvoegings-id die u opnieuw wilt instellen en voert u de actie naar wens uit.

## Wat nu

Nadat u uw acties plaatst, [vorm uw types van gegevenselement](data-element-types.md).
