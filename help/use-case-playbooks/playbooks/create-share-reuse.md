---
solution: Experience Platform
title: Afspeelboekinstanties maken, delen en opnieuw gebruiken
description: Leer hoe u playbook-instanties kunt maken, delen en opnieuw gebruiken om uw marketinggebruikskwestie te voltooien.
badgeBeta: label="Beta" type="Informative"
source-git-commit: e61e200b148e4d17041b3711bd63c796a44b05c8
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# (bètaversie) Afspeelboekinstanties maken, delen en opnieuw gebruiken

>[!AVAILABILITY]
>
>Deze functionaliteit is momenteel in Bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Als u een afspeelboek wilt gebruiken, navigeert u naar **[!UICONTROL Use Case Playbooks]>[!UICONTROL Playbooks]**. Blader en gebruik de verschillende zoek- en filteropties op de pagina om een bepaald afspeelboek te selecteren en aan de slag te gaan.

## Een instantie voor een afspeelboek maken {#create-playbook-instance}

Voordat u een instantie van een afspeelboek maakt, kunt u de beschikbare afspeelboeken raadplegen op [u kunt het juiste afspeelboek voor u vinden](/help/use-case-playbooks/playbooks/discover.md). Wanneer u gereed bent om verder te gaan met een afspeelboek en een instantie te maken, selecteert u **[!UICONTROL Create Instance]** om verder te gaan met het afspeelboek en technische middelen te genereren.

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

## Afspeelboeken opnieuw gebruiken {#reuse-playbooks}

Door veelvoudige instanties van zelfde playbook te creëren, kunt u het zelfde gebruiksgeval later uitvoeren, zonder de details van uw vorige implementatie van het gebruiksgeval te wijzigen.

## De playbook en de geproduceerde activa met andere teamleden delen {#share-playbook}

U kunt de gegenereerde instantie en elementen delen met andere teamleden. Hiervoor kopieert u de URL-koppeling van de browser en deelt u deze met uw team om een overzicht van de gegenereerde elementen te krijgen.

![URL die is gemarkeerd in een weergave voor afspeelboeken met gebruiksscenario&#39;s.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## Volgende stappen {#next-steps}

Door deze handleiding te lezen en de handleiding over het ontdekken van het juiste afspeelboek voor u, weet u nu hoe u de verschillende gedeelten van een afspeelboek kunt interpreteren en hoe u de elementen kunt gebruiken die worden gegenereerd nadat u een instantie van een afspeelboek hebt gemaakt.

Vervolgens kunt u door de catalogus met afspeelboeken bladeren om de juiste afspeellijst voor uw gebruik te vinden en de [gids voor problemen](/help/use-case-playbooks/playbooks/troubleshooting.md) als er problemen optreden.