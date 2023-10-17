---
title: Identiteitsservice en realtime klantprofiel
description: Meer informatie over de relatie tussen Identiteitsservice en Real-Time Klantprofiel
hide: true
hidefromtoc: true
source-git-commit: 03228eef47100096e98666966c4e5065eb7f478a
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# De relatie tussen Identiteitsservice en Real-Time Klantprofiel

>[!IMPORTANT]
>
>Op deze pagina wordt ervan uitgegaan dat het samenvoegbeleid de identiteitsgrafiek gebruikt. Voor meer informatie over samenvoegingsbeleid in Real-Time het Profiel van de Klant, lees de documentatie over [samenvoegbeleid en identiteitsstijgingen].

Hoewel u identiteitsservice en realtime klantprofiel tegelijk kunt gebruiken, zijn de twee functies van Adobe Experience Platform inherent niet hetzelfde.

* U kunt de Dienst van de Identiteit gebruiken om de identiteitsgrafiek te produceren en te handhaven die de ongelijke identiteiten van een individuele klant samenbrengt.
* U kunt het profiel Real-Time gebruiken om verschillende profielfragmenten samen te brengen en een samengevoegd profiel te maken. Dit proces vereist het gebruik van de identiteitsgrafiek.

Dit document beschrijft de gelijkenissen, verschillen, en verhouding tussen de Dienst van de Identiteit en het Profiel van de Klant in real time.

## Identiteitsservice versus realtime klantprofiel

De belangrijkste verschillen tussen Identiteitsservice en Real-Time Klantprofiel zijn als volgt:

| | Identiteitsservice | Klantprofiel in realtime |
| --- | --- |--- |
| **Doel** | <ul><li>U kunt de Dienst van de Identiteit gebruiken om identiteitsgrafieken tot stand te brengen en te beheren.</li></ul> | U kunt Real-Time profiel van de Klant gebruiken aan: <ul><li>Maak een 360-gradenweergave van een klantprofiel.</li><li>Profielen weergeven en beheren</li><li>Segmentprofielen om publiek te maken.</li></ul> |
| **Invoer** | <ul><li>Als u Identiteitsservice wilt gebruiken, moet u recordgegevens of tijdreeksgebeurtenissen invoeren die ten minste twee velden hebben die als identiteit zijn gemarkeerd. De gebieden die u als identiteit merkt worden dan opgenomen in de Dienst van de Identiteit.</li></ul> | **Als u profielen wilt samenvoegen, moet u**: <ul><li>Profielfragmenten: vertegenwoordigen een unieke primaire identiteit en de bijbehorende record- of gebeurtenisgegevens voor die id binnen een bepaalde gegevensset.</li><li>Identiteitsgrafieken: het profiel verwijst naar de identiteitsgrafiek voor een bepaald klantprofiel om alle profielfragmenten met dezelfde primaire identiteiten te identificeren.</li></ul> **Voor segmentkwalificatie moet u**: <ul><li>Samengevoegde profielen: een samengevoegd profiel is één weergave van een klant, waarbij verschillende profielfragmenten en identiteiten in één uitgebreide weergave worden verzameld.</li></ul> |
| **Proces** | <ul><li>Als u ten minste twee identiteiten hebt ingevoerd, koppelt Identiteitsservice deze identiteiten vervolgens aan elkaar.</li></ul> | <ul><li>In real-time Klantprofiel worden profielfragmenten samengevoegd terwijl wordt verwezen naar hun overeenkomstige identiteitsgrafieken.</li><li>Profielen kwalificeren voor segmenten op basis van segmenteringscriteria</li></ul> |
| **Uitvoer** | <ul><li>Het resultaat is een identiteitsgrafiek, die een reeks identiteiten met betrekking tot een individu is.</li></ul> | <ul><li>Het resultaat is een samengevoegd profiel, dat een enkele en uitgebreide weergave van een bepaalde klant is.</li><li>Profielen met gedefinieerde segmentlidmaatschappen</li></ul> |

{style="table-layout:auto"}

>[!BEGINSHADEBOX]

## Hoe wordt een samengevoegd profiel gemaakt?

Lees de onderstaande stappen om meer inzicht te krijgen in het proces van het maken van een samengevoegd profiel:

* Eerst verwijst het Real-Time Profiel van de Klant naar een identiteitsgrafiek en wint alle identiteiten terug.
* Vervolgens haalt het profiel alle profielfragmenten op die betrekking hebben op elke identiteit.
* Wanneer de bewerking voltooid is, voegt Profiel dan alle bestaande gebeurtenissen en kenmerken samen.
   * Indien nodig, past u prioriteitsregels toe om te bepalen welk kenmerk of welke gebeurtenis moet worden gebruikt

![Een stroomdiagram waarin wordt aangegeven hoe Identiteitsservice en het samenvoegen van profielen werken.](../images/identity-settings/identity-and-profile.png)

>[!ENDSHADEBOX]

### Wat betekent het om een gebied als identiteit te merken?

Als u een veld wilt markeren of aanwijzen als identiteit, geeft het Experience Platform de instructie dat veld in te voeren bij Identiteitsservice. Deze aanwijzing staat dan voor profielfragmenten toe om in het Profiel van de Klant in real time worden samengevoegd. Als er geen profielfragmenten aan de identiteit zijn gekoppeld, geeft u deze dan niet als identiteit aan.

#### Werken met primaire en secundaire identiteiten

Als u velden eenmaal als identiteiten hebt gemarkeerd, kunnen deze vervolgens worden gedefinieerd als primaire of secundaire identiteiten. De primaire en secundaire identiteiten zijn concepten deel van het Profiel van de Klant in real time.

* De primaire identiteit (ook wel &quot;primaire sleutel&quot; genoemd) is de identiteit waarin profielfragmenten worden opgeslagen.
* Als een bepaalde gegevensrij slechts één identiteit bevat, wordt die ene identiteit als primair aangemerkt.
* Als er twee of meer identiteiten zijn, wordt er één aangewezen als primair, en de rest als secundair.

De Dienst van de identiteit neemt slechts gebieden op die als identiteit worden aangewezen. Identiteitsdienst slaat geen informatie op over of een identiteit primair of secundair is.

## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Overzicht van regels voor identiteitsgrafiek](./overview.md)
* [Voorbeeldscenario&#39;s voor het configureren van identiteitsgrafiek-koppelingsregels](./example-scenarios.md)
* [Logica voor identiteitskoppeling](./identity-linking-logic.md)