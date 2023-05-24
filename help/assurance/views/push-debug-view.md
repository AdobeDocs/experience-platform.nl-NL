---
title: Foutopsporingsweergave duwen
description: Deze handleiding bevat informatie over de weergave Push Debug in Adobe Experience Platform Assurance.
exl-id: a9558ee2-2e80-4b0d-ab45-2020be85e634
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# Foutopsporingsweergave duwen

Met de Push Debug View in Adobe Experience Platform Assurance kunt u de Push-instelling voor uw app valideren en een testbericht naar uw apparaat verzenden.

## Clients

![Clients duwen](./images/push-debug-view/clients.png)

Het vervolgkeuzemenu voor de client bevat een lijst met elke unieke client die verbinding heeft met deze betrouwbaarheidssessie. Een client is een uniek apparaat of een unieke toepassing die voor een apparaat wordt geïnstalleerd. Als bijvoorbeeld een Android-apparaat en een iOS-apparaat met de sessie zijn verbonden, worden deze clients weergegeven in het vervolgkeuzemenu Clients.

Nadat u de app opnieuw hebt geïnstalleerd en opnieuw hebt aangesloten op een apparaat, wordt een andere client weergegeven. Als er al een apparaat met die naam bestaat, wordt #2 aan de naam toegevoegd.

Deze weergave is slechts ingeschakeld voor één client. Als u dus een andere client selecteert, worden de details op het scherm gewijzigd.

## Setup valideren

De **[!UICONTROL Validate Setup]** valideert en biedt aanvullende informatie over de pushinstellingen van de app. Er zijn drie deelvensters die validaties uitvoeren. Ze geven een groen vinkje weer als alle validaties succesvol zijn. Als er drie groene vinkjes zijn, is de app correct geconfigureerd voor pushberichten, schrijft de toepassing pushtokens naar het gebruikersprofiel en is een bijbehorende toepassingsoppervlak geconfigureerd.

Als iets niet werkt zoals verwacht, zal er een alarm met details over hoe te om dat probleem op te lossen zijn:

![Ongeldige status](./images/push-debug-view/invalid-state.png)

### Clientgegevens

Dit deelvenster controleert of het apparaat correct is geconfigureerd. Dit omvat het vormen van de uitbreiding in UI van de Inzameling van Gegevens, het initialiseren van de uitbreiding en zijn eerste vereisten in uw toepassing, en het vangen van het duptoken van het apparaat.

Indien geldig, zal het paneel ECID voor het apparaat, het duptoken, en de naam en het type van de zandbak van de Rand tonen.

### Profieldetails

Wanneer de client op de juiste wijze is ingesteld, controleert dit deelvenster of het apparaat naar profiel schrijft. Ook wordt gecontroleerd of de pushtoken in het profiel overeenkomt met de token op het apparaat.

Indien geldig, zal het paneel ECID voor het apparaat, het duptoken, app identiteitskaart van uw toepassing, het overseinenplatform tonen, en of het duptoken is vermeld. Het token kan om verschillende redenen worden geweigerd, zoals dat de gebruiker de app heeft verwijderd of dat de gebruiker pushberichten voor de app heeft uitgeschakeld.

![Geblokkeerd](./images/push-debug-view/deny-list-blocked.png)

Tot slot bevindt zich onder aan het deelvenster een koppeling waarmee dit specifieke profiel op een nieuw tabblad wordt geopend.

### Inloggegevens en configuratie van AppStore

Dit deelvenster controleert of de toepassings-id en het berichtplatform dat in het profiel is opgeslagen, een overeenkomend toepassingsoppervlak hebben gemaakt. In een toepassingsoppervlak worden de pushgegevens voor de toepassing geüpload.

Indien geldig, zal het profiel de naam van de toepassingsoppervlakte, toepassings identiteitskaart, en de naam van de overseinendienst tonen.

Tot slot bevindt zich onder aan het deelvenster een koppeling waarmee dit specifieke toepassingsoppervlak op een nieuw tabblad wordt geopend.

## Test push verzenden

De **[!UICONTROL Send Test Push]** kunt u gebruiken om een testbericht naar uw apparaat te verzenden.

Er zijn verschillende deelvensters die kunnen worden geconfigureerd om verschillende iOS- en Android-pushfuncties te testen. Zodra gevormd, uitgezocht **[!UICONTROL Send Test Push Notification]** om uw bericht te verzenden.

![Verzenden](./images/push-debug-view/send.png)

### Bericht

In de **[!UICONTROL Message]** kunt u een titel en tekst voor het bericht opgeven. De functie voor stille meldingen kan hier ook worden ingeschakeld.

![Berichtvenster](./images/push-debug-view/message-pane.png)

### Push-doel

De **[!UICONTROL Push Target]** kunt u aanpassen welk pushtoken en toepassingsoppervlak moet worden gebruikt bij het verzenden van het pushbericht.

Deze informatie wordt standaard verstrekt als de **[!UICONTROL Validate Setup]** worden drie groene vinkjes weergegeven. U kunt echter uw eigen pushtoken en toepassingsoppervlak opgeven, zelfs als uw app niet volledig is geconfigureerd.

![Doelvenster](./images/push-debug-view/target-pane.png)

### Klikken, gedrag

Van de **[!UICONTROL Click Behavior]** kunt u kiezen wat het gedrag moet zijn wanneer op het apparaat op de pushmelding wordt geklikt. De toepassing wordt standaard geopend, maar er kan een koppeling of een webpagina worden geopend.

Als u ervoor kiest een deplink te gebruiken, moet de ontwikkelaar van de app er een voor u maken.

![Gedragvenster](./images/push-debug-view/click-behavior.png)

### Rijke media

De **[!UICONTROL Rich Media]** kunt u extra media toevoegen aan uw bericht, zoals een afbeelding, video of GIF. De ontwikkelaar van de app moet code aan de app toevoegen om deze functie in te schakelen.

![Rich Pane](./images/push-debug-view/rich-pane.png)

### Knoppen

De **[!UICONTROL Buttons]** kunt u extra knoppen toevoegen aan de pushmelding. Met elke knop kunt u de app openen, een koppeling naar de app openen of een webpagina openen.

De ontwikkelaar van de app moet code aan de app toevoegen om deze functie in te schakelen.

![Deelvenster Knoppen](./images/push-debug-view/buttons-pane.png)

### Aangepaste gegevens

De **[!UICONTROL Custom Data]** kunt u aangepaste gegevens toevoegen aan het pushbericht. Elk sleutel/waardepaar wordt verzonden als meta-gegevens samen met het bericht en kan door ontwikkelaars worden gebruikt om krachtige ervaringen tot stand te brengen en extra het volgen toe te voegen.

![Aangepast venster](./images/push-debug-view/custom-pane.png)

## Testresultaten

Nadat u een bericht hebt verzonden, kunt u **[!UICONTROL Test Results]** ontvangt gegevens van de pushservices voor het bericht. Hier kunt u zien of heeft het bericht aan de Google/iOS overseinendiensten gemaakt:

![Testresultaten](./images/push-debug-view/test-results.png)

Als er problemen zijn opgetreden, worden deze hier weergegeven:

![Fout testresultaten](./images/push-debug-view/test-error.png)

## Geavanceerd

### Berichtlading weergeven

Naast de **[!UICONTROL Send Test Push Notification]** De knop is een set ovalen met een pop-upmenu. Van hier, kunt u de berichtlading bekijken. Dit laat u het nauwkeurige bericht zien dat naar de verre overseinendienst zal worden verzonden. U kunt deze lading controleren of zelfs kopiëren en kleven het in een Desktop duw testend hulpmiddel.

![Aangepast venster](./images/push-debug-view/message-payload.png)
