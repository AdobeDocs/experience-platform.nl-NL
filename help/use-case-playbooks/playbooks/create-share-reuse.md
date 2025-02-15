---
solution: Experience Platform
title: Afspeelboekinstanties maken, delen en opnieuw gebruiken
description: Leer hoe u playbook-instanties kunt maken, delen en opnieuw gebruiken om uw marketinggebruikskwestie te voltooien.
role: User, Developer
exl-id: b06d8186-c41f-4150-bac4-69c616151ef9
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Afspeelboekinstanties maken, delen en opnieuw gebruiken

Als u een afspeelboek wilt gebruiken, navigeert u naar **[!UICONTROL Use Case Playbooks]>[!UICONTROL Playbooks]** . Blader en gebruik de verschillende zoek- en filteropties op de pagina om een bepaald afspeelboek te selecteren en aan de slag te gaan.

## Een instantie voor een afspeelboek maken {#create-playbook-instance}

>[!CONTEXTUALHELP]
>id="platform_playbooks_create"
>title="Instantie maken"
>abstract="Genereer een lijst met middelen zoals reizen, publiek, schema&#39;s of bestemmingen die in reis- of activeringsscenario&#39;s kunnen worden gebruikt."

Alvorens tot een playbook instantie te leiden, onderzoek de beschikbare playbooks aan [ het juiste playbook ](/help/use-case-playbooks/playbooks/choose.md) kiezen. Wanneer u gereed bent om verder te gaan met een afspeelboek en een instantie te maken, selecteert u **[!UICONTROL Create Instance]** om verder te gaan met het afspeelboek en technische elementen te genereren.

![ creeer een geval van playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/create-playbook-instance.png)

Deze actie genereert verschillende elementen die u kunt gebruiken om het gebruik van hoofdletters en kleine letters te bereiken die in de afspeellijst worden beschreven.

![ mening van het Playbook van geproduceerde activa na wordt toegelaten.](/help/use-case-playbooks/assets/playbooks/ui-guide/play-view.png)

### Gebruik de configuratiebesturingselementen om instantienamen en beschrijvingen te bewerken {#edit-instance-metadata}

Nadat u een instantie hebt gemaakt op basis van een afspeelboek, kunt u deze personaliseren om deze te onderscheiden van andere instanties die zijn gemaakt op basis van hetzelfde afspeelboek. Selecteer de configuratiecontrole zoals hieronder getoond. Bewerk de naam, beschrijving en notities en selecteer **[!UICONTROL Save]** wanneer u klaar bent.

![ geef naam en beschrijving van een instantie uit.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-settings.gif)

### De gegenereerde elementen begrijpen {#understand-assets}

>[!IMPORTANT]
>
>Maak je geen zorgen! Dit is een veilige ruimte om te experimenteren en je kunt niets breken. Er zijn nog geen gegevens gekoppeld aan de elementen die u maakt. U moet eerst gegevens invoeren om de gebruiksgevallen te bereiken.

Het is belangrijk om te begrijpen dat de gegenereerde elementen verschillen op basis van het gebruiksgeval dat u inschakelt:

* Er worden verschillende elementen gegenereerd voor verschillende typen afspeelboeken. Deze elementen worden specifiek gemaakt voor het gebruik dat wordt gemaakt via de afspeelmap. Een afspeelboek genereert bijvoorbeeld een schema, een publiek, een reis en berichten. Een ander playbook produceert een schema, een publiek, en een bestemming om gegevens aan te activeren.
* De elementen zelf verschillen per afspeelboek. Voor het afspeelboek van **[!UICONTROL Send A Birthday Message To Guests]** heeft het publiek dat wordt gemaakt, bijvoorbeeld de regel `birthday=today AND year=any` .

Ter illustratie van een voorbeeld kunt u voor de **[!UICONTROL Abandoned Cart: Merchandise]** playbook zien dat er een specifieke reis wordt gemaakt die de berichten bevat die voor dit gebruik worden gemaakt.

![ Reis die van gebruikscasplaybook wordt gecreeerd.](/help/use-case-playbooks/assets/playbooks/ui-guide/journey-preview.png)

### De gegenereerde elementen gebruiken en bewerken {#use-and-edit-assets}

Wanneer u de elementen verkent die worden gegenereerd nadat u een instantie van een afspeelboek hebt gemaakt, kunt u alle gemaakte elementen bewerken.

Als u of iemand in uw team een ander exemplaar van de afspeellijst maakt, worden de bewerkte elementen bewaard en worden nieuwe elementen gemaakt voor de nieuwe instantie van de afspeelboek.

Het hierboven beschreven gedrag geldt voor alle elementen die worden gemaakt, behalve voor schema&#39;s. In het geval van schema&#39;s, worden de nieuwe schema&#39;s niet gecreeerd wanneer een nieuw geval van playbook wordt gecreeerd, zodat zult u het uitgegeven schema van een andere instantie van playbook in de pas gecreëerde instantie gebruiken.

>[!TIP]
>
>Test in de ontwikkelingssandbox en ga naar productie als u klaar bent.
>
>Wanneer objecten zijn gegenereerd, kunt u in de ontwikkelingssandboxen blijven testen door gegevens toe te voegen. U kunt de elementen zo lang testen als u wilt in de ontwikkelingssandbox en u kunt de elementlogica (publieksdefinities, reizen, schema&#39;s, enzovoort) in de productiesandbox herhalen wanneer u klaar bent. U kunt zich naar de ontwikkelingszandbak en dan naar de productiestandaard bewegen door de [ functionaliteit van het gegevensbewustzijn ](/help/use-case-playbooks/playbooks/data-awareness.md) te gebruiken.

## Afspeelboeken opnieuw gebruiken {#reuse-playbooks}

Door veelvoudige instanties van zelfde playbook te creëren, kunt u het zelfde gebruiksgeval later uitvoeren, zonder de details van uw vorige implementatie van het gebruiksgeval te wijzigen.

## De playbook en de geproduceerde activa met andere teamleden delen {#share-playbook}

U kunt de gegenereerde instantie en elementen delen met andere teamleden. Hiervoor kopieert u de URL-koppeling van de browser en deelt u deze met uw team om een overzicht van de gegenereerde elementen te krijgen.

![ URL benadrukte in een mening van het gebruiksgeval playbook.](/help/use-case-playbooks/assets/playbooks/ui-guide/playbook-url.png)

## De videoanalyse van het playbook proces van begin tot eind

Bekijk deze video om te leren om instanties van een Hoofdlettergebruik Playbook van begin tot eind te ontdekken, tot stand te brengen, te publiceren en problemen op te lossen, evenals hoe te om de activa te kopiëren die door playbook in andere zandbakken worden geproduceerd die in uw organisatie worden gevestigd.

>[!VIDEO](https://video.tv.adobe.com/v/3427058/?learn=on)

## Volgende stappen {#next-steps}

Door deze handleiding te lezen en de handleiding over het ontdekken van het juiste afspeelboek voor u, weet u nu hoe u de verschillende gedeelten van een afspeelboek kunt interpreteren en hoe u de elementen kunt gebruiken die worden gegenereerd nadat u een instantie van een afspeelboek hebt gemaakt.

Daarna, kunt u de playbooks catalogus doorbladeren om het juiste playbook voor uw gebruiksgeval te vinden en de [ het oplossen van problemengids ](/help/use-case-playbooks/playbooks/troubleshooting.md) te lezen als u om het even welke kwesties ontmoet.
