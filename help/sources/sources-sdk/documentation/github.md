---
keywords: Experience Platform;thuis;populaire onderwerpen;bronnen;connectors;bronconnectors;bronnen sdk;sdk;SDK
solution: Experience Platform
title: Gebruik de Interface van het Web van GitHub om een Pagina van de Documentatie van Bronnen te creëren
topic-legacy: tutorial
description: Dit document verstrekt stappen op hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen.
exl-id: 84b4219c-b3b2-4d0a-9a65-f2d5cd989f95
source-git-commit: adf7dbe5e32310fee680f996ffbde0fd6ddd993a
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Gebruik de het Webinterface van GitHub om een brondocumentatiepagina tot stand te brengen

Dit document verstrekt stappen op hoe te om de het Webinterface van GitHub aan auteursdocumentatie te gebruiken en een trekkingsverzoek (PR) voor te leggen.

>[!TIP]
>
>De volgende documenten uit de Contribute-handleiding voor Adobe kunnen worden gebruikt ter ondersteuning van het documentatieproces: <ul><li>[Gereedschappen voor Git- en Markeringsontwerp installeren](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/install-tools.html?lang=en)</li><li>[Git-opslagplaats lokaal instellen voor documentatie](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/local-repo.html?lang=en)</li><li>[GitHub-bijdrageworkflow voor grote wijzigingen](https://experienceleague.adobe.com/docs/contributor/contributor-guide/setup/full-workflow.html?lang=en)</li></ul>

## Opstelling uw milieu GitHub

De eerste stap in vestiging moet uw milieu GitHub aan het navigeren [Adobe Experience Platform GitHub-opslagplaats](https://github.com/AdobeDocs/experience-platform.en).

![platform-repo](../assets/platform-repo.png)

Selecteer vervolgens **Vork**.

![vork](../assets/fork.png)

Als de vork is voltooid, selecteert u **master** en voert u een naam voor de nieuwe vertakking in in het vervolgkeuzemenu dat wordt weergegeven. Zorg ervoor dat u een beschrijvende naam voor de vertakking opgeeft, aangezien dit wordt gebruikt om uw werk te bevatten en selecteer vervolgens **vertakking maken**.

![vertakking maken](../assets/create-branch.png)

In de de omslagstructuur van GitHub van uw forked bewaarplaats, navigeer aan [`experience-platform.en/help/sources/tutorials/api/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/api/create) en selecteer vervolgens in de lijst de juiste categorie voor uw bron. Als u bijvoorbeeld documentatie voor een nieuwe CRM-bron maakt, selecteert u **crm**.

>[!TIP]
>
>Als u documentatie voor UI creeert, dan navigeer aan [`experience-platform.en/help/sources/tutorials/ui/create/`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/tutorials/ui/create) en selecteer de juiste categorie voor uw bron. Als u uw afbeeldingen wilt toevoegen, navigeert u naar [`experience-platform.en/help/sources/images/tutorials/create/sdk`](https://github.com/AdobeDocs/experience-platform.en/tree/main/help/sources/images/tutorials/create) Voeg vervolgens uw schermafbeeldingen toe aan de `sdk` map.

![crm](../assets/crm.png)

Er wordt een map met bestaande CRM-bronnen weergegeven. Als u documentatie voor een nieuwe bron wilt toevoegen, selecteert u **Bestand toevoegen** en selecteer vervolgens **Nieuw bestand maken** in het vervolgkeuzemenu dat wordt weergegeven.

![maken-nieuw bestand](../assets/create-new-file.png)

Geef het bronbestand een naam `YOURSOURCE.md` waarbij UURSOURCE de naam van uw bron in Platform is. Als uw bedrijf bijvoorbeeld ACME CRM is, moet uw bestandsnaam `acme-crm.md`.

![git-interface](../assets/git-interface.png)

## Auteur de documentatiepagina voor uw bron

Als u de nieuwe bron wilt documenteren, plakt u de inhoud van het dialoogvenster [source documentation template](./template.md) in de GitHub-webeditor. U kunt de sjabloon ook downloaden [hier](../assets/api-template.zip).

Met het malplaatje dat over aan de interface van de Webredacteur van GitHub wordt gekopieerd, volg de instructies die op het malplaatje worden geschetst en geef de waarden uit die relevante informatie voor uw bron bevatten.

![plakken-sjabloon](../assets/paste-template.png)

Als u klaar bent, legt u het bestand in de vertakking vast.

![begaan](../assets/commit.png)

## De documentatie ter controle verzenden

Als het bestand is toegewezen, kunt u een pull-verzoek (PR) openen om uw werkvertakking samen te voegen in de master vertakking van de documentatieopslagplaats van Adobe. Controleer of de vertakking waaraan u hebt gewerkt, is geselecteerd en selecteer **Aanvraag vergelijken en intrekken**.

![compare-pr](../assets/compare-pr.png)

Zorg ervoor dat de basis- en vergelijkingsvertakkingen correct zijn. Voeg een notitie toe aan de PR, beschrijf de update en selecteer vervolgens **pull-verzoek maken**. Dit opent een PR om de werkende tak van uw werk in de master tak van de opslagplaats van de Adobe samen te voegen.

>[!TIP]
>
>Laat de **Bewerkingen door onderhoudsleiders toestaan** Schakel het selectievakje in om ervoor te zorgen dat het documentatieteam Adobe de PR kan bewerken.

![create-pr](../assets/create-pr.png)

Op dit punt, lijkt een bericht dat u ertoe aanzet om de Overeenkomst van de Vergunning van de Medewerker van de Adobe te ondertekenen (CLA). Dit is een verplichte stap. Nadat u CLA ondertekent, vernieuw de PR pagina en verzend het trekkingsverzoek.

U kunt bevestigen dat het trekkingsverzoek is voorgelegd door het lusje van trekkingsverzoeken in https://github.com/AdobeDocs/experience-platform.en te inspecteren.

![bevestiging-pr](../assets/confirm-pr.png)
