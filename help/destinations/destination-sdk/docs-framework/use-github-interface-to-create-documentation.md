---
title: 'Gebruik de het Webinterface van GitHub om een pagina van de bestemmingsdocumentatie tot stand te brengen '
seo-title: Use the GitHub web interface to create a destination documentation page
description: De instructies op deze pagina tonen u hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek voor te leggen.
seo-description: The instructions on this page show you how to use the GitHub web interface to author documentation and submit a pull request.
exl-id: 4780e05e-3d1d-4f1b-8441-df28d09c1a88
source-git-commit: d2452bf0e59866d3deca57090001c4c5a0935525
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 0%

---

# Gebruik de het Webinterface van GitHub om een pagina van de bestemmingsdocumentatie tot stand te brengen {#github-interface}

De instructies tonen hieronder u hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen. Voordat u de hier aangegeven stappen doorloopt, moet u [Uw doel documenteren in Adobe Experience Platform-doelen](./documentation-instructions.md).

>[!TIP]
>
>Raadpleeg ook de ondersteunende documentatie bij de Adobe:
>* [Gereedschappen voor Git- en Markeringsontwerp installeren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Git-opslagplaats lokaal instellen voor documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [GitHub-bijdrageworkflow voor grote wijzigingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Opstelling uw GitHub auteursmilieu {#set-up-environment}

1. Navigeer in uw browser naar `https://github.com/AdobeDocs/experience-platform.en`.
2. Als u [vork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) wilt opslaan in de opslagplaats, klikt u op **Fork** zoals in de onderstaande afbeelding wordt getoond.

   ![Documentatieregister voor vork Adobe](./assets/ssd-fork-repo.png)

3. Maak op uw vork van de repository een nieuwe vertakking voor uw project, zoals hieronder wordt weergegeven. Gebruik deze nieuwe vertakking voor uw werk.

   ![Nieuwe GitHub-vertakking maken](./assets/new-branch-github.gif)

4. Navigeer in de GitHub-mapstructuur van de forked-opslagplaats naar `experience-platform.en/help/destinations/catalog/[...]`, waarbij `[...]` de gewenste categorie voor uw bestemming is. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de categorie `personalization`. Selecteer **Bestand toevoegen > Nieuw bestand maken**.

   ![Nieuw bestand toevoegen](./assets/github-navigate-and-create-file.gif)

5. Geef uw bestemming `YOURDESTINATION.md` een naam, waarbij UW BESTEMMING de naam van uw bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand `moviestar.md` een naam.

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. U zult de inhoud van uw bestemmingspagina tot stand brengen die op [documentzelf-dienstmalplaatje](./self-service-template.md) wordt gebaseerd. **[De sjabloon](assets/yourdestination-template.zip)** downloaden en uitpakken om de  `.md` bestandssjabloon te extraheren.
2. Plak en bewerk de inhoud van de sjabloon met relevante informatie voor uw bestemming in een online markeringseditor, zoals [dillinger.io](https://dillinger.io/). Volg de instructies in de sjabloon voor meer informatie over wat u moet invullen en welke alinea&#39;s kunnen worden verwijderd.
3. Kopieer de inhoud van de prijsverhogingsredacteur in uw nieuw dossier in GitHub.
4. Voor om het even welke screenshots of beelden die u op het gebruiken van plan bent, gebruik de interface GitHub om de dossiers aan `experience-platform.en/help/destinations/assets/catalog/[...]` te uploaden, waar `[...]` de gewenste categorie voor uw bestemming is. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de categorie `personalization`. U moet een koppeling maken naar de afbeeldingen op de pagina die u maakt. Zie [instructies voor het koppelen naar afbeeldingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).

   ![Afbeelding uploaden naar GitHub](./assets/upload-image.gif)

5. Sla het bestand op in de vertakking als u klaar bent.

![Maken van bestand bevestigen](./assets/ssd-confirm-file-creation.png)

## De documentatie ter controle verzenden {#submit-review}

1. Nadat u het bestand hebt opgeslagen en de gewenste afbeeldingen hebt geüpload, kunt u een pull-verzoek (PR) openen om uw werkvertakking samen te voegen in de master vertakking van de documentatieopslagplaats van Adobe. Zorg ervoor dat de vertakking waaraan u hebt gewerkt, is geselecteerd en selecteer **Verzoek opvullen**.

![pull-verzoek maken](./assets/ssd-create-pull-request-1.png)

1. Zorg ervoor dat de basis en vergelijkingstakken correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer **Create trekkingsverzoek**. Dit opent een PR om de werkende tak van uw vork in de master tak van de opslagplaats van de Adobe samen te voegen.

   >[!TIP]
   >
   >Laat het selectievakje **Bewerkingen door onderhoudspersoneel toestaan** ingeschakeld zodat het documentatieteam Adobe wijzigingen in de PR kan aanbrengen.

   ![Een pull-verzoek maken naar de gegevensopslagplaats van Adobe-documentatie](./assets/ssd-create-pull-request-2.png)

1. Op dit punt, lijkt een bericht dat u ertoe aanzet om de Overeenkomst van de Vergunning van de Medewerker van de Adobe te ondertekenen (CLA). Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

1. U kunt bevestigen dat het trekkingsverzoek is voorgelegd door **Pull- verzoeken** tabel in `https://github.com/AdobeDocs/experience-platform.en` te inspecteren.

   ![PR is gelukt](./assets/ssd-pr-successful.png)

1. Bedankt! Het documentatieteam van de Adobe zal in het PR bereiken voor het geval dat om het even welk uitgeeft wordt vereist en u te laten weten wanneer de documentatie zal worden gepubliceerd.

>[!TIP]
>
>Als u afbeeldingen en koppelingen wilt toevoegen aan uw documentatie en voor andere vragen over Markdown, leest u [Using Markdown](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en) in de handleiding voor gezamenlijk schrijven van Adobe.
