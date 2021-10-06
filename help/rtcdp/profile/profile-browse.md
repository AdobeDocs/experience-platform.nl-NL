---
keywords: weergaveprofielen rtcdp;rtcdp, profielweergave;rtcdp-profielen
title: Bladeren door profielen in Real-time Customer Data Platform
description: Met Real-time Customer Data Platform kunt u in real-time door de gegevens van het klantprofiel bladeren via de Adobe Experience Platform-gebruikersinterface.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 6579e371a8729e926b7061418c786150a27d4876
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Bladeren door profielen in Real-time Customer Data Platform

Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren. Aangezien de individuele profielen op gegevens worden samengevoegd die in het systeem van diverse bronnen worden gebracht, wordt elk profiel een actionable, timestamped rekening van elke interactie uw klant met uw merk heeft.

In de gebruikersinterface van Adobe Experience Platform kunt u deze alleen-lezen profielen weergeven en belangrijke informatie over elk van uw individuele klanten bekijken, zoals hun voorkeuren, gebeurtenissen uit het verleden, interacties en de segmenten waartoe het individu behoort.

Real-time Customer Data Platform is gebouwd op Adobe Experience Platform en kan daardoor gebruikmaken van de mogelijkheden voor profielweergave in de gebruikersinterface van het Experience Platform. Raadpleeg de [Gebruikershandleiding voor realtime gebruikersprofiel](../../profile/ui/user-guide.md) voor een gedetailleerde handleiding voor het weergeven van klantprofielen in de gebruikersinterface van het Platform.

## Profielverbeteringen voor CDP en B2B Edition in realtime

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition is momenteel in bèta. De documentatie en functionaliteit kunnen worden gewijzigd.

Naast de mogelijkheden voor bladeren in profielen die door Adobe Experience Platform worden ondersteund, kunnen gebruikers van CDP- en B2B-edities in realtime toegang krijgen tot B2B-kenmerken en -gebeurtenissen binnen het klantprofiel op respectievelijk de tabbladen [!UICONTROL Attributes] en [!UICONTROL Events]. B2B-gegevens kunnen ook worden gebruikt om segmentatie uit te voeren, waarbij de segmenten onder de tab [!UICONTROL Segment membership] van de klant naast niet-B2B-segmenten worden weergegeven.

Met CDP, B2B Edition in realtime kunt u [!UICONTROL Accounts], [!UICONTROL Opportunities] en [!UICONTROL Source records] vanuit uw bedrijfsbronnen bladeren die aan een individuele klant zijn gekoppeld.

Om deze verhogingen te onderzoeken, begin door de stappen te volgen die in [Gebruikershandleiding ](../../profile/ui/user-guide.md) in real time van het Profiel van de Klant worden geschetst om een profiel door fusiebeleid of identiteitsnamespace te doorbladeren.

![](images/b2b-browse-profile.png)

De profieldetails omvatten toegang tot [!UICONTROL Accounts], [!UICONTROL Opportunities], en [!UICONTROL Source records] lusjes naast de standaardinformatie die in het klantenprofiel wordt verstrekt dat ook met B2B gebeurtenissen en attributen is verbeterd.

![](images/b2b-profile-detail.png)

### Het tabblad Accounts

Selecteer **[!UICONTROL Accounts]** om een lijst met accounts weer te geven die betrekking hebben op het profiel. Deze lijst bevat basisgegevens uit het accountprofiel, zoals de naam, website en branche van de account, en een koppeling naar het accountprofiel.

Voor meer informatie over het bekijken van en het onderzoeken van rekeningsprofielen, begin door [accountprofielen overzicht](../accounts/account-profile-overview.md) te lezen.

![](images/b2b-profile-accounts.png)

### Tabblad Kansen

Het tabblad **[!UICONTROL Opportunities]** bevat details over open en gesloten mogelijkheden met betrekking tot de account. Deze kansen kunnen in Experience Platform van veelvoudige bronnen worden opgenomen, nochtans in real time CDP, maakt B2B Uitgave het voor marketers gemakkelijk om al deze kansen samen op één plaats te zien.

Elke kans bevat informatie zoals de naam van de kans, de hoeveelheid kansen, het werkgebied en of de kans open, gesloten, gewonnen of verloren is.

![](images/b2b-profile-opportunities.png)

### Tabblad Bronrecords

Met de tab **[!UICONTROL Source records]** kunt u eenvoudig de meerdere bronrecords zien die afkomstig zijn van uw bedrijfsbronnen die bijdragen aan het profiel van één klant. Naast [!UICONTROL Person source key] en e-mailadres, verstrekt elke bronverslag ook het type van verslag (bijvoorbeeld, een &quot;contact&quot;of &quot;lood&quot;verslag), evenals de bron.

![](images/b2b-profile-source-records.png)
