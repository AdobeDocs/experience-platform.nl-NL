---
keywords: Experience Platform;profile;real-time customer profile;;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile;Union schema;UNION PROFILE;union profile
title: Gebruikershandleiding voor gebruikersprofiel voor realtime klanten
topic: guide
description: In de gebruikersinterface van Adobe Experience Platform (UI) kunt u gemakkelijk om het even welk samenvoegingsschema binnen uw organisatie bekijken en voorproef de gebieden, de identiteiten, de verhoudingen, en bijdragende schema's voor een specifieke klasse. Deze gids verstrekt gedetailleerde informatie over hoe te om verenigingsschema's te bekijken en te onderzoeken gebruikend het Platform UI.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 0%

---


# [!UICONTROL UI-hulplijn Unieschema]

In de gebruikersinterface van Adobe Experience Platform (UI) kunt u gemakkelijk om het even welk samenvoegingsschema binnen uw organisatie bekijken en voorproef de gebieden, de identiteiten, de verhoudingen, en bijdragende schema&#39;s voor een specifieke klasse. Deze gids verstrekt gedetailleerde informatie over hoe te om verenigingsschema&#39;s te bekijken en te onderzoeken gebruikend het Platform UI.

## Aan de slag

Deze gids UI vereist een inzicht in de diverse [!DNL Experience Platform] diensten betrokken bij het beheren van gegevens van het Profiel van de Klant in real time. Voordat u deze handleiding leest of in de gebruikersinterface werkt, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): Schakelt [!DNL Real-time Customer Profile] het overbruggen van identiteiten uit verschillende gegevensbronnen in wanneer deze worden ingepakt [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

## Verenigingsschema&#39;s begrijpen

Met het realtime klantprofiel kunt u robuuste, gecentraliseerde profielen maken met klantkenmerken en gebeurtenissen met een tijdstempel die door elke klant worden gebruikt voor systemen die met Adobe Experience Platform zijn geïntegreerd. Het formaat en de structuur van deze gegevens worden verstrekt door schema&#39;s van het Gegevensmodel van de Ervaring (XDM), met elk schema dat op een klasse XDM wordt gebaseerd en die gebieden bevatten die met die klasse compatibel zijn.

Schema&#39;s kunnen worden gemaakt voor meerdere gebruiksgevallen, waarbij wordt verwezen naar dezelfde klasse maar die velden bevatten die specifiek zijn voor het gebruik ervan. Wanneer een schema voor Profiel wordt toegelaten, wordt het deel van een verenigingsschema. Met andere woorden, verenigingsschema&#39;s zijn samengesteld uit veelvoudige schema&#39;s die de zelfde klasse delen en voor Profiel toegelaten. Met het samenvoegingsschema kunt u een samenvoeging zien van alle velden in schema&#39;s die dezelfde klasse delen. Het Profiel van de Klant in real time gebruikt het verenigingsschema om een holistische mening van elke individuele klant tot stand te brengen.

Het werken met unieschema&#39;s vereist een diep inzicht in schema&#39;s XDM. Voor meer informatie, gelieve te beginnen door de [grondbeginselen van schemacompositie](../../xdm/schema/composition.md)te lezen.

## Verenigingsschema&#39;s weergeven

Als u naar samenvoegingsschema&#39;s in de gebruikersinterface van het Platform wilt navigeren, selecteert u **[!UICONTROL Profielen]** in de linkernavigatie en selecteert u vervolgens het tabblad **[!UICONTROL Unieschema]** . Het tabblad [!UICONTROL Unieschema] wordt geopend en geeft het samenvoegingsschema weer voor de geselecteerde klasse.

![](../images/union-schema/union-schema-landing.png)

## Een klasse selecteren

Als u het samenvoegingsschema voor een specifieke XDM-klasse wilt weergeven, selecteert u de klasse in het vervolgkeuzemenu **[!UICONTROL Klasse]** . Vanwege het feit dat niet alle klassen vakbondsschema&#39;s hebben, zijn alleen klassen met vakbondsschema&#39;s (dat wil zeggen klassen met schema&#39;s die zijn ingeschakeld voor Profiel) beschikbaar in de vervolgkeuzelijst.

Nadat een klasse is geselecteerd, het schema dat wordt getoond werkt bij om op het verenigingsschema voor de geselecteerde klasse te wijzen. U kunt bijvoorbeeld **[!UICONTROL XDM Individueel profiel]** selecteren om het samenvoegingsschema voor die klasse weer te geven.

![](../images/union-schema/union-schema-class.png)

## Samenvoegingsschema&#39;s verkennen

U kunt het samenvoegingsschema verkennen door omhoog en omlaag te schuiven om de volledige schemastructuur weer te geven en door een rechte punthaakje (`>`) te selecteren om geneste velden uit te vouwen.

![](../images/union-schema/union-schema-explore.png)

Selecteer een veld om de details weer te geven, zoals de weergavenaam, het gegevenstype, de beschrijving, het pad, de gemaakte datum en de datum die als laatste is gewijzigd. U kunt ook een lijst met bijdragende schema&#39;s bekijken die het gebied bevatten u selecteerde.

![](../images/union-schema/union-schema-explore-field.png)

Wanneer u de naam van een bijdragend schema selecteert, worden de namen van gegevenssets met betrekking tot dat schema weergegeven die gegevens in het geselecteerde veld invoeren. Elke naam van een gegevensset wordt als een koppeling weergegeven. Het selecteren van een datasetnaam opent het activiteitenlusje voor die dataset in een nieuw venster.

Voor meer informatie over datasets, met inbegrip van het bekijken van datasetactiviteit en het voorvertonen van datasetgegevens in UI, gelieve de gids [van](../../catalog/datasets/user-guide.md)datasets UI te bezoeken.

![](../images/union-schema/union-schema-field-datasets.png)

## Contribute-schema&#39;s weergeven

U kunt ook bekijken welke specifieke schema&#39;s tot het unieschema bijdragen door **[!UICONTROL Alle bijdragende regelingen]** te selecteren om de lijst van schema&#39;s uit te breiden. Afhankelijk van de klasse u hebt geselecteerd en het aantal schema&#39;s die uw organisatie binnen Platform heeft gecreeerd, zou dit een korte lijst kunnen zijn die één enkel schema of een lange lijst bevat die vele schema&#39;s bevat.

![](../images/union-schema/union-schema-contributing-schemas.png)

Als u de naam van een specifiek schema selecteert, worden de velden binnen het samenvoegingsschema gemarkeerd die deel uitmaken van het schema dat u hebt geselecteerd. Nadat u een schema hebt geselecteerd, wordt het samenvoegingsschema grijs weergegeven met zwarte balken die de velden aangeven die deel uitmaken van het bijdragende schema.

![](../images/union-schema/union-schema-select-schema.png)

## Identiteiten weergeven

Via UI kunt u een lijst van identiteiten bekijken die in het unieschema inbegrepen zijn door **[!UICONTROL Identiteiten]** te selecteren om de lijst uit te breiden.

![](../images/union-schema/union-schema-identities.png)

Als u een individuele identiteit in de lijst selecteert, wordt het weergegeven schema automatisch bijgewerkt wanneer dat nodig is om het identiteitsveld weer te geven. Dit kan het uitbreiden van meerdere velden omvatten als het identiteitsveld is genest.

Het identiteitsveld wordt gemarkeerd in het samenvoegingsschema en de details van de identiteit worden rechts in het scherm weergegeven. De details omvatten een lijst van bijdragende schema&#39;s die het identiteitsgebied bevatten en u kunt neer boren om verbindingen aan de datasets met betrekking tot dat schema te vinden die gegevens in het geselecteerde identiteitsgebied opnemen.

![](../images/union-schema/union-schema-select-identity.png)

## Relaties weergeven

Het unieschema UI laat u ook toe om verhoudingen te zien die voor schema&#39;s zijn bepaald die op de geselecteerde schemaklasse worden gebaseerd. Het bepalen van een verhouding is een manier om twee regelingen te verbinden die tot verschillende klassen behoren om complexere inzichten in klantengegevens te bereiken.

Als er relaties zijn ingesteld voor de geselecteerde klasse, wordt met **[!UICONTROL Relaties]** een lijst weergegeven met velden die worden gebruikt om relaties te maken. Niet alle schema&#39;s gebruiken of vereisen vastgestelde verhoudingen, zodat is het gemeenschappelijk voor de relatiesectie om geen gebieden te bevatten.

Voor meer informatie over schemaverhoudingen, met inbegrip van hoe te om hen te bepalen gebruikend UI, bezoek [dit document op schemaverhoudingen](../../xdm/tutorials/relationship-ui.md).

![](../images/union-schema/union-schema-relationships.png)

Als u een relatieveld in de lijst selecteert, wordt het weergegeven schema zo nodig bijgewerkt om het gemarkeerde relatieveld weer te geven. Dit kan het uitbreiden van meerdere velden omvatten als het relatieveld is genest.

![](../images/union-schema/union-schema-select-relationship.png)

## Volgende stappen

Door deze gids te lezen, weet u nu hoe te om verenigingsschema&#39;s te bekijken en te navigeren gebruikend [!DNL Experience Platform] UI. Voor meer informatie over schema&#39;s, met inbegrip van hoe zij door Platform worden gebruikt, gelieve te beginnen door het [XDM systeemoverzicht](../../xdm/home.md)te lezen.
