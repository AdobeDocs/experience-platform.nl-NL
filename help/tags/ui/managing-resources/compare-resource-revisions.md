---
title: Bronrevisies vergelijken
description: Leer hoe u de geschiedenis van revisies voor een tagbron in Adobe Experience Platform kunt bekijken.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Bronrevisies vergelijken

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Vergelijk resourcerevisies om de geschiedenis van een individuele bron te zien.  U kunt de huidige status van de bron vergelijken met oudere versies of de momenteel gepubliceerde versie van een bron vergelijken met de meest recente set wijzigingen die zijn opgeslagen.

## Een vergelijking starten

Het initiëren van een vergelijking is het zelfde voor alle middeltypes.  Open de Edit mening voor een individuele middel, dan vind het drie puntenpictogram naast **[!UICONTROL Save]** knoop om beschikbare acties voor die middel te bekijken.  Selecteer **[!UICONTROL Compare Revisions]** in de lijst.

![Een vergelijking voor een extensie starten](../../images/compare-initiate-extension.png)

Voor extensies opent u de detailweergave door de knop **[!UICONTROL Configure]** te selecteren wanneer u de lijst met geïnstalleerde extensies weergeeft.  Selecteer een gegevenselement in de lijst voor gegevenselementen en -regels.

## De vergelijkingsweergave gebruiken

Wanneer u een vergelijking initieert, toont de standaardmening de recentste versie op het recht.  Deze versie bevat alle niet-opgeslagen wijzigingen die u in de bron hebt aangebracht in de weergave Bewerken. (Let op het label Niet-opgeslagen wijzigingen rechts in de onderstaande afbeelding.)

Links kun je kiezen uit bestaande revisies die je wilt vergelijken met &#39;Nieuwst&#39;.

![Versies van de extensie Analytics vergelijken](../../images/compare-interpret-extension.png)

Selecteer **[!UICONTROL Use These Changes]** om de instellingen van de geselecteerde revisie (links) naar de meest recente versie te kopiëren (rechts).  Hiermee kopieert u de instellingen van de oude revisie naar de laatste niet-opgeslagen wijzigingen.  Als u wilt dat deze wijzigingen behouden blijven, moet u **[!UICONTROL Save]** nadat u de vergelijkingsweergave hebt afgesloten.

>[!TIP]
>Individuele bronnen kunnen zowel kenmerken als instellingen hebben.  Deze instellingen worden opgeslagen als een JSON-blok. Dit is een gestructureerde manier om gegevens op te slaan, maar flexibel genoeg om extensieontwikkelaars in staat te stellen hun extensies naar wens uit te voeren.
>In de eerste versie van de vergelijkingsweergave worden de instellingen in onbewerkte vorm weergegeven als JSON. Dankzij toekomstige verbeteringen kunt u versies op verschillende manieren weergeven, inclusief gedetailleerde codevergelijkingen en het gebruik van de extensieweergaven die door de ontwikkelaars van de extensies worden geboden.

## Extensies vergelijken

Extensies hebben één scherm om de verschillen tussen versies weer te geven.

In de vergelijkingsweergave worden de verschillen tussen de instellingenversies gemarkeerd.  De toevoeging en de verwijdering aan individuele montages worden vermeld door een uitbreiding van een lijn in één van beide richting.

![Verschillende versies van de extensie Analytics vergelijken](../../images/compare-extension.png)

Hierboven kunt u de volgende wijzigingen zien:

* De extensie [!DNL Adobe Analytics] wordt bijgewerkt naar een nieuwe versie, die wordt aangegeven door de oranje versienummers bovenaan.
* De `orgID` en `currencyCode` worden veranderd in de montages die door de uitbreiding van de oranje sectie in de montages worden vermeld.

## Gegevenselementen vergelijken

De elementen van gegevens hebben één enkel scherm om verschillen te tonen, maar omdat de gegevenselementen extra attributen naast hun montages hebben, wordt de extra informatie getoond.  Kenmerken die zijn gewijzigd, worden in oranje gemarkeerd.

![Verschillende versies van een gegevenselement vergelijken](../../images/compare-data-element.png)

Hierboven kunt u de volgende wijzigingen zien:

* De naam is gewijzigd van &quot;Paginanaam 2&quot; in &quot;Mijn speciale paginanaam&quot;, zoals aangegeven door de oranje balk.
* Het type is gewijzigd van JavaScript-variabele in Pagina-info.
* De standaardwaarde van &quot;b&quot; is toegevoegd.
* De optie Kleine letters forceren is geselecteerd.
* &quot;Schone tekst&quot; is geselecteerd.
* De instellingen zijn gewijzigd. (De instellingen voor het type JavaScript-variabele verschillen van het type Pagina-info.)

Als het instellingenblok groot is, kunt u de sectie Instellingen uitvouwen zodat u deze beter kunt zien.

## Regels vergelijken

De regels bestaan uit vele regelcomponenten.  Om de veranderingen in een regel te begrijpen, moet u over de toevoeging en de verwijdering van componenten evenals wijzigingen aan een individuele component weten.  Als je versies van een regel vergelijkt, zijn er eigenlijk twee schermen.

Het eerste scherm toont een mening op hoog niveau, die veranderingen in de rangschikking van regelcomponenten binnen de regel benadrukt.  Wijzigingen worden gemarkeerd. Verschillende typen wijzigingen worden weergegeven.

![Verschillende versies van een regel vergelijken](../../images/compare-rule.png)

Hierboven kunt u de volgende wijzigingen zien:

* De regelnaam is veranderd van &quot;Analytics&quot; in &quot;Baseline Analytics&quot;, aangegeven door de oranje balk op Naam.
* De voorwaarde &quot;Core - Domain&quot; is toegevoegd, aangegeven door het oranje &quot;+&quot;-pictogram en de toevoeging van de component aan de rechterkant.
* De handeling &quot;[!DNL Adobe Analytics] - Variabelen wissen&quot; is verwijderd. Dit wordt aangegeven door het oranje pictogram &quot;-&quot; en de afwezigheid van de component aan de rechterkant.
* De actie &quot;[!DNL Adobe Analytics] - Variabelen instellen&quot; is gewijzigd. Deze actie wordt aangegeven door de oranje lijn tussen de versies van de component aan de linker- en rechterzijde. Deze lijn is recht als de componentenorde niet is veranderd.
* De actie &quot;[!DNL Adobe Analytics] - Vastgestelde Variabelen&quot;en &quot;[!DNL Adobe Analytics] - verzend Beacon&quot;actieorde is veranderd, die door de gebogen lijnen wordt vermeld die de verschillende versies van de componenten op de linker en juiste kanten verbinden

Om de specifieke wijzigingen in één van de regelcomponenten te bekijken, selecteer de specifieke component u zou willen bekijken.  De lijn verandert in blauw wanneer u de muis erboven plaatst.

![Selecteer de component die u gedetailleerder wilt weergeven](../../images/compare-rule-component-click.png)

De vergelijking voor een individuele regelcomponent gedraagt zich het zelfde als de vergelijking voor een gegevenselement.

![Verschillende versies van een afzonderlijke regelcomponent vergelijken](../../images/compare-rule-component.png)

Hierboven ziet u de volgende wijziging:

* De component rule is gewijzigd in add eVar2 met de waarde &quot;1&quot;.

Als het instellingenblok groot is, kunt u de sectie Instellingen uitvouwen zodat u deze beter kunt zien.
