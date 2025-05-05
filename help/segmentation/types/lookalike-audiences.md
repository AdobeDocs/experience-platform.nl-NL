---
solution: Experience Platform
title: Soortgelijke soorten publiek
description: Leer hoe u nieuwe hoogwaardige doelgroepen in Adobe Experience Platform kunt kiezen met behulp van look-alike-soorten publiek.
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '2158'
ht-degree: 0%

---

# Hulplijn voor vergelijkbaar publiek

>[!IMPORTANT]
>
>De blik-gelijke inzichten en het blik-gelijke publiek zijn slechts beschikbaar in de **B2C- uitgave**.

In Adobe Experience Platform bieden look-alike-gebruikers intelligente inzichten op elk van uw doelgroepen en maken ze gebruik van op computers gebaseerde inzichten om klanten met een hoge waarde te identificeren en als doel in te stellen met uw marketingcampagnes.

Met look-alike soorten publiek, kunt u uitgebreide soorten publiek tot stand brengen die klanten gelijkend op uw hoog presterende publiek of doelklanten gelijkend op eerder omgezette publiek richten.

## Terminologie {#terminology}

Zorg ervoor dat u de volgende concepten begrijpt voordat u aan de slag gaat met look-alike-soorten:

- **het publiek van de Basis**: Het basispubliek is het publiek dat u meer inzichten over wilt weten. Dit is het publiek dat het blik-gelijke model **&#x200B;**&#x200B;op gebaseerd is.
- **blik-gelijkaardig model**: Een blik-gelijkaardig model is een machine het leren model dat op elk geschikt basispubliek zonder enige klanteninput wordt getraind. Elk model ziet er hetzelfde uit en creëert de invloedrijke factoren en grafieken van de gelijkenis. Een blik-gelijkaardig model wordt **niet** gescoord.
- **kijkt-als publiek**: Een blik-gelijkaardig publiek is het publiek dat wordt gecreeerd wanneer een blik-gelijkaardig model met een geselecteerde gelijkenisdrempel op het basispubliek wordt toegepast. U kunt veelvoudige blik-alike publiek tot stand brengen gebruikend het zelfde blik-als model. Het publiek ziet er hetzelfde uit: wat wordt er gescoord.
- **Totale adresseerbare publieksgrootte**: De totale adresseerbare publieksgrootte is het totale aantal profielen in de afgelopen 30 dagen minus de populatie van het basispubliek in de afgelopen 30 dagen. Bijvoorbeeld, als een klant 10 miljoen profielen in de afgelopen 30 dagen heeft, en het basispubliek 1 miljoen profielen in de afgelopen 30 dagen heeft, is de totale adresseerbare publieksgrootte 9 miljoen profielen.

## Subsidiabiliteit {#eligibility}

Om blik-gelijke inzichten te gebruiken, moet het basispubliek **&#x200B;**&#x200B;aan de volgende toelatingscriteria voldoen:

- Het basispubliek **moet** binnen Experience Platform worden gecreeerd.
   - Extern-geproduceerd publiek is **niet** geschikt voor blik-gelijke inzichten.
- Het basispubliek **moet** op het standaard fusiebeleid zijn.
- Het basispubliek **moet** geen gebieden gebruiken die door gegevensbeheer worden beperkt.

## Modeldetails van het model {#details}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_notEligible"
>title="Niet in aanmerking komend"
>abstract="Dit publiek komt momenteel niet in aanmerking voor look-alike inzichten aangezien het minder dan het minimumaantal profielen kan hebben dat voor opleiding wordt vereist of de profieluitvoer nog niet in werking is gesteld."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_processing"
>title="Verwerking"
>abstract="Dit publiek wordt momenteel verwerkt. Het kan tot 24 uur duren voordat de verwerking is voltooid. Probeer het later opnieuw."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_error"
>title="Fout"
>abstract="Er is een fout opgetreden bij het verwerken van dit model. Verwijder dit model en maak het opnieuw op of probeer het later opnieuw."

In Adobe Experience Platform gebruikt het model &#39;look-alike&#39; drie verschillende typen gegevenspunten:

- Gewone bevolking in de afgelopen 30 dagen
- Ervaar gebeurtenissen in de afgelopen 30 dagen die in het Real-Time Profiel van de Klant zijn opgenomen
- Profielkenmerken die in de afgelopen 30 dagen zijn opgenomen in het realtime profiel van de klant

Al deze gegevenspunten worden omgezet in zeer belangrijke waardeparen die in het blik-gelijkaardige model worden gevoerd. Alleen de sleutelwaardeparen met een significant percentage overeenkomende profielen blijven behouden.

Op dit moment wordt het model van look-alike elke 24 uur uitgevoerd en worden de invloedrijke factoren en gelijksoortige grafieken voor het basispubliek gemaakt en opnieuw gemaakt. Het scoren voor de look-alike doelgroepen wordt ook vaak uitgevoerd.

## Rechten {#entitlements}

De volgende rechten gelden voor het gebruik van look-alike-soorten:

- De klanten van Real-Time CDP Prime hebben recht op **5** actieve blik-alike publiek in productiesandboxen
- De klanten van Real-Time CDP Ultimate hebben recht op **20** actieve look-alike publiek in productiesandboxen
- De zandbakken van de ontwikkeling zijn beperkt tot **5** blik-gelijke publiek voor alle klanten van Real-Time CDP

Pakketten met invoegtoepassingen, die later beschikbaar zullen zijn, verhogen de rechten voor de productie van sandboxen met 20 soorten publiek per verpakking.

Neem contact op met uw Adobe-vertegenwoordiger om te bevestigen dat u toegang hebt tot look-alike soorten publiek.

## Zichtbare inzichten weergeven {#view}

Zichtbare inzichten zijn ingebouwd met de pagina met publieksdetails. Als u de look-alike inzichten voor een publiek wilt bekijken, selecteert u **[!UICONTROL Audiences]** in de linkernavigatiebalk, gevolgd door **[!UICONTROL Browse]** , en het publiek waarvoor u de inzichten wilt weergeven.

![ de knoop van het publiek wordt benadrukt, evenals het basispubliek dat voor blik-gelijke modellering wordt gebruikt.](../images/types/lookalike/browse.png)

De pagina met publieksdetails wordt weergegeven. Selecteer het tabblad **[!UICONTROL Look-alike insights]** om de kijkgelijke inzichten van het publiek weer te geven. De pagina **[!UICONTROL Look-alike insights]** wordt weergegeven. Deze pagina heeft drie hoofdelementen: de gelijkenis en de bereikgrafiek, het kijkachtige publiek en de invloedrijke factoren.

![ het blik-gelijke inzichten lusje wordt benadrukt, tonend de blik-gelijke inzichten voor het basispubliek.](../images/types/lookalike/look-alike-insights.png)

### Gelijksoortigheid en bereik {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Gelijksoortigheid en bereik"
>abstract="Met de gelijkenis en het bereik van de grafiek wordt het verwachte bereik van een publiek dat er uitziet boven een bepaalde score voor gelijkenis weergegeven. U kunt de muisaanwijzer boven een specifiek punt in de grafiek plaatsen om het percentage voor gelijkenis en het verwachte aantal profielen voor het momenteel gemarkeerde punt weer te geven."

De gelijkenis en bereiksectie toont een grafiek die het verwachte bereik van een publiek dat van look-alike bestaat uit profielen boven een bepaalde gelijkenisscore in kaart brengt. De gelijkenisscore vertegenwoordigt de **afstand** van gelijkenis tussen het profiel van het basispubliek en het blik-gelijke profiel van het inzicht.

![ de gelijkenis en bereikgrafiek wordt benadrukt.](../images/types/lookalike/similarity-and-reach.png)

In deze grafiek wordt op de x-as het percentage gemeten waarmee een profiel en leden van het geselecteerde publiek op elkaar lijken. De score op basis van de overeenkomst varieert van 0% tot 100%, waarbij een hogere score op basis van gelijkenis aangeeft dat een profiel in termen van invloedrijke factorwaarden dichter bij de leden van het geselecteerde publiek ligt.

Op de y-as wordt het verwachte aantal profielen weergegeven met het percentage voor gelijkenis dat overeenkomt met de overeenkomende waarde van de x-as. Deze verwachte telling van profielen varieert van 0 tot de totale adresseerbare publieksgrootte of 25 miljoen profielen, welke lager is. Deze as wordt gemeten op a **logaritmische schaal** om de leesbaarheid van de grafiek te verbeteren.

Gelieve te merken op dat de grafiek **cumulatief** van rechts naar links is. Dit betekent dat op om het even welk punt in de grafiek, de waarde van de y-as het aantal profielen is die een gelijkenis **boven** de gelijkenisdrempel hebben. Als de x-as bijvoorbeeld 60% is en de y-as 10 miljoen, betekent dit dat er 10 miljoen profielen zijn met een gelijkenis van 60% of meer ten opzichte van het basispubliek.

U kunt de muisaanwijzer boven een specifiek punt in de grafiek plaatsen om het percentage voor gelijkenis en het verwachte aantal profielen voor het momenteel gemarkeerde punt weer te geven.

### Soortgelijk publiek {#list}

De blik-gelijke sectie van publiek toont een lijst van alle blik-gelijke publiek dat eerder voor het geselecteerde basispubliek is gecreeerd.

![ de blik-alike sectie van het publiek wordt benadrukt.](../images/types/lookalike/select-laa.png)

### Influentiële factoren {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Influentiële factoren"
>abstract="Influentiële factoren zijn kenmerken, gebeurtenissen en publiekslidmaatschappen die belangrijk zijn voor het verklaren van gelijkenis van een profiel aan leden van het basispubliek. De etiketten en het beleid van het gegevensgebruik kunnen worden gebruikt om bepaalde gegevens uit te sluiten om als invloedrijke factoren in blik-gelijkaardige modellen worden beschouwd."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/types/lookalike-audiences.html#exclude" text="Gegevens uitsluiten"

In de sectie met invloedrijke factoren worden de 100 belangrijkste factoren weergegeven die van invloed zijn op het model dat er op lijkt voor het geselecteerde basispubliek. Deze invloedrijke factoren zijn de profielattributen, de ervaringsgebeurtenissen, en de publiekslidmaatschappen die het belangrijkst in het verklaren van gelijkenissen in het basispubliek zijn. Met een goed begrip van de belangrijkste invloedrijke factoren kunt u uw marketinginhoud beter aanpassen aan dit publiek en aan elk publiek dat u eruit maakt. Niet alle invloedrijke factoren die van invloed zijn op het model dat er op lijkt, worden weergegeven.

Voor invloedrijke factoren die numeriek zijn, kunnen de sleutelwaardeparen in emmers worden gezet, afhankelijk van het aantal verschillende waarden die sleutel heeft. Als u bijvoorbeeld een sleutel van `income` hebt, zijn er waarschijnlijk veel unieke waarden. Hierdoor worden de sleutelwaardeparen in emmers geplaatst die er als `income=[0 -> 30000]`, `income=[30000 -> 50000]` en `income=[50000 -> 100000]` kunnen uitzien.

Deze emmers worden regelmatig opnieuw berekend om ervoor te zorgen dat de gegevens worden bijgewerkt.

![ wordt de invloedrijke factorsectie benadrukt.](../images/types/lookalike/influential-factors.png)

>[!NOTE]
>
>De invloedrijke factoren worden gesorteerd in volgorde van belangrijkheid en zijn onafhankelijk van elkaar.

| Veld | Beschrijving |
| ----- | ----------- |
| Type | Het type gegevens waaruit de invloedsfactor wordt afgeleid. Dit kan een profielattribuut, een ervaringsgebeurtenis, of een publiekslidmaatschap zijn. |
| Sleutel | De naam van het gegevensveld. Voor sleutels van het type van publiekslidmaatschap, vertegenwoordigt deze waarde **namespace** van het publiek waar de gegevens uit komen. Mogelijke waarden zijn `ups` (Segmentation Service) en `AO` (Audience Orchestration). Voor sleutels van andere types, vertegenwoordigt deze waarde het XDM gebiedspad. Als het bedrijf Luma bijvoorbeeld een aangepast veld met de naam &#39;inkomen&#39; heeft, is de sleutel `_luma.income` |
| Waarde | De waarde varieert afhankelijk van de invloedrijke factor die het vertegenwoordigt. Voor profielkenmerken of ervaringsgebeurtenissen vertegenwoordigt dit veld de waarde of het waardebereik van het gegevensveld dat de gelijkenis met de leden van het basispubliek aangeeft. Het waardebereik wordt geschreven in de vorm `[A -> B]` , waarbij `A` het onderste bereik vertegenwoordigt terwijl `B` het hogere bereik vertegenwoordigt. Voor publiekslidmaatschappen, is dit gebied de naam van het publiek. |
| Belang | Het relatieve belang van de invloedrijke factor. Dit kan hoog, gemiddeld of laag zijn. |

## Een publiek met een look-alike maken {#create}

>[!IMPORTANT]
>
>U **kunt niet** een blik-gelijkaardig publiek als basispubliek voor een ander publiek gebruiken kijkt-als. Dat wil zeggen, kunt u **niet** geketineerde blik-gelijke publiek tot stand brengen.

Als u een publiek wilt maken dat lijkt op het weergeven, moet u het publiek selecteren waarvan u het publiek wilt baseren op het soort weergave. Als u de lijst met beschikbare soorten publiek wilt openen, selecteert u **[!UICONTROL Audiences]** in de linkernavigatiebalk, gevolgd door **[!UICONTROL Browse]** . De lijst met soorten publiek wordt weergegeven. Op deze pagina kunt u het publiek selecteren dat u wilt gebruiken als uw basispubliek.

![ de knoop van het publiek wordt benadrukt, evenals het basispubliek dat voor blik-gelijke modellering wordt gebruikt.](../images/types/lookalike/browse.png)

Selecteer **[!UICONTROL Create look-alike audience]** op de pagina met publieksdetails om een publiek te maken dat er hetzelfde uitziet.

![ wordt de [!UICONTROL Create look-alike audience] knoop benadrukt.](../images/types/lookalike/create-look-alike-audience.png)

De pop-up **[!UICONTROL Create a look-alike audience]** wordt weergegeven. Op deze pagina kunt u het percentage voor gelijkenis instellen voor het publiek dat er hetzelfde uitziet.

![ popover [!UICONTROL Create a look-alike audience] wordt getoond.](../images/types/lookalike/create-audience.png)

U kunt dit percentage op drie verschillende manieren instellen:

- Sleep de schuifregelaar om het percentage voor gelijkenis in te stellen
- Voer het percentage voor gelijkenis in het numerieke invoervak naast de schuifregelaar in
- Houd de cursor boven de grafiek en selecteer de gewenste locatie om het percentage voor gelijkenis in te stellen

U kunt details over het publiek ook bijwerken kijkt-als, met inbegrip van zijn naam en beschrijving. Standaard wordt de naam van het publiek voor de look-alike-toets gegenereerd op basis van de naam van het basispubliek en het eerder opgegeven percentage voor gelijkenis.

![ de basisinformatie wordt benadrukt binnen [!UICONTROL Create a look-alike audience] popover.](../images/types/lookalike/basic-info.png)

Selecteer **[!UICONTROL Create]** om het maken van een soort publiek te voltooien.

![ creeer knoop wordt benadrukt binnen [!UICONTROL Create a look-alike audience] popover.](../images/types/lookalike/create-audience.png)

Het nieuwe publiek van de blik-alike publiek kan in de **[!UICONTROL Look-alike audiences]** sectie van de pagina van de publieksdetails worden betreden, en is ook beschikbaar in het Portaal van de Publiek en voor andere stroomafwaartse gebruik. Houd er rekening mee dat het enige tijd duurt voordat het publiek voor het look-alike wordt gescoord. Totdat een score wordt toegekend, wordt het aantal profielen weergegeven op 0.

## Weergave-gelijke publieksdetails weergeven {#view-details}

Als u de details van een publiek met een look-alike wilt weergeven, selecteert u het publiek voor de look-alike in het gedeelte **[!UICONTROL Look-alike audiences]** van het basispubliek.

![ de blik-alike sectie van het publiek wordt benadrukt.](../images/types/lookalike/select-laa.png)

De pagina met publieksdetails wordt weergegeven. Voor meer informatie over deze pagina, te lezen gelieve de [ sectie van publieksdetails van het Poortoverzicht van het Poort van het Publiek ](../ui/audience-portal.md#audience-details).

![ de Details van het publiek worden blik-alike getoond.](../images/types/lookalike/laa-details.png)

## Gegevensvelden uitsluiten van modellering als vergelijkbaar {#exclude}

>[!IMPORTANT]
>
> **u** bent verantwoordelijk voor het verzekeren dat de gegevens, met inbegrip van gevoelige gegevens, correct geëtiketteerd zijn en dat het beleid van het gegevensgebruik is bepaald en toegelaten om aan de wettelijke en regelgevende verplichtingen te voldoen waaronder u werkt. U zou zich ook moeten bewust zijn dat de gegevensgebieden of segmentlidmaatschap die **niet** direct gecorreleerd met gegevensgebieden typisch verbonden aan gevoelige of beschermde gegevenstypes een bron van potentiële vooroordelen kunnen zijn. **u** bent verantwoordelijk in het analyseren van uw gegevens om, het aangewezen beleid van het gegevensgebruik op uw gegevens te identificeren te etiketteren en toe te passen, met inbegrip van om het even welke gegevensgebieden die volmacht voor gevoelige of beschermde gegevenstypes kunnen en van modellering zouden moeten worden uitgesloten.

De blik-gelijkaardig publiek kan worden gevormd om gegevensgebieden uit te sluiten die voor de &quot;van de Gegevens actie&quot;van de marketing van Gegevens worden beperkt door de relevante etiketten en het beleid van het gegevensgebruik toe te passen. Gegevens die zijn gelabeld als beperkt in gebruik voor gegevenswetenschap, worden uit overweging genomen wanneer u een kijkachtig publieksmodel opleidt en wanneer u een kijkachtig publiek uit het opgeleide model genereert. 

>[!NOTE]
>
>Het kan tot 48 uur duren voordat wijzigingen in de labels voor gegevensgebruik op het basispubliek van kracht worden.

Het standaard &quot;C9&quot;etiket kan worden gebruikt om gegevens te etiketteren die niet voor gegevenswetenschap zouden moeten worden gebruikt en kunnen worden afgedwongen door het standaardbeleid &quot;van de Gegevens van de Beperking&quot;toe te laten. U kunt ook aanvullende beleidsregels maken om gegevens te beperken met andere labels, waaronder gevoelige labels, voor gebruik in gegevenswetenschap. Voor meer informatie bij het beheren van het beleid van het gegevensgebruik, te lezen gelieve de [ gids UI van het gegevensgebruiksbeleid ](../../data-governance/policies/user-guide.md). Voor meer informatie bij het beheren van de etiketten van het gegevensgebruik, te lezen gelieve de [ gids UI van de etiketten van het gegevensgebruik ](../../data-governance/labels/user-guide.md).

Door gebrek, als een basispubliek geen contractetiketten heeft, zal het modelleringsproces voor blik-alike publiek **om het even welk** gebied, dataset, of publiek uitsluiten dat op het toegelaten privacybeleid voor uw organisatie wordt gebaseerd.

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u geleerd hoe u look-alike inzichten kunt bekijken en op basis van deze inzichten een soort publiek kunt maken dat lijkt op look-alike. Voor meer informatie over publiek in Adobe Experience Platform UI, te lezen gelieve de [ gids UI van de Dienst van de Segmentatie ](./overview.md).
