---
title: Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen
description: De instructies op deze pagina tonen u hoe te om de het Webinterface te gebruiken GitHub aan auteur een documentatiepagina voor uw bestemming van het Experience Platform en het voor overzicht voor te leggen.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 0%

---

# Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen {#github-interface}

De instructies tonen hieronder u hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen. Alvorens door de hier vermelde stappen te gaan, zorg ervoor u [ Document uw bestemming in de Doelen van Adobe Experience Platform ](./documentation-instructions.md) leest.

>[!TIP]
>
>Raadpleeg ook de ondersteunende documentatie in de handleiding voor contribuanten van de Adobe:
>* [ installeer Git en de Authoring hulpmiddelen van de Prijsverhoging ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* {de plaats van de Git van de opstelling plaatselijk voor documentatie ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)[
>* [ GitHub bijdragewerkschema voor belangrijke veranderingen ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Opstelling uw GitHub auteursmilieu {#set-up-environment}

1. Navigeer in uw browser naar `https://github.com/AdobeDocs/experience-platform.en` .
2. Aan [ vork ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) de bewaarplaats, klik **Fork** zoals hieronder getoond. Dit leidt tot een exemplaar van de bewaarplaats van het Experience Platform in uw eigen rekening GitHub.

   ![ de documentatiebewaarplaats van de Adobe van het Fork ](../assets/docs-framework/ssd-fork-repository.gif)

3. Maak op uw vork van de repository een nieuwe vertakking voor uw project, zoals hieronder wordt weergegeven. Gebruik deze nieuwe vertakking voor uw werk.

   ![ creeer nieuwe tak GitHub ](../assets/docs-framework/new-branch-github.gif)

4. Navigeer in de GitHub-mapstructuur van de forked-gegevensopslagruimte naar `experience-platform.en/help/destinations/catalog/[...]` , waarbij `[...]` de gewenste categorie voor uw bestemming is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan het Experience Platform, selecteert u de categorie `personalization` . Selecteer **toevoegen dossier > creëren nieuw dossier**.

   ![ voeg nieuw dossier ](../assets/docs-framework/github-navigate-and-create-file.gif) toe

5. Geef uw bestemming een naam `YOURDESTINATION.md` , waarbij UW DOELSTELLING de naam van uw bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand de naam `moviestar.md` .

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. U zult de inhoud van uw bestemmingspagina tot stand brengen die op het [ wordt gebaseerd documentatie zelfbedienings malplaatje ](./self-service-template.md). **[Download](../assets/docs-framework/yourdestination-template.zip)** het malplaatje en unzip het om het `.md` dossiermalplaatje te halen.
2. Plak en geef de inhoud van het malplaatje met relevante informatie voor uw bestemming in een online prijsdalingsredacteur, zoals [ dillinger.io ](https://dillinger.io/) uit. Volg de instructies in de sjabloon voor meer informatie over wat u moet invullen en welke alinea&#39;s kunnen worden verwijderd.

   >[!TIP]
   >
   >U kunt uw browservenster op elk gewenst moment sluiten en later opnieuw openen. Uw werk wordt automatisch opgeslagen en u zult op u wachten wanneer u browser opnieuw opent.
3. Kopieer de inhoud van de prijsverhogingsredacteur in uw nieuw dossier in GitHub.
4. Voor om het even welke screenshots of beelden die u op het gebruiken van plan bent, gebruik de interface GitHub om de dossiers aan `experience-platform.en/help/destinations/assets/catalog/[...]` te uploaden, waar `[...]` de gewenste categorie voor uw bestemming is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan het Experience Platform, selecteert u de categorie `personalization` . U moet een koppeling maken naar de afbeeldingen op de pagina die u maakt. Zie [ instructies hoe te om aan beelden ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images) te verbinden.

   ![ upload beeld aan GitHub ](../assets/docs-framework/upload-image.gif)

5. Sla het bestand op in de vertakking als u klaar bent.

![ Bevestig dossierverwezenlijking ](../assets/docs-framework/ssd-confirm-file-creation.png)

## De documentatie ter controle verzenden {#submit-review}

>[!TIP]
>
>U kunt hier niets breken. Door de instructies in deze sectie te volgen, stelt u eenvoudig een documentupdate voor. Uw voorgestelde update wordt goedgekeurd of bewerkt door het Adobe Experience Platform-documentatieteam.

1. Nadat u het bestand hebt opgeslagen en de gewenste afbeeldingen hebt geüpload, kunt u een pull-verzoek (PR) openen om uw werkvertakking samen te voegen in de hoofdvertakking van de documentatieopslagplaats van de Adobe. Zorg ervoor de tak die u aan werkte wordt geselecteerd en selecteer **Contribute > Open trekkingsverzoek**.

![ creeer trektrekverzoek ](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Controleer of de basis- en vergelijkingsvertakkingen correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer **creeer trekkingsverzoek**. Dit opent een PR om de werkende tak van uw vork in de hoofdtak van de bewaarplaats van de Adobe samen te voegen.

   >[!TIP]
   >
   >Verlaat **uitgeeft door instandhouders** geselecteerde checkbox toestaat zodat het de documentatieteam van de Adobe aan PR kan uitgeven.

   ![ creeer trekkingsverzoek aan de documentatiebewaarplaats van de Adobe ](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Op dit punt, lijkt een bericht dat u ertoe aanzet om de Overeenkomst van de Vergunning van de Medewerker van de Adobe (CLA) te ondertekenen. Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

1. U kunt bevestigen dat het trekkingsverzoek is voorgelegd door de **verzoeken van de Trek** tabel in `https://github.com/AdobeDocs/experience-platform.en` te inspecteren.

   ![ PR succesvol ](../assets/docs-framework/ssd-pr-successful.png)

1. Bedankt! Het documentatieteam van de Adobe zal in het PR bereiken als om het even welke veranderingen worden vereist en u te laten weten wanneer de documentatie zal worden gepubliceerd.

>[!TIP]
>
>Om beelden en verbindingen aan uw documentatie toe te voegen, en voor een andere vragen rond Markering, lees [ Gebruikend Markdown ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) in de samenwerkingsgids van de Adobe het schrijven gids.
