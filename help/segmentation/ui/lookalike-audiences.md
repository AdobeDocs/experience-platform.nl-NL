---
solution: Experience Platform
title: Soortgelijke soorten publiek
description: Leer hoe u nieuwe hoogwaardige doelgroepen in Adobe Experience Platform kunt kiezen met behulp van look-Alike publiek.
badgeLimitedAvailability: label="Beperkte beschikbaarheid" type=Caution
source-git-commit: 4bd26857d2c714cd629fc46dbb9b6da6a29358c8
workflow-type: tm+mt
source-wordcount: '2088'
ht-degree: 0%

---


# Hulplijn voor soort publiek

>[!IMPORTANT]
>
>Let op: look-alike inzichten en look-Alike publiek bevinden zich in **beperkte beschikbaarheid**.

In Adobe Experience Platform bieden look-Alike Publiek intelligente inzichten op elk van uw publiek en maken het gebruik van computerleergebaseerd inzicht om klanten met een hoge waarde te identificeren en als doel in te stellen met uw marketingcampagnes.

Met kijkachtige Soorten Soorten Soorten publiek, kunt u uitgebreide soorten publiek tot stand brengen die klanten gelijkend op uw hoog presterende publiek of doelklanten gelijkend op eerder omgezette publiek richten.

## Terminologie {#terminology}

Voordat u aan de slag gaat met Soortgelijke soorten publiek, moet u de volgende concepten begrijpen:

- **Basispubliek**: Het basispubliek is het publiek waarover je meer inzichten wilt weten. Dit is het publiek dat het look-alike model is **gebaseerd** op.
- **Labeljauwmodel**: Een model dat lijkt op een computer is een leermodel dat is opgeleid voor elk in aanmerking komend basispubliek zonder dat de klant daar iets mee doet. Elk model ziet er hetzelfde uit en creëert de invloedrijke factoren en grafieken van de gelijkenis. Een look-alike-model doet dit **niet** wordt gescoord.
- **Kijk-naar-gelijkend publiek**: Een soort publiek dat er uitziet, is het publiek dat wordt gemaakt wanneer een model met een gelijkenis en een drempel voor geselecteerde gelijkenis wordt toegepast op het basispubliek. U kunt veelvoudige blik-als publiek tot stand brengen gebruikend het zelfde blik-als model. Het publiek ziet er anders uit: wat wordt er gescoord.
- **Totale adresseerbare publieksgrootte**: De totale adresseerbare publieksgrootte is het totale aantal profielen in de afgelopen 30 dagen minus de populatie van het basispubliek in de afgelopen 30 dagen. Bijvoorbeeld, als een klant 10 miljoen profielen in de afgelopen 30 dagen heeft, en het basispubliek 1 miljoen profielen in de afgelopen 30 dagen heeft, is de totale adresseerbare publieksgrootte 9 miljoen profielen.

## Modeldetails van het model {#details}

In Adobe Experience Platform gebruikt het model &#39;look-alike&#39; drie verschillende typen gegevenspunten:

- Gewone bevolking in de afgelopen 30 dagen
- Ervaar gebeurtenissen in de afgelopen 30 dagen die in het Real-Time Profiel van de Klant zijn opgenomen
- Profielkenmerken die in de afgelopen 30 dagen zijn opgenomen in het realtime profiel van de klant

Al deze gegevenspunten worden omgezet in zeer belangrijke waardeparen die in het blik-gelijkaardige model worden gevoerd. Alleen de sleutelwaardeparen met een significant percentage overeenkomende profielen blijven behouden.

Op dit moment wordt het model van look-alike elke 24 uur uitgevoerd en worden de invloedrijke factoren en gelijksoortige grafieken voor het basispubliek gemaakt en opnieuw gemaakt. Het scoren voor het kijkt-Alike publiek wordt ook vaak in werking gesteld.

## Rechten {#entitlements}

De volgende rechten gelden voor het gebruik van look-Alike-soorten publiek:

- Real-Time CDP Primaire klanten hebben recht op **5** actief soort publiek in productiesandboxen
- Real-Time CDP Ultimate-klanten hebben recht op **20** actief soort publiek in productiesandboxen
- Ontwikkelingssandboxen zijn beperkt tot **5** Soortgelijke soorten publiek voor alle Real-Time CDP-klanten

Pakketten met invoegtoepassingen, die later beschikbaar zullen zijn, verhogen de rechten voor de productie van sandboxen met 20 soorten publiek met een look-Alike per pack.

Neem contact op met uw Adobe als u wilt controleren of u toegang hebt tot Soortgelijke soorten publiek.

## Zichtbare inzichten weergeven {#view}

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

Zichtbare inzichten zijn ingebouwd met de pagina met publieksdetails. Als u de look-alike inzichten voor een publiek wilt bekijken, selecteert u **[!UICONTROL Audiences]** in de linkernavigatiebalk, gevolgd door **[!UICONTROL Browse]** en het publiek waarvoor u de inzichten wilt bekijken.

![De knop Soorten publiek wordt gemarkeerd en het basispubliek dat wordt gebruikt voor modellering op basis van look-alike.](../images/ui/lookalike-audiences/browse.png)

De pagina met publieksdetails wordt weergegeven. Selecteren **[!UICONTROL Look-alike insights]** om de kijkachtige inzichten van het publiek te bekijken. De pagina **[!UICONTROL Look-alike insights]** wordt weergegeven. Deze pagina bevat drie hoofdelementen: de gelijkenis en bereikgrafiek, het soort publiek dat er uitziet, en de invloedrijke factoren.

![Het tabblad Zichtbare inzichten wordt gemarkeerd en geeft de look-alike inzichten voor het basispubliek weer.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Gelijksoortigheid en bereik {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Gelijksoortigheid en bereik"
>abstract="Door de gelijkenis en het bereik van de grafiek wordt het verwachte bereik van een soort publiek dat eruit bestaat profielen boven een bepaalde score voor gelijkenis. U kunt de muisaanwijzer boven een specifiek punt in de grafiek plaatsen om het percentage voor gelijkenis en het verwachte aantal profielen voor het momenteel gemarkeerde punt weer te geven."

De gelijkenis en bereiksectie toont een grafiek die het verwachte bereik van een soort publiek dat kijkt-weg uit profielen boven een bepaalde gelijkheidsscore bestaat. De overeenkomstenscore vertegenwoordigt de **afstand** van overeenkomst tussen het profiel van het basispubliek en het profiel van het kijkgelijke inzicht.

![De gelijkenis en bereikgrafiek worden gemarkeerd.](../images/ui/lookalike-audiences/similarity-and-reach.png)

In deze grafiek wordt op de x-as het percentage gemeten waarmee een profiel en leden van het geselecteerde publiek op elkaar lijken. De score op basis van de overeenkomst varieert van 0% tot 100%, waarbij een hogere score op basis van gelijkenis aangeeft dat een profiel in termen van invloedrijke factorwaarden dichter bij de leden van het geselecteerde publiek ligt.

Op de y-as wordt het verwachte aantal profielen weergegeven met het percentage voor gelijkenis dat overeenkomt met de overeenkomende waarde van de x-as. Deze verwachte telling van profielen varieert van 0 tot de totale adresseerbare publieksgrootte of 25 miljoen profielen, welke lager is. Deze as wordt gemeten op een **logaritmische schaal** de leesbaarheid van de grafiek verbeteren.

De grafiek is **cumulatief** van rechts naar links. Dit betekent dat op elk punt in de grafiek de waarde van de y-as het aantal profielen is dat op dezelfde manier werkt **boven** de drempel voor gelijkenis. Als de x-as bijvoorbeeld 60% is en de y-as 10 miljoen, betekent dit dat er 10 miljoen profielen zijn met een gelijkenis van 60% of meer ten opzichte van het basispubliek.

U kunt de muisaanwijzer boven een specifiek punt in de grafiek plaatsen om het percentage voor gelijkenis en het verwachte aantal profielen voor het momenteel gemarkeerde punt weer te geven.

### Soortgelijke soorten publiek {#list}

In de sectie Soortgelijke soorten publiek wordt een lijst weergegeven met alle soorten publiek die er eerder voor het geselecteerde basispubliek zijn gemaakt.

![De sectie Soortgelijke soorten publiek wordt gemarkeerd.](../images/ui/lookalike-audiences/select-laa.png)

### Influentiële factoren {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Influentiële factoren"
>abstract="Influentiële factoren zijn kenmerken, gebeurtenissen en publiekslidmaatschappen die belangrijk zijn voor het verklaren van gelijkenis van een profiel aan leden van het basispubliek. De etiketten en het beleid van het gegevensgebruik kunnen worden gebruikt om bepaalde gegevens uit te sluiten om als invloedrijke factoren in blik-gelijkaardige modellen worden beschouwd."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html?lang=en#exclude" text="Gegevens uitsluiten"

In de sectie met invloedrijke factoren worden de 100 belangrijkste factoren weergegeven die van invloed zijn op het model dat er op lijkt voor het geselecteerde basispubliek. Deze invloedrijke factoren zijn de profielattributen, de ervaringsgebeurtenissen, en de publiekslidmaatschappen die het belangrijkst in het verklaren van gelijkenissen in het basispubliek zijn. Met een goed begrip van de belangrijkste invloedrijke factoren kunt u uw marketinginhoud voor dit publiek en alle soorten publiek die u eruit maakt, beter personaliseren. Niet alle invloedrijke factoren die van invloed zijn op het model dat er op lijkt, worden weergegeven.

Voor invloedrijke factoren die numeriek zijn, kunnen de sleutelwaardeparen in emmers worden gezet, afhankelijk van het aantal verschillende waarden die sleutel heeft. Als u bijvoorbeeld een sleutel van `income`Er zijn waarschijnlijk veel unieke waarden. Dientengevolge zullen de belangrijkste waardeparen in emmers worden geplaatst die als konden kijken `income=[0 -> 30000]`, `income=[30000 -> 50000]`, en `income=[50000 -> 100000]`.

Deze emmers worden regelmatig opnieuw berekend om ervoor te zorgen dat de gegevens worden bijgewerkt.

![De sectie invloedrijke factoren wordt benadrukt.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>De invloedrijke factoren worden gesorteerd in volgorde van belangrijkheid en zijn onafhankelijk van elkaar.

| Veld | Beschrijving |
| ----- | ----------- |
| Type | Het type gegevens waaruit de invloedsfactor wordt afgeleid. Dit kan een profielattribuut, een ervaringsgebeurtenis, of een publiekslidmaatschap zijn. |
| Sleutel | De naam van het gegevensveld. Voor sleutels van het type van publiekslidmaatschap, vertegenwoordigt deze waarde **namespace** van het publiek waar de gegevens vandaan komen. Mogelijke waarden zijn `ups` (Segmenteringsdienst) en `AO` (Audience Orchestration). Voor sleutels van andere types, vertegenwoordigt deze waarde het XDM gebiedspad. Als het bedrijf Luma bijvoorbeeld een aangepast veld heeft met de naam &#39;inkomen&#39;, is de sleutel `_luma.income` |
| Waarde | De waarde varieert afhankelijk van de invloedrijke factor die het vertegenwoordigt. Voor profielkenmerken of ervaringsgebeurtenissen vertegenwoordigt dit veld de waarde of het waardebereik van het gegevensveld dat de gelijkenis met de leden van het basispubliek aangeeft. Het waardebereik wordt geschreven in het formulier `[A -> B]`, waarbij `A` het laagste bereik vertegenwoordigt terwijl `B` geeft het hogere bereik aan. Voor publiekslidmaatschappen, is dit gebied de naam van het publiek. |
| Belang | Het relatieve belang van de invloedrijke factor. Dit kan hoog, gemiddeld of laag zijn. |

## Een soort publiek maken {#create}

>[!IMPORTANT]
>
>U **kan** Gebruik een publiek van het soort kijkt-Alike als als basispubliek voor een ander publiek van het soort kijkt-Alike. Dat wil zeggen, u **kan** Maak een keten van soorten publiek.

Als u een soort publiek wilt maken dat er uitziet, moet u het publiek selecteren waarvan u het soort publiek wilt baseren. Als u toegang wilt tot uw lijst met beschikbare soorten publiek, selecteert u **[!UICONTROL Audiences]** in de linkernavigatiebalk, gevolgd door **[!UICONTROL Browse]**. De lijst met soorten publiek wordt weergegeven. Op deze pagina kunt u het publiek selecteren dat u wilt gebruiken als uw basispubliek.

![De knop Soorten publiek wordt gemarkeerd en het basispubliek dat wordt gebruikt voor modellering op basis van look-alike.](../images/ui/lookalike-audiences/browse.png)

Selecteer op de pagina met publieksdetails de optie **[!UICONTROL Create look-alike audience]** om te beginnen met het maken van een soort publiek.

![De [!UICONTROL Create look-alike audience] wordt gemarkeerd.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

De **[!UICONTROL Create a look-alike audience]** wordt weergegeven. Op deze pagina kunt u het percentage voor gelijkenis instellen voor het vergelijkbare publiek.

![De [!UICONTROL Create a look-alike audience] popover wordt weergegeven.](../images/ui/lookalike-audiences/create-audience.png)

U kunt dit percentage op drie verschillende manieren instellen:

- Sleep de schuifregelaar om het percentage voor gelijkenis in te stellen
- Voer het percentage voor gelijkenis in het numerieke invoervak naast de schuifregelaar in
- Houd de cursor boven de grafiek en selecteer de gewenste locatie om het percentage voor gelijkenis in te stellen

U kunt ook details over het soort publiek, met inbegrip van zijn naam en beschrijving, bijwerken. Door gebrek, zal de blik-Alike naam van het Publiek worden geproduceerd gebaseerd op de naam van het basispubliek en het eerder gespecificeerde gelijkenispercentage.

![De basisinformatie wordt in de [!UICONTROL Create a look-alike audience] popover.](../images/ui/lookalike-audiences/basic-info.png)

Selecteren **[!UICONTROL Create]** om uw look-Alike Audience te voltooien.

![De knop Maken is gemarkeerd in het dialoogvenster [!UICONTROL Create a look-alike audience] popover.](../images/ui/lookalike-audiences/create-audience.png)

Het nieuwe publiek van het soort kijkt-Alike kan in worden betreden **[!UICONTROL Look-alike audiences]** van de pagina met publieksdetails, en is ook beschikbaar in het Portaal van de Publiek en voor andere downstreamtoepassingen. Houd er rekening mee dat het enige tijd duurt voordat de look-Alike Audience-score wordt toegekend. Totdat een score wordt toegekend, wordt het aantal profielen weergegeven op 0.

## Details over het uiterlijk van het publiek weergeven {#view-details}

Als u details van een soort publiek wilt weergeven, selecteert u het vergelijkbare publiek in het dialoogvenster **[!UICONTROL Look-Alike Audiences]** van het basispubliek.

![De sectie Soortgelijke soorten publiek wordt gemarkeerd.](../images/ui/lookalike-audiences/select-laa.png)

De pagina met publieksdetails wordt weergegeven. Lees voor meer informatie over deze pagina de [sectie met publieksdetails van de gebruikersinterface voor segmentatieservice](./overview.md#audience-details).

![De details van het kijkachtige publiek worden getoond.](../images/ui/lookalike-audiences/laa-details.png)

## Gegevensvelden uitsluiten van modellering als vergelijkbaar {#exclude}

Het kijkachtige publiek kan worden gevormd om gegevensgebieden uit te sluiten die voor de het in de handel brengen &quot;van Gegevens actie&quot;door de relevante etiketten en het beleid van het gegevensgebruik beperkt zijn. Gegevens die als beperkt van gebruik voor gegevenswetenschap worden geëtiketteerd zullen uit overweging worden verwijderd wanneer het leiden van een look-Alike model van het Publiek en wanneer het produceren van een look-Alike Publiek van het opgeleide model. 

Het standaard &quot;C9&quot;etiket kan worden gebruikt om gegevens te etiketteren die niet voor gegevenswetenschap zouden moeten worden gebruikt en kunnen worden afgedwongen door het standaardbeleid &quot;van de Gegevens van de Beperking&quot;toe te laten. U kunt ook aanvullende beleidsregels maken om gegevens te beperken met andere labels, waaronder gevoelige labels, voor gebruik in gegevenswetenschap. Lees voor meer informatie over het beheer van het beleid voor gegevensgebruik de [UI-gids voor gegevensgebruiksbeleid](../../data-governance/policies/user-guide.md). Lees voor meer informatie over het beheren van labels voor gegevensgebruik de [UI-handleiding voor gegevensgebruikslabels](../../data-governance/labels/user-guide.md).

Door gebrek, zal het modelleringsproces voor look-Alike Publiek uitsluiten **alle** gebied, dataset, of publiek dat op het toegelaten privacybeleid voor uw organisatie wordt gebaseerd. Als het basispubliek geen contractetiketten heeft, zal het modelleringsproces uitsluiten **alle** gebied, dataset, of publiek dat op het toegelaten privacybeleid voor uw organisatie wordt gebaseerd.

Houd er rekening mee dat **u** ervoor zorgen dat gegevens, inclusief gevoelige gegevens, op de juiste wijze worden geëtiketteerd en dat het beleid voor gegevensgebruik is gedefinieerd en ingeschakeld om te voldoen aan wettelijke en bestuursrechtelijke verplichtingen waaronder u werkt. U zou zich ook moeten bewust zijn dat de gegevensgebieden of segmentlidmaatschap die zijn **niet** rechtstreeks gecorreleerd met gegevensvelden die typisch worden geassocieerd met gevoelige of beschermde gegevenstypen kan een bron van potentiële afwijking zijn. **U** zijn verantwoordelijk voor het analyseren van uw gegevens om de juiste beleidsregels voor gegevensgebruik op uw gegevens te identificeren, te labelen en toe te passen, inclusief gegevensvelden die als proxy kunnen dienen voor gevoelige of beveiligde gegevenstypen en die van modellering moeten worden uitgesloten.

## Volgende stappen

Nadat u deze handleiding hebt gelezen, hebt u geleerd hoe u look-alike inzichten kunt bekijken en soorten publiek kunt maken die op deze inzichten zijn gebaseerd. Lees voor meer informatie over het publiek in de gebruikersinterface van Adobe Experience Platform de [Handleiding voor segmentatieservice](./overview.md).
