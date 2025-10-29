---
title: Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen
description: De instructies op deze pagina tonen u hoe te om de het Webinterface te gebruiken GitHub aan auteur een documentatiepagina voor uw bestemming van Experience Platform en het voor overzicht voor te leggen.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: ff094c0c2c75e097140626d77478b8da9a7edf04
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen {#github-interface}

De instructies tonen hieronder u hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen. Alvorens door de hier vermelde stappen te gaan, zorg ervoor u [&#x200B; Document uw bestemming in de Doelen van Adobe Experience Platform &#x200B;](./documentation-instructions.md) leest.

>[!TIP]
>
>Zie ook de ondersteunende documentatie in de handleiding voor contribuanten van Adobe:
>
>* [&#x200B; installeer Git en de Authoring hulpmiddelen van de Prijsverhoging &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* &lbrace;de plaats van de Git van de opstelling plaatselijk voor documentatie [&#128279;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [&#x200B; GitHub bijdragewerkschema voor belangrijke veranderingen &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Opstelling uw GitHub auteursmilieu {#set-up-environment}

1. Navigeer in uw browser naar `https://github.com/AdobeDocs/experience-platform.en` .
1. Aan [&#x200B; vork &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) de bewaarplaats, klik **Fork** zoals hieronder getoond. Dit leidt tot een exemplaar van de bewaarplaats van Experience Platform in uw eigen rekening GitHub.

   ![&#x200B; de documentatiebewaarplaats van Adobe van het Fork &#x200B;](../assets/docs-framework/ssd-fork-repository.gif)

1. Maak op uw vork van de repository een nieuwe vertakking voor uw project, zoals hieronder wordt weergegeven. Gebruik deze nieuwe vertakking voor uw werk.

   ![&#x200B; creeer nieuwe tak GitHub &#x200B;](../assets/docs-framework/new-branch-github.gif)

1. Navigeer in de GitHub-mapstructuur van de forked-gegevensopslagruimte naar `experience-platform.en/help/destinations/catalog/[...]` , waarbij `[...]` de gewenste categorie voor uw bestemming is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan Experience Platform, selecteert u de categorie `personalization` . Selecteer **toevoegen dossier > creëren nieuw dossier**.

   ![&#x200B; voeg nieuw dossier &#x200B;](../assets/docs-framework/github-navigate-and-create-file.gif) toe

1. Geef uw bestemming een naam `YOURDESTINATION.md` , waarbij UW DOELSTELLING de naam van uw bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand de naam `moviestar.md` .

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. U zult de inhoud van uw bestemmingspagina tot stand brengen die op het [&#x200B; wordt gebaseerd documentatie zelfbedienings malplaatje &#x200B;](./self-service-template.md). **[Download](../assets/docs-framework/yourdestination-template.zip)** het malplaatje en unzip het om het `.md` dossiermalplaatje te halen.
1. Plak en geef de inhoud van het malplaatje met relevante informatie voor uw bestemming in een online prijsdalingsredacteur, zoals [&#x200B; dillinger.io &#x200B;](https://dillinger.io/) uit. Volg de instructies in de sjabloon voor meer informatie over wat u moet invullen en welke alinea&#39;s kunnen worden verwijderd.

   >[!TIP]
   >
   >U kunt uw browservenster op elk gewenst moment sluiten en later opnieuw openen. Uw werk wordt automatisch opgeslagen en u zult op u wachten wanneer u browser opnieuw opent.
1. Kopieer de inhoud van de prijsverhogingsredacteur in uw nieuw dossier in GitHub.
1. Voor om het even welke screenshots of beelden die u op het gebruiken van plan bent, gebruik de interface GitHub om de dossiers aan `experience-platform.en/help/destinations/assets/catalog/[...]` te uploaden, waar `[...]` de gewenste categorie voor uw bestemming is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan Experience Platform, selecteert u de categorie `personalization` . U moet een koppeling maken naar de afbeeldingen op de pagina die u maakt. Zie [&#x200B; instructies hoe te om aan beelden &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images) te verbinden.

   ![&#x200B; upload beeld aan GitHub &#x200B;](../assets/docs-framework/upload-image.gif)

1. Sla het bestand op in de vertakking als u klaar bent.

   ![&#x200B; Bevestig dossierverwezenlijking &#x200B;](../assets/docs-framework/ssd-confirm-file-creation.png)

## De documentatie ter controle verzenden {#submit-review}

>[!TIP]
>
>U kunt hier niets breken. Door de instructies in deze sectie te volgen, stelt u eenvoudig een documentupdate voor. Uw voorgestelde update wordt goedgekeurd of bewerkt door het Adobe Experience Platform-documentatieteam.

1. Nadat u het bestand hebt opgeslagen en de gewenste afbeeldingen hebt geüpload, kunt u een pull-verzoek (PR) openen om uw werkvertakking samen te voegen in de hoofdvertakking van de Adobe-documentatieopslagplaats. Zorg ervoor de tak die u aan werkte wordt geselecteerd en selecteer **Contribute > Open trekkingsverzoek**.

   ![&#x200B; creeer trektrekverzoek &#x200B;](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Controleer of de basis- en vergelijkingsvertakkingen correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer **creeer trekkingsverzoek**. Dit opent een PR om de werkende tak van uw vork in de hoofdtak van de bewaarplaats van Adobe samen te voegen.

   >[!TIP]
   >
   >Verlaat **uitgeeft door instandhouders** geselecteerde checkbox toestaat zodat het de documentatieteam van Adobe aan PR kan uitgeven.

   ![&#x200B; creeer trekkingsverzoek aan de documentatiebewaarplaats van Adobe &#x200B;](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Op dit moment wordt een melding weergegeven waarin u wordt gevraagd de Adobe Contributor License Agreement (CLA) te ondertekenen. Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

1. U kunt bevestigen dat het trekkingsverzoek is voorgelegd door de **verzoeken van de Trek** tabel in `https://github.com/AdobeDocs/experience-platform.en` te inspecteren.

   ![&#x200B; PR succesvol &#x200B;](../assets/docs-framework/ssd-pr-successful.png)

1. Bedankt! Het Adobe-documentatieteam zal de PR bereiken voor het geval er wijzigingen nodig zijn en u laten weten wanneer de documentatie zal worden gepubliceerd.

>[!TIP]
>
>Om beelden en verbindingen aan uw documentatie toe te voegen, en voor andere vragen rond Markering, lees [&#x200B; Gebruikend Markdown &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) in Adobe het samenwerken schrijvende gids.
