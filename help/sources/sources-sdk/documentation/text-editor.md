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
>De volgende documenten uit de bijdragende gids van Adobe kunnen worden gebruikt om uw documentatieproces verder te steunen: <ul><li>[&#x200B; installeer Git en de Authoring hulpmiddelen van de Prijsverhoging &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=nl-NL)</li><li>&lbrace;de plaats van de Git van de opstelling plaatselijk voor documentatie [&#128279;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL)</li><li>[&#x200B; GitHub bijdragewerkschema voor belangrijkste veranderingen &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=nl-NL)</li></ul>

## Vereisten

Het volgende leerprogramma vereist dat u Desktop GitHub hebt die op uw lokale machine wordt geïnstalleerd. Als u geen Desktop GitHub hebt, kunt u de toepassing [&#x200B; hier &#x200B;](https://desktop.github.com/) downloaden.

## Verbind met GitHub en opstelling uw lokale auteursmilieu

De eerste stap in vestiging uw lokaal auteursmilieu moet aan de [&#x200B; bewaarplaats van Adobe Experience Platform navigeren GitHub &#x200B;](https://github.com/AdobeDocs/experience-platform.nl-NL).

![&#x200B; platform-repo &#x200B;](../assets/platform-repo.png)

Voor de belangrijkste pagina van de bewaarplaats van Experience Platform GitHub, uitgezochte **Fork**.

![&#x200B; vork &#x200B;](../assets/fork.png)

Om de bewaarplaats aan uw lokale machine te klonen, selecteer **Code**. Van het dropdown menu dat verschijnt, selecteert **HTTPS** en dan, selecteert **Open met Desktop GitHub**.

>[!TIP]
>
>Voor meer informatie, zie het leerprogramma op [&#x200B; de plaats van de Plaats van de Plaats plaatselijk voor documentatie &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL#create-a-local-clone-of-the-repository).

![&#x200B; open-git-Desktop &#x200B;](../assets/open-git-desktop.png)

Daarna, sta enkele ogenblikken voor Desktop GitHub toe om de `experience-platform.en` bewaarplaats te klonen.

![&#x200B; klonen &#x200B;](../assets/cloning.png)

Zodra het het klonen proces volledig is, hoofd aan Desktop GitHub om een nieuwe tak tot stand te brengen. Selecteer **Hoofd** van de hoogste navigatie en selecteer dan **Nieuwe tak**

![&#x200B; nieuw-tak &#x200B;](../assets/new-branch.png)

In popover paneel dat verschijnt, ga een beschrijvende naam voor uw tak in, en selecteer dan **tak** creëren.

![&#x200B; creeer-tak-vs &#x200B;](../assets/create-branch-vs.png)

Daarna, uitgezochte **publiceer tak**.

![&#x200B; publiceren-tak &#x200B;](../assets/publish-branch.png)

## Auteur de documentatiepagina voor uw bron

Met de bewaarplaats die aan uw lokale machine en een nieuwe gecreeerde tak wordt gekloond, kunt u nu beginnen de documentatiepagina voor uw nieuwe bron door de [&#x200B; tekstredacteur van uw keus &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=nl-NL#understand-markdown-editors) te ontwerpen.

Adobe adviseert dat u [&#x200B; Code van Visual Studio &#x200B;](https://code.visualstudio.com/) gebruikt en dat u de Authoring van de Markeringen van Adobe uitbreiding installeert. Om de uitbreiding te installeren, lanceer de Code van Visual Studio, en selecteer dan het **lusje van Uitbreidingen** van de linkernavigatie.

![&#x200B; uitbreiding &#x200B;](../assets/extension.png)

Daarna, ga `Adobe Markdown Authoring` in de onderzoeksbar in en selecteer dan **installeer** van de pagina die verschijnt.

![&#x200B; installeer &#x200B;](../assets/install.png)

Met uw lokale machine klaar, download het [&#x200B; malplaatje van de brondocumentatie &#x200B;](../assets/api-template.zip) en haal het dossier aan `experience-platform.en/help/sources/tutorials/api/create/...` met [`...`] die de categorie van uw keus vertegenwoordigen. Als u bijvoorbeeld een databasebron maakt, selecteert u de databasemap.

Volg ten slotte de instructies in de sjabloon en bewerk de sjabloon met de relevante informatie over de bron.

![&#x200B; geef-malplaatje uit &#x200B;](../assets/edit-template.png)

## De documentatie ter controle verzenden

Als u een pull-verzoek (PR) wilt maken en de documentatie ter controle wilt verzenden, slaat u uw werk eerst op in [!DNL Visual Studio Code] (of de door u gekozen teksteditor). Daarna, gebruikend Desktop GitHub, ga een begaat bericht in en selecteer **vastleggen om bron-documentatie** tot stand te brengen.

![&#x200B; bega-vs &#x200B;](../assets/commit-vs.png)

Daarna, uitgezochte **Push oorsprong** om uw werk aan de verre tak te uploaden.

![&#x200B; duw-oorsprong &#x200B;](../assets/push-origin.png)

Om een trekkrachtverzoek tot stand te brengen, creeer **het Volledige Verzoek**.

![&#x200B; creeer-pr-vs &#x200B;](../assets/create-pr-vs.png)

Zorg ervoor dat de basis- en vergelijkingsvertakkingen correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer dan **trekken verzoek** creëren. Dit opent een PR om de werkende tak van uw werk in de hoofdtak van de bewaarplaats van Adobe samen te voegen.

>[!TIP]
>
>Verlaat **uitgeeft door instandhouders** geselecteerde checkbox toestaan om ervoor te zorgen dat het de documentatieteam van Adobe aan PR kan uitgeven.

![&#x200B; creeer-pr &#x200B;](../assets/create-pr.png)

U kunt bevestigen dat het trekkingsverzoek is voorgelegd door het lusje van trekkingsverzoeken in https://github.com/AdobeDocs/experience-platform.nl-NL te inspecteren.

![&#x200B; bevestigen-pr &#x200B;](../assets/confirm-pr.png)
