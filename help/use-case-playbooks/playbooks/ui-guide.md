---
solution: Experience Platform
title: Handleiding voor afspeelinterface
description: Leer hoe te om Experience Platform UI te gebruiken om playbooks te bekijken en toe te laten.
badgeBeta: label="Beta" type="Informative"
source-git-commit: 63ea852ca9f9a45d1c071fd1033cbd44cbb427c6
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---


# (bèta) Een afspeelboek inschakelen en opnieuw gebruiken

>[!AVAILABILITY]
>
>Deze functionaliteit is momenteel in Bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Als u een afspeelboek wilt gebruiken, navigeert u naar **[!UICONTROL Use Case Playbooks]>[!UICONTROL Playbooks]**. Blader en gebruik de verschillende zoek- en filteropties op de pagina om een bepaald afspeelboek te selecteren en aan de slag te gaan.

## Zoeken en filteren {#search-and-filter}

Gebruik het zoekvenster en de filters op de pagina om de juiste afspeellijst voor uw gebruik te vinden.

U kunt bijvoorbeeld afspeelboeken filteren die u kunt gebruiken op basis van het werkgebied in de marketingtrechter waarop u zich wilt richten: conversie, betrokkenheid of retentie. U kunt de weergegeven afspeelboeken ook filteren op basis van de branche waarin u zich bevindt of op basis van de productrechten waartoe u toegang hebt: Adobe Journey Optimizer of Real-time CDP.

![Afspeelboeken filteren op basis van marketingtrechter, industrie of product](/help/use-case-playbooks/assets/playbooks/ui-guide/filter-by-funnel-industry-product.gif)

U kunt de zoekfunctionaliteit ook gebruiken om het juiste afspeelboek voor u te vinden. Hieronder ziet u een voorbeeld van hoe u een afspeelboek kunt vinden waarmee u zich kunt bezighouden met gebruikers die mogelijk hun winkelwagentje hebben verlaten.

![Neem contact op met gebruikers die mogelijk hun winkelwagentje hebben verlaten.](/help/use-case-playbooks/assets/playbooks/ui-guide/engage-abandoned-cart.gif)

Of, kunt u beschikbare playbooks door de kanalen filtreren die u van plan bent te gebruiken om uw klanten te bereiken, zoals u hieronder kunt zien:

![Filteren op kanaal](/help/use-case-playbooks/assets/playbooks/ui-guide/channel-select-filter.gif)

Experimenteer met de filters en zoekoptie en zoek het juiste afspeelboek voor u.

## Afspeelboek weergeven en elementen genereren {#view-playbook-generate-assets}

Voordat u een afspeelboek maakt en er exemplaren van maakt, moet u het controleren om er zeker van te zijn dat het in uw behoeften past. Alle afspeelboeken bevatten de onderstaande secties, zodat u beter inzicht krijgt in de gebruiksgevallen die ze behandelen. Wanneer u klaar bent om verder te gaan en elementen te genereren, selecteert u **[!UICONTROL Create Instance]**.

### Mindmap {#mindmap}

Gebruik de sectie mindmap in een afspeelboek om te begrijpen welke stappen van de workflow u met de afspeellijst kunt oplossen. Visualiseer de stroom van hoe alle geproduceerde voorwerpen u het gebruiksgeval kunnen helpen bereiken, vanuit het perspectief van de persoon die in het gebruiksgeval wordt gericht.

De mindmap begint met een definitie van wie in de gebruikersreis wordt bereikt en beschrijft bij elke stap als iets door Adobe, zoals een nieuw bericht of een herinnering wordt geleverd, of als het iets is dat de gerichte persoon deed dat het volgende bericht of de gebeurtenis teweegbracht.

![De afspeelmindmap is gemarkeerd.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-mindmap.png)


### Samenvatting {#summary}

Inspect de overzichtssectie om te begrijpen welke activa worden geproduceerd zodra u instanties van playbook creeert. De elementen die voor elk afspeelboek worden gegenereerd, worden aangepast aan het gebruiksscenario dat in het afspeelboek wordt ingeschakeld. Meer informatie over alle items in de overzichtssectie vindt u hieronder.

| Item | Beschrijving |
---------|----------|
| **[!UICONTROL Target audience]** | Beschrijft de karakters die u door dit gebruiksgeval playbook wilt bereiken. |
| **[!UICONTROL Marketing Channels]** | Beschrijft de kanalen die worden gebruikt om de karakters te bereiken die in playbook worden gericht. |
| **[!UICONTROL Technical assets]** | Een lijst met de technische elementen die worden gegenereerd nadat u instanties van het afspeelboek hebt gemaakt. De gegenereerde elementen verschillen per afspeelboek, afhankelijk van het gebruiksscenario. Sommige playbooks kunnen schema&#39;s, segmenten, en reizen produceren. Anderen kunnen doelen genereren. Zie de [De gegenereerde elementen begrijpen](#understand-assets) hieronder vindt u meer informatie over het gebruik en het hergebruik van de gegenereerde elementen. |

{style="table-layout:auto"}

![Overzicht van playbook gemarkeerd](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-summary.png)

### Instanties {#instances}

Schuif omlaag naar de sectie instances voor een overzicht van de instanties van dit afspeelboek die u of leden van uw team al hebben gemaakt. U kunt verschillende besturingselementen gebruiken om de weergegeven instanties te sorteren en te filteren, bijvoorbeeld om alleen de door u gemaakte instanties te zien. U kunt ook verschillende informatie over elk exemplaar zien, zoals hieronder vermeld.

| Item | Beschrijving |
|---------|----------|
| **[!UICONTROL Name]** | De naam van de instantie op basis van het afspeelboek. U kunt de naam en beschrijving van een instantie aanpassen. Lees de onderstaande sectie op [instantiemetagegevens bewerken](#edit-instance-metadata) voor meer informatie . |
| **[!UICONTROL Status]** | Geeft de status van de instantie aan. A **[!UICONTROL submitted]** -instantie is klaar voor gebruik. |
| **[!UICONTROL Created]** | Geeft aan wanneer de instantie is gemaakt. |
| **[!UICONTROL Created By]** | Geeft aan wie de instantie heeft gemaakt. |
| **[!UICONTROL Last Modified]** | Geeft aan wanneer de instantie voor het laatst is gewijzigd. |

{style="table-layout:auto"}

![Instantie van afspeelboek is gemarkeerd.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-instances.png)

## Afspeelboek inschakelen {#enable-playbook}

Wanneer u gereed bent om verder te gaan met een afspeelboek en een instantie te maken, selecteert u **[!UICONTROL Create Instance]** om verder te gaan met het afspeelboek en technische middelen te genereren.

![Maak een instantie van een afspeelboek.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Deze actie genereert verschillende elementen die u kunt gebruiken om het gebruik van hoofdletters en kleine letters te bereiken die in de afspeellijst worden beschreven.

![Weergave van gegenereerde elementen afspelen nadat deze is ingeschakeld.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Gebruik de configuratiecontroles om instantienamen en beschrijvingen uit te geven {#edit-instance-metadata}

Nadat u een instantie hebt gemaakt op basis van een afspeelboek, kunt u deze personaliseren om deze te onderscheiden van andere instanties die zijn gemaakt op basis van hetzelfde afspeelboek. Selecteer de configuratiecontrole zoals hieronder getoond. Bewerk de naam, beschrijving en notities en selecteer **[!UICONTROL Save]** als u klaar bent.

![Naam en beschrijving van een instantie bewerken.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### De gegenereerde elementen begrijpen {#understand-assets}

>[!IMPORTANT]
>
>Maak je geen zorgen! Dit is een veilige ruimte om te experimenteren en je kunt niets breken. Er zijn nog geen gegevens gekoppeld aan de elementen die u maakt. U moet eerst gegevens invoeren om de gebruiksgevallen te bereiken.

Het is belangrijk om te begrijpen dat de gegenereerde elementen verschillen op basis van het gebruiksgeval dat u inschakelt:

* Er worden verschillende elementen gegenereerd voor verschillende typen afspeelboeken. Deze elementen worden specifiek gemaakt voor het gebruik dat wordt gemaakt via de afspeelmap. Een afspeelboek genereert bijvoorbeeld een schema, een segment, een reis en berichten. Een ander playbook produceert een schema, een segment, en een bestemming om gegevens aan te activeren.
* De elementen zelf verschillen per afspeelboek. Bijvoorbeeld voor **[!UICONTROL Send A Birthday Message To Guests]** playbook, heeft het publiek dat wordt gecreeerd de regel `birthday=today AND year=any`.

Om een voorbeeld te illustreren, voor **[!UICONTROL Abandoned Cart: Merchandise]** playbook, kunt u zien dat een specifieke reis wordt gecreeerd die de berichten omvat die voor dit gebruiksgeval worden gecreeerd.

![Reis gemaakt op basis van een afspeelboek met gebruiksscenario&#39;s.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### De gegenereerde elementen gebruiken en bewerken {#use-and-edit-assets}

Wanneer u de elementen verkent die worden gegenereerd nadat u een instantie van een afspeelboek hebt gemaakt, kunt u alle gemaakte elementen bewerken.

Als u of iemand in uw team een ander exemplaar van de afspeellijst maakt, worden de bewerkte elementen bewaard en worden nieuwe elementen gemaakt voor de nieuwe instantie van de afspeelboek.

Het hierboven beschreven gedrag geldt voor alle elementen die worden gemaakt, behalve voor schema&#39;s. In het geval van schema&#39;s, worden de nieuwe schema&#39;s niet gecreeerd wanneer een nieuw geval van playbook wordt gecreeerd, zodat zult u het uitgegeven schema van een andere instantie van playbook in de pas gecreëerde instantie gebruiken.

>[!TIP]
>
>Test in de ontwikkelingssandbox en ga naar productie als u klaar bent.
>
>Wanneer objecten zijn gegenereerd, kunt u in de ontwikkelingssandboxen blijven testen door gegevens toe te voegen. U kunt de elementen zo lang testen als u wilt in de ontwikkelingssandbox en u kunt de elementlogica (segmentdefinities, reizen, schema&#39;s, enzovoort) in de productiesandbox herhalen wanneer u klaar bent.

### Afspeelboeken opnieuw gebruiken {#reuse-playbooks}

Door veelvoudige instanties van zelfde playbook te creëren, kunt u het zelfde gebruiksgeval later uitvoeren, zonder de details van uw vorige implementatie van het gebruiksgeval te wijzigen.

### De playbook en de geproduceerde activa met andere teamleden delen {#share-playbook}

U kunt de gegenereerde instantie en elementen delen met andere teamleden. Hiervoor kopieert u de URL-koppeling van de browser en deelt u deze met uw team om een overzicht van de gegenereerde elementen te krijgen.

![URL die is gemarkeerd in een weergave voor afspeelboeken met gebruiksscenario&#39;s.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Volgende stappen {#next-steps}

Door deze UI-gids te lezen, weet u nu hoe u de verschillende secties van een afspeelboek kunt interpreteren en hoe u de elementen kunt gebruiken die worden gegenereerd nadat u een instantie van een afspeelboek hebt gemaakt. Vervolgens kunt u door de catalogus met afspeelboeken bladeren om de juiste afspeellijst voor uw gebruikscase te vinden en de gids voor probleemoplossing te lezen als u fouten tegenkomt.