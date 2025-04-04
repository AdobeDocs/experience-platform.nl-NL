---
title: Ondersteuning voor Web In-app Messaging in Web SDK configureren
description: Leer hoe u de Web SDK-tagextensie configureert voor ondersteuning van Web In-app Messaging.
exl-id: 90a19ef4-e94c-4f16-a26a-8919ad2dbd6f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Ondersteuning voor Web In-app Messaging in Web SDK configureren

In-app berichten zijn meldingen die u naar gebruikers in uw webtoepassing kunt sturen en die hen naar bepaalde aandachtspunten kunnen sturen.

U kunt deze meldingen voor verschillende doeleinden gebruiken, zoals het promoten van nieuwe functies, het aanbieden van speciale aanbiedingen of het vergemakkelijken van het aan boord nemen van gebruikers.

Door in-app berichten te gebruiken, kunt u effectief met uw publiek in gesprek gaan en hen naar belangrijke aspecten van uw toepassing sturen.

>[!IMPORTANT]
>
>Het Overseinen van het Web in-app is een [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) eigenschap, die het Web SDK gebruikt om de gepersonaliseerde inhoud te leveren.
>
>Voor gedetailleerde instructies op hoe te om uw het Overseinen van het Web in-App campagne te vormen, zie de [ documentatie van Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html).


## Vereisten {#prerequisites}

### Web SDK-extensie {#extension-version}

Voor de functionaliteit voor berichten via webtoepassingen is de nieuwste versie van de Web SDK-tagextensie vereist.

### Een CSP configureren voor web in-app berichten {#csp}

Wanneer u [ het Overseinen van het Web in-App ](../personalization/web-in-app-messaging.md) vormt, moet u de volgende richtlijn in uw CSP omvatten:

```
default-src  blob:;
```

Voor meer informatie over het vormen van CSP, zie de [ specifieke documentatie ](../use-cases/configuring-a-csp.md).

## Webberichten in de app configureren met de SDK-tagextensie Web {#tag-extension}

Verwijs naar de [ pagina van de de agentenconfiguratie van SDK van het Web ](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) om te begrijpen waar u de hieronder beschreven montages kunt vinden.

Nadat u [ ](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) de de markeringsuitbreiding van SDK van het Web hebt geïnstalleerd, volg de stappen hieronder om de uitbreiding voor Web in-app Overseinen te vormen.

Schakel in de sectie **[!UICONTROL Personalization]** de optie **[!UICONTROL Enable personalization storage]** in. Met deze optie kan de SDK van het Web bijhouden welke ervaringen de gebruiker heeft gezien bij het laden van pagina&#39;s.

![ Beeld dat de optie van de verpersoonlijkingsopslag in de de configuratiepagina van de markeringsuitbreiding toont.](assets/web-in-app-messaging/enable-personalization-storage.png)


Het Web in-app Overseinen steunt twee types van trekkers:

* [Gegevens verzenden naar Experience Platform](#send-data-platform)
* [De berichten handmatig activeren](#manual-trigger)

Raadpleeg de volgende secties om de Web SDK-tagextensie te configureren op basis van de triggers die u wilt gebruiken.

### Configuratiestappen voor de trigger **[!UICONTROL Send data to Experience Platform]** {#send-data-platform}

Selecteer het markeringsbezit dat uw uitbreiding van SDK van het Web bevat, en [ creeer een nieuwe regel ](../../tags/ui/managing-resources/rules.md##create-a-rule) met de volgende montages:

1. **[!UICONTROL Extension]**: [!UICONTROL Core]
2. **[!UICONTROL Event Type]**: [!UICONTROL Library Loaded (Page Top)]

   ![ Beeld dat het scherm van de gebeurtenisconfiguratie toont.](assets/web-in-app-messaging/rule-configuration.png)

3. Selecteer **[!UICONTROL Keep Changes]** om de gebeurtenisconfiguratie op te slaan.

Vervolgens moet u een handeling toevoegen aan de regel die u hebt gemaakt.

1. Selecteer **[!UICONTROL Add]** in de sectie [!DNL Actions] .
   ![ Beeld dat uitgeeft regelscherm.](assets/web-in-app-messaging/add-action.png)

2. Gebruik de volgende **[!UICONTROL Action]** -instellingen:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action Type]**: [!UICONTROL Send event]

     ![ Beeld dat het scherm van de actieconfiguratie toont.](assets/web-in-app-messaging/action-configuration.png)

3. Schakel rechts in het scherm in de sectie **[!UICONTROL Personalization]** de optie **[!UICONTROL Render visual personalization decisions]** in.
   ![ Beeld dat het scherm van de verpersoonlijkingsconfiguratie toont.](assets/web-in-app-messaging/render-visual-personalization.png)

4. Op de rechterkant van het scherm, in de **[!UICONTROL Decision context]** sectie, bepaal de **[!UICONTROL Key]**/ **[!UICONTROL Value]** paren die u in uw campagneconfiguratie gebruikte, om voor het in-app bericht in aanmerking te komen.
   ![ Beeld dat het scherm van de verpersoonlijkingsconfiguratie toont.](assets/web-in-app-messaging/decision-context.png)

5. Selecteer **[!UICONTROL Keep Changes]** om uw configuratie op te slaan.


Vervolgens moet u de nieuwe regel toevoegen aan de bibliotheek met eigenschappen van de tag. Ga hiertoe naar **[!UICONTROL Publishing Flow]** en selecteer de regel die u eerder hebt gemaakt.

![ Beeld dat het bibliotheekscherm toont.](assets/web-in-app-messaging/add-rule-to-library.png)

Nadat u de regel aan de bibliotheek hebt toegevoegd, selecteert u **[!UICONTROL Save & Build to Development]**.

![ Beeld dat het scherm van de verpersoonlijkingsconfiguratie toont.](assets/web-in-app-messaging/publish-flow.png)

Het configuratieproces is nu voltooid en uw bericht is klaar om aan uw gebruikers te worden getoond.

### Configuratiestappen voor het gebruik van handmatige triggers {#manual-trigger}

Selecteer het markeringsbezit dat uw uitbreiding van SDK van het Web bevat, en [ creeer een nieuwe regel ](../../tags/ui/managing-resources/rules.md##create-a-rule) met de volgende montages:

1. **[!UICONTROL Extension]**: [!UICONTROL Core]
2. **[!UICONTROL Event Type]**: [!UICONTROL Click]
3. Stel de trigger voor een specifiek element op de pagina in, herkenbaar aan een CSS-kiezer van uw keuze.

   ![ Beeld dat het scherm van de gebeurtenisconfiguratie toont.](assets/web-in-app-messaging/event-configuration-manual.png)


Vervolgens moet u een handeling toevoegen aan de regel die u hebt gemaakt.

1. Selecteer **[!UICONTROL Add]** in de sectie [!DNL Actions] .
   ![ Beeld dat uitgeeft regelscherm.](assets/web-in-app-messaging/add-action.png)

2. Gebruik de volgende **[!UICONTROL Action]** -instellingen:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action Type]**: [!UICONTROL Evaluate rulesets]

     ![ Beeld dat het scherm van de actieconfiguratie toont.](assets/web-in-app-messaging/manual-trigger-action.png)

3. Schakel rechts van het scherm de optie **[!UICONTROL Render visual personalization decisions]** in.
   ![ Beeld dat het scherm van de verpersoonlijkingsconfiguratie toont.](assets/web-in-app-messaging/manual-trigger-render.png)


4. Op de rechterkant van het scherm, in de **[!UICONTROL Decision context]** sectie, bepaal de **[!UICONTROL Key]**/ **[!UICONTROL Value]** paren die u in uw campagneconfiguratie gebruikte, om voor het in-app bericht in aanmerking te komen.
   ![ Beeld dat het scherm van de verpersoonlijkingsconfiguratie toont.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. Selecteer **[!UICONTROL Keep Changes]** om uw configuratie op te slaan.

Vervolgens moet u de nieuwe regel toevoegen aan de bibliotheek met eigenschappen van de tag. Ga hiertoe naar **[!UICONTROL Publishing Flow]** en selecteer de regel die u eerder hebt gemaakt.

![ Beeld dat het bibliotheekscherm toont.](assets/web-in-app-messaging/add-rule-to-library.png)

Nadat u de regel aan de bibliotheek hebt toegevoegd, selecteert u **[!UICONTROL Save & Build to Development]**.

![ Beeld dat het scherm van de verpersoonlijkingsconfiguratie toont.](assets/web-in-app-messaging/publish-flow.png)

Het configuratieproces is nu voltooid en uw bericht is klaar om aan uw gebruikers te worden getoond.

## Webberichten in de app configureren met behulp van de Web SDK JavaScript-bibliotheek {#js-library}

Als alternatief voor het gebruiken van de de markeringsuitbreiding van SDK van het Web, kunt u Web in-App Overseinen direct van de bibliotheek van SDK van het Web vormen.



U kunt binnen-app berichten van Adobe Journey Optimizer op twee manieren weergeven.

### Methode 1: hiermee wordt de inhoud van de personalisatie automatisch opgehaald {#automatic}

Als u wilt dat Web SDK de personalisatie-inhoud automatisch ophaalt bij het laden van de pagina, gebruikt u de opdracht `sendEvent` , zoals in het onderstaande voorbeeld wordt getoond.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### Methode 2: hiermee wordt de inhoud van de personalisatie handmatig opgehaald op basis van gebruikersactie {#manual}

Als u de verpersoonlijkingsinhoud alleen wilt weergeven nadat de gebruiker een specifieke handeling heeft uitgevoerd, gebruikt u de opdracht `evaluateRulesets` , zoals in het onderstaande voorbeeld wordt getoond.

In dit voorbeeld wordt de personalisatie-inhoud weergegeven wanneer een gebruiker op de knop **[!UICONTROL Buy Now]** op uw website klikt.

```js
 alloy("evaluateRulesets", {
     renderDecisions: true,
     personalization: {
         decisionContext: {
             "userAction": "buy_now"
         }
     }
 });
```

### Opslag voor personalisatie configureren {#personalization-storage}

Met de configuratieoptie `personalizationStorageEnabled` kunt u ervoor kiezen om in-app berichten voor een bepaald aantal keren of telkens wanneer gebruikers een pagina bezoeken, weer te geven.

In de [ configuratie van SDK van het Web ](../commands/configure/overview.md) plaats de `personalizationStorageEnabled` optie volgens uw behoeften:

* `personalizationStorageEnabled: true` brengt het in-app bericht met de frequentie teweeg u in de [ campagne van Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html#configure-inapp) bepaalde.
* `personalizationStorageEnabled: false` activeert het bericht in de app bij het laden van elke pagina.
