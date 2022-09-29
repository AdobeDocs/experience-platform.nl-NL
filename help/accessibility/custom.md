---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd;profiel;rtcp;XDM-grafieken
title: Aangepaste toegankelijkheidsoplossingen voor Experience Platform
topic-legacy: guide
type: Documentation
description: Meer informatie over aangepaste toegankelijkheidsoplossingen in de Adobe Experience Platform-gebruikersinterface.
exl-id: cb5ad99e-8a95-4c9e-aae6-1d0036ecf052
source-git-commit: 7f4202c9c4a132ed9d74c495f6608357eac8003f
workflow-type: tm+mt
source-wordcount: '1601'
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

Gebruikers kunnen met de Tab-toets naar links in het scherm Home gaan. Selecteren **Shift + Tab** retourneert de gebruiker naar het Basisscherm.

![De navigatie links van het Experience Platform.](images/left-navigation-select.png)

Met de linkernavigatie in focus, **Tab** Hiermee kunnen gebruikers de interactie uitvouwen en samenvouwen. De mogelijkheid om de linkernavigatie uit te vouwen of samen te vouwen wordt geactiveerd met **Enter (Return)**.

![De navigatie naar Experience Platform links is samengevouwen.](images/left-navigation-collapse.png)

Met de linkernavigatie in focus, navigeren de pijltoetsen omhoog en omlaag naar elk item in de navigatie en doorlopend (met andere woorden, verschuift de focus niet weg totdat de gebruiker met de Tab-toets van de linkernavigatie af gaat). Wanneer deze optie is geselecteerd, wordt de focus voor navigatie-items weergegeven. De huidige selectie wordt weergegeven met een gemarkeerde en bolle tekst. Bij het selecteren van een navigatiepunt links, **Enter (Return)** Hiermee wordt het geselecteerde UI-item in het rechterdeelvenster geopend, maar de focus blijft in de linkernavigatie totdat de gebruiker de Tab-toets verlaat.

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
| Afspelen en pauzeren | Tab<br/>Spatiebalk | Gebruiken **Tab** om de focus op de afspeelknop in te stellen. **Spatiebalk** Het afspelen van video wordt gestart en het afspelen van video wordt gepauzeerd. |
| Scrubber | Tab<br/>Pijl-links<br/>Pijl-rechts | Gebruik **Tab** focusscrubber. Met de scrubber in focus, **pijl-links en pijl-rechts** De videoweergave wordt respectievelijk 5 seconden voor en achter overgeslagen. |
| Dempen | Tab<br/>Spatiebalk | Gebruiken **Tab** om het dempingsvolume-element actief te maken. Gebruiken **spatiebalk** om het afspelen van video te dempen of te dempen. |
| Volume | Tab<br/>Pijl-links<br/>Pijl-rechts | Gebruiken **Tab** om de nadruk te leggen op het element volume. **Pijl-links en Pijl-rechts** volume respectievelijk omhoog en omlaag verplaatsen. |
| [!UICONTROL Closed Captions] (&quot;cc&quot;) | Tab<br/>Enter<br/>Pijl-omhoog<br/>Pijl-omlaag | **Tab** tot [!UICONTROL Closed Captions] (&quot;cc&quot;) element. Gebruiken **Enter** om het menu te openen, en **pijl-omhoog en pijl-omlaag** om een taal voor bijschriften te selecteren. **Enter** bevestigt uw selectie. |
| [!UICONTROL Quality] | Tab<br/>Enter<br/>Pijl-omhoog<br/>Pijl-omlaag | Gebruiken **Tab** om de focus op [!UICONTROL Quality] element. Gebruiken **Enter** om het menu en de **pijl-omhoog en pijl-omlaag** om de videokwaliteit te selecteren. **Enter** bevestigt uw selectie. |
| Volledig scherm | Tab<br/>Spatiebalk of Enter<br/>Escape | Gebruiken **Tab** om het element Volledig scherm te activeren. Gebruiken **spatiebalk of Enter** om de weergave Volledig scherm te activeren. **Escape** (&quot;esc&quot;) sluit de modus Volledig scherm af. |
| Sluiten | Tab<br/>Spatiebalk of Enter | Gebruiken **Tab** om de knop Sluiten actief te maken. Gebruiken **spatiebalk of Enter** om het videodialoogvenster af te sluiten. |

>[!NOTE]
>
>Op elk gewenst moment tijdens het afspelen kan de escape-toets (&quot;esc&quot;) worden gebruikt om het ingesloten videodialoogvenster te sluiten.

![Het ingesloten videodialoogvenster met nummers die navigatie-elementen op het toetsenbord identificeren.](images/video-dialog.png)

## Bestanden slepen en neerzetten

In Experience Platform zijn alle zones waar bestanden worden geselecteerd en waar ze worden gesleept, toegankelijk voor het toetsenbord. Gebruiken **Tab** om te markeren **[!UICONTROL Choose files]** en gebruiken **Enter of spatiebalk** om deze te selecteren, wordt de interface voor bestandsselectie van het besturingssysteem aangeroepen.

Nadat een bestand is geüpload, kunt u met het toetsenbord navigeren door een verwijderpictogram om het geselecteerde bestand te verwijderen en een nieuw bestand te uploaden. Gebruikers kunnen **Tab** focussen op het verwijderpictogram en **Enter of spatiebalk** om het te selecteren. Nadat het bestand is verwijderd, **[!UICONTROL Choose files]** wordt automatisch scherpgesteld en kan worden geselecteerd.

Als het geüploade bestand niet de juiste indeling heeft, wordt een foutpictogram weergegeven met een foutbericht en de **[!UICONTROL Choose files]** focus en selecteerbaar.

![Een gebied voor het slepen en neerzetten van een bestand met een foutbericht en de knop Bestanden kiezen in focus.](images/drag-and-drop.png)

Als u een muis gebruikt om de zone voor slepen en neerzetten te selecteren, wordt ook de gebruikersinterface voor de bestandsselectie aangeroepen, of een muisgebruiker kan een bestand selecteren en naar de zone slepen om te beginnen met uploaden.

![Een gebied van het dossier belemmering-en-daling in nadruk aangezien een muisgebruiker een dossier in de streek sleept.](images/drag-and-drop-mouse-over.png)

## Tabel bladeren

Alle tabellen in de gebruikersinterface van het Experience Platform zijn toegankelijk via het toetsenbord. U kunt met een aantal sneltoetsen bladeren door tabelrijen en -kolommen en er met deze rijen en kolommen mee werken:

* In de tabelkoptekst kunt u de opdracht **pijl-omlaag** om door de tabel te bladeren. De kopballen van de lijst zijn selecteerbaar wanneer het navigeren via **Tab** en u kunt de sorteervolgorde wijzigen met **spatiebalk**.
* **Pijltoetsen omhoog en omlaag** Hiermee gaat u omhoog en omlaag door de rijen in de tabel.
* Wanneer een rij is geselecteerd of de focus heeft, gebruikt u **Enter** op de rij staan details in het rechterspoor.
* Wanneer een rij is geselecteerd of de focus heeft, gebruikt u **pijltoetsen** om door elk punt in de rij te bewegen.
* Gebruiken **Enter** om een item in de rij te selecteren. Gebruikers met schermlezers worden gewaarschuwd als een nieuw venster moet worden geopend.
* Wanneer u tot 200% of meer zoomt, kunt u de **spoorwegcontrole** pictogram als de juiste spoorstaaf samenvouwt om meer het bekijken ruimte voor de lijst te verstrekken.

![Het pictogram van de spoorinspecteur in nadruk wanneer een gebruiker aan 200% zoomt.](images/rail-inspector.png)

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

* De Schema-editor ondersteunt toetsenbordnavigatie, inclusief het gebruik van **Tab** naar navigatie door UI-elementen.
* **Tab** gaat het onderzoeksgebied, dan in de schemaboom in.
* De boomstructuur van het schema steunt het gebruik van pijlsleutels om door schema boom UI te navigeren
   * **Pijlen omhoog en omlaag** kan worden gebruikt om de boom te doorlopen.
   * **Pijlen links en rechts** U kunt knooppunten uitvouwen en samenvouwen of schakelen tussen inline-handelingen in de schemastructuur.
* **Enter (Return)** activeert individuele knoopdetails in het detailpaneel op het recht.
* De **Home** -toets keert terug naar de bovenkant van de boom.
* De **Einde** Hiermee navigeert u naar de onderkant van de structuur.
* De schemastructuur bevat ook ARIA-labels voor schermlezers.

## Gebruikersinterface van Segment Builder

Wanneer het gebruiken van de Bouwer van het Segment UI om, met segmenten binnen Experience Platform tot stand te brengen uit te geven en in wisselwerking te staan, verbeteren de volgende eigenschappen toegankelijkheid:

* De gebruikersinterface van Segment Builder is toegankelijk via toetsenbordnavigatie.
* Schermlezers herkennen markeringen voor opmaakcodes voor koppen en kunnen de kop samen met het niveau ervan aankondigen.
* Andere ondersteunende hulpmiddelen kunnen de visuele weergave van een pagina wijzigen door correct gecodeerde koppen te gebruiken om een omtrek of een alternatieve weergave weer te geven.

U kunt nu de linker- en rechterrails van het gesegmenteerde canvas samenvouwen of uitvouwen om meer schermruimte te verkrijgen. Deze functie is vooral handig omdat deze bij 200% zoomen volledige functionaliteit biedt.

![Het segmentbuildercanvas met de openingswidgets voor linker- en rechterspoor gemarkeerd.](images/left-right-rail-expandables.png)

## Query Service-editor

De volgende toegankelijkheidsfuncties zijn beschikbaar in de Query Service-editor:

* Het kleurcontrast in de gebruikersinterface van de Query Service voldoet aan toegankelijkheidsvereisten.
* Toetsenbordnavigatie wordt ondersteund buiten de gebruikersinterface van de editor. De editor-gebruikersinterface is een ingesloten codespiegel.

## Het lusje van de Mening van het systeem in Bronnen en Doelen

Wanneer u door de **[!UICONTROL System View]** in Bronnen en doelen verbetert de volgende functionaliteit de toegankelijkheid:

* **Tab** Hiermee wordt de focus op de eerste bronverbindingskaart ingesteld
   * **Tab** opnieuw om zich op de knoop binnen de kaart te concentreren
   * Selecteren **Enter** om de vraag aan actieknoop binnen de kaart te activeren
* Selecteren **Enter** op de aansluitkaart worden ook meer details in het rechterspoor aangehaald
   * Wanneer de rechterspoorstaaf wordt geactiveerd, wordt de focus op dat gebied ingesteld. **Tab** is gericht op **Sluiten** voor de rechterspoorruit. Selecteren **Tab** weer de focus door het rechterdeelvenster van het spoor
   * Als er meer dan één bronverbindingskaart is, **Tab** doorloopt de verbindingen
   * Gebruiken **pijltoetsen (omhoog, omlaag, links en rechts)** om door de lijst van bronnen te bewegen
   * Selecteren **Tab** om de focus op het rechterdeelvenster van het spoor in te stellen
