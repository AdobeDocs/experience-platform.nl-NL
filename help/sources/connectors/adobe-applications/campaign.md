---
keywords: Experience Platform;thuis;populaire onderwerpen;Adobe Campaign Managed Cloud Services;campagne;campagne beheerde services
title: Adobe Campaign Managed Cloud Services
description: Leer hoe te om Campagne Beheerde Cloud Services met Platform te verbinden gebruikend het gebruikersinterface
source-git-commit: 99f65889aecf8c045dbb72053ebaca9429c3ebe1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Adobe Campaign Managed Cloud Services biedt een Managed Services-platform voor het ontwerpen van ervaringen met klanten over meerdere kanalen en biedt een omgeving voor visuele campagneorchestratie, realtime interactiebeheer en uitvoering via meerdere kanalen. Ga naar [Adobe Campaign v8-documentatie](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) voor meer informatie .

Met de Adobe Campaign Managed Cloud Services-bron kunt u Adobe Campaign v8-leveringslogboeken en -logboekgegevens naar Adobe Experience Platform overbrengen.

## Vereisten

Voordat u een bronverbinding kunt maken om uw campagne v8 naar het Experience Platform te brengen, moet u eerst aan de volgende voorwaarden voldoen:

* [De import van het gebeurtenislogboek instellen met de Adobe Campaign-clientconsole](#view-delivery-and-tracking-log-data)
* [Een XDM ExperienceEvent-schema maken](#create-a-schema)
* [Een gegevensset maken](#create-a-dataset)

### Loggegevens voor levering en bijhouden weergeven {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>U moet toegang hebben tot de Adobe Campaign v8 Client Console om uw logboekgegevens in Campagne te bekijken. Ga naar [Campagne v8-documentatie](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) voor informatie over het downloaden en installeren van de clientconsole.

Meld u via de clientconsole aan bij uw Campagne v8-exemplaar. Onder de [!DNL Explorer] tab, selecteert u [!DNL Administration] en selecteer vervolgens [!DNL Configuration]. Selecteer vervolgens [!DNL Data schemas] en past vervolgens de `broadLog` filter voor naam of label. Selecteer in de lijst die wordt weergegeven het bronschema van de geadresseerde leveringslogs met de naam `broadLogRcp`.

![De Adobe Campaign v8 clientconsole met het geselecteerde tabblad Explorer, de knooppunten Beheer, Configuratie en Gegevensschema&#39;s zijn uitgevouwen en gefilterd op &#39;wide&#39;.](./images/campaign/explorer.png)

Selecteer vervolgens de **Gegevens** tab.

![De Adobe Campaign v8 clientconsole met het gegevenstabblad geselecteerd.](./images/campaign/data.png)

Klik met de rechtermuisknop of toetsaanslag in het deelvenster Gegevens om het contextmenu te openen. Selecteer **Lijst configureren...**

![De Adobe Campaign v8 clientconsole met het contextmenu geopend en de lijstoptie Configureren geselecteerd.](./images/campaign/configure.png)

Het lijstconfiguratievenster verschijnt, die u van een interface voorzien waar u om het even welke gewenste gebieden aan de reeds bestaande lijst kunt toevoegen om de gegevens in het gegevenspaneel te bekijken.

![Een lijst van configuraties voor ontvankelijke leveringslogboeken die voor het bekijken kunnen worden toegevoegd.](./images/campaign/list-configuration.png)

Nu kunt u uw ontvankelijke leveringslogboeken, met inbegrip van de configuratiegebieden bekijken die in de vorige stap worden toegevoegd.

>[!TIP]
>
>U kunt dezelfde stappen herhalen, maar filteren op `tracking` om de gegevens van het trackinglogboek weer te geven.

![In de logboeken voor levering aan ontvangers wordt informatie weergegeven over de naam, het leveringskanaal, de interne leveringsnaam en het label van de laatste gebruiker.](./images/campaign/recipient-delivery-logs.png)

### Een schema maken {#create-a-schema}

Maak vervolgens een XDM ExperienceEvent-schema voor zowel leveringslogboeken als trackinglogboeken. U moet de het gebiedsgroep van Logboeken van de Levering van de Campagne op uw schema van leveringslogboeken en de het gebiedsgroep van Logs van het Volgen van de Campagne op uw het volgen logboekschema toepassen. U moet ook de `externalID` veld als primaire identiteit van uw schema.

>[!NOTE]
>
>Uw XDM ExperienceEvent-schema moet geschikt zijn voor profiel om uw Campagnegegevens in te voeren op [!DNL Real-time Customer Profile].

Voor gedetailleerde instructies over hoe te om een schema tot stand te brengen, lees de gids op [een XDM-schema maken in de gebruikersinterface](../../../xdm/tutorials/create-schema-ui.md).

### Een gegevensset maken {#create-a-dataset}

Tot slot moet u een dataset voor uw schema&#39;s tot stand brengen. Voor gedetailleerde instructies op hoe te om een dataset tot stand te brengen, lees de gids op [het creëren van een dataset in UI](../../../catalog/datasets/user-guide.md).

## Een Adobe Campaign Managed Cloud Services-bronverbinding maken met de gebruikersinterface van het Platform

Nu u uw gegevenslogboeken in de de cliëntconsole van de Campagne hebt betreden, creeerde een schema, en een dataset, kunt u nu te werk gaan om een bronverbinding tot stand te brengen om uw gegevens van Managed Services van de Campagne aan Platform te brengen.

Lees de handleiding voor gedetailleerde instructies over hoe u uw AMP 8-leveringslogboeken en trackinglogbestanden naar Experience Platfrom kunt brengen [het creëren van een Gecentreerde Managed Services bronverbinding in UI](../../tutorials/ui/create/adobe-applications/campaign.md).