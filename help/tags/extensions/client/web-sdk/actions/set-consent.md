---
title: Goedkeuring instellen
description: Hiermee stelt u de gewenste toestemming voor de bezoeker in.
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Goedkeuring instellen

De **[!UICONTROL Set consent]** actie bepaalt als de markeringsuitbreiding gegevens (opt in) zou moeten verzenden, gegevens (opt out) zou verwerpen, of [&#x200B; standaardtoestemming &#x200B;](../configure/consent.md) (onbekende toestemming) gebruiken. Wanneer een gebruiker toestemming op uw site toestaat of weigert, kunt u deze handeling gebruiken om hun voorkeuren te synchroniseren met de tagextensie. Het JavaScript-bibliotheekequivalent van deze actie is de opdracht [`setConsent`](/help/collection/js/commands/setconsent.md) .

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel vervolgens de waarde [!UICONTROL Action type] in op **[!UICONTROL Set consent]** .

De tagextensie ondersteunt de volgende standaarden:

* **[norm Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Zowel worden 1.0 als 2.0 normen gesteund.
* **[het Kader van de Transparantie &amp; van de Toestemming IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Als u deze norm gebruikt, wordt het Echte Profiel van de Klant van de bezoeker - tijd bijgewerkt met de toestemmingsinformatie als uw implementatie correct wordt gevormd:
   1. Het XDM individuele profielschema bevat [&#x200B; IAB TCF 2.0 de gebiedsgroep van de Toestemming &#x200B;](/help/xdm/field-groups/profile/iab.md).
   1. Het schema van de Gebeurtenis van de Ervaring bevat [&#x200B; IAB TCF 2.0 de gebiedsgroep van de Toestemming &#x200B;](/help/xdm/field-groups/event/iab.md).

Adobe raadt u aan om voorkeuren voor het bevestigingsvenster afzonderlijk op te slaan, bijvoorbeeld in een gegevenselement. De uitbreiding van de tag biedt geen manier om toestemming op te halen. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de tagextensie, kunt u deze actie uitvoeren op elke pagina die wordt geladen.

## Beschikbare velden

Dit handelingstype ondersteunt de volgende configuratieopties:

* **[!UICONTROL Instance]**: De SDK-instantie waarop de handeling van toepassing is. Dit vervolgkeuzemenu is uitgeschakeld als uw implementatie één SDK-exemplaar gebruikt.
* **[!UICONTROL Identity map]**: Een gegevenselement dat bepaalt hoe een ECID wordt gegenereerd en aan welke ID&#39;s toestemmingsinformatie is gekoppeld.
* **[!UICONTROL Consent information]**: hiermee wordt bepaald of u een formulier wilt invullen of een gegevenselement wilt opgeven met informatie over toestemming.
* **[!UICONTROL Standard]**: De toestemmingsnorm die u wilt gebruiken. Beschikbare opties omvatten &quot;[!UICONTROL Adobe]&quot;en &quot;[!UICONTROL IAB TCF]&quot;.
* **[!UICONTROL Version]**: De versie van de toestemmingsnorm die u wilt gebruiken.
* **[!UICONTROL Datastream configuration overrides]**: deze opdracht ondersteunt de configuratieoverschrijvingen van de gegevensstroom, zodat u zelf kunt bepalen welke apps en services deze gegevens ontvangen. Wanneer u een gegevensstroomconfiguratieopheffing in zowel een individueel bevel als binnen de de configuratiemontages van de markeringsuitbreiding plaatst, neemt het individuele bevel belangrijkheid. Zie [&#x200B; de configuratiemet voeten treedt van de Gegevensstroom &#x200B;](../configure/configuration-overrides.md) voor meer informatie.

## Een regel maken die informatie over toestemming bijwerkt

De ideale tijd om deze handeling te gebruiken is wanneer de voorkeuren voor toestemming van een klant zijn gewijzigd. U kunt een labelregel maken om naar deze wijziging te luisteren.

1. Navigeer binnen een eigenschap tag naar **[!UICONTROL Rules]** en selecteer **[!UICONTROL Add rule]** .
1. Geef de regel een gewenste naam, dan selecteer het &quot;`+`&quot;pictogram naast **[!UICONTROL Events]**.
1. Stel de volgende eigenschappen links in:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. Open de editor aan de rechterkant en gebruik de volgende code als sjabloon:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

1. Selecteer **[!UICONTROL Keep changes]**.

Het bovenstaande aangepaste codeblok doet twee dingen:

* De regel wordt geactiveerd wanneer de voorkeuren voor toestemming zijn gewijzigd.
* Plaatst twee gegevenselementen: **IAB TCF het ToestemmingsKoord** en **IAB TCF Toestemming GDPR**.

Deze gegevenselementen zijn nuttig wanneer het plaatsen van de &quot;[!UICONTROL Set Consent]&quot;actie:

1. Selecteer het pictogram &#39;`+`&#39; naast **[!UICONTROL Actions]** .
1. Stel de volgende eigenschappen links in:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. Stel de volgende eigenschappen in aan de rechterkant:
   * **[!UICONTROL Standard]**: [!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**: [!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**: [!UICONTROL Provide a data element] , met de waarde `%IAB TCF Consent GDPR%`

![&#x200B; IAB plaatste de Actie van de Toestemming &#x200B;](../assets/iab-action.png)

>[!NOTE]
>
>U kunt deze gegevenselementen niet kiezen met de gegevenselementkiezer omdat ze zijn gemaakt met aangepaste code. U moet in de naam van het gegevenselement met de percentagetekens typen.
