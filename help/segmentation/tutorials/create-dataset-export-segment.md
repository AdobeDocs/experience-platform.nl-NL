---
solution: Experience Platform
title: Creeer een Dataset voor het Uitvoeren van een Publiek
type: Tutorial
description: Leer hoe te om een dataset tot stand te brengen die voor het uitvoeren van een publiek kan worden gebruikt gebruikend het Experience Platform UI.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# Een gegevensset maken voor het exporteren van een publiek

Met [!DNL Adobe Experience Platform] kunt u klantprofielen segmenteren naar soorten publiek op basis van specifieke kenmerken. Zodra een segmentdefinitie wordt gecreeerd, kunt u het resulterende publiek naar een dataset uitvoeren waar het kan worden betreden en op gehandeld. Opdat de uitvoer succesvol is, moet de dataset behoorlijk worden gevormd.

Deze zelfstudie doorloopt de stappen die nodig zijn om een dataset te maken die kan worden gebruikt om een publiek te exporteren met de [!DNL Experience Platform] UI.

Dit leerprogramma is direct verwant met de stappen die in het leerprogramma op [&#x200B; worden geschetst die en tot segmenteringsresultaten toegang hebben &#x200B;](./evaluate-a-segment.md) evalueren. De evaluatiezelfstudie voor segmentdefinitie biedt stappen voor het maken van een gegevensset met de API [!DNL Catalog Service] , terwijl in deze zelfstudie stappen worden beschreven voor het maken van een gegevensset met de gebruikersinterface van [!DNL Experience Platform] .

## Aan de slag

Als u een publiek wilt exporteren, moet de dataset zijn gebaseerd op de [!DNL XDM Individual Profile Union Schema] . Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van alle schema&#39;s samenvoegt die de zelfde klasse delen. Voor meer informatie over verenigingsschema&#39;s, verwijs naar de gids op [&#x200B; de grondbeginselen van schemacompositie &#x200B;](../../xdm/schema/composition.md#union).

Als u verenigingsschema&#39;s wilt weergeven in de gebruikersinterface, selecteert u **[!UICONTROL Profiles]** in de linkernavigatie en selecteert u vervolgens **[!UICONTROL Union Schema]** zoals hieronder wordt weergegeven.

![&#x200B; het lusje van het unieschema wordt benadrukt.](../images/tutorials/segment-export-dataset/union.png)

## Werkruimte Gegevensbestanden

In de werkruimte van [!UICONTROL Datasets] kunt u alle gegevenssets voor uw organisatie weergeven en beheren.

Selecteer **[!UICONTROL Datasets]** in de linkernavigatie om tot de werkruimte toegang te hebben, dan uitgezochte **[!UICONTROL Browse]**. Dit lusje toont een lijst van datasets en hun details. Afhankelijk van de breedte van elke kolom moet u mogelijk naar links of rechts schuiven om alle kolommen weer te geven.

>[!NOTE]
>
>Selecteer het filterpictogram naast de zoekbalk om filtermogelijkheden te gebruiken om alleen die datasets weer te geven die zijn ingeschakeld voor [!DNL Real-Time Customer Profile] .

![&#x200B; De datasetwerkruimte wordt getoond.](../images/tutorials/segment-export-dataset/browse.png)

## Een gegevensset maken

Selecteer **[!UICONTROL Create Dataset]** om een gegevensset te maken.

![&#x200B; de Create datasetknoop wordt benadrukt.](../images/tutorials/segment-export-dataset/create-dataset.png)

Selecteer **[!UICONTROL Create Dataset from Schema]** in het volgende scherm.

![&#x200B; Create dataset van schemaoptie wordt benadrukt.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM Individueel profiel verenigingsschema selecteren

Zoek het schema &quot;[!UICONTROL XDM Individual Profile]&quot; op het **[!UICONTROL Select Schema]** -scherm om het schema [!DNL XDM Individual Profile Union Schema] voor gebruik in uw dataset te selecteren. Zodra u het schema selecteert, kunt u bevestigen of het het verenigingsschema onder **[!UICONTROL API Usage]** in het juiste spoor is. Als het [!UICONTROL Schema] pad eindigt met `_union` , is het een samenvoegingsschema.

>[!NOTE]
>
>Ondanks het feit dat de verenigingsschema&#39;s aan het Profiel van de Klant in real time door definitie deelnemen, zijn zij vermeld als &quot;Niet toegelaten&quot;wegens het feit dat zij niet voor Profiel op de zelfde manier zoals traditionele schema&#39;s worden toegelaten.

Selecteer het keuzerondje naast **[!UICONTROL XDM Individual Profile]** en selecteer vervolgens **[!UICONTROL Next]** .

![&#x200B; het individuele schema van het Profiel XDM wordt benadrukt.](../images/tutorials/segment-export-dataset/select-schema.png)

## Gegevensset configureren

Op het volgende scherm, moet u uw dataset een naam geven. U kunt ook een optionele beschrijving toevoegen.

**Nota&#39;s op datasetnamen:**

* De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
* Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
* U zou extra informatie over de dataset moeten verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst onderscheiden.

Als de gegevensset een naam en beschrijving heeft, selecteert u **[!UICONTROL Finish]** .

![&#x200B; de Configure datasetpagina wordt getoond. De configuratieopties worden benadrukt.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Gegevensactiviteit

Zodra de dataset wordt gecreeerd, wordt u gebracht de activiteitenpagina voor die dataset. U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

De juiste spoorlijn bevat informatie met betrekking tot uw nieuwe dataset zoals dataset ID, naam, beschrijving, schema, en meer. Noteer **[!UICONTROL Dataset ID]** omdat deze waarde vereist is om de workflow voor het exporteren van doelgroepen te voltooien.

![&#x200B; de pagina van de datasetactiviteit wordt getoond. De dataset ID wordt benadrukt, aangezien deze waarde voor toekomstige stappen moet worden genoteerd.](../images/tutorials/segment-export-dataset/activity.png)

## Volgende stappen

Nu u een dataset hebt gecreeerd die op [!DNL XDM Individual Profile Union Schema] wordt gebaseerd, kunt u dataset ID gebruiken om [&#x200B; voort te gaan evaluerend en tot de resultaten van de segmentdefinitie toegang te hebben &#x200B;](./evaluate-a-segment.md) leerprogramma.

Op dit ogenblik, gelieve terug te keren naar het evaluerende de resultaatleerprogramma van de segmentdefinitie en uit [&#x200B; op te halen die profielen voor publieksleden &#x200B;](./evaluate-a-segment.md#generate-profiles) stap van het uitvoeren van een publiekswerkschema produceren.
