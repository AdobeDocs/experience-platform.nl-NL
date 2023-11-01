---
title: Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken
description: De instructies op deze pagina tonen u hoe te om een tekstredacteur te gebruiken om in uw lokale milieu te werken aan auteur een documentatiepagina voor uw Experience Platform bestemming en het voor overzicht voor te leggen.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken {#local-authoring}

In de instructies op deze pagina ziet u hoe u een teksteditor kunt gebruiken om in uw lokale omgeving te werken aan de auteur van documentatie en een pull-verzoek (PR) in te dienen. Voordat u de hier aangegeven stappen doorloopt, moet u ervoor zorgen dat u [Uw doel documenteren in Adobe Experience Platform-doelen](./documentation-instructions.md).

>[!TIP]
>
>Raadpleeg ook de ondersteunende documentatie in de handleiding voor contribuanten van de Adobe:
>* [Gereedschappen voor Git- en Markeringsontwerp installeren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* [Git-opslagplaats lokaal instellen voor documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)
>* [GitHub-bijdrageworkflow voor grote wijzigingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Verbind met GitHub en opstelling uw lokale auteursmilieu {#set-up-environment}

1. Blader in uw browser naar `https://github.com/AdobeDocs/experience-platform.en`
2. Naar [vork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) in de repository klikt u op **Vork** zoals hieronder weergegeven. Dit leidt tot een exemplaar van de bewaarplaats van het Experience Platform in uw eigen rekening GitHub.

   ![Documentatieopslagplaats voor Adobe van vork](../assets/docs-framework/ssd-fork-repository.gif)

3. Kloont de opslagplaats naar uw lokale computer. Selecteren **Code > HTTPS > Openen met GitHub Desktop**, zoals hieronder weergegeven. Zorg ervoor dat u [GitHub Desktop](https://desktop.github.com/) geïnstalleerd. Lees voor meer informatie [Een lokale kloon maken van de opslagplaats](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository) in de handleiding voor contribuanten van de Adobe.

   ![Documentatieopslagplaats voor Adobe klonen naar lokale omgeving](../assets/docs-framework/clone-local.png)

4. Ga in uw lokale bestandsstructuur naar `experience-platform.en/help/destinations/catalog/[...]`, waarbij `[...]` is de gewenste rubriek voor uw bestemming. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de optie `personalization` map.

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. De documentatiepagina is gebaseerd op de [self-service doelsjabloon](../docs-framework/self-service-template.md). Download de [doelsjabloon](../assets/docs-framework/yourdestination-template.zip). Pak het uit en extraheer het bestand `yourdestination-template.md` in de in stap 4 hierboven vermelde directory.  De naam van het bestand wijzigen `YOURDESTINATION.md`, waarbij YOURDESTINATION de naam van je bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand een naam `moviestar.md`.
2. Open uw nieuwe bestand in uw [teksteditor van keuze](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors). Adobe raadt u aan [Visual Studio-code](https://code.visualstudio.com/) en installeer de Adobe Markdown Authoring-extensie. Om de uitbreiding, de open Code van Visual Studio te installeren, selecteer **[!DNL Extensions]** links op het scherm en zoek naar `adobe markdown authoring`. Selecteer de extensie en klik op **[!DNL Install]**.
   ![De extensie Adobe Markdown Authoring installeren](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Bewerk de sjabloon met relevante informatie voor uw doel. Volg de instructies in de sjabloon.
4. Ga voor alle schermafbeeldingen of afbeeldingen die u wilt toevoegen aan uw documentatie naar `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, waarbij `[...]` is de gewenste rubriek voor uw bestemming. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de optie `personalization` map. Maak een nieuwe map voor uw bestemming en sla uw afbeeldingen hier op. U moet er een koppeling naar maken vanaf de pagina die u ontwerpt. Zie [instructies voor het koppelen naar afbeeldingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images).
5. Sla het bestand waaraan u werkt op als u klaar bent.

## De documentatie ter controle verzenden {#submit-review}

>[!TIP]
>
>U kunt hier niets breken. Door de instructies in deze sectie te volgen, stelt u eenvoudig een documentupdate voor. Uw voorgestelde update wordt goedgekeurd of bewerkt door het Adobe Experience Platform-documentatieteam.

1. In de Desktop van GitHub, creeer een het werk tak voor uw updates en selecteer **Vertakking publiceren** om de vertakking naar GitHub te publiceren.

![Nieuwe lokale vertakking](../assets/docs-framework/new-branch-local.gif)

1. In GitHub Desktop, [begaan](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) uw werk, zoals hieronder getoond.

   ![Lokaal vastleggen](../assets/docs-framework/commit-local.png)

1. In GitHub Desktop, [duwen](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) uw werk aan [extern](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) vertakking, zoals hieronder weergegeven.

   ![Push your commit](../assets/docs-framework/push-local-to-remote.png)

1. In de het Webinterface van GitHub, open een trekkingsverzoek (PR) om uw werkende tak in de hoofdtak van de de documentatiebewaarplaats van de Adobe samen te voegen. Zorg ervoor dat de vertakking die u hebt bewerkt is geselecteerd en selecteer **Contribute > pull-verzoek openen**.

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
