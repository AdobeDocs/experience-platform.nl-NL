---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: Automatische beleidscontrole
topic: guide
description: Dit document behandelt hoe het beleid van het gegevensgebruik automatisch wordt afgedwongen wanneer het activeren van segmenten aan bestemmingen in Experience Platform.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 0%

---


# Automatische beleidshandhaving

Zodra de gegevens worden geëtiketteerd en het gebruiksbeleid wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiekssegmenten aan bestemmingen, dwingt Adobe Experience Platform automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

## Vereisten

Deze handleiding vereist een goed begrip van de diensten van de Platform die betrokken zijn bij de automatische handhaving. Raadpleeg de volgende documentatie voor meer informatie voordat u doorgaat met deze handleiding:

* [Adobe Experience Platform Data Governance](../home.md): Het kader waardoor het Platform de naleving van het gegevensgebruik door het gebruik van etiketten en beleid afdwingt.
* [Klantprofiel](../../profile/home.md) in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): De segmenteringsmotor binnen  [!DNL Platform] die wordt gebruikt om publiekssegmenten van uw klantenprofielen tot stand te brengen op klantengedrag en attributen worden gebaseerd.
* [Doelen](../../destinations/home.md): Doelen zijn vooraf gebouwde integraties met veelgebruikte toepassingen die het mogelijk maken om gegevens van Platform naadloos te activeren voor kanaalmarketingcampagnes, e-mailcampagnes, gerichte reclame en nog veel meerY.

## Handelingenstroom {#flow}

Het volgende diagram illustreert hoe de beleidshandhaving in de gegevensstroom van segmentactivering wordt geïntegreerd:

![](../images/enforcement/enforcement-flow.png)

Wanneer een segment voor het eerst wordt geactiveerd, [!DNL Policy Service] controleert op beleidsovertredingen op basis van de volgende factoren:

* De labels voor gegevensgebruik die worden toegepast op velden en gegevenssets binnen het segment dat moet worden geactiveerd.
* Het marketingdoel van de bestemming.

>[!NOTE]
>
>Als er gegevensgebruikslabels zijn die slechts op bepaalde gebieden binnen een dataset (eerder dan de volledige dataset) zijn toegepast, komt de handhaving van die gebieden-vlakke etiketten op activering slechts onder de volgende voorwaarden voor:
>
>* De velden worden gebruikt in de segmentdefinitie.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.


## Gegevensverbinding {#lineage}

De verbinding van gegevens speelt een sleutelrol in hoe het beleid in Platform wordt afgedwongen. In algemene termen verwijst de datalijn naar de oorsprong van een set gegevens en wat er met de gegevens gebeurt (of waar deze naartoe worden verplaatst).

In de context van [!DNL Data Governance], laat lijn gegevensgebruiksetiketten toe om van datasets aan stroomafwaartse diensten te verspreiden die hun gegevens, zoals het Profiel van de Klant in real time en bestemmingen verbruiken. Hierdoor kan het beleid op verschillende belangrijke punten in de gegevensreis door het Platform worden geëvalueerd en afgedwongen, en wordt de gegevensconsument een context geboden waarin hij kan zien waarom een beleidsovertreding heeft plaatsgevonden.

In Experience Platform gaat het bij de beleidshandhaving om de volgende begrotingslijn:

1. Gegevens worden in het Platform opgenomen en in **datasets** opgeslagen.
1. Klantprofielen worden geïdentificeerd en samengesteld op basis van deze gegevenssets door gegevensfragmenten samen te voegen volgens het **samenvoegbeleid**.
1. Groepen profielen worden op basis van gemeenschappelijke kenmerken onderverdeeld in **segmenten**.
1. Segmenten worden geactiveerd naar lagere **doelen**.

Elke fase in de bovenstaande tijdlijn vertegenwoordigt een entiteit die kan bijdragen tot het overtreden van een beleid, zoals in de onderstaande tabel wordt beschreven:

| Gegevenslijnfase | Rol bij de handhaving van het beleid |
| --- | --- |
| Gegevensset | Datasets bevatten gegevensgebruikslabels (toegepast op de dataset of het gebiedsniveau) die bepalen welke gebruiksgevallen de volledige dataset of specifieke gebieden kunnen worden gebruikt voor. Beleidsovertredingen treden op als een dataset of veld met bepaalde labels wordt gebruikt voor een doel dat door een beleid wordt beperkt. |
| Samenvoegbeleid | Het beleid van de fusie is de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven wanneer het samenvoegen van fragmenten van veelvoudige datasets. De schendingen van het beleid zullen voorkomen als uw samenvoegbeleid wordt gevormd zodat de datasets met beperkte etiketten aan een bestemming worden geactiveerd. Zie de gids op [voegt beleid](../../profile/ui/merge-policies.md) voor meer informatie samen. |
| Segment | De regels van het segment bepalen welke attributen van klantenprofielen zouden moeten worden omvat. Afhankelijk van de velden die een segmentdefinitie bevat, neemt het segment alle toegepaste gebruikslabels voor die velden over. Beleidsovertredingen treden op als u een segment activeert waarvan de geërfte labels worden beperkt door het toepasselijke beleid van de doelbestemming, op basis van het geval van marketinggebruik. |
| Bestemming | Bij het instellen van een bestemming kan een marketingactie (ook wel een marketingcase genoemd) worden gedefinieerd. Dit gebruiksgeval correleert met een marketingactie zoals gedefinieerd in een beleid voor gegevensgebruik. Met andere woorden, bepaalt het marketinggeval dat u voor een bestemming definieert, welk beleid voor gegevensgebruik op die bestemming van toepassing is. Beleidsovertredingen treden op als u een segment activeert waarvan de gebruikslabels zijn beperkt door het toepasselijke beleid van de doelbestemming. |

Wanneer beleidsschendingen voorkomen, verstrekken de resulterende berichten die in UI verschijnen nuttige hulpmiddelen om de schending bijdragende gegevenslijn te onderzoeken helpen de kwestie oplossen. Meer details worden verstrekt in de volgende sectie.

## Beleidsovertredingsberichten {#enforcement}

Als een beleidsschending voorkomt van het proberen om een segment (of [het aanbrengen van uitgeeft aan reeds geactiveerd segment](#policy-enforcement-for-activated-segments)) te activeren wordt de actie verhinderd en een popover lijkt erop wijzend dat één of meerdere beleid zijn overtreden. Nadat een schending is geactiveerd, wordt de knop **[!UICONTROL Opslaan]** uitgeschakeld voor de entiteit die u wijzigt, totdat de juiste componenten worden bijgewerkt om te voldoen aan het beleid voor gegevensgebruik.

Selecteer een beleidsovertreding in de linkerkolom van de pop-up om details voor die schending te tonen.

![](../images/enforcement/violation-policy-select.png)

Het schendingsbericht geeft een overzicht van het beleid dat is overtreden, met inbegrip van de voorwaarden het beleid wordt gevormd om te controleren, de specifieke actie die de schending teweegbracht, en een lijst van mogelijke resoluties voor de kwestie.

![](../images/enforcement/violation-summary.png)

Een grafiek van de gegevenslijn wordt getoond onder de schendingssamenvatting, toestaand u om te visualiseren welke datasets, fusiebeleid, segmenten, en bestemmingen betrokken bij de beleidsschending waren. De entiteit die u momenteel wijzigt, wordt in de grafiek gemarkeerd en geeft aan welk punt in de flow de schending veroorzaakt. U kunt een entiteitsnaam in de grafiek selecteren om de detailpagina voor de entiteit in kwestie te openen.

![](../images/enforcement/data-lineage.png)

U kunt het **[!UICONTROL Filter]** pictogram (![](../images/enforcement/filter.png)) ook gebruiken om de getoonde entiteiten door categorie te filtreren. U moet ten minste twee categorieën selecteren om de gegevens weer te geven.

![](../images/enforcement/lineage-filter.png)

Selecteer **[!UICONTROL Lijstweergave]** om de gegevenskoppeling als een lijst weer te geven. Als u wilt terugschakelen naar de visuele grafiek, selecteert u **[!UICONTROL Padweergave]**.

![](../images/enforcement/list-view.png)

## Beleidshandhaving voor geactiveerde segmenten {#policy-enforcement-for-activated-segments}

De handhaving van het beleid is nog op segmenten van toepassing nadat zij zijn geactiveerd, beperkt om het even welke veranderingen in een segment of zijn bestemming die in een beleidsschending zouden resulteren. Vanwege de manier waarop [datalijn](#lineage) in beleidshandhaving werkt, kan een van de volgende handelingen mogelijk een schending veroorzaken:

* Labels voor gegevensgebruik bijwerken
* Gegevenssets voor een segment wijzigen
* Het veranderen van segmentpredikaten
* Doelconfiguraties wijzigen

Als een van de bovenstaande acties een schending veroorzaakt, wordt die actie verhinderd worden bewaard en een bericht van de beleidsschending wordt getoond, die ervoor zorgen dat uw geactiveerde segmenten aan het beleid van het gegevensgebruik blijven voldoen wanneer wordt gewijzigd.

## Volgende stappen

In dit document wordt beschreven hoe automatische beleidshandhaving in Experience Platform werkt. Voor stappen op hoe te om beleidshandhaving in uw toepassingen programmatically te integreren gebruikend API vraag, zie de gids op [op API-Gebaseerde handhaving](./api-enforcement.md).