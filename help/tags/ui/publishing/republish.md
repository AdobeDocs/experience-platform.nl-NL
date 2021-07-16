---
title: Bibliotheek opnieuw publiceren
description: Leer hoe u een vorige tagbibliotheek opnieuw publiceert in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Bibliotheek opnieuw publiceren

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De vijf meest recente bibliotheken die aan uw productiemilieu op een bezit van het Web zijn gepubliceerd zijn beschikbaar voor recentere herwinning. Deze functie is handig wanneer u een probleem aantreft in uw productiebibliotheek en u onmiddellijk terug moet keren naar een bekende goede toestand.

Het ophaalproces is afhankelijk van uw omgevingsinstellingen op het moment dat de bibliotheek oorspronkelijk werd gepubliceerd. Dit is belangrijk omdat het ophalen van een gearchiveerde bibliotheek niets op uw livesite verandert, terwijl het ophalen van een gewone bibliotheek dat wel doet.

De volgende opties zijn beschikbaar:

* **Host: Beheerd door Adobe, Archief: Uit:** Als u de door de host van Adobe beheerde bibliotheek gebruikt en uw bibliotheek niet archiveert, kunt u deze oudere bibliotheken opnieuw publiceren.

* **Host: Beheerd door Adobe, Archief: Aan:** Als u de bibliotheek van de host Beheerd door Adobe gebruikt en u archiveert, kunt u deze oudere bibliotheken downloaden.

* **Host: SFTP, archiveren: Aan of Uit:** Als u de gastheer SFTP gebruikt, wordt verondersteld dat u uw eigen archiveringsstrategieën op zijn plaats hebt en geen terugwinningsopties beschikbaar zijn.

Ophaalopties voor mobiele eigenschappen zijn nog niet beschikbaar.

## Opnieuw publiceren

Elke tagomgeving bevat een koppeling naar een bibliotheekbestand. Aan elke bibliotheek die u in die omgeving maakt, kan naar die koppeling worden verwezen.

Wanneer u aan een ontwikkelings of het opvoeren milieu bouwt, wordt de oude bouwstijl schoongemaakt en de nieuwe bouwstijl wordt opgesteld. Voor uw productieomgeving wordt deze koppeling bijgewerkt om naar de laatste build te verwijzen, maar de vijf meest recente builds worden bewaard voordat ze worden opgeruimd.

Deze vijf meest recente builds in uw productiemilieu zijn degenen die voor terugwinning beschikbaar zijn.

Wanneer u een oudere bibliotheek opnieuw publiceert, werkt het Platform de milieuverbinding bij om aan één van deze oudere bouwstijlen te richten die nog niet is schoongemaakt.  Platform geeft ook een leegmaakverzoek uit aan de CDN-cache van randknooppunten om aan te geven dat de bibliotheek is bijgewerkt en dat een nieuwe kopie moet worden opgehaald van de oorsprong.

Dit betekent dat wanneer u een oudere bibliotheek opnieuw publiceert:

* Er worden geen wijzigingen aangebracht in de bronnen (of historische revisies) in de eigenschap tag

* De manier waarop ontwikkelings- en staging-omgevingen berekenen wat upstream is, verandert niet

Overweeg het scenario wanneer u wegens een probleem met een specifieke regel terugdraait. De herziening van de regels die nu in productie is, zou bijvoorbeeld drie oude herzieningen kunnen zijn.  Wanneer u die regel in de UI van de Inzameling van Gegevens bekijkt om het te bevestigen, weerspiegelt het nog de recentste opgeslagen veranderingen eerder dan wat momenteel in productie is.

Om deze reden, deelt het Platform u mee dat een bezit in een opnieuw gepubliceerde staat als herinnering is dat wat u in het gebruikersinterface van de Inzameling van Gegevens ziet een weinig verder verwijderd uit Productie dan normaal is. Deze melding is niet toegestaan en wordt de eerste keer dat u de eigenschap weergeeft, eenmaal per browsersessie weergegeven.

### Een oudere bibliotheek opnieuw publiceren

![Bibliotheek opnieuw publiceren](images/retrieve_republish.png)

Vanuit het scherm Publiceren:

1. Zoek de bibliotheek in de Gepubliceerde kolom die u zou willen opnieuw publiceren.
1. Selecteer de ellips (`...`) in de hoger-juiste hoek van de kaart van de Bibliotheek.
1. Selecteer **[!UICONTROL Republish]**.

## Download

Het downloaden van een gearchiveerde bibliotheek is eenvoudiger. U verwijst niet direct naar deze .zip dossiers overal, zodat kunt u eenvoudig de oudere bibliotheek aan uw computer downloaden en uw normaal proces in werking stellen.

### Hoe te om een oudere bibliotheek te downloaden

![Een bibliotheek downloaden](images/retrieve_download.png)

Vanuit het scherm Publiceren:

1. Zoek de bibliotheek in de kolom Published die u wilt downloaden.
1. Selecteer de ellips (`...`) in de hoger-juiste hoek van de kaart van de Bibliotheek.
1. Selecteer **[!UICONTROL Download]**.
