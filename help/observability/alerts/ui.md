---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: UI-gids voor waarschuwingen
description: Leer hoe u waarschuwingen beheert in de gebruikersinterface van het Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 8d63e9fa4c7eb09ffb90edca612a6e6d44dd18fa
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Handleiding Waarschuwingsinterface

In de Adobe Experience Platform-gebruikersinterface kunt u een geschiedenis bekijken van ontvangen waarschuwingen op basis van meetgegevens die zijn onthuld door Adobe Experience Platform Observability Insights. UI staat u toe ook om, beschikbare waakzame regels te bekijken, toe te laten onbruikbaar te maken en in te tekenen.

>[!NOTE]
>
>Voor een inleiding op signaleringen in Experience Platform raadpleegt u de [waarschuwingsoverzicht](./overview.md).

Selecteer **[!UICONTROL Alerts]** in de linkernavigatie.

![Waarschuwingen op pagina markeren [!UICONTROL Alerts] in de linkernavigatie.](../images/alerts/ui/workspace.png)

## Waarschuwingsregels beheren

De **[!UICONTROL Browse]** worden de beschikbare regels weergegeven die een waarschuwing kunnen activeren.

![Een lijst met beschikbare waarschuwingen wordt weergegeven in het gedeelte [!UICONTROL Browse] tab.](../images/alerts/ui/rules.png)

Selecteer een regel in de lijst om de beschrijving en de configuratieparameters ervan in de rechtertrack weer te geven, inclusief de drempel en de ernst.

![Een waarschuwingsregel die de details in de rechterspoorlijn toont.](../images/alerts/ui/rule-details.png)

De ovaal selecteren (**...**) naast de naam van een regel en in een vervolgkeuzelijst worden besturingselementen weergegeven om de waarschuwing in of uit te schakelen (afhankelijk van de huidige status) en om zich te abonneren op e-mailberichten voor de waarschuwing of het abonnement op te zeggen.

![De geselecteerde ellipsen tonen het drop-down menu.](../images/alerts/ui/disable-subscribe.png)

## Waarschuwingsabonnees beheren

>[!NOTE]
>
> Als u een waarschuwing wilt toewijzen aan een gebruikers-id van een Adobe, een extern e-mailadres of een lijst met e-mailgroepen, moet u een beheerder zijn.

De **[!UICONTROL Browse]** worden de beschikbare regels weergegeven die een waarschuwing kunnen activeren.

![Een lijst met beschikbare waarschuwingsregels in het dialoogvenster [!UICONTROL Browse] tab.](../images/alerts/ui/rules.png)

De ovaal selecteren (**...**) naast de naam van een regel worden in een vervolgkeuzelijst besturingselementen weergegeven. Selecteer **[!UICONTROL Manage alert subscribers]**.

![Selecteer de ellipsen om het drop-down menu te tonen. De [!UICONTROL Manage alert subscribers] wordt gemarkeerd.](../images/alerts/ui/manage-alert-subscribers.png)

De [!UICONTROL Manage alert subscribers] wordt weergegeven. Als u meldingen wilt toewijzen aan specifieke gebruikers, voert u de gebruikers-id, het externe e-mailadres of een lijst met e-mailgroepen van die gebruikers in en drukt u op Enter.

>[!NOTE]
>
>Als u deze kennisgeving tegelijk naar meerdere gebruikers wilt verzenden, geeft u een lijst op met gebruikers-id&#39;s of e-mailadressen, gescheiden door komma&#39;s.

![De pagina voor het beheren van waarschuwingsabonnees met ingevoerde e-mailadressen.](../images/alerts/ui/manage-alert-add-email.png)

De e-mailadressen worden weergegeven in de lijst met huidige abonnees. Selecteer **[!UICONTROL Update]**.

![De pagina voor het beheren van waarschuwingsabonnees die abonnees markeren en [!UICONTROL Update].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

U hebt gebruikers toegevoegd aan uw lijst met waarschuwingen. De verzonden gebruikers ontvangen nu e-mailmeldingen voor deze waarschuwing zoals in de onderstaande afbeelding wordt weergegeven.

![Een e-mailvoorbeeld van het waarschuwingsbericht dat wordt ontvangen.](../images/alerts/ui/manage-alert-subscribers-email.png)

## E-mailwaarschuwingen inschakelen

Waarschuwingsberichten kunnen rechtstreeks naar uw e-mail worden verzonden.

Selecteer het belpictogram (![belpictogram](../images/alerts/ui/bell-icon.png)) in het bovenste lint aan de rechterkant om meldingen en aankondigingen weer te geven. Selecteer in het vervolgkeuzemenu dat wordt weergegeven het cogopictogram (![cogpictogram](../images/alerts/ui/cog-icon.png)) voor toegang tot de pagina met voorkeuren voor Experiencen Cloud.

![Een lijst met waarschuwingen die het belpictogram en het cogingspictogram markeren.](../images/alerts/ui/edit-preferences.png)

De **Profiel** wordt weergegeven. Selecteer de **[!UICONTROL Notifications]** in de linkernavigatie voor toegang tot de voorkeuren voor e-mailwaarschuwingen.

![De paginamarkering Profiel [!UICONTROL Notifications] in de linkernavigatie.](../images/alerts/ui/profile.png)

Naar de **E-mails** onder aan de pagina selecteert u **[!UICONTROL Instant notifications]**

![De sectie E-mails wordt gemarkeerd op de pagina Profiel.](../images/alerts/ui/notifications.png)

Alle waarschuwingen waarop je bent geabonneerd, worden nu verzonden naar het e-mailadres dat is verbonden met je Adobe ID-account.

## Berichtengeschiedenis weergeven

De **[!UICONTROL History]** toont de geschiedenis van ontvangen alarm voor uw organisatie, met inbegrip van de regel die de alarm, teweeggebrachte datum, en opgeloste datum (indien van toepassing) teweegbracht.

![Een lijst met ontvangen waarschuwingen wordt weergegeven in het dialoogvenster [!UICONTROL History] tab.](../images/alerts/ui/history.png)

Selecteer een vermeld alarm en meer details verschijnen in het juiste spoor, met inbegrip van een korte samenvatting van de gebeurtenis die de alarm teweegbracht.

![Een waarschuwing met details in het rechterspoor.](../images/alerts/ui/history-details.png)

## Volgende stappen

Dit document biedt een overzicht van het weergeven en beheren van waarschuwingen in de gebruikersinterface van het platform. Zie het overzicht op [Waarnembaarheidsinzichten](../home.md) voor meer informatie over de mogelijkheden van de dienst.
