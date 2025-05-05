---
keywords: Experience Platform;home;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Gebruik de Interface van het Web van GitHub om een Pagina van de Documentatie van Bronnen te creëren
description: Dit document verstrekt stappen op hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen.
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Gebruik de het Webinterface van GitHub om een brondocumentatiepagina tot stand te brengen

Dit document verstrekt stappen op hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen.

>[!TIP]
>
>De volgende documenten uit de bijdragende gids van Adobe kunnen worden gebruikt om uw documentatieproces verder te steunen: <ul><li>[ installeer Git en de Authoring hulpmiddelen van de Prijsverhoging ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)</li><li>&lbrace;de plaats van de Git van de opstelling plaatselijk voor documentatie [&#128279;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)</li><li>[ GitHub bijdragewerkschema voor belangrijkste veranderingen ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html)</li></ul>

## Opstelling uw milieu GitHub

De eerste stap in vestiging uw milieu GitHub moet aan de [ bewaarplaats van Adobe Experience Platform navigeren GitHub ](https://github.com/AdobeDocs/experience-platform.en).

![ platform-repo ](../assets/platform-repo.png)

Daarna, uitgezochte **Vlek**.

![ vork ](../assets/fork.png)

Zodra het vork volledig is, selecteer **meester** en ga een naam voor uw nieuwe tak in het dropdown menu in dat verschijnt. Zorg ervoor dat u een beschrijvende naam voor uw tak verstrekt aangezien dit zal worden gebruikt om uw werk te bevatten, en selecteer dan **tak** creëren.

![ creeer-tak ](../assets/create-branch.png)

In de GitHub omslagstructuur van uw forked bewaarplaats, navigeer aan [`experience-platform.en/help/sources/tutorials/api/create/` ](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) en selecteer dan de aangewezen categorie voor uw bron van de lijst. Bijvoorbeeld, als u documentatie voor een nieuwe bron van CRM creeert, uitgezochte **crm**.

>[!TIP]
>
>Als u documentatie voor UI creeert, dan navigeer aan [`experience-platform.en/help/sources/tutorials/ui/create/` ](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) en selecteer de aangewezen categorie voor uw bron. Als u afbeeldingen wilt toevoegen, navigeert u naar [`experience-platform.en/help/sources/images/tutorials/create/sdk` ](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) en voegt u uw schermafbeeldingen toe aan de map `sdk` .

![ crm ](../assets/crm.png)

Er wordt een map met bestaande CRM-bronnen weergegeven. Om documentatie voor een nieuwe bron toe te voegen, **voeg dossier** toe en selecteer dan **creeer nieuw dossier** van het drop-down menu dat verschijnt.

![ creeer-nieuw-dossier ](../assets/create-new-file.png)

Geef het bronbestand een naam `YOURSOURCE.md` waarbij UURSOURCE de naam van uw bron in Experience Platform is. Als uw bedrijf bijvoorbeeld ACME CRM is, moet uw bestandsnaam `acme-crm.md` zijn.

![ git-interface ](../assets/git-interface.png)

## Auteur de documentatiepagina voor uw bron

Beginnen uw nieuwe bron te documenteren, kleef de inhoud van het [ malplaatje van de brondocumentatie ](./template.md) in de het Webredacteur van GitHub. U kunt het malplaatje [&#128279;](../assets/api-template.zip) ook hier downloaden.

Met het malplaatje dat over aan de interface van de Webredacteur van GitHub wordt gekopieerd, volg de instructies die op het malplaatje worden geschetst en geef de waarden uit die relevante informatie voor uw bron bevatten.

![ deeg-malplaatje ](../assets/paste-template.png)

Als u klaar bent, legt u het bestand in de vertakking vast.

![ begaat ](../assets/commit.png)

## De documentatie ter controle verzenden

Nadat het bestand is toegewezen, kunt u een pull-verzoek (PR) openen om uw werkvertakking samen te voegen in de hoofdvertakking van de Adobe-documentatieopslagplaats. Zorg ervoor dat de tak u aan hebt gewerkt wordt geselecteerd, en selecteer dan **vergelijken &amp; trekken verzoek**.

![ vergelijking-pr ](../assets/compare-pr.png)

Zorg ervoor dat de basis- en vergelijkingsvertakkingen correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer dan **trekken verzoek** creëren. Dit opent een PR om de werkende tak van uw werk in de hoofdtak van de bewaarplaats van Adobe samen te voegen.

>[!TIP]
>
>Verlaat **uitgeeft door instandhouders** geselecteerde checkbox toestaan om ervoor te zorgen dat het de documentatieteam van Adobe aan PR kan uitgeven.

![ creeer-pr ](../assets/create-pr.png)

Op dit moment wordt een melding weergegeven waarin u wordt gevraagd de Adobe Contributor License Agreement (CLA) te ondertekenen. Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

U kunt bevestigen dat het trekkingsverzoek is voorgelegd door het lusje van trekkingsverzoeken in https://github.com/AdobeDocs/experience-platform.en te inspecteren.

![ bevestigen-pr ](../assets/confirm-pr.png)
