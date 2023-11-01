---
title: Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen
description: De instructies op deze pagina tonen u hoe te om de het Webinterface te gebruiken GitHub aan auteur een documentatiepagina voor uw bestemming van het Experience Platform en het voor overzicht voor te leggen.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# Gebruik de GitHub Webinterface om een pagina van de bestemmingsdocumentatie tot stand te brengen {#github-interface}

De instructies tonen hieronder u hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen. Voordat u de hier aangegeven stappen doorloopt, moet u ervoor zorgen dat u [Uw doel documenteren in Adobe Experience Platform-doelen](./documentation-instructions.md).

>[!TIP]
>
>Raadpleeg ook de ondersteunende documentatie in de handleiding voor contribuanten van de Adobe:
>* [Gereedschappen voor Git- en Markeringsontwerp installeren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Git-opslagplaats lokaal instellen voor documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [GitHub-bijdrageworkflow voor grote wijzigingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Opstelling uw GitHub auteursmilieu {#set-up-environment}

1. Blader in uw browser naar `https://github.com/AdobeDocs/experience-platform.en`.
2. Naar [vork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) in de repository klikt u op **Vork** zoals hieronder weergegeven. Dit leidt tot een exemplaar van de bewaarplaats van het Experience Platform in uw eigen rekening GitHub.

   ![Documentatieopslagplaats voor Adobe van vork](../assets/docs-framework/ssd-fork-repository.gif)

3. Maak op uw vork van de repository een nieuwe vertakking voor uw project, zoals hieronder wordt weergegeven. Gebruik deze nieuwe vertakking voor uw werk.

   ![Nieuwe GitHub-vertakking maken](../assets/docs-framework/new-branch-github.gif)

4. In de de omslagstructuur van GitHub van de forked bewaarplaats, navigeer aan `experience-platform.en/help/destinations/catalog/[...]`, waarbij `[...]` is de gewenste rubriek voor uw bestemming. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de optie `personalization` categorie. Selecteren **Bestand toevoegen > Nieuw bestand maken**.

   ![Nieuw bestand toevoegen](../assets/docs-framework/github-navigate-and-create-file.gif)

5. Geef uw bestemming een naam `YOURDESTINATION.md`, waarbij YOURDESTINATION de naam van je bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand een naam `moviestar.md`.

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. U maakt de inhoud van de doelpagina op basis van de [zelfservicesjabloon voor documentatie](./self-service-template.md). **[Downloaden](../assets/docs-framework/yourdestination-template.zip)** de sjabloon uit en decomprimeer deze om de `.md` bestandssjabloon.
2. Plak en bewerk de inhoud van de sjabloon met relevante informatie voor uw doel in een online markeringseditor, zoals [dillinger.io](https://dillinger.io/). Volg de instructies in de sjabloon voor meer informatie over wat u moet invullen en welke alinea&#39;s kunnen worden verwijderd.

   >[!TIP]
   >
   >U kunt uw browservenster op elk gewenst moment sluiten en later opnieuw openen. Uw werk wordt automatisch opgeslagen en u zult op u wachten wanneer u browser opnieuw opent.
3. Kopieer de inhoud van de prijsverhogingsredacteur in uw nieuw dossier in GitHub.
4. Voor om het even welke screenshots of beelden die u op het gebruiken van plan bent, gebruik de interface GitHub om de dossiers te uploaden aan `experience-platform.en/help/destinations/assets/catalog/[...]`, waarbij `[...]` is de gewenste rubriek voor uw bestemming. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de optie `personalization` categorie. U moet een koppeling maken naar de afbeeldingen op de pagina die u maakt. Zie [instructies voor het koppelen naar afbeeldingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).

   ![Afbeelding uploaden naar GitHub](../assets/docs-framework/upload-image.gif)

5. Sla het bestand op in de vertakking als u klaar bent.

![Maken van bestand bevestigen](../assets/docs-framework/ssd-confirm-file-creation.png)

## De documentatie ter controle verzenden {#submit-review}

>[!TIP]
>
>U kunt hier niets breken. Door de instructies in deze sectie te volgen, stelt u eenvoudig een documentupdate voor. Uw voorgestelde update wordt goedgekeurd of bewerkt door het Adobe Experience Platform-documentatieteam.

1. Nadat u het bestand hebt opgeslagen en de gewenste afbeeldingen hebt geüpload, kunt u een pull-verzoek (PR) openen om uw werkvertakking samen te voegen in de hoofdvertakking van de documentatieopslagplaats van de Adobe. Zorg ervoor dat de vertakking is geselecteerd waaraan u hebt gewerkt en selecteer **Contribute > pull-verzoek openen**.

![pull-verzoek maken](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Controleer of de basis- en vergelijkingsvertakkingen correct zijn. Voeg een notitie toe aan de PR, beschrijf de update en selecteer **pull-verzoek maken**. Dit opent een PR om de werkende tak van uw vork in de hoofdtak van de bewaarplaats van de Adobe samen te voegen.

   >[!TIP]
   >
   >Laat de **Bewerkingen door onderhoudsleiders toestaan** Schakel het selectievakje in zodat het documentatieteam van de Adobe de PR kan bewerken.

   ![Een aantrekverzoek maken naar de documentatieopslagplaats van de Adobe](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Op dit punt, lijkt een bericht dat u ertoe aanzet om de Overeenkomst van de Vergunning van de Medewerker van de Adobe (CLA) te ondertekenen. Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

1. U kunt bevestigen dat het trekkingsverzoek is verzonden door de **Pull-aanvragen** tab in `https://github.com/AdobeDocs/experience-platform.en`.

   ![PR succesvol](../assets/docs-framework/ssd-pr-successful.png)

1. Bedankt! Het documentatieteam van de Adobe zal in het PR bereiken als om het even welke veranderingen worden vereist en u te laten weten wanneer de documentatie zal worden gepubliceerd.

>[!TIP]
>
>Als u afbeeldingen en koppelingen wilt toevoegen aan uw documentatie en voor andere vragen over Markdown, leest u [Markering gebruiken](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html) in de handleiding voor gezamenlijk schrijven van Adobe.
