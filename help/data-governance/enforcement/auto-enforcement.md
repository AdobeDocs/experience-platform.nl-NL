---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: Automatische beleidscontrole
description: In dit document wordt beschreven hoe beleidsregels voor gegevensgebruik automatisch worden toegepast wanneer gebruikers naar bestemmingen in Experience Platform worden geactiveerd.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: f4f4deda02c96e567cbd0815783f192d1c54096c
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 0%

---

# Automatische beleidshandhaving

>[!IMPORTANT]
>
>Automatische beleidshandhaving is alleen beschikbaar voor organisaties die deze hebben aangeschaft **Adobe Gezondheidsschild** of **Privacy- en beveiligingsschild van Adobe**.

Zodra het gegeven wordt geëtiketteerd en het beleid van het gegevensgebruik wordt bepaald, kunt u de naleving van het gegevensgebruik met beleid afdwingen. Wanneer het activeren van publiek aan bestemmingen, dwingt Adobe Experience Platform automatisch gebruiksbeleid af als om het even welke schendingen voorkomen.

>[!NOTE]
>
>Dit document richt zich op de handhaving van het beleid inzake gegevensbeheer en instemming. Raadpleeg de documentatie over [attribuut-based toegangsbeheer](../../access-control/abac/overview.md).

## Vereisten

Deze gids vereist een goed begrip van de diensten van het Platform die bij automatische handhaving betrokken zijn. Raadpleeg de volgende documentatie voor meer informatie voordat u doorgaat met deze handleiding:

* [Adobe Experience Platform Data Governance](../home.md): Het kader waardoor Platform de naleving van het gegevensgebruik door het gebruik van etiketten en beleid afdwingt.
* [Klantprofiel in realtime](../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): De segmenteringsengine binnen [!DNL Platform] gebruikt om publiek van uw klantenprofielen tot stand te brengen die op klantengedrag en attributen worden gebaseerd.
* [Doelen](../../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en meer toestaan.

## Handelingenstroom {#flow}

Het volgende diagram illustreert hoe de beleidshandhaving in de gegevensstroom van publieksactivering wordt geïntegreerd:

![Een illustratie van hoe de beleidshandhaving in de gegevensstroom van publieksactivering wordt geïntegreerd.](../images/enforcement/enforcement-flow.png)

Wanneer een publiek voor het eerst wordt geactiveerd, [!DNL Policy Service] controles voor toepasselijk beleid op basis van de volgende factoren:

* De labels voor gegevensgebruik die zijn toegepast op velden en gegevenssets binnen het publiek dat moet worden geactiveerd.
* Het marketingdoel van de bestemming.
* De profielen waarvoor toestemming is gegeven om te worden opgenomen in de activering van het publiek, op basis van het beleid voor geconfigureerde toestemming.

>[!NOTE]
>
>Als er gegevensgebruikslabels zijn die slechts op bepaalde gebieden binnen een dataset (eerder dan de volledige dataset) zijn toegepast, komt de handhaving van die gebieden-vlakke etiketten op activering slechts onder de volgende voorwaarden voor:
>
>* De velden worden gebruikt in het publiek.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.

## Gegevensverbinding {#lineage}

De lijn van gegevens speelt een zeer belangrijke rol in hoe het beleid in Platform wordt afgedwongen. In algemene termen verwijst gegevenskoppeling naar de oorsprong van een set gegevens en naar wat er met de gegevens gebeurt (of waar deze naartoe worden verplaatst).

In de context van het Beleid van Gegevens, laat lijn gegevensgebruiksetiketten toe om van schema&#39;s aan stroomafwaartse diensten te verspreiden die hun gegevens, zoals het Profiel van de Klant in real time en Doelen verbruiken. Hierdoor kan het beleid op verschillende belangrijke punten in de gegevensreis door Platform worden geëvalueerd en afgedwongen, en wordt de gegevensconsument een context geboden waarin hij kan zien waarom een beleidsovertreding heeft plaatsgevonden.

In Experience Platform gaat het bij de beleidshandhaving om de volgende begrotingslijn:

1. Gegevens worden opgenomen in Platform en opgeslagen in **gegevenssets**.
1. Klantprofielen worden geïdentificeerd en samengesteld op basis van deze gegevenssets door gegevensfragmenten samen te voegen volgens de **samenvoegingsbeleid**.
1. Groepen profielen zijn verdeeld in **publiek** op basis van gemeenschappelijke kenmerken.
1. Soorten publiek wordt geactiveerd naar een lagere laag **bestemmingen**.

Elke fase in de bovenstaande tijdlijn vertegenwoordigt een entiteit die kan bijdragen tot de handhaving van het beleid, zoals in de onderstaande tabel wordt aangegeven:

| Gegevenslijnfase | Rol bij de handhaving van beleid |
| --- | --- |
| Gegevensset | Datasets bevatten gegevensgebruikslabels (toegepast op het niveau van het schemagebied of het volledige datasetniveau) die bepalen welke gebruiksgevallen de volledige dataset of specifieke gebieden kunnen worden gebruikt voor. Beleidsovertredingen treden op als een dataset of veld met bepaalde labels wordt gebruikt voor een doel dat door een beleid wordt beperkt.<br><br>Eventuele toestemmingskenmerken die van uw klanten worden verzameld, worden ook in gegevenssets opgeslagen. Als u toegang tot toestemmingsbeleid hebt, zullen om het even welke profielen die niet aan de vereisten van de toestemmingsattributen van uw beleid voldoen van publiek worden uitgesloten die aan een bestemming worden geactiveerd. |
| Samenvoegbeleid | Het beleid van de fusie is de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven wanneer het samenvoegen van fragmenten van veelvoudige datasets. De schendingen van het beleid zullen voorkomen als uw samenvoegbeleid wordt gevormd zodat de datasets met beperkte etiketten aan een bestemming worden geactiveerd. Zie de [overzicht van samenvoegbeleid](../../profile/merge-policies/overview.md) voor meer informatie . |
| Audience | De regels van de segmentatie bepalen welke attributen van klantenprofielen zouden moeten worden omvat. Afhankelijk van de velden die een segmentdefinitie bevat, neemt het publiek alle toegepaste gebruikslabels voor die velden over. Beleidsovertredingen treden op als u een publiek activeert waarvan de geërfte labels worden beperkt door het toepasselijke beleid van de doelbestemming, op basis van het geval van marketinggebruik. |
| Bestemming | Bij het instellen van een bestemming kan een marketingactie (ook wel een marketingcase genoemd) worden gedefinieerd. Dit gebruiksgeval correleert met een marketingactie zoals gedefinieerd in een beleid. Met andere woorden, de marketingactie die u voor een bestemming definieert, bepaalt welk beleid voor gegevensgebruik en toestemmingsbeleid van toepassing zijn op die bestemming.<br><br>Het beleid van het gegevensgebruik komt schendingen voor als u een publiek activeert de waarvan gebruiksetiketten voor de marketing actie van de doelbestemming beperkt zijn.<br><br>(Beta) Wanneer een publiek wordt geactiveerd, worden profielen die niet de vereiste toestemmingskenmerken voor de marketingactie bevatten (zoals gedefinieerd in uw toestemmingsbeleid), uitgesloten van het geactiveerde publiek. |

>[!IMPORTANT]
>
>Sommige beleidsregels voor gegevensgebruik kunnen twee of meer labels met een AND-relatie opgeven. Een beleid kan bijvoorbeeld een marketingactie beperken als labels `C1` EN `C2` beide aanwezig zijn, maar deze handeling niet beperkt indien slechts één van deze etiketten aanwezig is.
>
>Wat de automatische handhaving betreft, wordt in het kader van gegevensbeheer de activering van afzonderlijke doelgroepen niet als een combinatie van gegevens beschouwd. Daarom is het voorbeeld `C1 AND C2` beleid is **NOT** worden afgedwongen als deze labels in afzonderlijke doelgroepen zijn opgenomen. In plaats daarvan wordt dit beleid alleen afgedwongen wanneer beide labels bij activering in hetzelfde publiek aanwezig zijn.

Wanneer beleidsschendingen voorkomen, verstrekken de resulterende berichten die in UI verschijnen nuttige hulpmiddelen om de schending bijdragende gegevenslijn te onderzoeken helpen de kwestie oplossen. Meer details worden verstrekt in de volgende sectie.

## Beleidshandhavingsberichten {#enforcement}

In de volgende secties worden de verschillende beleidshandhavingsberichten beschreven die in de interface van het Platform worden weergegeven:

* [Beleidsschending gegevensgebruik](#data-usage-violation)
* [Goedkeuring van het beleid](#consent-policy-evaluation)

### Beleidsschending gegevensgebruik {#data-usage-violation}

Als een beleidsovertreding optreedt tijdens een poging een publiek te activeren (of [het aanbrengen van uitgeeft aan een reeds geactiveerd publiek](#policy-enforcement-for-activated-audiences)) de actie wordt voorkomen en een pop-up lijkt erop te wijzen dat een of meer beleidsmaatregelen zijn overtreden. Als een schending is opgetreden, wordt de **[!UICONTROL Save]** De knop is uitgeschakeld voor de entiteit die u wijzigt totdat de juiste componenten worden bijgewerkt om te voldoen aan het beleid voor gegevensgebruik.

Selecteer een beleidsovertreding in de linkerkolom van de pop-up om details voor die schending te tonen.

![](../images/enforcement/violation-policy-select.png)

Het schendingsbericht geeft een overzicht van het beleid dat is overtreden, met inbegrip van de voorwaarden het beleid wordt gevormd om te controleren, de specifieke actie die de schending teweegbracht, en een lijst van mogelijke resoluties voor de kwestie.

![](../images/enforcement/violation-summary.png)

Een grafiek van de gegevenslijn wordt getoond onder de schendingssamenvatting, toestaand u om te visualiseren welke datasets, fusiebeleid, publiek, en bestemmingen betrokken bij de beleidsschending waren. De entiteit die u momenteel wijzigt, wordt in de grafiek gemarkeerd en geeft aan welk punt in de flow de schending veroorzaakt. U kunt een entiteitsnaam in de grafiek selecteren om de detailpagina voor de entiteit in kwestie te openen.

![](../images/enforcement/data-lineage.png)

U kunt ook de opdracht **[!UICONTROL Filter]** icon (![](../images/enforcement/filter.png)) om de weergegeven entiteiten op categorie te filteren. U moet ten minste twee categorieën selecteren om de gegevens weer te geven.

![](../images/enforcement/lineage-filter.png)

Selecteren **[!UICONTROL List view]** om de gegevenskoppeling als een lijst weer te geven. Als u wilt terugschakelen naar de visuele grafiek, selecteert u **[!UICONTROL Path view]**.

![](../images/enforcement/list-view.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

Als u [gemaakt toestemmingsbeleid](../policies/user-guide.md#consent-policy) en u activeert een publiek naar een bestemming, kunt u zien hoe uw toestemmingsbeleid het percentage profielen beïnvloedt die in de activering inbegrepen zijn.

#### Verbetering van het beleid voor goedkeuring voor betaalde media {#consent-policy-enhancement}

Verbetering van de toestemming voor beleidshandhaving op [partij](../../destinations/destination-types.md#file-based) en [streaming](../../destinations/destination-types.md#streaming-destinations) er zijn bestemmingen gemaakt, inclusief betaalde mediaperichtingen. Deze uitbreiding is beschikbaar voor klanten van het privacyschild en het beveiligingsschild of het gezondheidsschild en verwijdert proactief profielen van batch- en streamingbestemmingen als de status van toestemming verandert. Het zorgt er ook voor dat wijzigingen in de toestemming onmiddellijk worden doorgevoerd, zodat het juiste publiek altijd wordt aangewezen.

Deze verbeteringen staan voor groter vertrouwen in uw marketing strategie toe aangezien het de behoefte voor marketers verwijdert om toestemmingsattributen aan hun segmentuitdrukking manueel toe te voegen. Dit zorgt ervoor dat er geen profielen onbedoeld worden gebruikt voor marketingervaringen wanneer de toestemming is ingetrokken of niet langer in aanmerking komt voor een toestemmingsbeleid. Het beleid van de marketingtoestemming dat regels vastlegt voor hoe toestemmings- of voorkeursgegevens moeten worden beheerd in verschillende marketingworkflows, wordt nu automatisch toegepast in activeringsworkflows in downstreamoplossingen.

>[!NOTE]
>
>Er zijn geen wijzigingen in de gebruikersinterface als gevolg van deze verbetering.

#### Evaluatie vóór activering

Zodra u het **[!UICONTROL Review]** stap wanneer [een doel activeren](../../destinations/ui/activation-overview.md), selecteert u **[!UICONTROL View applied policies]**.

![De knop Toegepast beleid weergeven in de doelworkflow voor activeren](../images/enforcement/view-applied-policies.png)

Er wordt een dialoogvenster voor beleidscontrole weergegeven waarin u een voorbeeld kunt zien van de invloed die het beleid voor uw toestemming heeft op het publiek met toestemming van het geactiveerde publiek.

![Dialoogvenster voor beleidscontrole voor toestemming in de gebruikersinterface van het platform](../images/enforcement/consent-policy-check.png)

Het dialoogvenster toont het publiek met toestemming voor één publiek per keer. Om de beleidsevaluatie voor een verschillend publiek te bekijken, gebruik dropdown menu boven het diagram om van de lijst te selecteren.

![De publieksschakelaar in de dialoog van de beleidscontrole.](../images/enforcement/audience-switcher.png)

Gebruik het linkerspoor om tussen het toepasselijke toestemmingsbeleid voor het geselecteerde publiek te schakelen. Beleid dat niet is geselecteerd, wordt weergegeven in &quot;[!UICONTROL Other policies]&quot; deel van het diagram.

![Beleidsschakelaar in het dialoogvenster Beleidscontrole](../images/enforcement/policy-switcher.png)

In het diagram wordt de overlapping tussen drie groepen profielen weergegeven:

1. Profielen die in aanmerking komen voor het geselecteerde publiek
1. Profielen die in aanmerking komen voor het geselecteerde toestemmingsbeleid
1. Profielen die in aanmerking komen voor het andere toepasselijke toestemmingsbeleid voor het publiek (aangeduid als &quot;[!UICONTROL Other policies]&quot; in het diagram)

De profielen die voor alle drie bovengenoemde groepen in aanmerking komen, vertegenwoordigen het publiek met instemming, samengevat in het juiste spoor.

![Samenvattingssectie in het dialoogvenster Beleidscontrole](../images/enforcement/summary.png)

Houd de muisaanwijzer boven een van de soorten publiek in het diagram om het aantal profielen in het diagram weer te geven.

![Het benadrukken van een diagramsectie in de dialoog van de beleidscontrole](../images/enforcement/highlight-segment.png)

Het publiek met toestemming wordt vertegenwoordigd door de centrale overlapping van het diagram en kan worden gemarkeerd zoals de andere secties.

![Toestemming voor publiek in diagram markeren](../images/enforcement/consented-audience.png)

#### Stroom run-handhaving

Wanneer de gegevens aan een bestemming worden geactiveerd, tonen de gegevens van de stroomlooppas het aantal identiteiten die wegens actief toestemmingsbeleid werden uitgesloten.

![Metrische gegevens van uitgesloten identiteiten voor een gegevensstroomuitvoering](../images/enforcement/dataflow-run-enforcement.png)

## Beleidshandhaving voor geactiveerd publiek {#policy-enforcement-for-activated-audiences}

De handhaving van het beleid is nog op publiek van toepassing nadat zij zijn geactiveerd, beperkt om het even welke veranderingen in een publiek of zijn bestemming die in een beleidsschending zouden resulteren. Als gevolg van [gegevensverbinding](#lineage) De werken in beleidshandhaving, kunnen om het even welke volgende acties potentieel een schending teweegbrengen:

* Labels voor gegevensgebruik bijwerken
* Gegevenssets voor een publiek wijzigen
* Voorspelingen voor het publiek wijzigen
* Doelconfiguraties wijzigen

Als een van de bovenstaande acties een schending veroorzaakt, wordt die actie verhinderd worden bewaard en een bericht van de beleidsschending wordt getoond, die ervoor zorgen dat uw geactiveerde publiek aan het beleid van het gegevensgebruik blijft voldoen wanneer wordt gewijzigd.

## Volgende stappen

In dit document wordt beschreven hoe automatische beleidshandhaving in Experience Platform werkt. Voor stappen op hoe te om beleidshandhaving in uw toepassingen programmatically te integreren gebruikend API vraag, zie de gids op [Op API gebaseerde handhaving](./api-enforcement.md).
