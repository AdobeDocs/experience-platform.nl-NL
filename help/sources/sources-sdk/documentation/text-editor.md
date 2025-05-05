---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Een teksteditor in uw lokale omgeving gebruiken om een documentatiepagina voor bronnen te maken
description: Dit document bevat stappen voor het gebruik van uw lokale omgeving bij het schrijven van documentatie voor uw bron en het indienen van een pull-verzoek (PR).
exl-id: 4cc89d1d-bc42-473d-ba54-ab3d1a2cd0d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# Een teksteditor in uw lokale omgeving gebruiken om een pagina met brondocumentatie te maken

Dit document bevat stappen voor het gebruik van uw lokale omgeving bij het schrijven van documentatie voor uw bron en het indienen van een pull-verzoek (PR).

>[!TIP]
>
>De volgende documenten uit de bijdragende gids van Adobe kunnen worden gebruikt om uw documentatieproces verder te steunen: <ul><li>[ installeer Git en de Authoring hulpmiddelen van de Prijsverhoging ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=nl-NL)</li><li>&lbrace;de plaats van de Git van de opstelling plaatselijk voor documentatie [&#128279;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL)</li><li>[ GitHub bijdragewerkschema voor belangrijkste veranderingen ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=nl-NL)</li></ul>

## Vereisten

Het volgende leerprogramma vereist dat u Desktop GitHub hebt die op uw lokale machine wordt geïnstalleerd. Als u geen Desktop GitHub hebt, kunt u de toepassing [ hier ](https://desktop.github.com/) downloaden.

## Verbind met GitHub en opstelling uw lokale auteursmilieu

De eerste stap in vestiging uw lokaal auteursmilieu moet aan de [ bewaarplaats van Adobe Experience Platform navigeren GitHub ](https://github.com/AdobeDocs/experience-platform.en).

![ platform-repo ](../assets/platform-repo.png)

Voor de belangrijkste pagina van de bewaarplaats van Experience Platform GitHub, uitgezochte **Fork**.

![ vork ](../assets/fork.png)

Om de bewaarplaats aan uw lokale machine te klonen, selecteer **Code**. Van het dropdown menu dat verschijnt, selecteert **HTTPS** en dan, selecteert **Open met Desktop GitHub**.

>[!TIP]
>
>Voor meer informatie, zie het leerprogramma op [ de plaats van de Plaats van de Plaats plaatselijk voor documentatie ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL#create-a-local-clone-of-the-repository).

![ open-git-Desktop ](../assets/open-git-desktop.png)

Daarna, sta enkele ogenblikken voor Desktop GitHub toe om de `experience-platform.en` bewaarplaats te klonen.

![ klonen ](../assets/cloning.png)

Zodra het het klonen proces volledig is, hoofd aan Desktop GitHub om een nieuwe tak tot stand te brengen. Selecteer **Hoofd** van de hoogste navigatie en selecteer dan **Nieuwe tak**

![ nieuw-tak ](../assets/new-branch.png)

In popover paneel dat verschijnt, ga een beschrijvende naam voor uw tak in, en selecteer dan **tak** creëren.

![ creeer-tak-vs ](../assets/create-branch-vs.png)

Daarna, uitgezochte **publiceer tak**.

![ publiceren-tak ](../assets/publish-branch.png)

## Auteur de documentatiepagina voor uw bron

Met de bewaarplaats die aan uw lokale machine en een nieuwe gecreeerde tak wordt gekloond, kunt u nu beginnen de documentatiepagina voor uw nieuwe bron door de [ tekstredacteur van uw keus ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=nl-NL#understand-markdown-editors) te ontwerpen.

Adobe adviseert dat u [ Code van Visual Studio ](https://code.visualstudio.com/) gebruikt en dat u de Authoring van de Markeringen van Adobe uitbreiding installeert. Om de uitbreiding te installeren, lanceer de Code van Visual Studio, en selecteer dan het **lusje van Uitbreidingen** van de linkernavigatie.

![ uitbreiding ](../assets/extension.png)

Daarna, ga `Adobe Markdown Authoring` in de onderzoeksbar in en selecteer dan **installeer** van de pagina die verschijnt.

![ installeer ](../assets/install.png)

Met uw lokale machine klaar, download het [ malplaatje van de brondocumentatie ](../assets/api-template.zip) en haal het dossier aan `experience-platform.en/help/sources/tutorials/api/create/...` met [`...`] die de categorie van uw keus vertegenwoordigen. Als u bijvoorbeeld een databasebron maakt, selecteert u de databasemap.

Volg ten slotte de instructies in de sjabloon en bewerk de sjabloon met de relevante informatie over de bron.

![ geef-malplaatje uit ](../assets/edit-template.png)

## De documentatie ter controle verzenden

Als u een pull-verzoek (PR) wilt maken en de documentatie ter controle wilt verzenden, slaat u uw werk eerst op in [!DNL Visual Studio Code] (of de door u gekozen teksteditor). Daarna, gebruikend Desktop GitHub, ga een begaat bericht in en selecteer **vastleggen om bron-documentatie** tot stand te brengen.

![ bega-vs ](../assets/commit-vs.png)

Daarna, uitgezochte **Push oorsprong** om uw werk aan de verre tak te uploaden.

![ duw-oorsprong ](../assets/push-origin.png)

Om een trekkrachtverzoek tot stand te brengen, creeer **het Volledige Verzoek**.

![ creeer-pr-vs ](../assets/create-pr-vs.png)

Zorg ervoor dat de basis- en vergelijkingsvertakkingen correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer dan **trekken verzoek** creëren. Dit opent een PR om de werkende tak van uw werk in de hoofdtak van de bewaarplaats van Adobe samen te voegen.

>[!TIP]
>
>Verlaat **uitgeeft door instandhouders** geselecteerde checkbox toestaan om ervoor te zorgen dat het de documentatieteam van Adobe aan PR kan uitgeven.

![ creeer-pr ](../assets/create-pr.png)

U kunt bevestigen dat het trekkingsverzoek is voorgelegd door het lusje van trekkingsverzoeken in https://github.com/AdobeDocs/experience-platform.en te inspecteren.

![ bevestigen-pr ](../assets/confirm-pr.png)
