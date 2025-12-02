---
title: Proposities toepassen
description: Render voorstellen in enig-paginatoepassingen zonder stijgende metriek.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---

# Proposities toepassen

Met het actietype **[!UICONTROL Apply propositions]** kunt u profielen weergeven in toepassingen van één pagina zonder dat de metriek toeneemt. Dit handelingstype is handig wanneer u werkt met toepassingen van één pagina waarin delen van de pagina opnieuw worden weergegeven, waardoor eventuele al op de pagina toegepaste aanpassingen mogelijk worden overschreven.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel vervolgens de waarde [!UICONTROL Action type] in op **[!UICONTROL Apply propositions]** .

![ de Markeringen UI die van Experience Platform het Apply actietype van Voorstellen tonen.](../assets/apply-propositions.png)

## Gebruiksscenario’s

U kunt dit actietype voor diverse gebruiksgevallen gebruiken, zoals:

1. **geeft mbox HTML aanbiedingen** terug. Proposities die expliciet via een bereik of oppervlak van een **[!UICONTROL Send event]** -actie worden aangevraagd, worden niet automatisch gerenderd. U kunt het actietype **[!UICONTROL Apply propositions]** gebruiken om Web SDK te vertellen waar te om hen terug te geven door de propositiemeta-gegevens te specificeren.
2. **geef de aanbiedingen voor een mening op een enig-paginatoepassing** terug. Als bij het renderen van een weergavewijzigingsgebeurtenis de analysegegevens nog niet beschikbaar zijn, kunt u de handeling **[!UICONTROL Apply propositions]** gebruiken om de weergavevoorstellingen boven aan de pagina weer te geven. Zie [ bovenkant en bodem van paginagebeurtenissen (Tweede paginamening - Optie 2) ](/help/collection/use-cases/personalization/top-bottom-page-events.md) voor meer details. Als u dit wilt gebruiken, voert u een **[!UICONTROL View name]** in het formulier in.
3. **teruggeven voorstellingen**. Wanneer uw site gebruikmaakt van een framework zoals Reageren om inhoud opnieuw te renderen, moet u mogelijk de personalisatie opnieuw toepassen. In dergelijke gevallen kunt u hiervoor het actietype **[!UICONTROL Apply propositions]** gebruiken.

Dit actietype verzendt geen vertoningsgebeurtenis voor teruggegeven voorstellingen. Het houdt spoor van teruggegeven voorstellingen zodat zij in verdere **[!UICONTROL Send event]** vraag kunnen worden omvat.

## Beschikbare velden

Dit handelingstype ondersteunt de volgende velden:

* **[!UICONTROL Instance]**: De SDK-instantie waarop de handeling van toepassing is. Dit vervolgkeuzemenu is uitgeschakeld als uw implementatie één SDK-exemplaar gebruikt.
* **[!UICONTROL Propositions]**: Een array van propositieobjecten die u opnieuw wilt renderen.
* **[!UICONTROL View name]**: De naam van de weergave die moet worden weergegeven.
* **[!UICONTROL Proposition metadata]**: Een object dat bepaalt hoe HTML-aanbiedingen kunnen worden toegepast. U kunt deze informatie opgeven via het formulier of via een gegevenselement. Het bevat de volgende eigenschappen:
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
