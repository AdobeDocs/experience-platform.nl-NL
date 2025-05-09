---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;label api voor gegevensgebruik;beleidservice-api;overzicht van labels voor gegevensgebruik
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
description: Leer hoe labels voor gegevensgebruik worden gebruikt om naleving van gegevensbeheer in Adobe Experience Platform af te dwingen.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 916eb01ea7878366620b859c1d6a667a88b850c9
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# Overzicht van labels voor gegevensgebruik {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Toegang tot gevoelige en beveiligde gegevens beheren"
>abstract="<h2>Beschrijving</h2><p>De toegang tot specifieke gegevensattributen en/of segmenten controleren, die u toestaan om flexibele werkschema&#39;s voor de diverse personen en teams te ontwerpen die Experience Platform gebruiken gevallen.</p>"

Adobe Experience Platform staat u toe om de etiketten van het gegevensgebruik op datasets en gebieden toe te passen, die elk categoriseren volgens verwant [ beleid van het gegevensbeheer ](../policies/overview.md) en [ toegangsbeheerbeleid ](../../access-control/abac/ui/policies.md).

Dit document biedt een overzicht van labels voor gegevensgebruik in [!DNL Experience Platform] .

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het beleid dat van toepassing is op die gegevens. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. Op basis van de aanbevolen procedures worden labelgegevens aangemoedigd zodra deze worden opgenomen in [!DNL Experience Platform] of zodra gegevens beschikbaar komen voor gebruik in [!DNL Experience Platform] .

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

[!DNL Experience Platform] biedt verschillende &#39;core&#39; labels voor gegevensgebruik buiten de box, die een groot aantal algemene beperkingen bestrijken die van toepassing zijn op gegevensbeheer. Voor meer informatie over deze etiketten en het governancebeleid zij vertegenwoordigen, zie de gids op [ de etiketten van het het kerngegevensgebruik ](reference.md).

Naast de labels die Adobe biedt, kunt u ook uw eigen aangepaste labels voor uw organisatie definiëren. Zie de sectie op [ het leiden etiketten ](#manage-labels) voor meer informatie.

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten die door [ de Dienst van de Segmentatie van Adobe Experience Platform ](../../segmentation/home.md) worden gecreeerd erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat Experience Platform toe om automatische beleidshandhaving te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Daarom kunt u gemakkelijker identificeren welke attributen van uw segmenten zouden moeten worden uitgesloten en hen verhinderen etiketten van uitgesloten gebieden over te nemen.

Voor meer informatie over hoe de automatische handhaving in Experience Platform werkt, zie het overzicht op [ automatische beleidshandhaving ](../enforcement/auto-enforcement.md).

### Overerving van Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] heeft de mogelijkheid om segmenten te delen met Adobe Audience Manager. Alle besturingselementen voor gegevensexport die zijn toegepast op Audience Manager-segmenten, worden omgezet in equivalente labels en marketingacties die worden herkend door [!DNL Experience Platform] Data Governance.

Voor een verwijzing op hoe de specifieke Controles van de Uitvoer van Gegevens aan de etiketten van het gegevensgebruik in [!DNL Experience Platform] in kaart brengen, gelieve te verwijzen naar de [ documentatie van Audience Manager ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=nl-NL#aam-data-export-control-in-aep).

## Labels voor gegevensgebruik beheren in [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instructies"
>abstract="<ul><li>Etiketteer XDM Gebieden en Segmenten om de gebieden en of de segmenten te classificeren die u toegang tot wilt beperken.</li><li>Met labelrollen kunt u labels toevoegen aan een rol en zo de leden van deze rol met labels definiëren waarvoor beperkingen gelden.</li><li>Creeer beleid, leidt een beleid tot een verhouding tussen de etiketten op geëtiketteerde voorwerpen zoals gebieden XDM en Segmenten en de etiketten op rollen. Als de etiketten aanpassen, dan of kan een vergunning of een beperkte toegang worden bepaald.</li></ul>"

U kunt labels voor gegevensgebruik beheren met behulp van [!DNL Experience Platform] API&#39;s of de gebruikersinterface. Raadpleeg de onderstaande subsecties voor meer informatie over elke subsectie.

### UI gebruiken

Met de werkruimte van **[!UICONTROL Policies]** in de gebruikersinterface van [!DNL Experience Platform] kunt u kern- en aangepaste labels voor uw organisatie weergeven en beheren. U kunt de **[!UICONTROL Schemas]** werkruimte gebruiken om [ etiketten op uw schema&#39;s van de Gegevens van de Ervaring toe te passen (XDM) ](../../xdm/tutorials/labels.md), of te leren hoe te [ douaneetiketten in **[!UICONTROL Policies]** UI ](./user-guide.md) creëren en te beheren door de gebruikersgids van de etiketten van het gegevensgebruik in plaats daarvan te lezen.

>[!IMPORTANT]
>
>Labels kunnen niet meer worden toegepast op velden op het niveau van de gegevensset. Deze workflow is vervangen door labels op schemaniveau. Alle labels die eerder op het niveau van gegevenssetobjecten zijn toegepast, worden tot 31 mei 2024 nog steeds ondersteund via de gebruikersinterface van Experience Platform. Om ervoor te zorgen dat uw etiketten over alle schema&#39;s verenigbaar zijn, moeten om het even welke etiketten die eerder aan gebieden op het datasetniveau worden vastgemaakt door u over het komende jaar worden gemigreerd aan het schemaniveau. Zie de sectie op [ migrerend eerder toegepaste etiketten ](../e2e.md#migrate-labels) voor instructies op hoe te om dit te doen.

### API&#39;s gebruiken

Het `/labels` eindpunt in de [ Dienst API van het Beleid ](https://www.adobe.io/experience-platform-apis/references/policy-service/) staat u toe om de etiketten van het gegevensgebruik programmatically te beheren, met inbegrip van het creëren van douaneetiketten. Verwijs naar de [ gids van het etiketteneindpunt ](../api/labels.md) voor meer informatie.

De [ Dienst API van de Dataset ](https://www.adobe.io/experience-platform-apis/references/dataset-service/) wordt gebruikt om etiketten voor dataset en gebieden te beheren. Zie de gids op [ het leiden datasetetiketten ](./dataset-api.md) voor meer informatie.

## Volgende stappen

Dit document bevatte een inleiding op de labels voor gegevensgebruik en hun rol binnen het kader voor gegevensbeheer. Raadpleeg de documentatie in deze handleiding voor meer informatie over het beheren van labels in [!DNL Experience Platform] .
