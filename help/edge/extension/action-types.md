---
title: Handelingstypen in de Adobe Experience Platform Web SDK-extensie
description: Leer meer over de verschillende actietypen die door de uitbreiding van SDK van het Web van Adobe Experience Platform in Adobe Experience Platform Launch worden verstrekt.
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---


# Typen handelingen

Nadat u de [uitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension.md) voor [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) vormt, vorm uw actietypes.

Op deze pagina worden de beschikbare actietypen beschreven.

## Gebeurtenis verzenden

Verzendt een gebeurtenis naar Adobe [!DNL Experience Platform] zodat Adobe Experience Platform de gegevens kan verzamelen die u verzendt en op die informatie kan handelen. Selecteer een instantie (als u meerdere exemplaren hebt). Als de gebeurtenis aan het begin van een paginading of tijdens een meningsverandering in één enkele paginatoepassing gebeurt, uitgezocht **[!UICONTROL komt bij het begin van een mening voor]**.

Alle gegevens die u wilt verzenden, kunnen worden verzonden in het veld **[!UICONTROL XDM Data]**. Gebruik een JSON-object dat voldoet aan de structuur van uw XDM-schema. Dit object kan op uw pagina worden gemaakt of via een **[!UICONTROL Aangepaste code]** **[!UICONTROL Gegevenselement]**.

## Goedkeuring instellen

Nadat u toestemming van uw gebruiker hebt ontvangen, moet deze toestemming aan het Web SDK van Adobe Experience Platform worden meegedeeld door het &quot;Vastgestelde type van de Actie van de Toestemming te gebruiken&quot;. Momenteel worden twee typen standaarden ondersteund: &quot;Adobe&quot; en &quot;IAB TCF.&quot; Zie [Voorkeuren voor instemming van de klant](../consent/supporting-consent.md) ondersteunen. Bij gebruik van Adobe versie 2.0 wordt alleen een waarde voor een gegevenselement ondersteund. U moet een gegevenselement maken dat wordt omgezet in het toestemmingsobject.

In deze handeling krijgt u ook een optioneel veld met een identiteitskaarten, zodat identiteiten kunnen worden gesynchroniseerd zodra de toestemming is ontvangen. Het synchroniseren is nuttig wanneer de toestemming als &quot;In behandeling&quot;, of &quot;uit&quot;wordt gevormd omdat de toestemmingsvraag waarschijnlijk de eerste vraag aan brand is.

## Samenvoegings-id van gebeurtenis opnieuw instellen

Als u de samenvoegingsidentiteitskaart van de gebeurtenis op uw pagina wilt terugstellen, kunt u dit met deze actie doen. Als u de id opnieuw wilt instellen, selecteert u de samenvoegings-id die u opnieuw wilt instellen en voert u de actie naar wens uit.

## Wat nu

Nadat u uw actietypes plaatst, [vorm uw types van gegevenselement](data-element-types.md).