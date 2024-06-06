---
title: Edge Delivery View
description: Deze handleiding bevat informatie over de Edge Delivery-weergave in Adobe Experience Platform Assurance.
source-git-commit: d6b5894a5c5ba3907a8e6dd0d1864f773dd6325c
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---

# Edge Delivery View in Assurance

De **[!UICONTROL Edge Delivery]** weergave in **[!UICONTROL Adobe Experience Platform Assurance]** biedt de mogelijkheid om te inspecteren en te valideren [!UICONTROL AJO Inbound] Edge-levering van berichten aan uw web- en mobiele apps. Deze mening is vooral nuttig voor het oplossen van problemen de levering van [!UICONTROL AJO Inbound] internet- en mobiele campagnes en reizen.

## Aan de slag

Controleer voordat u doorgaat of u toegang hebt tot de volgende services:

- De [UI voor gegevensverzameling van Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Meer informatie over installeren **[!UICONTROL Assurance]** in uw toepassing te lezen [Implementatie van de betrouwbaarheidsgids](../tutorials/implement-assurance.md).

## Betrouwbaarheid met Edge-levering gebruiken

Wanneer u een **[!UICONTROL Assurance]** sessie kunt u de **[!UICONTROL Edge Delivery]** weergeven **[!UICONTROL Assurance]**. Selecteer onder aan het linkerdeelvenster de optie **[!UICONTROL Configure]** om de **[!UICONTROL Edge Delivery]** en **Opslaan** het.

![Voeg de plug-in toe door Configure linksonder te selecteren](./images/edge-delivery/add-plugin.png)

Selecteer de optie **[!UICONTROL Edge Delivery]** in de **[!UICONTROL Adobe Journey Optimizer]** te valideren.

![De levering van de rand kan in de de meningsgroep van Adobe Journey Optimizer worden betreden](./images/edge-delivery/ajo-plugins.png)

## Aanvraaglijst

In het hoofdvenster van de weergave wordt de lijst met aanvragen voor randlevering weergegeven. In deze lijst worden alle [!UICONTROL Inbound AJO] verzoeken aan Experience Edge die door de **[!UICONTROL Inbound Delivery Service]**, met inbegrip van verzoeken om verpersoonlijkingsbesluiten terug te winnen, evenals de interacties van het spoorverpersoonlijkingsvoorstel (zoals vertoning, klik, trekker, of ontslag).

Verzoeken worden geordend met een tijdstempel, met de meest recente aanvragen bovenaan. Naast de tijdstempel bevat de lijst ook een kolom met de aanvraag-id en een kolom met het type aanvraag. Dit kan een van de volgende zijn:

- **[!UICONTROL Experience Delivery]**: Een verzoek om personalisatiebeslissingen op te halen
- **[!UICONTROL Experience Interactions]**: Een verzoek om interacties voor personalisatievoorstellen bij te houden
- **[!UICONTROL Experience Delivery & Interactions]**: Een verzoek om verpersoonlijkingsbesluiten terug te winnen, met inbegrip van verpersoonlijkingspropositieinteractie
- **[!UICONTROL Preview Delivery]**: Een verzoek om de beslissingen voor het aanpassen van voorvertoningen op te halen

Verzoeken kunnen ook worden gefilterd door een zoekterm in te voeren in de zoekbalk boven aan de lijst. Dit is nuttig wanneer het filtreren door specifieke waarden, zoals IDs.

![De lijst van Binnenkomende verzoeken wordt getoond in de belangrijkste mening](./images/edge-delivery/request-list.png)

## Gedetailleerde aanvraagweergaven

Zodra een verzoek in de belangrijkste mening wordt geselecteerd, wordt gedetailleerde informatie over het geselecteerde verzoek getoond op het recht. Deze weergave bevat de volgende secties:

### Overzicht aanvragen

In deze sectie vindt u een overzicht op hoog niveau van de geselecteerde aanvraag, inclusief [!UICONTROL Organization ID], [!UICONTROL Edge cluster], [!UICONTROL Request ID] en [!UICONTROL Request type], [!UICONTROL Sandbox ID], [!UICONTROL Sandbox name], [!UICONTROL Datastream ID], alsmede de lijst van aanvraagoppervlakken in geval van [!UICONTROL Experience Delivery] verzoeken.

![De overzichtssectie van het verzoek verstrekt high-level verzoekdetails](./images/edge-delivery/request-overview.png)

### Profiel

Deze sectie biedt informatie over de profielgegevens die worden gebruikt tijdens de verwerking van de aanvraag, zoals de identiteitskaart, het lidmaatschap van een segment en de instellingen voor toestemming.\
De [!UICONTROL Profile] Deze sectie is zeer nuttig wanneer het oplossen van problemenkwesties zoals levering niet werkt zoals verwacht wegens ontbrekend of vertraagd segmentlidmaatschap of opt-out toestemmingsmontages.

![De sectie Profiel bevat het identiteitsoverzicht, segmentlidmaatschap en toestemmingsinstellingen](./images/edge-delivery/profile.png)

### Gekwalificeerde activiteiten

Deze sectie verstrekt een lijst van activiteiten die voor het geselecteerde verzoek, met inbegrip van het activiteitstype, IDs, identiteitsnamespace, oppervlakten, programma, en publiek werden gekwalificeerd. Meer gedetailleerde informatie over de activiteit vindt u in de [RAW-sectie over tracering](#execution).

![Sectie Gekwalificeerde activiteiten bevat de details van gekwalificeerde activiteiten](./images/edge-delivery/qualified-activities.png)

### Ongekwalificeerde activiteiten

Deze sectie bevat een lijst met activiteiten die zijn uitgesloten van kwalificatie. Naast het type activiteit, IDs, identiteitsnamespaces, oppervlakten, programma&#39;s, en publiek, omvat deze sectie ook een lijst van redenen de activiteit niet gekwalificeerd was.

![De sectie Niet-gekwalificeerde activiteiten bevat niet-gekwalificeerde activiteitdetails en uitsluitingsredenen](./images/edge-delivery/unqualified-activities.png)

### Berichtdetails

Deze sectie verstrekt gedetailleerde informatie over de berichten die voor het geselecteerde verzoek werden geleverd. Het omvat bericht IDs, fragmenten, besluitvormingsbeleid, [!UICONTROL Offer Decisioning] en de context van de berichtselectie.

![Sectie met geleverde berichtdetails zoals bericht-id&#39;s en selectiecontext, fragmenten, besluitvormingsbeleid en beslissingsparameters](./images/edge-delivery/message-details.png)

### Interacties

Deze sectie bevat gedetailleerde informatie over de interacties die in de geselecteerde aanvraag zijn bijgehouden. Het omvat het interactietype (onder `propositionEventType`), alsmede de bijbehorende metagegevens over de positie, zoals metagegevens over de activiteit (onder `scopeDetails.activity`) en propositiegebeurtenistoken (in `scopeDetails.characteristics.eventToken`).

![Interacties worden bijgehouden via propositietokens en bijbehorende metagegevens over activiteiten](./images/edge-delivery/interactions.png)

### Onbewerkte sporen

In deze sectie ziet u de onbewerkte sporen van de geselecteerde aanvraag. Het omvat de volledige samenvatting van het verzoek, met inbegrip van het eigenlijke verzoek zoals het in **[!UICONTROL Inbound Delivery Service]**, uitvoeringsspoor en reactiespoor. Dit is nuttig voor geavanceerde probleemoplossing, zoals levering die niet werkt zoals u had verwacht als gevolg van de onbeschikbaarheid van de leveringsservice, ontbrekende of onjuiste gegevens, of voor een beter begrip van de volledige stroom van de aanvraagverwerking.

#### Verzoek

Het aanvraagspoor omvat het volledige verzoek zoals het door de **[!UICONTROL Inbound Delivery Service]** **[!UICONTROL Konductor]** upstream. Het omvat de verzoekkopballen, het lichaam, en andere meta-gegevens. Bijvoorbeeld, kan de nuttige lading XDM van het verzoek in worden geïnspecteerd `event.body.xdm` veld.

![De gedetailleerde verzoekinformatie met inbegrip van kopballen en lichaam kan in het verzoekspoor worden gevonden](./images/edge-delivery/request.png)

#### Uitvoering

Het uitvoerspoor omvat het volledige spoor van het verzoek aangezien het door **[!UICONTROL Inbound Delivery Service]**. Het toont de uitvoeringscontext, activiteitenkwalificatie, berichtselectie, en andere verwerkingsstappen. Alle fouten of waarschuwingen die tijdens de verwerking van de aanvraag zijn opgetreden, kunt u vinden in `context.messages` en `context.exceptions` velden. Gedetailleerde informatie over activiteitskwalificatie vindt u in het gedeelte `context.qualifiedActivitiesDetailed` en `context.unqualifiedActivitiesDetailed` velden.

![Het spoor van de uitvoering omvat uitvoeringscontext, activiteitenkwalificatie, berichtselectie, en andere verwerkingsdetails](./images/edge-delivery/execution.png)

#### Antwoord

Het reactiespoor omvat de volledige reactie aangezien het door is teruggekeerd **[!UICONTROL Inbound Delivery Service]** stroomafwaarts tot **[!UICONTROL Konductor]**. Dit omvat de responsheaders, de hoofdtekst en andere metagegevens. De volledige reactieinstantie kan worden geïnspecteerd door het bericht met identiteitskaart te kopiëren `1` naar het klembord met de **[!UICONTROL Copy Value]** en plakken in een JSON-viewer.

![Respontrace bevat de volledige responsstructuur die stroomafwaarts is geretourneerd](./images/edge-delivery/response.png)
