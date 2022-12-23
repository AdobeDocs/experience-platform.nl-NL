---
keywords: Experience Platform;profiel;realtime klantprofiel;verenigd profiel;verenigd profiel;verenigd;Profiel;rtcp;inschakelen profiel;Profiel inschakelen;Unieschema;UNION-PROFIEL;verenigingsprofiel
title: UI-gids Unieschema
topic-legacy: guide
type: Documentation
description: In de gebruikersinterface van Adobe Experience Platform (UI) kunt u gemakkelijk om het even welk samenvoegingsschema binnen uw organisatie bekijken en voorproef de gebieden, de identiteiten, de verhoudingen, en bijdragende schema's voor een specifieke klasse. Deze gids verstrekt gedetailleerde informatie over hoe te om verenigingsschema's te bekijken en te onderzoeken gebruikend het Platform UI.
exl-id: 52af0d77-e37d-4ed8-9dee-71a50b337b4e
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 0%

---

# [!UICONTROL Union schema] UI-hulplijn

In de gebruikersinterface van Adobe Experience Platform (UI) kunt u gemakkelijk om het even welk samenvoegingsschema binnen uw organisatie bekijken en voorproef de gebieden, de identiteiten, de verhoudingen, en bijdragende schema&#39;s voor een specifieke klasse. Deze gids verstrekt gedetailleerde informatie over hoe te om verenigingsschema&#39;s te bekijken en te onderzoeken gebruikend het Platform UI.

## Aan de slag

Deze UI-gids vereist inzicht in de verschillende [!DNL Experience Platform] services die betrokken zijn bij het beheren van gegevens in realtime-klantprofiel. Voordat u deze handleiding leest of in de gebruikersinterface werkt, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-time Customer Profile]](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Identity Service]](../../identity-service/home.md): Inschakelen [!DNL Real-time Customer Profile] door identiteiten van verschillende gegevensbronnen te overbruggen aangezien zij worden opgenomen in [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring.

## Verenigingsschema&#39;s begrijpen

Met het realtime klantprofiel kunt u robuuste, gecentraliseerde profielen maken met klantkenmerken en gebeurtenissen met een tijdstempel die door elke klant worden gebruikt voor systemen die met Adobe Experience Platform zijn geïntegreerd. Het formaat en de structuur van deze gegevens worden verstrekt door schema&#39;s van het Gegevensmodel van de Ervaring (XDM), met elk schema dat op een klasse XDM wordt gebaseerd en die gebieden bevatten die met die klasse compatibel zijn.

Schema&#39;s kunnen worden gemaakt voor meerdere gebruiksgevallen, waarbij wordt verwezen naar dezelfde klasse maar die velden bevatten die specifiek zijn voor het gebruik ervan. Wanneer een schema voor Profiel wordt toegelaten, wordt het deel van een verenigingsschema. Met andere woorden, verenigingsschema&#39;s zijn samengesteld uit veelvoudige schema&#39;s die de zelfde klasse delen en voor Profiel toegelaten. Met het samenvoegingsschema kunt u een samenvoeging zien van alle velden in schema&#39;s die dezelfde klasse delen. Het Profiel van de Klant in real time gebruikt het verenigingsschema om een holistische mening van elke individuele klant tot stand te brengen.

Het werken met unieschema&#39;s vereist een diep inzicht in schema&#39;s XDM. Voor meer informatie, gelieve te beginnen door te lezen [grondbeginselen van de schemacompositie](../../xdm/schema/composition.md).

## Verenigingsschema&#39;s weergeven

Om aan verenigingsschema&#39;s binnen het Platform UI te navigeren, selecteer **[!UICONTROL Profiles]** in de linkernavigatie selecteert u vervolgens de **[!UICONTROL Union Schema]** tab. De [!UICONTROL Union Schema] wordt geopend om het samenvoegingsschema voor de geselecteerde klasse weer te geven.

![De pagina Unieschema wordt weergegeven, met het tabblad Profiel en Unieschema gemarkeerd.](../images/union-schema/landing.png)

## Een klasse selecteren

Als u het samenvoegingsschema voor een specifieke XDM-klasse wilt weergeven, selecteert u de klasse in het dialoogvenster **[!UICONTROL Class]** vervolgkeuzelijst. Vanwege het feit dat niet alle klassen vakbondsschema&#39;s hebben, zijn alleen klassen met vakbondsschema&#39;s (dat wil zeggen klassen met schema&#39;s die zijn ingeschakeld voor Profiel) beschikbaar in de vervolgkeuzelijst.

Nadat een klasse is geselecteerd, het schema dat wordt getoond werkt bij om op het verenigingsschema voor de geselecteerde klasse te wijzen. U kunt bijvoorbeeld **[!UICONTROL XDM Individual Profile]** om het verenigingsschema voor die klasse te bekijken.

![Een vervolgkeuzelijst met de klassen van het vakbondsschema wordt gemarkeerd.](../images/union-schema/class.png)

## Samenvoegingsschema&#39;s verkennen

U kunt het samenvoegingsschema verkennen door omhoog en omlaag te schuiven om de volledige schemastructuur weer te geven en door een rechterpunthaakje te selecteren (`>`) om geneste velden uit te vouwen.

![Een set geneste velden in het samenvoegingsschema wordt uitgebreid.](../images/union-schema/explore.png)

Selecteer een veld om de details weer te geven, zoals de weergavenaam, het gegevenstype, de beschrijving, het pad, de gemaakte datum en de datum die als laatste is gewijzigd. U kunt ook een lijst met bijdragende schema&#39;s bekijken die het gebied bevatten u selecteerde.

![Een veld voor een samenvoegingsschema wordt gemarkeerd. De details over het benadrukte gebied worden getoond op rechterzijbalk.](../images/union-schema/explore-field.png)

Wanneer u de naam van een bijdragend schema selecteert, worden de namen van gegevenssets met betrekking tot dat schema weergegeven die gegevens in het geselecteerde veld invoeren. Elke naam van een gegevensset wordt als een koppeling weergegeven. Het selecteren van een datasetnaam opent het activiteitenlusje voor die dataset in een nieuw venster.

Voor meer informatie over datasets, met inbegrip van het bekijken van de activiteit van de dataset en het voorvertonen van datasetgegevens in UI, gelieve te bezoeken [UI-gids voor gegevenssets](../../catalog/datasets/user-guide.md).

![De lijst van datasets met betrekking tot het schema wordt benadrukt.](../images/union-schema/datasets.png)

## Contribute-schema&#39;s weergeven

U kunt ook bekijken welke specifieke schema&#39;s tot het unieschema bijdragen door te selecteren **[!UICONTROL All contributing schemas]** om de lijst met schema&#39;s uit te vouwen. Afhankelijk van de klasse u hebt geselecteerd en het aantal schema&#39;s die uw organisatie binnen Platform heeft gecreeerd, zou dit een korte lijst kunnen zijn die één enkel schema of een lange lijst bevat die vele schema&#39;s bevat.

![De lijst van schema&#39;s die tot het unieschema bijdragen wordt benadrukt.](../images/union-schema/contributing-schemas.png)

Als u de naam van een specifiek schema selecteert, worden de velden binnen het samenvoegingsschema gemarkeerd die deel uitmaken van het schema dat u hebt geselecteerd. Nadat u een schema hebt geselecteerd, wordt het samenvoegingsschema grijs weergegeven met zwarte balken die de velden aangeven die deel uitmaken van het bijdragende schema.

![Het geselecteerde bijdragende schema wordt benadrukt. De velden die deel uitmaken van het bijdragende schema blijven zwart, terwijl de velden die geen deel uitmaken van het bijdragende schema, grijs worden weergegeven.](../images/union-schema/select-schema.png)

## Identiteiten weergeven

Via de interface kunt u een lijst weergeven met identiteiten die zijn opgenomen in het vakschema door **[!UICONTROL Identities]** om de lijst uit te vouwen.

![De identiteiten die tot het unieschema behoren worden benadrukt.](../images/union-schema/identities.png)

Als u een individuele identiteit in de lijst selecteert, wordt het weergegeven schema automatisch bijgewerkt wanneer dat nodig is om het identiteitsveld weer te geven. Dit kan het uitbreiden van meerdere velden omvatten als het identiteitsveld is genest.

Het identiteitsveld wordt gemarkeerd in het samenvoegingsschema en de details van de identiteit worden rechts in het scherm weergegeven. De details omvatten een lijst van bijdragende schema&#39;s die het identiteitsgebied bevatten en u kunt neer boren om verbindingen aan de datasets met betrekking tot dat schema te vinden die gegevens in het geselecteerde identiteitsgebied opnemen.

![De geselecteerde identiteit wordt gemarkeerd. Details over de geselecteerde identiteit worden weergegeven op de rechterzijbalk.](../images/union-schema/select-identity.png)

## Relaties weergeven

Het unieschema UI laat u ook toe om verhoudingen te zien die voor schema&#39;s zijn bepaald die op de geselecteerde schemaklasse worden gebaseerd. Het bepalen van een verhouding is een manier om twee regelingen te verbinden die tot verschillende klassen behoren om complexere inzichten in klantengegevens te bereiken.

Als er relaties zijn ingesteld voor de geselecteerde klasse, selecteert u **[!UICONTROL Relationships]** geeft een lijst weer met velden die worden gebruikt om relaties te maken. Niet alle schema&#39;s gebruiken of vereisen vastgestelde verhoudingen, zodat is het gemeenschappelijk voor de relatiesectie om geen gebieden te bevatten.

Ga voor meer informatie over schema-relaties, waaronder hoe u deze kunt definiëren met de interface [dit document over schema-relaties](../../xdm/tutorials/relationship-ui.md).

![De verhoudingen die tot het unieschema behoren worden benadrukt.](../images/union-schema/relationships.png)

Als u een relatieveld in de lijst selecteert, wordt het weergegeven schema zo nodig bijgewerkt om het gemarkeerde relatieveld weer te geven. Dit kan het uitbreiden van meerdere velden omvatten als het relatieveld is genest.

![De geselecteerde relatie wordt gemarkeerd. Het corresponderende veld voor de relatie wordt ook gemarkeerd.](../images/union-schema/select-relationship.png)

## Volgende stappen

Door deze gids te lezen, weet u nu hoe te om verenigingsschema&#39;s te bekijken en te navigeren gebruikend [!DNL Experience Platform] UI. Voor meer informatie over schema&#39;s, zoals hoe zij door Platform worden gebruikt, gelieve te beginnen door te lezen [XDM System, overzicht](../../xdm/home.md).
