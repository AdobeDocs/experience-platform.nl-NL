---
keywords: Experience Platform;huis;populaire onderwerpen;dataset;Dataset;tijd om te leven;ttl;tijd-aan-levende;
solution: Experience Platform
title: Tijd-aan-levende op Datasets
description: Dit document biedt algemene richtlijnen over tijd-aan-leven (TTL) voor datasets in de opslag van het Profiel voor Adobe Experience Platform.
source-git-commit: 878c04c688268f8cf1850c3e8d40f958a6d2d69b
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---


# De tijd-aan-levende van de Dienst van het profiel (TTL)

Met profielservice kunnen gebruikers tijd-aan-live (TTL) toepassen op gegevens in de profielopslag. TTL is een mechanisme dat de hoeveelheid tijd beperkt die de gegevens binnen een dataset leven. Hiermee kunt u automatisch gegevens verwijderen uit het profielarchief die niet meer nuttig zijn voor uw gebruiksgevallen.

Profiel ondersteunt momenteel alleen Experience Event TTL.

## Experience Event TTL

Dankzij Experience Event TTL kunt u TTL toepassen op gegevenssets die geschikt zijn voor klantprofiel in realtime om gegevens te verwijderen uit de profielopslag die niet langer geldig is.

>[!NOTE]
>
>U zult steun moeten contacteren om de Gebeurtenis TTL van de Ervaring op uw datasets toe te laten.

Na het toelaten van de Gebeurtenis TTL van de Ervaring op een profiel-Toegelaten dataset, zal het Platform automatisch de waarde van de Vervaltijd van TTL op de gegevens van de Gebeurtenis van de Ervaring in een proces in twee stappen toepassen:

1. Voor alle nieuwe gegevens die in de gegevensset worden opgenomen, wordt de vervalwaarde van TTL toegepast tijdens de opname.
2. Alle bestaande gegevens in de dataset zullen de de vervalwaarde van TTL hebben retroactief wordt toegepast als éénmalige backfill systeembaan. Zodra de vervalwaarde van TTL op de dataset is geplaatst, zullen de gebeurtenissen die ouder zijn dan de vervalwaarde van TTL onmiddellijk worden gelaten vallen zodra de systeembaan loopt. Alle andere gebeurtenissen worden verwijderd zodra ze hun waarde voor de vervaldatum van TTL halen vanuit de tijdstempel van de gebeurtenis.

>[!NOTE]
>
>Zodra TTL wordt toegepast, zullen om het even welke gegevens die ouder zijn dan het aantal dagen van TTL **permanent worden geschrapt** en kunnen niet worden hersteld.
> 
>Bovendien, zorg ervoor dat het raadplegingsvenster voor het segment binnen de grens van TTL is. Anders, kunnen de segmentresultaten onjuist worden na het toepassen van TTL. Als u bijvoorbeeld een TTL van 30 dagen toepaste en een segment had dat tot 45 dagen geleden probeerde gegevens te bekijken, zou het segment onjuiste profielen produceren.
> 
>Dientengevolge, zou u zelfde TTL voor alle datasets moeten houden, indien mogelijk, om het effect van verschillende waarden van TTL over verschillende datasets in de segmenteringslogica te vermijden.

Als u bijvoorbeeld op 15 mei een TTL-waarde van 30 dagen hebt toegepast, worden de volgende stappen uitgevoerd:

1. Voor alle nieuwe gebeurtenissen wordt een TTL-waarde van 30 dagen toegepast wanneer deze wordt opgenomen.
2. Alle bestaande gebeurtenissen met een tijdstempel die ouder is dan 15 april worden onmiddellijk verwijderd met de systeemtaak.
3. Alle bestaande gebeurtenissen met een tijdstempel die nieuwer is dan 15 april hebben een vervalwaarde van TTL 30 dagen na hun tijdstempel voor de gebeurtenis. Als een gebeurtenis dus een tijdstempel heeft van 18 april, wordt deze verwijderd dertig dagen na de datum van die tijdstempel, die 18 mei zou zijn.

