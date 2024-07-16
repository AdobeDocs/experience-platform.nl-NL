---
title: Bibliotheek opnieuw publiceren
description: Leer hoe u een vorige tagbibliotheek opnieuw publiceert in Adobe Experience Platform.
exl-id: 026b01f2-a93d-4e8a-9ed2-47c4f011e70f
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Bibliotheek opnieuw publiceren

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

De vijf meest recente bibliotheken die aan uw productiemilieu op een bezit van het Web zijn gepubliceerd zijn beschikbaar voor recentere herwinning. Deze functie is handig wanneer u een probleem aantreft in uw productiebibliotheek en u onmiddellijk terug moet keren naar een bekende goede toestand.

Het ophaalproces is afhankelijk van uw omgevingsinstellingen op het moment dat de bibliotheek oorspronkelijk werd gepubliceerd. Dit is belangrijk omdat het ophalen van een gearchiveerde bibliotheek niets op uw livesite verandert, terwijl het ophalen van een gewone bibliotheek dat wel doet.

De volgende opties zijn beschikbaar:

* **Gastheer: Beheerd door Adobe, Archief: Van:** als u Beheerd door de gastheer van de Adobe gebruikt en u archiveert uw bibliotheek niet, kunt u deze oudere bibliotheken opnieuw publiceren.

* **Gastheer: Beheerd door Adobe, Archief: Op:** als u Beheerd door de gastheer van de Adobe gebruikt en u uw bibliotheek archiveert, dan kunt u deze oudere bibliotheken downloaden.

* **Gastheer: SFTP, Archief: Aan of weg:** als u de gastheer van SFTP gebruikt, wordt aangenomen dat u uw eigen archiefstrategieën op zijn plaats hebt en geen terugwinningsopties beschikbaar zijn.

Ophaalopties voor mobiele eigenschappen zijn nog niet beschikbaar.

## Opnieuw publiceren

Elke tagomgeving bevat een koppeling naar een bibliotheekbestand. Aan elke bibliotheek die u in die omgeving maakt, kan naar die koppeling worden verwezen.

Wanneer u aan een ontwikkelings of het opvoeren milieu bouwt, wordt de oude bouwstijl schoongemaakt en de nieuwe bouwstijl wordt opgesteld. Voor uw productieomgeving wordt deze koppeling bijgewerkt om naar de laatste build te verwijzen, maar de vijf meest recente builds worden bewaard voordat ze worden opgeruimd.

Deze vijf meest recente builds in uw productiemilieu zijn degenen die voor terugwinning beschikbaar zijn.

Wanneer u een oudere bibliotheek opnieuw publiceert, werkt Platform de milieuverbinding bij om aan één van deze oudere bouwstijlen te richten die nog niet is schoongemaakt.  Platform geeft ook een zuiveringsverzoek aan het CDN geheime voorgeheugen van randknopen uit om erop te wijzen dat de bibliotheek is bijgewerkt en een vers exemplaar van de oorsprong zou moeten worden teruggewonnen.

Dit betekent dat wanneer u een oudere bibliotheek opnieuw publiceert:

* Er worden geen wijzigingen aangebracht in de bronnen (of historische revisies) in de eigenschap tag

* De manier waarop ontwikkelings- en staging-omgevingen berekenen wat upstream is, verandert niet

Overweeg het scenario wanneer u wegens een probleem met een specifieke regel terugdraait. De herziening van de regels die nu in productie is, zou bijvoorbeeld drie oude herzieningen kunnen zijn.  Wanneer u die regel in UI bekijkt om het te bevestigen, weerspiegelt het nog de recentste opgeslagen veranderingen eerder dan wat momenteel in productie is.

Om deze reden, deelt het Platform u mee dat een bezit in een opnieuw gepubliceerde staat als herinnering is dat wat u in het gebruikersinterface van de Inzameling van Gegevens ziet een weinig verder verwijderd uit Productie dan normaal is. Deze melding is niet toegestaan en wordt de eerste keer dat u de eigenschap weergeeft, eenmaal per browsersessie weergegeven.

### Een oudere bibliotheek opnieuw publiceren

![ publiceer een bibliotheek ](images/retrieve_republish.png)

Vanuit het scherm Publiceren:

1. Zoek de bibliotheek in de Gepubliceerde kolom die u zou willen opnieuw publiceren.
1. Selecteer de ellips (`...`) in de hoger-juiste hoek van de kaart van de Bibliotheek.
1. Selecteer **[!UICONTROL Republish]**.

## Downloaden

Het downloaden van een gearchiveerde bibliotheek is eenvoudiger. U verwijst niet direct naar deze .zip dossiers overal, zodat kunt u eenvoudig de oudere bibliotheek aan uw computer downloaden en uw normaal proces in werking stellen.

### Hoe te om een oudere bibliotheek te downloaden

![ Download een bibliotheek ](images/retrieve_download.png)

Vanuit het scherm Publiceren:

1. Zoek de bibliotheek in de kolom Published die u wilt downloaden.
1. Selecteer de ellips (`...`) in de hoger-juiste hoek van de kaart van de Bibliotheek.
1. Selecteer **[!UICONTROL Download]**.
