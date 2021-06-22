---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd;profiel;rtcp;XDM-grafieken
title: Aangepaste toegankelijkheidsoplossingen voor Experience Platform
topic: hulplijn
type: Documentation
description: Meer informatie over aangepaste toegankelijkheidsoplossingen in de Adobe Experience Platform-gebruikersinterface.
source-git-commit: 81db01c3e8d332e1fc8127d779c3a584bb498858
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 0%

---


# Aangepaste toegankelijkheidsoplossingen voor Experience Platform

Adobe Experience Platform wordt voortdurend uitgebreid om aan de behoeften van alle soorten gebruikers te voldoen en voldoet aan de wereldwijde normen die personen met een visuele, auditieve, mobiliteitsfunctie of andere handicap omvatten. In dit document worden aangepaste toegankelijkheidsoplossingen in de gebruikersinterface van het Experience Platform beschreven.

## Overzicht van homepage en gebruikersinterface

De gebruikersinterface van het Experience Platform voldoet aan vereiste contrastverhoudingen voor normale tekst, grafiek, en UI componenten. De kleuren van de gebruikersinterface zijn ook gekozen om toegankelijkheid voor alle gebruikers te ondersteunen, inclusief gebruikers met een visuele handicap.

In Platform, kunnen de elementen UI die met een wijzer klikbaar of actionable zijn ook worden betrokken gebruikend een toetsenbord. Dit omvat de linkernavigatie, videospelers, lijsten, en meer.

Experience Platform streeft ernaar te voldoen aan internationale toegankelijkheidsnormen, waaronder de Web Content Accessibility Guidelines 2.1 Level A en Level AA en de Web Accessibility Initiative - Accessible Rich Internet Applications (WAI-ARIA) webstandaarden.

![De homepage van de gebruikersinterface van Adobe Experience Platform.](images/homepage.png)

## Linkernavigatie

De linkernavigatie binnen de interface van het Experience Platform is toetsenbord-toegankelijk en verstrekt kleurencontrast in normale, aanwijs, en selectiestaten die aan toegankelijkheidsnormen voldoen.

Gebruikers kunnen met de Tab-toets naar links in het scherm Home gaan. Als u **Shift + Tab** selecteert, wordt de gebruiker teruggezet naar het Basisscherm.

![De navigatie links van het Experience Platform.](images/left-navigation-select.png)

Met de linkernavigatie in focus neemt **Tab** gebruikers naar de interactie uit- en samenvouwen. De mogelijkheid om de linkernavigatie uit of samen te vouwen, wordt geactiveerd met **Enter (Return)**.

![De navigatie naar Experience Platform links is samengevouwen.](images/left-navigation-collapse.png)

Met de linkernavigatie in focus, navigeren de pijltoetsen omhoog en omlaag naar elk item in de navigatie en doorlopend (met andere woorden, verschuift de focus niet weg totdat de gebruiker met de Tab-toets van de linkernavigatie af gaat). Wanneer deze optie is geselecteerd, wordt de focus voor navigatie-items weergegeven. De huidige selectie wordt weergegeven met een gemarkeerde en bolle tekst. Wanneer u een navigatiepunt links selecteert, wordt het geselecteerde UI-item in het rechterdeelvenster met **Enter (Return)** geopend, maar blijft de focus in de linkernavigatie totdat de gebruiker de Tab-toets verlaat.

![De Experience Platform linkernavigatie met Geselecteerde Bronnen.](images/left-navigation-sources.png)

Sommige functies in het Platform zijn niet voor alle gebruikers ingeschakeld. Deze items worden in de navigatie weergegeven, maar kunnen niet worden geselecteerd. Wanneer u met een toetsenbord navigeert, worden deze items overgeslagen tijdens de pijlnavigatie en kunnen ze niet worden geselecteerd met **Enter (Return)**.

![Secties van de navigatie links van het Experience Platform die niet voor de gebruiker zijn ingeschakeld, kunnen niet worden geselecteerd.](images/left-navigation-sections-disabled.png)

## Dialoogvenster Ingesloten video

Video&#39;s kunnen binnen het Experience Platform worden weergegeven door toetsenbordnavigatie te gebruiken om een beschikbare videokoppeling te markeren en te selecteren. Hiermee wordt een ingesloten videodialoogvenster geopend in de gebruikersinterface van het Platform.

![Een blauwe rand rondom een geselecteerd element om aan te geven dat focus is toegepast.](images/profile-overview-tab.png)

## Toegankelijkheid van het dialoogvenster Video

U kunt ook via het toetsenbord navigeren in het dialoogvenster Ingesloten video. In de volgende tabel wordt de volledige toetsenbordnavigatie beschreven die beschikbaar is voor het ingesloten videodialoogvenster.

| Dialoogelement | Toegankelijkheid toetsenbord | Beschrijving |
|---|---|---|
| Afspelen en pauzeren | Tab<br/>Spatiebalk | Gebruik **Tab** om focus in te stellen op de afspeelknop. **Het afspelen van** spatiebalken begint met het afspelen van video en wordt gepauzeerd. |
| Scrubber | Tab<br/>Pijl-links<br/>Pijl-rechts | Wanneer de video speelt, gebruik **Tab** om scrubber te concentreren. Met de scrubber in nadruk, **linker en juiste pijlsleutels** overslaan videoplayback voor en achter 5 seconden, respectievelijk. |
| Dempen | Tab<br/>Spatiebalk | Gebruik **Tab** om het dempvolume-element te activeren. Gebruik **spatiebalk** om het afspelen van video te dempen of te dempen. |
| Volume | Tab<br/>Pijl-links<br/>Pijl-rechts | Gebruik **Tab** om te focussen op het element volume. **Met pijl-links en pijl-rechts** verplaatst u respectievelijk het volume omhoog en omlaag. |
| [!UICONTROL Closed Captions] (&quot;cc&quot;) | Tab<br/>Enter<br/>Up arrow<br/>Down arrow | **** Tabto  [!UICONTROL Closed Captions] (&quot;cc&quot;)-element. Gebruik **Enter** om het menu te openen, en **pijl-omhoog en -omlaag** om een taal voor bijschriften te selecteren. **Uw** keuze wordt bevestigd. |
| [!UICONTROL Quality] | Tab<br/>Enter<br/>Up arrow<br/>Down arrow | Gebruik **Tab** om het [!UICONTROL Quality]-element scherpstellen. Gebruik **Enter** om het menu en **pijl-omhoog en -omlaag te openen** om de videokwaliteit te selecteren. **Uw** keuze wordt bevestigd. |
| Volledig scherm | Tab<br/>Spatiebalk of Enter<br/>Escape | Gebruik **Tab** om het element Volledig scherm te activeren. Gebruik **spatiebalk of Enter** om de weergave Volledig scherm te activeren. **Escape**  (&quot;esc&quot;) sluit de modus Volledig scherm af. |
| Sluiten | Tab<br/>Spatiebalk of Enter | Gebruik **Tab** om de knop Sluiten actief te maken. Gebruik **spatiebalk of Enter** om het videodialoogvenster te sluiten. |

>[!NOTE]
>
>Op elk gewenst moment tijdens het afspelen kan de escape-toets (&quot;esc&quot;) worden gebruikt om het ingesloten videodialoogvenster te sluiten.

![Het ingesloten videodialoogvenster met nummers die navigatie-elementen op het toetsenbord identificeren.](images/video-dialog.png)

## Bestanden slepen en neerzetten

In Experience Platform zijn alle zones waar bestanden worden geselecteerd en waar ze worden gesleept, toegankelijk voor het toetsenbord. Als u **Tab** gebruikt om **[!UICONTROL Choose files]** te markeren en **Enter of spacebar** gebruikt om deze te selecteren, wordt de interface voor bestandsselectie van het besturingssysteem geactiveerd.

Nadat een bestand is geüpload, kunt u met het toetsenbord navigeren door een verwijderpictogram om het geselecteerde bestand te verwijderen en een nieuw bestand te uploaden. Gebruikers kunnen **Tab** gebruiken om het verwijderpictogram te activeren en **Enter of spacebar** om het te selecteren. Wanneer het bestand is verwijderd, wordt **[!UICONTROL Choose files]** automatisch scherpgesteld en kan het worden geselecteerd.

Als het geüploade bestand niet de juiste indeling heeft, wordt een foutpictogram weergegeven met een foutbericht en is de knop **[!UICONTROL Choose files]** scherp en selecteerbaar.

![Een gebied voor het slepen en neerzetten van een bestand met een foutbericht en de knop Bestanden kiezen in focus.](images/drag-and-drop.png)

Als u een muis gebruikt om de zone voor slepen en neerzetten te selecteren, wordt ook de gebruikersinterface voor de bestandsselectie aangeroepen, of een muisgebruiker kan een bestand selecteren en naar de zone slepen om te beginnen met uploaden.

![Een gebied van het dossier belemmering-en-daling in nadruk aangezien een muisgebruiker een dossier in de streek sleept.](images/drag-and-drop-mouse-over.png)

## Tabel bladeren

Alle tabellen in de gebruikersinterface van het Experience Platform zijn toegankelijk via het toetsenbord. U kunt met een aantal sneltoetsen bladeren door tabelrijen en -kolommen en er met deze rijen en kolommen mee werken:

* Van de lijstkopbal, gebruik **benedenpijl** om de lijst te doorbladeren. De kopballen van de lijst zijn selecteerbaar wanneer het navigeren via **Tab**, en u kunt de sorteerorde veranderen gebruikend **spacebar**.
* **Met de pijltoetsen omhoog en omlaag** gaat u omhoog en omlaag door de rijen in de tabel.
* Wanneer een rij wordt geselecteerd of in nadruk, gebruikend **Enter** op de rij details in het juiste spoor verstrekt.
* Als een rij is geselecteerd of de focus heeft, gebruikt u **pijltoetsen** om door elk item in de rij te gaan.
* Gebruik **Enter** om een item in de rij te selecteren. Gebruikers met schermlezers worden gewaarschuwd als een nieuw venster moet worden geopend.

### Toegankelijkheid van tabeltoetsenbord doorbladeren

| Toegankelijkheid toetsenbord | Beschrijving |
|---|---|
| HOME (Function + pijl-links) | Wanneer de rij geconcentreerd is, neemt gebruikers naar het eerste punt in de rij |
| END (Function + pijl-rechts) | Wanneer de rij geconcentreerd is, neemt gebruikers aan het laatste punt in de rij |
| Pagina omhoog | Hiermee verplaatst u 10 rijen omhoog in de tabel (per pagina) |
| Page down | Hiermee verplaatst u 10 rijen omlaag in de tabel (per pagina) |
| Control + HOME | Hiermee gaat u naar de eerste rij in de tabel |
| Control + END | Goes to first win table per page |

## Gebruikersinterface van Schema-editor

De UI van de Redacteur van het Schema wordt toegankelijk gemaakt door de volgende functionaliteit:

* De Schema-editor ondersteunt toetsenbordnavigatie, inclusief het gebruik van **Tab** voor navigatie door UI-elementen.
* **De** lusjes het onderzoeksgebied, dan in de schemaboom.
* De boomstructuur van het schema steunt het gebruik van pijlsleutels om door schema boom UI te navigeren
   * **Met pijl-omhoog en** pijl-omlaag doorloopt u de structuur.
   * **Linker- en** rechterpijl kunnen worden gebruikt om knooppunten uit of samen te vouwen of om te schakelen tussen inline-handelingen in de schemastructuur.
* **Enter (Return)** activeert de afzonderlijke knooppuntdetails in het detailpaneel rechts.
* De **Home** sleutel keert aan de bovenkant van de boom terug.
* De **End** sleutel navigeert aan de bodem van de boom.
* De schemastructuur bevat ook ARIA-labels voor schermlezers.

## Gebruikersinterface van Segment Builder

Wanneer het gebruiken van de Bouwer van het Segment UI om, met segmenten binnen Experience Platform tot stand te brengen uit te geven en in wisselwerking te staan, verbeteren de volgende eigenschappen toegankelijkheid:

* De gebruikersinterface van Segment Builder is toegankelijk via toetsenbordnavigatie.
* Schermlezers herkennen markeringen voor opmaakcodes voor koppen en kunnen de kop samen met het niveau ervan aankondigen.
* Andere ondersteunende hulpmiddelen kunnen de visuele weergave van een pagina wijzigen door correct gecodeerde koppen te gebruiken om een omtrek of een alternatieve weergave weer te geven.

## Query Service-editor

De volgende toegankelijkheidsfuncties zijn beschikbaar in de Query Service-editor:

* Het kleurcontrast in de gebruikersinterface van de Query Service voldoet aan toegankelijkheidsvereisten.
* Toetsenbordnavigatie wordt ondersteund buiten de gebruikersinterface van de editor. De editor-gebruikersinterface is een ingesloten codespiegel.

## Het lusje van de Mening van het systeem in Bronnen en Doelen

Wanneer het doorbladeren van **[!UICONTROL System View]** in Bronnen en Doelen, verbetert de volgende functionaliteit toegankelijkheid:

* **De** tabsets richten zich op de eerste bronverbindingskaart
   * **Tik nogmaals** op de knop in de kaart
   * Selecteer **Enter** om de vraag aan actieknoop binnen de kaart te activeren
* Als u **Enter** op de verbindingskaart selecteert, worden ook meer details geactiveerd in de rechtertrack
   * Wanneer de rechterspoorstaaf wordt geactiveerd, wordt de focus op dat gebied ingesteld. **** Tabs is gericht op  **** Closefor the right rail pane. Als u **Tab** nogmaals selecteert, wordt de focus weer door het deelvenster Rechterrails verplaatst
   * Als er meer dan één bronverbindingskaart is, **Tab** beweegt zich door de verbindingen
   * Gebruik **pijltoetsen (omhoog, omlaag, links en rechts)** om door de lijst met bronnen te gaan
   * Selecteer **Tab** om de focus in te stellen op het deelvenster Rechterrails