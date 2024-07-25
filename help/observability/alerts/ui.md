---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: UI-gids voor waarschuwingen
description: Leer hoe u waarschuwingen beheert in de gebruikersinterface van het Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Handleiding Waarschuwingsinterface

In de Adobe Experience Platform-gebruikersinterface kunt u een geschiedenis bekijken van ontvangen waarschuwingen op basis van meetgegevens die zijn onthuld door Adobe Experience Platform Observability Insights. UI staat u toe ook om, beschikbare waakzame regels te bekijken, toe te laten onbruikbaar te maken en in te tekenen.

>[!NOTE]
>
>Voor een inleiding aan alarm in Experience Platform, zie het [ alarm overzicht ](./overview.md).

Selecteer **[!UICONTROL Alerts]** in de linkernavigatie om aan de slag te gaan.

![ Alarm pagina die [!UICONTROL Alerts] in de linkernavigatie benadrukt.](../images/alerts/ui/workspace.png)

## Waarschuwingsregels beheren

Het tabblad **[!UICONTROL Browse]** bevat een lijst met de beschikbare regels die een waarschuwing kunnen activeren.

![ een lijst van beschikbare alarm toont in [!UICONTROL Browse] tabel.](../images/alerts/ui/rules.png)

Selecteer een regel in de lijst om de beschrijving en de configuratieparameters ervan in de rechtertrack weer te geven, inclusief de drempel en de ernst.

![ benadrukte een waakzame regel die details in het juiste spoor toont.](../images/alerts/ui/rule-details.png)

Selecteer de ellips (**...**) naast de naam van een regel, en een dropdown vertoningencontroles om de alarm (afhankelijk van zijn huidige status) toe te laten of onbruikbaar te maken, en om aan e-mailberichten voor de alarm in te tekenen of af te melden.

![ de geselecteerde ellipsen openbaren het drop-down menu.](../images/alerts/ui/disable-subscribe.png)

## Waarschuwingsabonnees beheren

>[!NOTE]
>
> Als u een waarschuwing wilt toewijzen aan een gebruikers-id van een Adobe, een extern e-mailadres of een lijst met e-mailgroepen, moet u een beheerder zijn.

Het tabblad **[!UICONTROL Browse]** bevat een lijst met de beschikbare regels die een waarschuwing kunnen activeren.

![ een lijst van beschikbare waakzame regels die in [!UICONTROL Browse] worden getoond tabel.](../images/alerts/ui/rules.png)

Selecteer de ellips (**...**) naast de naam van een regel, een dropdown vertoningencontroles. Selecteer **[!UICONTROL Manage alert subscribers]**.

![ selecteer de ellipsen om het drop-down menu te tonen. De optie [!UICONTROL Manage alert subscribers] wordt gemarkeerd. ](../images/alerts/ui/manage-alert-subscribers.png)

De pagina [!UICONTROL Manage alert subscribers] wordt weergegeven. Als u meldingen wilt toewijzen aan specifieke gebruikers, voert u de gebruikers-id, het externe e-mailadres of een lijst met e-mailgroepen van die gebruikers in en drukt u op Enter.

>[!NOTE]
>
>Als u deze kennisgeving tegelijk naar meerdere gebruikers wilt verzenden, geeft u een lijst op met gebruikers-id&#39;s of e-mailadressen, gescheiden door komma&#39;s.

![ beheert waakzame pagina die van abonnees ingaat e-mailadressen toont.](../images/alerts/ui/manage-alert-add-email.png)

De e-mailadressen worden weergegeven in de lijst met huidige abonnees. Selecteer **[!UICONTROL Update]**.

![ beheert waakzame abonnees pagina die abonnees en [!UICONTROL Update] benadrukken.](../images/alerts/ui/manage-alert-subscribers-added-email.png)

U hebt gebruikers toegevoegd aan uw lijst met waarschuwingen. De verzonden gebruikers ontvangen nu e-mailmeldingen voor deze waarschuwing zoals in de onderstaande afbeelding wordt weergegeven.

![ een e-mailvoorbeeld van het waakzame bericht dat wordt ontvangen.](../images/alerts/ui/manage-alert-subscribers-email.png)

## E-mailwaarschuwingen inschakelen

Waarschuwingsberichten kunnen rechtstreeks naar uw e-mail worden verzonden.

Selecteer het klokpictogram (![ klokpictogram ](/help/images/icons/bell.png)) dat in het hoogste lint op het recht wordt gevestigd om berichten en aankondigingen te tonen. In dropdown die verschijnt, selecteer het cogopictogram (![ cog pictogram ](/help/images/icons/settings.png)) om tot de de voorkeurspagina van het Experience Cloud toegang te hebben.

![ een lijst van alarm die het belpictogram en het cogpictogram benadrukken wordt getoond.](../images/alerts/ui/edit-preferences.png)

De **pagina van het Profiel** wordt getoond. Selecteer **[!UICONTROL Notifications]** in de linkernavigatie om de voorkeuren voor e-mailwaarschuwingen te openen.

![ de pagina die van het Profiel [!UICONTROL Notifications] in de linkernavigatie benadrukt.](../images/alerts/ui/profile.png)

De rol aan de **sectie van E-mail** bij de bodem van de pagina en selecteert **[!UICONTROL Instant notifications]**

![ de E-mails sectie die in de pagina van het Profiel wordt benadrukt.](../images/alerts/ui/notifications.png)

Alle waarschuwingen waarop je bent geabonneerd, worden nu verzonden naar het e-mailadres dat is verbonden met je Adobe ID-account.

## Berichtengeschiedenis weergeven

Het tabblad **[!UICONTROL History]** geeft de geschiedenis weer van ontvangen waarschuwingen voor uw organisatie, inclusief de regel die de waarschuwing heeft geactiveerd, de geactiveerde datum en de opgeloste datum (indien van toepassing).

![ een lijst van ontvangen alarm toont in [!UICONTROL History] tabel.](../images/alerts/ui/history.png)

Selecteer een vermeld alarm en meer details verschijnen in het juiste spoor, met inbegrip van een korte samenvatting van de gebeurtenis die de alarm teweegbracht.

![ een alarm benadrukte tonend details in het juiste spoor.](../images/alerts/ui/history-details.png)

## Volgende stappen

Dit document biedt een overzicht van het weergeven en beheren van waarschuwingen in de gebruikersinterface van het platform. Zie het overzicht op [ Inzichten van de Waarneming ](../home.md) voor meer informatie over de mogelijkheden van de dienst.
