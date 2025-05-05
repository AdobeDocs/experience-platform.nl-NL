---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Campaign Managed Cloud Services;campagne;campagne beheerde services
title: Adobe Campaign Managed Cloud Services
description: Leer hoe u via de gebruikersinterface verbinding kunt maken tussen Campagne Managed Cloud Services en Experience Platform
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Adobe Campaign Managed Cloud Services biedt een Managed Services-platform voor het ontwerpen van ervaringen met klanten over meerdere kanalen en biedt een omgeving voor visuele campagneorchestratie, realtime interactiebeheer en uitvoering via meerdere kanalen. Bezoek de [ documentatie van Adobe Campaign v8 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=nl) voor meer informatie.

Met de Adobe Campaign Managed Cloud Services-bron kunt u Adobe Campaign v8-leveringslogboeken en -logboekgegevens naar Adobe Experience Platform overbrengen.

## Vereisten

Voordat u een bronverbinding kunt maken om uw campagne v8 naar Experience Platform te brengen, moet u eerst aan de volgende voorwaarden voldoen:

* [De import van het gebeurtenislogboek instellen met de Adobe Campaign-clientconsole](#view-delivery-and-tracking-log-data)
* [Een XDM ExperienceEvent-schema maken](#create-a-schema)
* [Een gegevensset maken](#create-a-dataset)

### Loggegevens voor levering en bijhouden weergeven {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>U moet toegang hebben tot de Adobe Campaign v8 Client Console om uw logboekgegevens in Campagne te bekijken. Bezoek de [ documentatie van de Campagne v8 ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=nl-NL) voor informatie over hoe te om de cliëntconsole te downloaden en te installeren.

Meld u via de clientconsole aan bij uw Campagne v8-exemplaar. Selecteer [!DNL Administration] onder de tab [!DNL Explorer] en selecteer vervolgens [!DNL Configuration] . Selecteer vervolgens [!DNL Data schemas] en pas vervolgens het filter `broadLog` toe voor de naam of het label. Selecteer in de lijst die wordt weergegeven, het bronschema voor de logbestand van de geadresseerde met de naam `broadLogRcp` .

![ de de cliëntconsole van Adobe Campaign v8 met het geselecteerde lusje van de Ontdekkingsreiziger, het Beleid, de Configuratie, en de schemaknopen van Gegevens breidden uit en het filtreren plaatste aan &quot;breed&quot;.](./images/campaign/explorer.png)

Daarna, selecteer de **Gegevens** tabel.

![ de Adobe Campaign v8 cliëntconsole met het geselecteerde gegevenslusje.](./images/campaign/data.png)

Klik met de rechtermuisknop of toetsaanslag in het deelvenster Gegevens om het contextmenu te openen. Van hier, uitgezochte **vormt lijst...**

![ de Adobe Campaign v8 cliëntconsole met het contextafhankelijke open menu en de Configure geselecteerde lijstoptie.](./images/campaign/configure.png)

Het lijstconfiguratievenster verschijnt, die u van een interface voorzien waar u om het even welke gewenste gebieden aan de reeds bestaande lijst kunt toevoegen om de gegevens in het gegevenspaneel te bekijken.

![ een lijst van configuraties voor ontvankelijke leveringslogboeken die voor het bekijken kunnen worden toegevoegd.](./images/campaign/list-configuration.png)

Nu kunt u uw ontvankelijke leveringslogboeken, met inbegrip van de configuratiegebieden bekijken die in de vorige stap worden toegevoegd.

>[!TIP]
>
>U kunt dezelfde stappen herhalen, maar filtreer voor `tracking` om de gegevens van het trackinglogboek weer te geven.

![ de ontvankelijke leveringslogboeken die met informatie over zijn laatste gewijzigde naam, leveringskanaal, interne leveringsnaam, en etiket worden getoond.](./images/campaign/recipient-delivery-logs.png)

### Een schema maken {#create-a-schema}

Maak vervolgens een XDM ExperienceEvent-schema voor zowel leveringslogboeken als trackinglogboeken. U moet de het gebiedsgroep van Logboeken van de Levering van de Campagne op uw schema van leveringslogboeken en de het gebiedsgroep van Logs van het Volgen van de Campagne op uw het volgen logboekschema toepassen. U moet het veld `externalID` ook definiëren als de primaire identiteit van het schema.

>[!NOTE]
>
>Uw XDM ExperienceEvent-schema moet geschikt zijn voor profiel om uw Campagnegegevens in te voeren op [!DNL Real-Time Customer Profile] .

Voor gedetailleerde instructies op hoe te om een schema tot stand te brengen, lees de gids bij [ creërend een schema XDM in UI ](../../../xdm/tutorials/create-schema-ui.md).

### Een gegevensset maken {#create-a-dataset}

Tot slot moet u een dataset voor uw schema&#39;s tot stand brengen. Voor gedetailleerde instructies op hoe te om een dataset tot stand te brengen, lees de gids bij [ het creëren van een dataset in UI ](../../../catalog/datasets/user-guide.md).

## Een Adobe Campaign Managed Cloud Services-bronverbinding maken met de interface van Experience Platform

Nu u uw gegevenslogboeken in de de cliëntconsole van de Campagne hebt betreden, creeerde een schema, en een dataset, kunt u nu te werk gaan om een bronverbinding tot stand te brengen om uw gegevens van Managed Services van de Campagne aan Experience Platform te brengen.

Voor gedetailleerde instructies op hoe te om uw de leveringslogboeken van de Campagne v8 en het volgen logboekgegevens aan het Platfrom van de Ervaring te brengen, lees de gids op [ creërend een Gecampagneerde Managed Services bronverbinding in UI ](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>Er is een randgeval waarin de interactie van een onlangs verwijderde e-mailontvanger met een e-mail persoonlijke informatie opnieuw in Experience Platform zou kunnen opnemen. In sommige gevallen, zou dit marketing aan die gebruiker kunnen re-toelaten.
>
>* Dit scenario is alleen actief tussen het moment dat een privacyverzoek in Experience Platform is uitgevoerd en het moment dat het in Adobe Campaign Classic is uitgevoerd. Nadat het verzoek in Campagne wordt uitgevoerd, is er een controle om ervoor te zorgen het verslag niet wordt uitgevoerd naar Campagne. Voer na 72 uur na de uitvoering een GDPR-verzoek opnieuw uit om dit probleem op te lossen.