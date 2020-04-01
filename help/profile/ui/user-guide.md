---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Gebruikershandleiding voor het profiel van de klant in realtime
topic: guide
translation-type: tm+mt
source-git-commit: b5412b891a9457fa5e801d1f0479fc59fb08bf1b

---


# Gebruikershandleiding voor het profiel van de klant in realtime

Het profiel van de Klant in real time leidt tot een holistische mening van elk van uw individuele klanten, die gegevens van veelvoudige kanalen met inbegrip van online, off-line, CRM, en derdegegevens combineren.

Dit document fungeert als richtlijn voor interactie met Real-time klantprofiel in de gebruikersinterface van het Adobe Experience Platform.

## Aan de slag

Deze gebruikershandleiding vereist inzicht in de verschillende services van het Experience Platform die betrokken zijn bij het beheren van het realtime-klantprofiel. Lees de documentatie voor de volgende services voordat u deze gebruikershandleiding leest:

* [Klantprofiel](../home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Identiteitsservice](../../identity-service/home.md): Laat het Profiel van de Klant in real time toe door identiteiten van ongelijke gegevensbronnen te overbruggen die in Platform worden opgenomen.
* [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.

## Profieloverzicht

Klik in de gebruikersinterface [van het](http://platform.adobe.com)ervaringsplatform op **Profielen** in de linkernavigatie om het tabblad _Overzicht_ te openen in de werkruimte _Profielen_ . Dit lusje toont verscheidene widgets die informatie op hoog niveau over de opslag van het Profiel, met inbegrip van het totale adresseerbare publiek, het aantal verslagen van het Profiel verstrekken die binnen de vorige week werden ingebed, evenals statistieken betreffende succesvolle en ontbroken verslagen voor de zelfde tijdspanne.

![](../images/user-guide/profile-overview.png)

## Profielvoorbeelden weergeven

Klik op **Bladeren** om een voorbeeldlijst met beschikbare profielen weer te geven. Dit voorbeeld bevat maximaal 50 profielen van het totale aantal [profielen](#profile-count). De voorbeelden worden vernieuwd door een automatische taak waarmee nieuwe profielgegevens worden opgehaald terwijl deze worden ingevoerd. In elk weergegeven profiel worden de id, voornaam, achternaam en persoonlijke e-mail weergegeven. Als u op de id van een weergegeven profiel klikt, worden de details van het profiel weergegeven in de [profielviewer](#profile-viewer).

![](../images/user-guide/profile-samples.png)

U kunt de kenmerken die in de lijst worden weergegeven, aanpassen door op het pictogram voor de kolomkiezer te klikken. Hiermee wordt een vervolgkeuzelijst weergegeven met veelvoorkomende profielkenmerken die u kunt toevoegen of verwijderen.

![](../images/user-guide/column-selector.png)

### Aantal profielen {#profile-count}

Het aantal profielen geeft het totale aantal profielen weer dat uw organisatie heeft binnen het Experience Platform, nadat het standaard samenvoegbeleid van uw organisatie profielfragmenten heeft samengevoegd tot één profiel voor elke afzonderlijke klant. Met andere woorden, uw organisatie kan veelvoudige profielfragmenten met betrekking tot één enkele klant hebben die met uw merk over verschillende kanalen interactie heeft, maar deze fragmenten zouden samen (volgens het standaard fusiebeleid) worden samengevoegd en een telling van &quot;1&quot;profiel terugkeren omdat zij allen met het zelfde individu verwant zijn.

Het aantal profielen omvat ook zowel profielen met kenmerken (recordgegevens) als profielen (zoals Adobe Analytics-profielen) die alleen tijdreeksgegevens (gebeurtenisgegevens) bevatten. De telling wordt regelmatig vernieuwd om een bijgewerkt totaal aantal profielen binnen Platform te verstrekken. Telkens wanneer een opname van profielen de telling met meer dan 5% verhoogt of vermindert, wordt een baan automatisch teweeggebracht om de telling bij te werken. Als uw organisatie streamingopname gebruikt, worden taken elk uur gepland om nieuwe gegevens op te halen.

![](../images/user-guide/profile-count.png)

### Profielzoekopdracht

Als u een gekoppelde identiteit kent voor een bepaald profiel (zoals het e-mailadres), kunt u dat profiel opzoeken door op Een profiel **** zoeken te klikken. Dit is de meest betrouwbare manier om toegang te krijgen tot een specifiek profiel, ongeacht of het wordt weergegeven in de lijst met voorbeelden.

![](../images/user-guide/find-a-profile.png)

Selecteer in het dialoogvenster dat wordt weergegeven een geschikte naamruimte voor de id in de vervolgkeuzelijst (&quot;E-mail&quot; in dit voorbeeld) en voer hieronder de waarde voor de id in voordat u op **OK** klikt. Indien gevonden, worden de details van het doelprofiel weergegeven in de profielviewer, zoals beschreven in de volgende sectie.

![](../images/user-guide/find-a-profile-details.png)

### Profielviewer {#profile-viewer}

Als u een specifiek profiel selecteert of zoekt, wordt het scherm _Details_ van de profielviewer geopend. Deze pagina bevat informatie over het geselecteerde profiel, zoals de basiskenmerken van het profiel, gekoppelde identiteiten en beschikbare contactkanalen. De weergegeven profielgegevens zijn samengevoegd vanuit meerdere profielfragmenten en vormen één weergave van de individuele klant.

![](../images/user-guide/profile-viewer-detail.png)

De profielviewer biedt ook tabbladen waarmee u gebeurtenissen en segmentlidmaatschappen kunt weergeven die aan dit profiel zijn gekoppeld, indien aanwezig.

![](../images/user-guide/profile-viewer-events-seg.png)

## Beleid samenvoegen

Klik op **Beleid** samenvoegen om een lijst weer te geven met samenvoegbeleid dat tot uw organisatie behoort. Elk vermeld beleid toont zijn naam, al dan niet het standaardsamenvoegbeleid, en het schema dat het op van toepassing is.

![](../images/user-guide/profile-merge-policies.png)

Voor meer informatie bij het werken met fusiebeleid in UI, zie de de gebruikersgids [van het Beleid van de](merge-policies.md)Fusie.

## Unieschema

Klik op **Unieschema** om de samenvoegingsschema&#39;s voor de opslag van uw profielgegevens weer te geven. Een verenigingsschema is een samenvoeging van alle gebieden van het Model van de Gegevens van de Ervaring (XDM) onder de zelfde klasse, de waarvan schema&#39;s voor gebruik in het Profiel van de Klant in real time zijn toegelaten. Klik op een klasse in de lijst links om de structuur van het samenvoegingsschema op het canvas weer te geven.

![](../images/user-guide/profile-union-schema.png)

Zie de sectie over verenigingsschema&#39;s in de [schemacompositie gids](../../xdm/schema/composition.md) voor meer informatie over verenigingsschema&#39;s en hun rol in het Profiel van de Klant in real time.

## Volgende stappen

Door deze handleiding te lezen, weet u nu hoe u de profielgegevens kunt bekijken en beheren met de interface van het Experience Platform. Voor informatie over hoe te hefboomwerking de gegevens van het Profiel van de Klant in real time om publiekssegmenten te produceren, zie de documentatie [van de](../../segmentation/home.md)Segmentatie.