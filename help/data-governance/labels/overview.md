---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;label api voor gegevensgebruik;beleidservice-api;overzicht van labels voor gegevensgebruik
solution: Experience Platform
title: Overzicht van labels voor gegevensgebruik
description: Leer hoe labels voor gegevensgebruik worden gebruikt om naleving van gegevensbeheer in Adobe Experience Platform af te dwingen.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 5d34781e06c0fa8bfd2e52f73e336d92d16192f6
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Overzicht van labels voor gegevensgebruik {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Toegang tot gevoelige en beveiligde gegevens beheren"
>abstract="<h2>Beschrijving</h2><p>De toegang van de controle tot specifieke gegevensattributen en/of segmenten, die u toestaan om flexibele werkschema&#39;s voor de diverse persona&#39;s en teams te ontwerpen die Experience Platform gebruiken gevallen.</p>"

Met Adobe Experience Platform kunt u gegevensgebruikslabels toepassen op gegevenssets en velden, waarbij elke tag wordt ingedeeld op basis van verwante [beleid inzake gegevensbeheer](../policies/overview.md) en [toegangsbeheerbeleid](../../access-control/abac/ui/policies.md).

Dit document biedt een overzicht van labels voor gegevensgebruik in [!DNL Experience Platform].

## Werken met labels voor gegevensgebruik

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het beleid dat van toepassing is op die gegevens. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het wordt opgenomen in [!DNL Experience Platform]of zodra gegevens beschikbaar zijn voor gebruik in [!DNL Platform].

De etiketten van het gebruik van gegevens die op het datasetniveau worden toegepast worden verspreid aan alle gebieden binnen de dataset. De etiketten kunnen ook direct op individuele gebieden (kolomkopballen) in een dataset, zonder propagatie worden toegepast.

[!DNL Platform] biedt verschillende &#39;core&#39; labels voor gegevensgebruik buiten de box, die een groot aantal gemeenschappelijke beperkingen bestrijken die van toepassing zijn op gegevensbeheer. Zie de handleiding voor meer informatie over deze labels en het beleid voor governance dat ze vertegenwoordigen [basislabels voor gegevensgebruik](reference.md).

Naast de labels die door de Adobe worden verschaft, kunt u ook uw eigen aangepaste labels voor uw organisatie definiëren. Zie de sectie over [beheren, labels](#manage-labels) voor meer informatie .

## Labelovererving voor publiekssegmenten

Alle publiekssegmenten gemaakt door [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erven de gebruiksetiketten van hun overeenkomstige datasets. Dit staat Experience Platform toe om automatische beleidshandhaving te verstrekken wanneer het activeren van segmenten aan bestemmingen.

Naast het erven van dataset-vlakke etiketten, erven de segmenten alle gebied-vlakke etiketten van hun bijbehorende datasets door gebrek. Daarom kunt u gemakkelijker identificeren welke attributen van uw segmenten zouden moeten worden uitgesloten en hen verhinderen etiketten van uitgesloten gebieden over te nemen.

Voor meer informatie over hoe de automatische handhaving in Platform werkt, zie het overzicht over [automatische beleidshandhaving](../enforcement/auto-enforcement.md).

### Overerving van Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] kan segmenten delen met Adobe Audience Manager. Om het even welke Controles van de Uitvoer van Gegevens die op de segmenten van de Audience Manager zijn toegepast worden vertaald in gelijkwaardige etiketten en marketing acties die door worden erkend [!DNL Experience Platform] Data Governance.

Voor een verwijzing naar hoe de specifieke Controles van de Uitvoer van Gegevens aan de etiketten van het gegevensgebruik in kaart brengen [!DNL Platform], gelieve de [Documentatie Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Labels voor gegevensgebruik beheren in [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instructies"
>abstract="<ul><li>Etiketteer XDM Gebieden en Segmenten om de gebieden en of de segmenten te classificeren die u toegang tot wilt beperken.</li><li>Met labelrollen kunt u labels toevoegen aan een rol en zo de leden van deze rol met labels definiëren waarvoor beperkingen gelden.</li><li>Creeer beleid, leidt een beleid tot een verhouding tussen de etiketten op geëtiketteerde voorwerpen zoals gebieden XDM en Segmenten en de etiketten op rollen. Als de etiketten aanpassen, dan of kan een vergunning of een beperkte toegang worden bepaald.</li></ul>"

U kunt gegevensgebruikslabels beheren met [!DNL Experience Platform] API&#39;s of de gebruikersinterface. Raadpleeg de onderstaande subsecties voor meer informatie over elke subsectie.

### UI gebruiken

De **[!UICONTROL Policies]** werkruimte in de [!DNL Experience Platform] UI staat u toe om kern en douanelabels voor uw organisatie te bekijken en te beheren. U kunt de **[!UICONTROL Schemas]** werkruimte naar [labels toepassen op uw XDM-schema&#39;s (Experience Data Model)](../../xdm/tutorials/labels.md), of leer hoe te [aangepaste labels maken en beheren in de **[!UICONTROL Policies] UI](./user-guide.md) door in plaats daarvan de gebruikershandleiding voor de labels voor gegevensgebruik te lezen.

>[!IMPORTANT]
>
>Labels kunnen niet meer worden toegepast op velden op het niveau van de gegevensset. Deze workflow is vervangen door labels op schemaniveau. Alle labels die eerder op het niveau van gegevenssetobjecten zijn toegepast, worden tot 31 mei 2024 nog steeds ondersteund via de interface van het platform. Om ervoor te zorgen dat uw etiketten over alle schema&#39;s verenigbaar zijn, moeten om het even welke etiketten die eerder aan gebieden op het datasetniveau worden vastgemaakt door u over het komende jaar worden gemigreerd aan het schemaniveau. Zie de sectie over [eerder toegepaste labels migreren](../e2e.md#migrate-labels) voor instructies over hoe te om dit te doen.

### API&#39;s gebruiken

De `/labels` in de [Policy Service API](https://www.adobe.io/experience-platform-apis/references/policy-service/) Hiermee kunt u gegevensgebruikslabels programmatisch beheren, inclusief het maken van aangepaste labels. Zie de [eindhulplijn voor labels](../api/labels.md) voor meer informatie .

De [Dataset-service-API](https://www.adobe.io/experience-platform-apis/references/dataset-service/) wordt gebruikt om etiketten voor dataset en gebieden te beheren. Zie de handleiding op [gegevenssetlabels beheren](./dataset-api.md) voor meer informatie .

## Volgende stappen

Dit document bevatte een inleiding op de labels voor gegevensgebruik en hun rol binnen het kader voor gegevensbeheer. Raadpleeg de documentatie bij deze handleiding voor meer informatie over het beheren van labels in [!DNL Experience Platform].
