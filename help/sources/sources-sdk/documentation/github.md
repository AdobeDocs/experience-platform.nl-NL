---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Gebruik de Interface van het Web van GitHub om een Pagina van de Documentatie van Bronnen te creëren
description: Dit document verstrekt stappen op hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen.
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: acf1d4b9b2de6e0f674aca1f44b2504f3792327d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Gebruik de het Webinterface van GitHub om een brondocumentatiepagina tot stand te brengen

Dit document verstrekt stappen op hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen.

>[!TIP]
>
>De volgende documenten uit de bijdragende gids van Adobe kunnen worden gebruikt om uw documentatieproces verder te steunen: <ul><li>[&#x200B; installeer Git en de Authoring hulpmiddelen van de Prijsverhoging &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=nl-NL)</li><li>&lbrace;de plaats van de Git van de opstelling plaatselijk voor documentatie [&#128279;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL)</li><li>[&#x200B; GitHub bijdragewerkschema voor belangrijkste veranderingen &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=nl-NL)</li></ul>

## Opstelling uw milieu GitHub

De eerste stap in vestiging uw milieu GitHub moet aan de [&#x200B; bewaarplaats van Adobe Experience Platform navigeren GitHub &#x200B;](https://github.com/AdobeDocs/experience-platform.nl-NL).

![&#x200B; platform-repo &#x200B;](../assets/platform-repo.png)

Daarna, uitgezochte **Vlek**.

![&#x200B; vork &#x200B;](../assets/fork.png)

Zodra de vork volledig is, uitgezochte **belangrijkste** en ga een naam voor uw nieuwe tak in het dropdown menu in dat verschijnt. Zorg ervoor dat u een beschrijvende naam voor uw tak verstrekt aangezien dit zal worden gebruikt om uw werk te bevatten, en selecteer dan **tak** creëren.

![&#x200B; creeer-tak &#x200B;](../assets/create-branch.png)

In de GitHub omslagstructuur van uw forked bewaarplaats, navigeer aan [`experience-platform.en/help/sources/tutorials/api/create/` &#x200B;](https://github.com/AdobeDocs/experience-platform.nl-NL/tree/main/help/sources/tutorials/api/create) en selecteer dan de aangewezen categorie voor uw bron van de lijst. Bijvoorbeeld, als u documentatie voor een nieuwe bron van CRM creeert, uitgezochte **crm**.

>[!TIP]
>
>Als u documentatie voor UI creeert, dan navigeer aan [`experience-platform.en/help/sources/tutorials/ui/create/` &#x200B;](https://github.com/AdobeDocs/experience-platform.nl-NL/tree/main/help/sources/tutorials/ui/create) en selecteer de aangewezen categorie voor uw bron. Als u afbeeldingen wilt toevoegen, navigeert u naar [`experience-platform.en/help/sources/images/tutorials/create/sdk` &#x200B;](https://github.com/AdobeDocs/experience-platform.nl-NL/tree/main/help/sources/images/tutorials/create) en voegt u uw schermafbeeldingen toe aan de map `sdk` .

![&#x200B; crm &#x200B;](../assets/crm.png)

Er wordt een map met bestaande CRM-bronnen weergegeven. Om documentatie voor een nieuwe bron toe te voegen, **voeg dossier** toe en selecteer dan **creeer nieuw dossier** van het drop-down menu dat verschijnt.

![&#x200B; creeer-nieuw-dossier &#x200B;](../assets/create-new-file.png)

Geef het bronbestand een naam `YOURSOURCE.md` waarbij UURSOURCE de naam van uw bron in Experience Platform is. Als uw bedrijf bijvoorbeeld ACME CRM is, moet uw bestandsnaam `acme-crm.md` zijn.

![&#x200B; git-interface &#x200B;](../assets/git-interface.png)

## Auteur de documentatiepagina voor uw bron

Beginnen uw nieuwe bron te documenteren, kleef de inhoud van het [&#x200B; malplaatje van de brondocumentatie &#x200B;](./template.md) in de het Webredacteur van GitHub. U kunt het malplaatje [&#x200B; &#x200B;](../assets/api-template.zip) ook hier downloaden.

Met het malplaatje dat over aan de interface van de Webredacteur van GitHub wordt gekopieerd, volg de instructies die op het malplaatje worden geschetst en geef de waarden uit die relevante informatie voor uw bron bevatten.

![&#x200B; deeg-malplaatje &#x200B;](../assets/paste-template.png)

Als u klaar bent, legt u het bestand in de vertakking vast.

![&#x200B; begaat &#x200B;](../assets/commit.png)

## De documentatie ter controle verzenden

Nadat het bestand is toegewezen, kunt u een pull-verzoek (PR) openen om uw werkvertakking samen te voegen in de hoofdvertakking van de Adobe-documentatieopslagplaats. Zorg ervoor dat de tak u aan hebt gewerkt wordt geselecteerd, en selecteer dan **vergelijken &amp; trekken verzoek**.

![&#x200B; vergelijking-pr &#x200B;](../assets/compare-pr.png)

Zorg ervoor dat de basis- en vergelijkingsvertakkingen correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer dan **trekken verzoek** creëren. Dit opent een PR om de werkende tak van uw werk in de belangrijkste tak van de bewaarplaats van Adobe samen te voegen.

>[!TIP]
>
>Verlaat **uitgeeft door instandhouders** geselecteerde checkbox toestaan om ervoor te zorgen dat het de documentatieteam van Adobe aan PR kan uitgeven.

![&#x200B; creeer-pr &#x200B;](../assets/create-pr.png)

Op dit moment wordt een melding weergegeven waarin u wordt gevraagd de Adobe Contributor License Agreement (CLA) te ondertekenen. Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

U kunt bevestigen dat het trekkingsverzoek is voorgelegd door het lusje van trekkingsverzoeken in https://github.com/AdobeDocs/experience-platform.nl-NL te inspecteren.

![&#x200B; bevestigen-pr &#x200B;](../assets/confirm-pr.png)
