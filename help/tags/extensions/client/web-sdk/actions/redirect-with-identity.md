---
title: Omleiden met identiteit
description: Hiermee kunt u een bezoeker-id delen over de domeinen van uw organisatie.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Omleiden met identiteit

Met het actietype **[!UICONTROL Redirect with identity]** kunt u een bezoeker-id delen van de huidige pagina naar een ander domein dat eigendom is van uw organisatie. Deze is ontworpen voor gebruik met een klikgebeurtenis en een vergelijkingsvoorwaarde voor waarden. Deze lijkt functioneel op de opdracht [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) in de JavaScript-bibliotheek.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel vervolgens de waarde [!UICONTROL Action type] in op **[!UICONTROL Redirect with identity]** .

## Gebruiksscenario’s

* **identificeer een individu over domeinen**: Als een bezoeker van één domein aan een andere klikt die door uw organisatie wordt bezeten, kunt u deze actie gebruiken zodat zij nog als het zelfde individu worden beschouwd. Deze identificatiemethode is vooral handig als u rapporten hebt waarin gegevens uit meerdere domeinen worden gecombineerd, zodat bezoekersinflatie wordt voorkomen.
* **identificeer een individu van een mobiele app aan een Web app**: Als een bezoeker binnen uw mobiele app is en zij een verbinding aan uw Web app klikken, kunt u deze actie gebruiken zodat het Web SDK erkent dat het het zelfde individu is. Deze workflow maakt een consistente ervaring voor rapportage en personalisatie mogelijk.

## Beschikbare velden

* **[!UICONTROL Instance]**: De SDK-instantie waarop de handeling van toepassing is. Dit vervolgkeuzemenu is uitgeschakeld als uw implementatie één SDK-exemplaar gebruikt.
* **[!UICONTROL Datastream configuration overrides]**: deze opdracht ondersteunt de configuratieoverschrijvingen van de gegevensstroom, zodat u zelf kunt bepalen welke apps en services deze gegevens ontvangen. Wanneer u een gegevensstroomconfiguratieopheffing in zowel een individueel bevel als binnen de de configuratiemontages van de markeringsuitbreiding plaatst, neemt het individuele bevel belangrijkheid. Zie [ de configuratiemet voeten treedt van de Gegevensstroom ](../configure/configuration-overrides.md) voor meer informatie.

## Voorbeeldregel

Dit bevel wordt typisch gebruikt met een specifieke regel die op kliks en controles gewenste domeinen let.

+++Criteria voor regelgebeurtenissen

Triggers wanneer op een ankertag met een eigenschap `href` wordt geklikt.

* **[!UICONTROL Extension]**: Kern
* **[!UICONTROL Event type]**: klikken
* **[!UICONTROL When the user clicks on]**: specifieke elementen
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![ gebeurtenis van de Regel ](../assets/id-sharing-event-configuration.png)

+++

+++Regelvoorwaarde

Triggers worden alleen op de gewenste domeinen geactiveerd.

* **[!UICONTROL Logic type]**: Standaard
* **[!UICONTROL Extension]**: Kern
* **[!UICONTROL Condition Type]**: vergelijking van waarden
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Komt overeen met Regex
* **[!UICONTROL Right Operand]**: Een reguliere expressie die overeenkomt met de gewenste domeinen. Bijvoorbeeld: `adobe.com$|behance.com$`

![ voorwaarde van de Regel ](../assets/id-sharing-condition-configuration.png)

+++

+++Handeling regel

Voeg de identiteit toe aan de URL.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: Omleiden met identiteit

![ actie van de Regel ](../assets/id-sharing-action-configuration.png)

+++
