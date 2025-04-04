---
keywords: Experience Platform;home;populaire onderwerpen;Beleidshandhaving;Automatische handhaving;API-gebaseerde handhaving;gegevensbeheer
solution: Experience Platform
title: Automatische beleidscontrole
description: In dit document wordt beschreven hoe beleidsregels voor gegevensgebruik automatisch worden toegepast wanneer gebruikers naar bestemmingen in Experience Platform worden geactiveerd.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 0%

---

# Automatische beleidshandhaving

Labels en beleidsregels voor gegevensgebruik zijn beschikbaar voor alle Adobe Experience Platform-gebruikers. Bepaal het beleid van het gegevensgebruik en pas de etiketten van het gegevensgebruik toe om ervoor te zorgen dat om het even welke gevoelige, identificeerbare, of contractuele gegevens correct worden behandeld. Deze maatregelen helpen de regels voor gegevensbeheer van uw organisatie af te dwingen voor de manier waarop gegevens kunnen worden benaderd, verwerkt, opgeslagen en gedeeld.

Om uw organisatie tegen potentiële risico&#39;s en verplichtingen te helpen beschermen, handhaaft Experience Platform automatisch gebruiksbeleid als om het even welke schendingen voorkomen wanneer het activeren van publiek aan bestemmingen.

>[!IMPORTANT]
>
>Het beleid van de toestemming en de automatische handhaving van het toestemmingsbeleid zijn slechts beschikbaar voor organisaties die **het Schild van de Gezondheidszorg van Adobe** of **Privacy &amp; het Schild van de Veiligheid van Adobe** hebben gekocht.

Dit document richt zich op de handhaving van het beleid inzake gegevensbeheer en instemming. Voor informatie over toegangsbeheerbeleid, verwijs naar de documentatie over [ op attribuut-gebaseerde toegangsbeheer ](../../access-control/abac/overview.md).

## Vereisten

Deze handleiding vereist een goed begrip van de Experience Platform-diensten die betrokken zijn bij automatische handhaving. Raadpleeg de volgende documentatie voor meer informatie voordat u doorgaat met deze handleiding:

* [ het Beheer van Gegevens van Adobe Experience Platform ](../home.md): Het kader waardoor Experience Platform naleving van het gegevensgebruik door het gebruik van etiketten en beleid afdwingt.
* [ Real-Time Profiel van de Klant ](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [ de Dienst van de Segmentatie van Adobe Experience Platform ](../../segmentation/home.md): De segmenteringsmotor binnen [!DNL Experience Platform] wordt gebruikt om publiek van uw klantenprofielen tot stand te brengen die op klantengedrag en attributen worden gebaseerd.
* [ Doelen ](../../destinations/home.md): De bestemmingen zijn pre-gebouwde integratie met algemeen gebruikte toepassingen die voor de naadloze activering van gegevens van Experience Platform voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en meer toestaan.

## Handelingenstroom {#flow}

Het volgende diagram illustreert hoe de beleidshandhaving in de gegevensstroom van publieksactivering wordt geïntegreerd:

![ een illustratie van hoe de beleidshandhaving in de gegevensstroom van publieksactivering wordt geïntegreerd.](../images/enforcement/enforcement-flow.png)

Wanneer een publiek voor het eerst wordt geactiveerd, controleert [!DNL Policy Service] op het toepasselijke beleid op basis van de volgende factoren:

* De labels voor gegevensgebruik die zijn toegepast op velden en gegevenssets binnen het publiek dat moet worden geactiveerd.
* Het marketingdoel van de bestemming.
* De profielen waarvoor toestemming is gegeven om te worden opgenomen in de activering van het publiek, op basis van het beleid voor geconfigureerde toestemming.

>[!NOTE]
>
>Als er gegevensgebruikslabels zijn die alleen op bepaalde velden zijn toegepast, wordt de handhaving van die veldniveaulabels bij activering alleen uitgevoerd als aan ten minste een van de volgende voorwaarden is voldaan:
>
>* De velden worden gebruikt in het publiek.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.

## Gegevensverbinding {#lineage}

Gegevenskoppeling speelt een sleutelrol in de manier waarop het beleid in Experience Platform wordt afgedwongen. In algemene termen verwijst gegevenskoppeling naar de oorsprong van een set gegevens en naar wat er met de gegevens gebeurt (of waar deze naartoe worden verplaatst).

In de context van het Beleid van Gegevens, laat lijn gegevensgebruiksetiketten toe om van schema&#39;s aan stroomafwaartse diensten te verspreiden die hun gegevens, zoals het Profiel van de Klant in real time en Doelen verbruiken. Hierdoor kan het beleid op verschillende belangrijke punten in de gegevensreis door Experience Platform worden geëvalueerd en gehandhaafd, en wordt de gegevensconsument een context geboden waarin hij kan zien waarom een beleidsovertreding heeft plaatsgevonden.

In Experience Platform gaat het bij de handhaving van het beleid om het volgende traject:

1. Het gegeven wordt opgenomen in Experience Platform en opgeslagen in **datasets**.
1. De profielen van de klant worden geïdentificeerd en worden geconstrueerd van die datasets door gegevensfragmenten volgens het **fusiebeleid** samen te voegen.
1. De groepen profielen zijn verdeeld in **publiek** dat op gemeenschappelijke attributen wordt gebaseerd.
1. Het publiek wordt geactiveerd aan stroomafwaartse **bestemmingen**.

Elke fase in de bovenstaande tijdlijn vertegenwoordigt een entiteit die kan bijdragen tot de handhaving van het beleid, zoals in de onderstaande tabel wordt aangegeven:

| Gegevenslijnfase | Rol bij de handhaving van beleid |
| --- | --- |
| Gegevensset | Datasets bevatten gegevensgebruikslabels (toegepast op het niveau van het schemagebied of het volledige datasetniveau) die bepalen welke gebruiksgevallen de volledige dataset of specifieke gebieden kunnen worden gebruikt voor. Beleidsovertredingen treden op als een dataset of veld met bepaalde labels wordt gebruikt voor een doel dat door een beleid wordt beperkt.<br><br> om het even welke toestemmingsattributen die van uw klanten worden verzameld worden ook opgeslagen in datasets. Als u toegang tot toestemmingsbeleid hebt, zullen om het even welke profielen die niet aan de vereisten van de toestemmingsattributen van uw beleid voldoen van publiek worden uitgesloten die aan een bestemming worden geactiveerd. |
| Samenvoegbeleid | Het beleid van de fusie is de regels die Experience Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven wanneer het samenvoegen van fragmenten van veelvoudige datasets. De schendingen van het beleid zullen voorkomen als uw samenvoegbeleid wordt gevormd zodat de datasets met beperkte etiketten aan een bestemming worden geactiveerd. Zie het [ overzicht van het samenvoegingsbeleid ](../../profile/merge-policies/overview.md) voor meer informatie. |
| Doelgroep | De regels van de segmentatie bepalen welke attributen van klantenprofielen zouden moeten worden omvat. Afhankelijk van de velden die een segmentdefinitie bevat, neemt het publiek alle toegepaste gebruikslabels voor die velden over. Beleidsovertredingen treden op als u een publiek probeert te activeren waarvan de geërfte labels worden beperkt door het toepasselijke beleid van de doelbestemming, op basis van de Gebruiksscenario&#39;s voor marketingdoeleinden. |
| Bestemming | Bij het instellen van een bestemming kan een marketingactie (ook wel een marketingcase genoemd) worden gedefinieerd. Dit gebruiksgeval correleert met een marketingactie zoals gedefinieerd in een beleid. Met andere woorden, de marketingactie die u voor een bestemming definieert, bepaalt welk beleid voor gegevensgebruik en toestemmingsbeleid van toepassing zijn op die bestemming.<br><br> de schendingen van het het gebruiksbeleid van Gegevens komen voor als u probeert om een publiek te activeren de waarvan gebruiksetiketten voor de marketing van de doelbestemming actie beperkt zijn.<br><br> (Beta) Wanneer een publiek wordt geactiveerd, worden profielen die niet de vereiste toestemmingskenmerken voor de marketingactie bevatten (zoals gedefinieerd in uw toestemmingsbeleid), uitgesloten van het geactiveerde publiek. |

>[!IMPORTANT]
>
>Sommige beleidsregels voor gegevensgebruik kunnen twee of meer labels met een AND-relatie opgeven. Een beleid kan bijvoorbeeld een marketingactie beperken als labels `C1` EN `C2` beide aanwezig zijn, maar beperkt dezelfde actie niet als slechts een van deze labels aanwezig is.
>
>Wat de automatische handhaving betreft, wordt in het kader van gegevensbeheer de activering van afzonderlijke doelgroepen niet als een combinatie van gegevens beschouwd. Daarom wordt het voorbeeld `C1 AND C2` beleid **NIET** afgedwongen als deze etiketten in afzonderlijk publiek inbegrepen zijn. In plaats daarvan wordt dit beleid alleen afgedwongen wanneer beide labels bij activering in hetzelfde publiek aanwezig zijn.

Wanneer beleidsschendingen voorkomen, verstrekken de resulterende berichten die in UI verschijnen nuttige hulpmiddelen om de schending bijdragende gegevenslijn te onderzoeken helpen de kwestie oplossen. Meer details worden verstrekt in de volgende sectie.

## Beleidshandhavingsberichten {#enforcement}

In de volgende secties worden de verschillende beleidshandhavingsberichten beschreven die in de gebruikersinterface van Experience Platform worden weergegeven:

* [Beleidsschending gegevensgebruik](#data-usage-violation)
* [Goedkeuring van het beleid](#consent-policy-evaluation)

### Beleidsschending gegevensgebruik {#data-usage-violation}

Als een beleidsschending voorkomt van het proberen om een publiek (of [ te activeren die uitgeeft aan een reeds geactiveerd publiek ](#policy-enforcement-for-activated-audiences)) te activeren wordt de actie verhinderd en popover lijkt erop wijzend dat één of meerdere beleid zijn geschonden. Nadat een schending is geactiveerd, wordt de knop **[!UICONTROL Save]** uitgeschakeld voor de entiteit die u wijzigt, totdat de juiste componenten worden bijgewerkt om te voldoen aan het beleid voor gegevensgebruik.

Selecteer een beleidsnaam om details voor die schending te tonen.

![ een dialoog die op een beleidsschending wijst is voorgekomen met de benadrukte beleidsnaam.](../images/enforcement/violation-policy-select.png)

Het schendingsbericht geeft een overzicht van het beleid dat is overtreden, met inbegrip van de voorwaarden het beleid wordt gevormd om te controleren, de specifieke actie die de schending teweegbracht, en een lijst van mogelijke resoluties voor de kwestie.

![ de dialoog van de beleidsschending van A met de benadrukte geschonden schendingssamenvatting.](../images/enforcement/violation-summary.png)

Een grafiek van de gegevenslijn wordt getoond onder de schendingssamenvatting, toestaand u om te visualiseren welke datasets, fusiebeleid, publiek, en bestemmingen betrokken bij de beleidsschending waren. De entiteit die u momenteel wijzigt, wordt in de grafiek gemarkeerd en geeft aan welk punt in de flow de schending veroorzaakt. U kunt een entiteitsnaam in de grafiek selecteren om de detailpagina voor de entiteit in kwestie te openen.

![ dialoog van de beleidsschending van A met de benadrukte grafiek van de gegevenslijn.](../images/enforcement/data-lineage.png)

U kunt het **[!UICONTROL Filter]** pictogram (![ ook gebruiken A filterpictogram.](/help/images/icons/filter.png)) om de weergegeven entiteiten op categorie te filteren. U moet ten minste twee categorieën selecteren om de gegevens weer te geven.

![ dialoog van de beleidsschending van A met de benadrukte filter en drop-down menu van de gegevenslijn.](../images/enforcement/lineage-filter.png)

Selecteer **[!UICONTROL List view]** om de gegevenskoppeling als een lijst weer te geven. Selecteer **[!UICONTROL Path view]** om terug te schakelen naar de visuele grafiek.

![ de dialoog van de beleidsschending van A met de benadrukte mening van de de wegweg van de gegevenslijn.](../images/enforcement/list-view.png)

#### Labels zijn toegepast {#labels-successfully-applied}

Als u het beleid van het gegevensgebruik creeert alvorens u uw schemagebieden etiketteert, kunt u een dialoog van de schending van het governancebeleid ontmoeten zodra u etiketten op uw schema toepast. In dit geval kunt u een deel van uw schema labelen. Het tabblad [!UICONTROL Labels successfully applied] geeft aan welke labels zijn toegepast, aangezien er voor dat veld geen beleidsbeperkingen gelden.

Gebruik het diagram van de gegevenslijn om te begrijpen welke andere configuratieveranderingen moeten worden aangebracht alvorens u het etiket aan uw schemagebied kunt toevoegen.

![ dialoog van de beleidsschending van A met het [!UICONTROL Labels successfully applied] benadrukte lusje.](../images/enforcement/labels-successfully-applied.png)

### Goedkeuring van het beleid {#consent-policy-evaluation}

Wanneer het activeren van een publiek aan een bestemming, kunt u zien hoe uw [ toestemmingsbeleid ](../policies/user-guide.md) het bereik van uw publiek tijdens het [ overzichtsstadium van het [!UICONTROL Activate Destinations] werkschema ](#pre-activation-evaluation) beïnvloedt.

>[!NOTE]
>
>Beleid voor toestemming is alleen beschikbaar voor organisaties die Adobe Healthcare Shield of Adobe Privacy &amp; Security Shield hebben aangeschaft.

#### Verbetering van het beleid voor goedkeuring voor betaalde media {#consent-policy-enhancement}

Een verhoging om beleidshandhaving op [ partij ](../../destinations/destination-types.md#file-based) en [ het stromen ](../../destinations/destination-types.md#streaming-destinations) bestemmingen met inbegrip van betaalde media activering goed te keuren is gemaakt. Deze uitbreiding is beschikbaar voor klanten van het privacyschild en het beveiligingsschild of het gezondheidsschild en verwijdert proactief profielen van batch- en streamingbestemmingen als de status van toestemming verandert. Het zorgt er ook voor dat wijzigingen in de toestemming onmiddellijk worden doorgevoerd, zodat het juiste publiek altijd wordt aangewezen.

Deze verbeteringen staan voor groter vertrouwen in uw marketing strategie toe aangezien het de behoefte voor marketers verwijdert om toestemmingsattributen aan hun segmentuitdrukking manueel toe te voegen. Dit zorgt ervoor dat er geen profielen onbedoeld worden gebruikt voor marketingervaringen wanneer de toestemming is ingetrokken of niet langer in aanmerking komt voor een toestemmingsbeleid. Het beleid van de marketingtoestemming dat regels vastlegt voor hoe toestemmings- of voorkeursgegevens moeten worden beheerd in verschillende marketingworkflows, wordt nu automatisch toegepast in activeringsworkflows in downstreamoplossingen.

>[!NOTE]
>
>Er zijn geen wijzigingen in de gebruikersinterface als gevolg van deze verbetering.

#### Evaluatie vóór activering {#pre-activation-evaluation}

Zodra u de **[!UICONTROL Review]** stap bereikt wanneer [ het activeren van een bestemming ](../../destinations/ui/activation-overview.md), selecteer **[!UICONTROL View applied policies]**.

![ Mening toegepaste beleidsknoop in activeert bestemmingswerkschema ](../images/enforcement/view-applied-policies.png)

Er wordt een dialoogvenster voor beleidscontrole weergegeven waarin u een voorbeeld kunt zien van de invloed die het beleid voor uw toestemming heeft op het publiek met instemming van het publiek dat moet worden geactiveerd.

![ de dialoog van de de beleidscontrole van de toestemming in Experience Platform UI ](../images/enforcement/consent-policy-check.png)

Het dialoogvenster toont het publiek met toestemming voor één publiek per keer. Om de beleidsevaluatie voor een verschillend publiek te bekijken, gebruik dropdown menu boven het diagram om van de lijst te selecteren.

![ de publieksschakelaar in de dialoog van de beleidscontrole.](../images/enforcement/audience-switcher.png)

Gebruik het linkerspoor om tussen het toepasselijke toestemmingsbeleid voor het geselecteerde publiek te schakelen. Het beleid dat niet wordt geselecteerd wordt vertegenwoordigd in &quot;[!UICONTROL Other policies]&quot;sectie van het diagram.

![ de schakelaar van het Beleid in de dialoog van de beleidscontrole ](../images/enforcement/policy-switcher.png)

In het diagram wordt de overlapping tussen drie groepen profielen weergegeven:

1. Profielen die in aanmerking komen voor het geselecteerde publiek
1. Profielen die in aanmerking komen voor het geselecteerde toestemmingsbeleid
1. Profielen die voor het andere toepasselijke toestemmingsbeleid voor het publiek (die als &quot;[!UICONTROL Other policies]&quot;in het diagram wordt bedoeld) in aanmerking komen

De profielen die voor alle drie bovengenoemde groepen in aanmerking komen, vertegenwoordigen het publiek met instemming, samengevat in het juiste spoor.

![ Summiere sectie in de dialoog van de beleidscontrole ](../images/enforcement/summary.png)

Houd de muisaanwijzer boven een van de soorten publiek in het diagram om het aantal profielen in het diagram weer te geven.

![ benadrukkend een diagramsectie in de dialoog van de beleidscontrole ](../images/enforcement/highlight-segment.png)

Het publiek met toestemming wordt vertegenwoordigd door de centrale overlapping van het diagram en kan worden gemarkeerd zoals de andere secties.

![ benadrukkend het toegelaten publiek in het diagram ](../images/enforcement/consented-audience.png)

#### Stroom run-handhaving

Wanneer de gegevens aan een bestemming worden geactiveerd, tonen de gegevens van de stroomlooppas het aantal identiteiten die wegens actief toestemmingsbeleid werden uitgesloten.

![ Uitgesloten identiteitsmetriek voor een dataflow looppas ](../images/enforcement/dataflow-run-enforcement.png)

## Beleidshandhaving voor geactiveerd publiek {#policy-enforcement-for-activated-audiences}

De handhaving van het beleid is nog op publiek van toepassing nadat zij zijn geactiveerd, beperkt om het even welke veranderingen in een publiek of zijn bestemming die in een beleidsschending zouden resulteren. Wegens hoe [ gegevenslijn ](#lineage) in beleidshandhaving werkt, kunnen om het even welke volgende acties een schending potentieel teweegbrengen:

* Labels voor gegevensgebruik bijwerken
* Gegevenssets voor een publiek wijzigen
* Voorspelingen voor het publiek wijzigen
* Doelconfiguraties wijzigen

Als een van de bovenstaande acties een schending veroorzaakt, wordt die actie verhinderd worden bewaard en een bericht van de beleidsschending wordt getoond, die ervoor zorgen dat uw geactiveerde publiek aan het beleid van het gegevensgebruik blijft voldoen wanneer wordt gewijzigd.

## Volgende stappen

In dit document wordt beschreven hoe automatische beleidshandhaving in Experience Platform werkt. Voor stappen op hoe te om beleidshandhaving in uw toepassingen programmatically te integreren gebruikend API vraag, zie de gids op [ op API-Gebaseerde handhaving ](./api-enforcement.md).
