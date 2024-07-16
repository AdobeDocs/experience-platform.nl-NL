---
title: Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken
description: De instructies op deze pagina tonen u hoe te om een tekstredacteur te gebruiken om in uw lokale milieu te werken aan auteur een documentatiepagina voor uw Experience Platform bestemming en het voor overzicht voor te leggen.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---

# Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken {#local-authoring}

In de instructies op deze pagina ziet u hoe u een teksteditor kunt gebruiken om in uw lokale omgeving te werken aan de auteur van documentatie en een pull-verzoek (PR) in te dienen. Alvorens door de hier vermelde stappen te gaan, zorg ervoor u [ Document uw bestemming in de Doelen van Adobe Experience Platform ](./documentation-instructions.md) leest.

>[!TIP]
>
>Raadpleeg ook de ondersteunende documentatie in de handleiding voor contribuanten van de Adobe:
>* [ installeer Git en de Authoring hulpmiddelen van de Prijsverhoging ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html)
>* {de plaats van de Git van de opstelling plaatselijk voor documentatie ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html)[
>* [ GitHub bijdragewerkschema voor belangrijke veranderingen ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html).

## Verbind met GitHub en opstelling uw lokale auteursmilieu {#set-up-environment}

1. Blader in uw browser naar `https://github.com/AdobeDocs/experience-platform.en`
2. Aan [ vork ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#fork-the-repository) de bewaarplaats, klik **Fork** zoals hieronder getoond. Dit leidt tot een exemplaar van de bewaarplaats van het Experience Platform in uw eigen rekening GitHub.

   ![ de documentatiebewaarplaats van de Adobe van het Fork ](../assets/docs-framework/ssd-fork-repository.gif)

3. Kloont de opslagplaats naar uw lokale computer. Selecteer **Code > HTTPS > Open met Desktop GitHub**, zoals hieronder getoond. Zorg ervoor u ](https://desktop.github.com/) geïnstalleerde Desktop GitHub [ hebt. Voor verdere verwijzing, leest [ een lokale kloon van de bewaarplaats ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html#create-a-local-clone-of-the-repository) in de de bijdragegids van de Adobe creëren.

   ![ de documentatiebewaarplaats van de Adobe van de Kloon aan lokaal milieu ](../assets/docs-framework/clone-local.png)

4. Navigeer in uw lokale bestandsstructuur naar `experience-platform.en/help/destinations/catalog/[...]` , waar `[...]` de gewenste categorie voor uw doel is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan het Experience Platform, selecteert u de map `personalization` .

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. Uw documentatiepagina is gebaseerd op het [ zelfbedienings bestemmingsmalplaatje ](../docs-framework/self-service-template.md). Download het [ bestemmingsmalplaatje ](../assets/docs-framework/yourdestination-template.zip). Pak het uit en extraheer het bestand `yourdestination-template.md` naar de map die in stap 4 hierboven is vermeld.  Wijzig de naam van het bestand in `YOURDESTINATION.md` , waarbij UW BESTEMMING de naam van uw bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand de naam `moviestar.md` .
2. Open uw nieuw dossier in uw [ tekstredacteur van keus ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html#understand-markdown-editors). De Adobe adviseert dat u [ Code van Visual Studio ](https://code.visualstudio.com/) gebruikt en de Authoring van de Markeringen van de Adobe uitbreiding installeert. Als u de extensie wilt installeren, opent u Visual Studio-code, selecteert u het tabblad **[!DNL Extensions]** links van het scherm en zoekt u naar `adobe markdown authoring` . Selecteer de extensie en klik op **[!DNL Install]** .
   ![ installeer de uitbreiding van de Authoring van de Markeringen van de Adobe ](../assets/docs-framework/install-adobe-markdown-extension.gif)
3. Bewerk de sjabloon met relevante informatie voor uw doel. Volg de instructies in de sjabloon.
4. Ga voor alle schermafbeeldingen of afbeeldingen die u aan de documentatie wilt toevoegen naar `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]` , waar `[...]` de gewenste categorie voor uw doel is. Als u bijvoorbeeld een aanpassingsdoel toevoegt aan het Experience Platform, selecteert u de map `personalization` . Maak een nieuwe map voor uw bestemming en sla uw afbeeldingen hier op. U moet er een koppeling naar maken vanaf de pagina die u ontwerpt. Zie [ instructies hoe te om aan beelden ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html#link-to-images) te verbinden.
5. Sla het bestand waaraan u werkt op als u klaar bent.

## De documentatie ter controle verzenden {#submit-review}

>[!TIP]
>
>U kunt hier niets breken. Door de instructies in deze sectie te volgen, stelt u eenvoudig een documentupdate voor. Uw voorgestelde update wordt goedgekeurd of bewerkt door het Adobe Experience Platform-documentatieteam.

1. In de Desktop van GitHub, creeer een werkende tak voor uw updates en selecteer **tak van Publish** om de tak aan GitHub te publiceren.

![ Nieuwe vertakking lokale ](../assets/docs-framework/new-branch-local.gif)

1. In de Desktop van GitHub, [ begaat ](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) uw werk, zoals hieronder getoond.

   ![ lokale Vastleggen ](../assets/docs-framework/commit-local.png)

1. In Desktop GitHub, [ duw ](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) uw werk aan de [ verre ](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) tak, zoals hieronder getoond.

   ![ duw uw begaat ](../assets/docs-framework/push-local-to-remote.png)

1. In de het Webinterface van GitHub, open een trekkingsverzoek (PR) om uw werkende tak in de hoofdtak van de de documentatiebewaarplaats van de Adobe samen te voegen. Zorg ervoor de tak u aan werkte wordt geselecteerd en selecteert **Contribute > Open trekkingsverzoek**.

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
