---
title: Soorten publiek-AI-widgets van dashboard
description: Leer hoe de AI van de Klant belangrijke inzichten met betrekking tot kurn of neiging over het Echte publiek van het Profiel van de Klant van uw organisatie verstrekt.
hide: true
hidefromtoc: true
source-git-commit: 74dcb35b389a962a5238c1fd5ef1370a76bdd57e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 2%

---

# Klanten-AI-widgets voor publiek-dashboard {#customer-ai-audiences-widgets}

Klant-AI wordt gebruikt om aangepaste eigenschapscores zoals churn en conversie voor individuele profielen op schaal te genereren. De AI van de klant doet dit door bestaande gegevens van de Gebeurtenis van de Consumentenervaring te analyseren om te voorspellen **scores voor churn- of conversiedichtheid**. Deze zeer nauwkeurige modellen van de klantenneiging staan voor nauwkeurigere segmentatie en het richten toe. De [verdeling van scores](#customer-ai-distribution-of-scores) en [overzicht van scores](#customer-ai-scoring-summary) inzichten tonen de verdeeldheid in uw publiek aan . Ze benadrukken welke profielen de hoge/lage/gemiddelde dichtheid zijn en hoe deze over het aantal profielen worden verdeeld.

<!-- 
THe links when required
* [[!UICONTROL Customer AI scoring summary]](#customer-ai-scoring-summary)
* [[!UICONTROL Customer AI distribution of scores]](#customer-ai-distribution-of-scores) 
-->

## [!UICONTROL Customer AI distribution of scores] {#customer-ai-distribution-of-scores}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_distributionOfScores"
>title="Verdeling van scores"
>abstract="Deze widget visualiseert de verdeling van het totale aantal profielen aan de hand van hun eigenschapscores in stappen van 5 procent. De verdeling van het profielaantal wordt bepaald door het AI-model en het geselecteerde samenvoegbeleid. U kunt het AI-model wijzigen in het vervolgkeuzemenu onder de titel van de widget."

De [!UICONTROL Customer AI distribution of scores] widget categoriseert het totale aantal profielen op basis van hun populatiescore . De verdeling van het profielaantal wordt bepaald door het AI model en het geselecteerde fusiebeleid, dan visualiseerd in vijf percententoename die op hun neiging wijzen. Het aantal profielen wordt opgegeven langs de Y-as en de dichtheidsscores langs de X-as.

>[!NOTE]
>
>Als de visualisatie een conversiesnelheidsscore is, worden de hoge scores groen en de lage scores rood weergegeven. Als je de eigenheid van de kroon voorspelt, wordt deze gespiegeld, dan zijn de hoge scores rood en zijn de lage scores groen. Het gemiddelde emmertje blijft geel ongeacht welk aandrijvingstype u kiest.

Het AI-model waarmee de densiteitsscores worden bepaald, wordt gekozen uit de vervolgkeuzelijst onder de titel van de widget. Het vervolgkeuzemenu bevat een lijst met alle geconfigureerde AI-modellen van de Klant. Selecteer het juiste AI-model voor uw analyse in de lijst met beschikbare modellen. Als er geen AI-model van de Klant beschikbaar is, geeft een bericht in de widget u de opdracht ten minste één AI-model van de Klant te configureren en wordt een hyperlink naar de configuratiepagina van het AI-model van de Klant weergegeven. Zie de documentatie voor instructies op [hoe te om een instantie van de KlantAI te vormen](../../intelligent-services/customer-ai/user-guide/configure.md).

>[!NOTE]
>
>Selecteer de vervolgkeuzelijst direct onder het tabblad Overzicht om het samenvoegbeleid te wijzigen dat bepaalt welke profielen in de analyse worden opgenomen. Zie de sectie over [beleid samenvoegen](#merge-policies) voor een korte beschrijving, of [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md) voor meer informatie .

Als u naar de pagina Gedetailleerde inzichten voor het geselecteerde AI-model van de Klant wilt navigeren, selecteert u **[!UICONTROL View model details]**.

![Het Experience Platform Soorten publiek dashboard met het [!UICONTROL Customer AI distribution of scores] widget en [!UICONTROL View model details] gemarkeerd.](../images/segments/customer-ai-distribution-of-scores.png)

De gedetailleerde pagina met modelinzichten wordt weergegeven.

![De pagina met inzichten voor de AI van de Klant.](../images/profiles/customer-ai-insights-page.png)

Meer informatie over de AI van de Klant vindt u op de [Dreamweaver-handleiding voor inzichten](../../intelligent-services/customer-ai/user-guide/discover-insights.md).

## [!UICONTROL Customer AI scoring summary] {#customer-ai-scoring-summary}

>[!CONTEXTUALHELP]
>id="platform_dashboards_segments_scoringSummary"
>title="Overzicht van scores"
>abstract="Deze widget geeft het totale aantal scoreprofielen weer en categoriseert deze in emmers met een hoge, gemiddelde en lage dichtheid. Het donutdiagram illustreert de proportionele samenstelling van totale profielen in hoge, gemiddelde en lage dichtheid."

Deze widget geeft het totale aantal profielen met een score weer en categoriseert deze in emmers met een hoge, gemiddelde en lage dichtheid, respectievelijk groen, geel en rood. Een donutdiagram wordt gebruikt om de proportionele samenstelling van totale profielen tussen hoge, gemiddelde en lage eigenschappen als groen, geel en rood te illustreren. Een profiel komt in aanmerking voor een hoge dichtheid van meer dan 75, een gemiddelde dichtheid tussen 25 en 74 en een lage dichtheid onder 24. Een legenda geeft de kleurcode en drempelwaarden van eigenschappen aan. De tellingen van het profiel voor de hoge, middelgrote, en lage eigenschappen worden getoond in een dialoog wanneer de curseur over de respectieve sectie van de donutgrafiek beweegt.

>[!NOTE]
>
>Als de visualisatie een conversiesnelheidsscore is, worden de hoge scores groen en de lage scores rood weergegeven. Als je de eigenheid van de kroon voorspelt, wordt deze gespiegeld, dan zijn de hoge scores rood en zijn de lage scores groen. Het gemiddelde emmertje blijft geel ongeacht welk aandrijvingstype u kiest.

Het vervolgkeuzemenu onder de widgettitel bevat een lijst met alle geconfigureerde AI-modellen van de Klant. Selecteer het juiste AI-model voor uw analyse in de lijst met beschikbare modellen. Als er geen AI-model van de Klant beschikbaar is, geeft een bericht in de widget u de opdracht ten minste één AI-model van de Klant te configureren en wordt een hyperlink naar de configuratiepagina van het AI-model van de Klant weergegeven. Zie de documentatie op [hoe te om een instantie van de KlantAI te vormen](../../intelligent-services/customer-ai/user-guide/configure.md) voor gedetailleerde instructies.

>[!NOTE]
>
>Het totale aantal berekende profielen is afhankelijk van het gekozen samenvoegingsbeleid. Als u het gebruikte samenvoegingsbeleid wilt wijzigen, selecteert u de vervolgkeuzelijst direct onder het tabblad Overzicht. Zie de sectie over [beleid samenvoegen](#merge-policies) voor een korte beschrijving, of [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md) voor meer informatie .

![Het dashboard Soorten publiek van het Experience Platform met de overzichtswidget voor scores van de Klant AI gemarkeerd.](../images/segments/customer-ai-scoring-summary.png)

Selecteren **[!UICONTROL View model details]** om naar de gedetailleerde pagina met inzichten voor het geselecteerde AI-model van de Klant te navigeren. Meer informatie over de AI van de Klant vindt u op de [Dreamweaver-handleiding voor inzichten](../../intelligent-services/customer-ai/user-guide/discover-insights.md).
