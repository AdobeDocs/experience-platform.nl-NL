---
title: Identiteitsservice en realtime klantprofiel
description: Meer informatie over de relatie tussen Identiteitsservice en Real-Time Klantprofiel
exl-id: 09961b8e-f736-4fcc-ac53-88b55cca7d55
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# De relatie tussen Identiteitsservice en Real-Time Klantprofiel

>[!IMPORTANT]
>
>Op deze pagina wordt ervan uitgegaan dat het samenvoegbeleid de identiteitsgrafiek gebruikt. Voor meer informatie over samenvoegingsbeleid in Real-Time het Profiel van de Klant, lees de documentatie over [samenvoegbeleid en identiteitsstijgingen](../profile/merge-policies/overview.md#identity-stitching).

Hoewel u identiteitsservice en realtime klantprofiel tegelijk kunt gebruiken, zijn de twee functies van Adobe Experience Platform inherent niet hetzelfde.

* U kunt de Dienst van de Identiteit gebruiken om de identiteitsgrafiek te produceren en te handhaven die de ongelijke identiteiten van een individuele klant samenbrengt.
* U kunt het profiel Real-Time gebruiken om verschillende profielfragmenten samen te brengen en een samengevoegd profiel te maken. Dit proces vereist het gebruik van de identiteitsgrafiek.

Dit document beschrijft de gelijkenissen, de verschillen, en de verhouding tussen de Dienst van de Identiteit en het Profiel van de Klant in real time.

## Identiteitsservice versus realtime klantprofiel

De belangrijkste verschillen tussen Identiteitsservice en Real-Time Klantprofiel zijn als volgt:

| | Identiteitsservice | Klantprofiel in realtime |
| --- | --- |--- |
| **Doel** | <ul><li>U kunt de Dienst van de Identiteit gebruiken om identiteitsgrafieken tot stand te brengen en te beheren.</li></ul> | U kunt Real-Time profiel van de Klant gebruiken aan: <ul><li>Maak een 360-gradenweergave van een klantprofiel.</li><li>Profielen weergeven en beheren.</li></ul> |
| **Invoer** | <ul><li>Als u Identiteitsservice wilt gebruiken, moet u recordgegevens of tijdreeksgebeurtenissen invoeren die ten minste twee velden hebben die als identiteit zijn gemarkeerd. De gebieden die u als identiteit merkt worden dan opgenomen in de Dienst van de Identiteit.</li></ul> | <ul><li>Profielfragmenten: vertegenwoordigen een unieke primaire identiteit en de bijbehorende record- of gebeurtenisgegevens voor die id binnen een bepaalde gegevensset.</li><li>Identiteitsgrafieken: het profiel verwijst naar de identiteitsgrafiek voor een bepaald klantprofiel om alle profielfragmenten met dezelfde primaire identiteiten te identificeren.</li></ul> |
| **Proces** | <ul><li>Als u ten minste twee identiteiten hebt ingevoerd, koppelt Identiteitsservice deze identiteiten vervolgens aan elkaar.</li></ul> | <ul><li>In real-time Klantprofiel worden profielfragmenten samengevoegd terwijl wordt verwezen naar hun overeenkomstige identiteitsgrafieken.</li></ul> |
| **Uitvoer** | <ul><li>Het resultaat is een identiteitsgrafiek, die een reeks identiteiten met betrekking tot een individu is.</li></ul> | <ul><li>Het resultaat is een samengevoegd profiel, dat een enkele en uitgebreide weergave van een bepaalde klant is. Dit profiel kan dan in aanmerking komen voor een segment.</li></ul> |

{style="table-layout:auto"}

## Samengevoegd proces voor het maken van profielen

Lees de onderstaande stappen om meer inzicht te krijgen in het proces van het maken van een samengevoegd profiel:

* Eerst verwijst het Real-Time Profiel van de Klant naar een identiteitsgrafiek en wint alle identiteiten terug.
* Vervolgens haalt Profiel profielfragmenten op met primaire identiteiten in de identiteitsgrafiek.
* Wanneer de bewerking voltooid is, voegt Profiel dan alle bestaande gebeurtenissen en kenmerken samen.
   * Als er conflicterende kenmerkinformatie is, worden kenmerken gekozen op basis van de samenvoegmethode. Lees voor meer informatie de [overzicht van samenvoegbeleid](../profile/merge-policies/overview.md).

![Een stroomdiagram waarin wordt aangegeven hoe Identiteitsservice en het samenvoegen van profielen werken.](./images/merge-profile-process.png)

## Een veld aanwijzen als identiteit

In het Model van Gegevens van de Ervaring (XDM), om een gebied als identiteit te merken of aan te wijzen is een instructie voor Experience Platform om dat bepaalde gebied aan de Dienst van de Identiteit in te gaan. Deze aanwijzing staat dan voor profielfragmenten toe om in het Profiel van de Klant in real time worden samengevoegd. Als er geen profielfragmenten aan de identiteit zijn gekoppeld, geeft u deze dan niet als identiteit aan.

### Werken met primaire en secundaire identiteiten

Als u velden eenmaal als identiteiten hebt gemarkeerd, kunnen deze vervolgens worden gedefinieerd als primaire of secundaire identiteiten. De primaire en secundaire identiteiten zijn concepten deel van het Profiel van de Klant in real time.

* De primaire identiteit (ook wel &quot;primaire sleutel&quot; genoemd) is de identiteit waarin profielfragmenten worden opgeslagen.
* Als een bepaalde gegevensrij slechts één identiteit bevat, wordt die ene identiteit als primair aangemerkt.
* Als er twee of meer identiteiten zijn, wordt er één aangewezen als primair, en de rest als secundair.

De identiteitsdienst brengt banden tussen identiteiten tot stand zolang er ten minste twee gebieden als identiteit zijn gemerkt. Identiteitsdienst slaat geen informatie op over of een identiteit primair of secundair is.

