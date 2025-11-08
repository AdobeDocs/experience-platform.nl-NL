---
title: Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken
description: In de instructies op deze pagina ziet u hoe u een teksteditor kunt gebruiken om in uw lokale omgeving te werken en een documentatiepagina voor uw Experience Platform-bestemming te maken en ter controle te verzenden.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken {#local-authoring}

In de instructies op deze pagina ziet u hoe u een teksteditor kunt gebruiken om in uw lokale omgeving te werken aan de auteur van documentatie en een pull-verzoek (PR) in te dienen. Alvorens door de hier vermelde stappen te gaan, zorg ervoor u [&#x200B; Document uw bestemming in de Doelen van Adobe Experience Platform &#x200B;](./documentation-instructions.md) leest.

>[!TIP]
>
>Zie ook de ondersteunende documentatie in de handleiding voor contribuanten van Adobe:
>
>* [&#x200B; installeer Git en de Authoring hulpmiddelen van de Prijsverhoging &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=nl-NL)
>* &lbrace;de plaats van de Git van de opstelling plaatselijk voor documentatie [&#128279;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL)
>* [&#x200B; GitHub bijdragewerkschema voor belangrijke veranderingen &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=nl-NL).

## Verbind met GitHub en opstelling uw lokale auteursmilieu {#set-up-environment}

1. Blader in uw browser naar `https://github.com/AdobeDocs/experience-platform.nl-NL`
2. Aan [&#x200B; vork &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL#fork-the-repository) de bewaarplaats, klik **Fork** zoals hieronder getoond. Dit leidt tot een exemplaar van de bewaarplaats van Experience Platform in uw eigen rekening GitHub.

   ![&#x200B; de documentatiebewaarplaats van Adobe van het Fork &#x200B;](../assets/docs-framework/ssd-fork-repository.gif)

3. Kloont de opslagplaats naar uw lokale computer. Selecteer **Code > HTTPS > Open met Desktop GitHub**, zoals hieronder getoond. Zorg ervoor u [&#x200B; geïnstalleerde Desktop GitHub &#x200B;](https://desktop.github.com/) hebt. Voor verdere verwijzing, lees [&#x200B; een lokale kloon van de bewaarplaats &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=nl-NL#create-a-local-clone-of-the-repository) in de de contributorgids van Adobe creëren.

   ![&#x200B; de documentatiebewaarplaats van Adobe van de Kloon aan lokaal milieu &#x200B;](../assets/docs-framework/clone-local.png)

4. Navigeer in uw lokale bestandsstructuur naar `experience-platform.en/help/destinations/catalog/[...]` , waar `[...]` de gewenste categorie voor uw doel is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan Experience Platform, selecteert u de map `personalization` .

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. Uw documentatiepagina is gebaseerd op het [&#x200B; zelfbedienings bestemmingsmalplaatje &#x200B;](../docs-framework/self-service-template.md). Download het [&#x200B; bestemmingsmalplaatje &#x200B;](../assets/docs-framework/yourdestination-template.zip). Pak het uit en extraheer het bestand `yourdestination-template.md` naar de map die in stap 4 hierboven is vermeld.  Wijzig de naam van het bestand in `YOURDESTINATION.md` , waarbij UW BESTEMMING de naam van uw bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand de naam `moviestar.md` .
2. Open uw nieuw dossier in uw [&#x200B; tekstredacteur van keus &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=nl-NL#understand-markdown-editors). Adobe adviseert dat u [&#x200B; Code van Visual Studio &#x200B;](https://code.visualstudio.com/) gebruikt en de Verkennende uitbreiding van de Markeringen van Adobe installeert. Als u de extensie wilt installeren, opent u Visual Studio-code, selecteert u het tabblad **[!DNL Extensions]** links van het scherm en zoekt u naar `adobe markdown authoring` . Selecteer de extensie en klik op **[!DNL Install]** .
   ![&#x200B; installeer Adobe Markdown Authoring uitbreiding &#x200B;](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Bewerk de sjabloon met relevante informatie voor uw doel. Volg de instructies in de sjabloon.
4. Ga voor alle schermafbeeldingen of afbeeldingen die u aan de documentatie wilt toevoegen naar `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]` , waar `[...]` de gewenste categorie voor uw doel is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan Experience Platform, selecteert u de map `personalization` . Maak een nieuwe map voor uw bestemming en sla uw afbeeldingen hier op. U moet er een koppeling naar maken vanaf de pagina die u ontwerpt. Zie [&#x200B; instructies hoe te om aan beelden &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=nl-NL#link-to-images) te verbinden.
5. Sla het bestand waaraan u werkt op als u klaar bent.

## De documentatie ter controle verzenden {#submit-review}

>[!TIP]
>
>U kunt hier niets breken. Door de instructies in deze sectie te volgen, stelt u eenvoudig een documentupdate voor. Uw voorgestelde update wordt goedgekeurd of bewerkt door het Adobe Experience Platform-documentatieteam.

1. In de Desktop van GitHub, creeer een werkende tak voor uw updates en selecteer **publiceer tak** om de tak aan GitHub te publiceren.

![&#x200B; Nieuwe vertakking lokale &#x200B;](../assets/docs-framework/new-branch-local.gif)

1. In de Desktop van GitHub, [&#x200B; begaat &#x200B;](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) uw werk, zoals hieronder getoond.

   ![&#x200B; lokale Vastleggen &#x200B;](../assets/docs-framework/commit-local.png)

1. In Desktop GitHub, [&#x200B; duw &#x200B;](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) uw werk aan de [&#x200B; verre &#x200B;](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) tak, zoals hieronder getoond.

   ![&#x200B; duw uw begaat &#x200B;](../assets/docs-framework/push-local-to-remote.png)

1. Open in de GitHub-webinterface een pull-aanvraag (PR) om uw werkende vertakking samen te voegen in de hoofdvertakking van de Adobe-documentatieopslagplaats. Zorg ervoor de tak u aan werkte wordt geselecteerd en selecteert **bijdraagt > Open trekkingsverzoek**.

   ![&#x200B; creeer trektrekverzoek &#x200B;](../assets/docs-framework/ssd-create-pull-request-1.gif)

1. Controleer of de basis- en vergelijkingsvertakkingen correct zijn. Voeg een nota aan PR toe, beschrijvend uw update, en selecteer **creeer trekkingsverzoek**. Dit opent een PR om de werkende tak van uw vork in de hoofdtak van de bewaarplaats van Adobe samen te voegen.

   >[!TIP]
   >
   >Verlaat **uitgeeft door instandhouders** geselecteerde checkbox toestaat zodat het de documentatieteam van Adobe aan PR kan uitgeven.

   ![&#x200B; creeer trekkingsverzoek aan de documentatiebewaarplaats van Adobe &#x200B;](../assets/docs-framework/ssd-create-pull-request-2.png)

1. Op dit moment wordt een melding weergegeven waarin u wordt gevraagd de Adobe Contributor License Agreement (CLA) te ondertekenen. Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

1. U kunt bevestigen dat het trekkingsverzoek is voorgelegd door de **verzoeken van de Trek** tabel in `https://github.com/AdobeDocs/experience-platform.nl-NL` te inspecteren.

![&#x200B; PR succesvol &#x200B;](../assets/docs-framework/ssd-pr-successful.png)

1. Bedankt! Het Adobe-documentatieteam zal de PR bereiken voor het geval er wijzigingen nodig zijn en u laten weten wanneer de documentatie zal worden gepubliceerd.

>[!TIP]
>
>Om beelden en verbindingen aan uw documentatie toe te voegen, en voor andere vragen rond Markering, lees [&#x200B; Gebruikend Markdown &#x200B;](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=nl-NL) in Adobe het samenwerken schrijvende gids.
