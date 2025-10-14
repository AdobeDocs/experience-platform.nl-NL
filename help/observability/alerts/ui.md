---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: UI-gids voor waarschuwingen
description: Leer hoe u waarschuwingen beheert in de Experience Platform-gebruikersinterface.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 57261ca37bf10e394f47ea4bb3c01856a18b197d
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 4%

---

# Handleiding Waarschuwingsinterface

In de Adobe Experience Platform-gebruikersinterface kunt u een geschiedenis bekijken van ontvangen waarschuwingen op basis van meetgegevens die zijn onthuld door Adobe Experience Platform Observability Insights. UI staat u toe ook om, beschikbare waakzame regels te bekijken, toe te laten onbruikbaar te maken en in te tekenen.

>[!NOTE]
>
>Voor een inleiding aan alarm in Experience Platform, zie het [&#x200B; alarm overzicht &#x200B;](./overview.md).

Selecteer **[!UICONTROL Alerts]** in de linkernavigatie om aan de slag te gaan.

![&#x200B; Alarm pagina die [!UICONTROL Alerts] in de linkernavigatie benadrukt.](../images/alerts/ui/workspace.png)

## Waarschuwingsregels beheren {#manage-rules}

Het tabblad **[!UICONTROL Browse]** bevat een lijst met de beschikbare regels die een waarschuwing kunnen activeren.

![&#x200B; een lijst van beschikbare alarm toont in [!UICONTROL Browse] tabel.](../images/alerts/ui/rules.png)

Selecteer een regel in de lijst om de beschrijving en de configuratieparameters ervan in de rechtertrack weer te geven, inclusief de drempel en de ernst.

![&#x200B; benadrukte een waakzame regel die details in het juiste spoor toont.](../images/alerts/ui/rule-details.png)

Selecteer de ellips (**...**) naast de naam van een regel, en een dropdown vertoningencontroles om de alarm (afhankelijk van zijn huidige status) toe te laten of onbruikbaar te maken, en om aan e-mailberichten voor de alarm in te tekenen of af te melden.

![&#x200B; de geselecteerde ellipsen openbaren het drop-down menu.](../images/alerts/ui/disable-subscribe.png)

## Waarschuwingsabonnees beheren {#manage-subscribers}

>[!NOTE]
>
> Als u een waarschuwing wilt toewijzen aan een Adobe-gebruikersnaam, een extern e-mailadres of een lijst met e-mailgroepen, moet u een beheerder zijn.

Het tabblad **[!UICONTROL Browse]** bevat een lijst met de beschikbare regels die een waarschuwing kunnen activeren.

![&#x200B; een lijst van beschikbare waakzame regels die in [!UICONTROL Browse] worden getoond tabel.](../images/alerts/ui/rules.png)

Selecteer de ellips (**...**) naast de naam van een regel, een dropdown vertoningencontroles. Selecteer **[!UICONTROL Manage alert subscribers]**.

![&#x200B; selecteer de ellipsen om het drop-down menu te tonen. De optie [!UICONTROL Manage alert subscribers] wordt gemarkeerd. &#x200B;](../images/alerts/ui/manage-alert-subscribers.png)

De pagina [!UICONTROL Manage alert subscribers] wordt weergegeven. Als u berichten wilt toewijzen aan specifieke gebruikers, voert u hun Adobe-gebruikersnaam, extern e-mailadres of een lijst met e-mailgroepen in en drukt u op Enter.

>[!NOTE]
>
>Als u deze kennisgeving tegelijk naar meerdere gebruikers wilt verzenden, geeft u een lijst op met gebruikers-id&#39;s of e-mailadressen, gescheiden door komma&#39;s.

![&#x200B; beheert waakzame pagina die van abonnees ingaat e-mailadressen toont.](../images/alerts/ui/manage-alert-add-email.png)

De e-mailadressen worden weergegeven in de lijst met huidige abonnees. Selecteer **[!UICONTROL Update]**.

![&#x200B; beheert waakzame abonnees pagina die abonnees en [!UICONTROL Update] benadrukken.](../images/alerts/ui/manage-alert-subscribers-added-email.png)

U hebt gebruikers toegevoegd aan uw lijst met waarschuwingen. De verzonden gebruikers ontvangen nu e-mailmeldingen voor deze waarschuwing zoals in de onderstaande afbeelding wordt weergegeven.

![&#x200B; een e-mailvoorbeeld van het waakzame bericht dat wordt ontvangen.](../images/alerts/ui/manage-alert-subscribers-email.png)

## E-mailwaarschuwingen inschakelen {#enable-email}

Waarschuwingsberichten kunnen rechtstreeks naar uw e-mail worden verzonden.

Selecteer het klokpictogram (![&#x200B; klokpictogram &#x200B;](/help/images/icons/bell.png)) dat in het hoogste lint op het recht wordt gevestigd om berichten en aankondigingen te tonen. In dropdown die verschijnt, selecteer het cogapictogram (![&#x200B; cog pictogram &#x200B;](/help/images/icons/settings.png)) om tot de de voorkeurenpagina van Experience Cloud toegang te hebben.

![&#x200B; een lijst van alarm die het belpictogram en het cogpictogram benadrukken wordt getoond.](../images/alerts/ui/edit-preferences.png)

De **pagina van het Profiel** wordt getoond. Selecteer **[!UICONTROL Notifications]** in de linkernavigatie om de voorkeuren voor e-mailwaarschuwingen te openen.

![&#x200B; de pagina die van het Profiel [!UICONTROL Notifications] in de linkernavigatie benadrukt.](../images/alerts/ui/profile.png)

De rol aan de **sectie van E-mail** bij de bodem van de pagina en selecteert **[!UICONTROL Instant notifications]**

![&#x200B; de E-mails sectie die in de pagina van het Profiel wordt benadrukt.](../images/alerts/ui/notifications.png)

Alle waarschuwingen waarop je bent geabonneerd, worden nu verzonden naar het e-mailadres dat is verbonden met je Adobe ID-account.

## Drempel voor waarschuwingen aanpassen {#alert-threshold}

De drempelwaarden van de alarm kunnen voor de volgende waakzame types worden aangepast:

| Type waarschuwing | Aangepaste parameter |
|---|---|
| Vertraging segmenttaak | Vertragingsdrempel |
| Vertraging bij exporteren segment | Vertragingsdrempel |
| Vertraging bij uitvoering van bestemming | Vertragingsdrempel |
| Vertraging bij uitvoering identiteitsserviceworkflow | Vertragingsdrempel |
| Vertraging bij uitvoering van profielworkflow | Vertragingsdrempel |
| Foutsnelheid voor profielstreaming | Foutdrempel |
| Overgeslagen snelheid van inname profiel streaming | Foutdrempel |
| Vertraging bij uitvoering van workflow voor bronnen | Vertragingsdrempel |
| Foutpercentage van opname van bronnen overschreden | Foutdrempel |
| Vertraging bij het uitvoeren van query&#39;s | Vertragingsdrempel |
| Activeringssnelheid overschreden | Foutdrempel |

Selecteer de ellips (**...**) naast de naam van een regel, een dropdown vertoningencontroles. Selecteer **[!UICONTROL Edit]**.

![&#x200B; de [!UICONTROL Edit] optie wordt benadrukt voor de geselecteerde regel.](../images/alerts/ui/threshold-edit.png)

De pagina **[!UICONTROL Customize alert]** wordt weergegeven. Werk de drempelwaarde bij tot de gewenste minuten en selecteer vervolgens **[!UICONTROL Confirm]** .

![&#x200B; de Customize waakzame pagina die [!UICONTROL Threshold] en [!UICONTROL Confirm] opties benadrukt.](../images/alerts/ui/threshold-update.png)

U wordt teruggestuurd naar de pagina **[!UICONTROL Alerts]** . Als u de drempelinstellingen voor de waarschuwing wilt weergeven, selecteert u de regel in de lijst. U kunt de drempelinstellingen voor de waarschuwing zien in de rechterrail, inclusief details zoals de status en ernst.

![&#x200B; een alarm benadrukte tonend details in het juiste spoor en het benadrukken [!UICONTROL Threshold].](../images/alerts/ui/threshold-view.png)

## Berichtengeschiedenis weergeven {#alert-history}

Het tabblad **[!UICONTROL History]** geeft de geschiedenis weer van ontvangen waarschuwingen voor uw organisatie, inclusief de regel die de waarschuwing heeft geactiveerd, de geactiveerde datum en de opgeloste datum (indien van toepassing).

![&#x200B; een lijst van ontvangen alarm toont in [!UICONTROL History] tabel.](../images/alerts/ui/history.png)

Selecteer een vermeld alarm en meer details verschijnen in het juiste spoor, met inbegrip van een korte samenvatting van de gebeurtenis die de alarm teweegbracht.

![&#x200B; een alarm benadrukte tonend details in het juiste spoor.](../images/alerts/ui/history-details.png)

## Volgende stappen

Dit document biedt een overzicht van het weergeven en beheren van waarschuwingen in de gebruikersinterface van Experience Platform. Zie het overzicht op [&#x200B; Inzichten van de Waarneming &#x200B;](../home.md) voor meer informatie over de mogelijkheden van de dienst.
