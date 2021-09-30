---
title: Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken
description: De instructies op deze pagina tonen u hoe te om een tekstredacteur te gebruiken om in uw lokale milieu te werken aan auteur een documentatiepagina voor uw Experience Platform bestemming en het voor overzicht voor te leggen.
exl-id: 125f2d10-0190-4255-909c-5bd5bb59fcba
source-git-commit: 1bbff0fa54f1b7ef1ee70efd2a85cd43b34b2f5a
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# Een teksteditor in uw lokale omgeving gebruiken om een doeldocumentatiepagina te maken {#local-authoring}

In de instructies op deze pagina ziet u hoe u een teksteditor kunt gebruiken om in uw lokale omgeving te werken aan de auteur van documentatie en een pull-verzoek (PR) in te dienen. Voordat u de hier aangegeven stappen doorloopt, moet u [Uw doel documenteren in Adobe Experience Platform-doelen](./documentation-instructions.md).

>[!TIP]
>
>Raadpleeg ook de ondersteunende documentatie bij de Adobe:
>* [Gereedschappen voor Git- en Markeringsontwerp installeren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)
>* [Git-opslagplaats lokaal instellen voor documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)
>* [GitHub-bijdrageworkflow voor grote wijzigingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en).


## Verbind met GitHub en opstelling uw lokale auteursmilieu {#set-up-environment}

1. Navigeer in uw browser naar `https://github.com/AdobeDocs/experience-platform.en`
2. Als u [vork](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#fork-the-repository) de opslagplaats wilt, klikt u op **Fork** zoals hieronder wordt weergegeven. Dit leidt tot een exemplaar van de bewaarplaats van het Experience Platform in uw eigen rekening GitHub.

   ![Documentatieregister voor vork Adobe](./assets/ssd-fork-repository.gif)

3. Kloont de opslagplaats naar uw lokale computer. Selecteer **Code > HTTPS > Openen met Desktop GitHub**, zoals hieronder getoond. Zorg ervoor u [GitHub Desktop](https://desktop.github.com/) geïnstalleerd hebt. Lees [Een lokale kloon maken van de gegevensopslagruimte](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en#create-a-local-clone-of-the-repository) in de handleiding voor Adobe-contribuanten voor meer informatie.

   ![Adobe-documentatieopslagplaats klonen naar lokale omgeving](./assets/clone-local.png)

4. Navigeer in uw lokale bestandsstructuur naar `experience-platform.en/help/destinations/catalog/[...]`, waarbij `[...]` de gewenste categorie voor uw bestemming is. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de map `personalization`.

## Auteur de documentatiepagina voor uw bestemming {#author-documentation}

1. Uw documentatiepagina is gebaseerd op [self-service bestemmingsmalplaatje](./self-service-template.md). Download [doelsjabloon](assets/yourdestination-template.zip). Pak het uit en extraheer het bestand `yourdestination-template.md` naar de map die in stap 4 hierboven is vermeld.  Wijzig de naam van het bestand `YOURDESTINATION.md`, waarbij YOURDESTINATION de naam van uw bestemming in Adobe Experience Platform is. Als uw bedrijf bijvoorbeeld Moviestar heet, geeft u het bestand `moviestar.md` een naam.
2. Open het nieuwe bestand in de teksteditor van uw keuze](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en#understand-markdown-editors). [ Adobe adviseert dat u [Visual Studio Code](https://code.visualstudio.com/) gebruikt en de de Authoring van de Markeringen van de Adobe uitbreiding installeert. Als u de extensie wilt installeren, opent u Visual Studio-code, selecteert u het tabblad **[!DNL Extensions]** links van het scherm en zoekt u `adobe markdown authoring`. Selecteer de extensie en klik op **[!DNL Install]**.
   ![Adobe Markdown Authoring-extensie installeren](./assets/install-adobe-markdown-extension.gif)
3. Bewerk de sjabloon met relevante informatie voor uw doel. Volg de instructies in de sjabloon.
4. Ga voor alle schermafbeeldingen of afbeeldingen die u wilt toevoegen aan de documentatie naar `GitHub/experience-platform.en/help/destinations/assets/catalog/[...]`, waarbij `[...]` de gewenste categorie voor uw doel is. Als u bijvoorbeeld een verpersoonlijkingsbestemming aan Experience Platform toevoegt, selecteert u de map `personalization`. Maak een nieuwe map voor uw bestemming en sla uw afbeeldingen hier op. U moet er een koppeling naar maken vanaf de pagina die u ontwerpt. Zie [instructies voor het koppelen naar afbeeldingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en#link-to-images).
5. Sla het bestand waaraan u werkt op als u klaar bent.

## De documentatie ter controle verzenden {#submit-review}

>[!TIP]
>
>U kunt hier niets breken. Door de instructies in deze sectie te volgen, stelt u eenvoudig een documentupdate voor. De door u voorgestelde update wordt goedgekeurd of bewerkt door het Adobe Experience Platform-documentatieteam.

1. In de Desktop van GitHub, creeer een het werk tak voor uw updates en selecteer **Publish tak** om de tak aan GitHub te publiceren.

![Nieuwe lokale vertakking](./assets/new-branch-local.gif)

1. In de Desktop van GitHub, [commit](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#commit) uw werk, zoals hieronder getoond.

   ![Lokaal vastleggen](./assets/commit-local.png)

1. In de Desktop van GitHub, [duw](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#push) uw werk aan de [verre ](https://docs.github.com/en/free-pro-team@latest/github/getting-started-with-github/github-glossary#remote) tak, zoals hieronder getoond.

   ![Push your commit](./assets/push-local-to-remote.png)

1. In de het Webinterface van GitHub, open een trekkingsverzoek (PR) om uw werkende tak in de master tak van de de documentatiebewaarplaats van de Adobe samen te voegen. Controleer of de vertakking waaraan u hebt gewerkt, is geselecteerd en selecteer **Contribute > pull request** openen.

   ![pull-verzoek maken](./assets/ssd-create-pull-request-1.gif)

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
