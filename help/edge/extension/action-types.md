---
title: Handelingstypen in de Adobe Experience Platform Web SDK-extensie
description: Leer meer over de verschillende actietypen die door de uitbreiding van SDK van het Web van Adobe Experience Platform in Adobe Experience Platform Launch worden verstrekt.
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Typen handelingen

Nadat u de [uitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension.md) voor [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) vormt, vorm uw actietypes.

Op deze pagina worden de beschikbare actietypen beschreven.

## Gebeurtenis verzenden

Verzendt een gebeurtenis naar Adobe [!DNL Experience Platform] zodat Adobe Experience Platform de gegevens kan verzamelen die u verzendt en op die informatie kan handelen. U moet een instantie selecteren (als u meerdere instanties hebt). Als de gebeurtenis aan het begin van een paginading of tijdens een meningsverandering in één enkele paginatoepassing gebeurt, uitgezocht **[!UICONTROL komt bij het begin van een mening voor]**.

Alle gegevens die u wilt verzenden, kunnen worden verzonden in het veld **[!UICONTROL XDM Data]**. Dit moet een JSON-object zijn dat voldoet aan de structuur van uw XDM-schema. Dit object kan op uw pagina worden gemaakt of via een **[!UICONTROL Aangepaste code]** **[!UICONTROL Gegevenselement]**.

## Goedkeuring instellen

Nadat u toestemming van uw gebruiker hebt ontvangen, moet dit aan de SDK van het Web van Adobe Experience Platform worden meegedeeld. U doet dit door het handelingstype &quot;Goedkeuring instellen&quot; te gebruiken. Momenteel worden twee typen standaarden ondersteund: &quot;Adobe&quot; en &quot;IAB TCF.&quot; Als u de standaard Adobe gebruikt, kunt u de toestemming momenteel instellen op &quot;In&quot;, &quot;Uit&quot; of u kunt de toestemming verstrekken met behulp van een gegevenselement. Als u de IAB TCF-standaard gebruikt, geeft u de versie en waarde op die u wilt gebruiken, en aanvullende informatie over GDPR.

In deze handeling krijgt u ook een optioneel veld met een identiteitskaarten zodat identiteiten kunnen worden gesynchroniseerd zodra de toestemming is ontvangen. Dit kan nuttig zijn wanneer de toestemming als &quot;In behandeling&quot;wordt gevormd omdat de toestemmingsvraag waarschijnlijk de eerste vraag zal zijn om te branden.

## Samenvoegings-id van gebeurtenis opnieuw instellen

Als u de samenvoegingsidentiteitskaart van de gebeurtenis op uw pagina wilt terugstellen kunt u dit met deze actie doen. Als u de id opnieuw wilt instellen, moet u de samenvoegings-id selecteren die u opnieuw wilt instellen en de handeling naar wens uitvoeren.

## Wat nu

Nadat u uw actietypes plaatst, [vorm uw types van gegevenselement](data-element-types.md).