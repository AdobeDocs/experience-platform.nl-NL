---
keywords: Experience Platform;huis;populaire onderwerpen;de Dienst van de segmentatie;segmentatie;creeer een dataset;het segment van het uitvoerpubliek;het uitvoersegment;
solution: Experience Platform
title: Creeer een Dataset voor het Uitvoeren van een Segment van de Publiek
topic-legacy: tutorial
type: Tutorial
description: Deze zelfstudie doorloopt de stappen die worden vereist om een dataset tot stand te brengen die voor het uitvoeren van een publiekssegment kan worden gebruikt gebruikend het Experience Platform UI.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 44d7e11e79ed0e6041ff2e4438ddb7141ae3532d
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%

---

# Een dataset maken voor het exporteren van een publiekssegment

[!DNL Adobe Experience Platform] staat u toe om klantenprofielen in publiek te segmenteren dat op specifieke attributen wordt gebaseerd. Zodra een segment wordt gecreeerd, kunt u dat publiek naar een dataset uitvoeren waar het kan worden betreden en worden gehandeld. Opdat de uitvoer succesvol is, moet de dataset behoorlijk worden gevormd.

Deze zelfstudie doorloopt de stappen die worden vereist om een dataset tot stand te brengen die kan worden gebruikt om een publiekssegment uit te voeren gebruikend [!DNL Experience Platform] UI.

Deze zelfstudie houdt rechtstreeks verband met de stappen die worden beschreven in de zelfstudie over [het evalueren en benaderen van segmentresultaten](./evaluate-a-segment.md). De zelfstudie van de segmentevaluatie biedt stappen voor het maken van een dataset met de [!DNL Catalog Service] API, terwijl deze zelfstudie stappen beschrijft om een dataset te maken met de [!DNL Experience Platform] UI.

## Aan de slag

Als u een segment wilt exporteren, moet de gegevensset zijn gebaseerd op [!DNL XDM Individual Profile Union Schema]. Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van alle schema&#39;s samenvoegt die de zelfde klasse delen. Voor meer informatie over verenigingsschema&#39;s, verwijs naar de gids op [de grondbeginselen van schemacompositie](../../xdm/schema/composition.md#union).

Om verenigingsschema&#39;s in UI te bekijken, selecteer **[!UICONTROL Profiles]** in de linkernavigatie, dan uitgezocht **[!UICONTROL Union Schema]** zoals hieronder getoond.

![Verenigingsschema-tabblad in gebruikersinterface van Experience Platform](../images/tutorials/segment-export-dataset/union.png)


## Werkruimte Gegevensbestanden

Met de werkruimte [!UICONTROL Datasets] kunt u alle gegevenssets voor uw organisatie weergeven en beheren.

Selecteer **[!UICONTROL Datasets]** in de linkernavigatie om tot de werkruimte toegang te hebben, dan uitgezocht **[!UICONTROL Browse]**. Dit lusje toont een lijst van datasets en hun details. Afhankelijk van de breedte van elke kolom moet u mogelijk naar links of rechts schuiven om alle kolommen weer te geven.

>[!NOTE]
>
>Selecteer het filterpictogram naast de onderzoeksbar om het filtreren mogelijkheden te gebruiken om slechts die datasets te bekijken die voor [!DNL Real-time Customer Profile] worden toegelaten.

![Gegevensbestanden weergeven](../images/tutorials/segment-export-dataset/browse.png)

## Een gegevensset maken

Selecteer **[!UICONTROL Create Dataset]** om een gegevensset te maken.

![Gegevensset maken selecteren](../images/tutorials/segment-export-dataset/create-dataset.png)

Selecteer **[!UICONTROL Create Dataset from Schema]** in het volgende scherm.

![Gegevensbron selecteren](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM Individueel profiel verenigingsschema selecteren

Om [!DNL XDM Individual Profile Union Schema] voor gebruik in uw dataset te selecteren, vind &quot;[!UICONTROL XDM Individual Profile]&quot;schema op **[!UICONTROL Select Schema]** scherm. Zodra u het schema selecteert, kunt u bevestigen of het het verenigingsschema onder **[!UICONTROL API Usage]** in het juiste spoor is. Als de weg [!UICONTROL Schema] met `_union` beëindigt, is het een verenigingsschema.

>[!NOTE]
>
>Ondanks het feit dat de unieschema&#39;s aan het Profiel van de Klant in real time door definitie deelnemen, zijn zij vermeld als &quot;Niet toegelaten&quot;wegens het feit dat zij niet voor Profiel op de zelfde manier zoals traditionele schema&#39;s worden toegelaten.

Selecteer het keuzerondje naast **[!UICONTROL XDM Individual Profile]** en selecteer **[!UICONTROL Next]**.

![Schema selecteren](../images/tutorials/segment-export-dataset/select-schema.png)

## Gegevensset configureren

Op het volgende scherm, moet u uw dataset een naam geven. U kunt ook een optionele beschrijving toevoegen.

**Opmerkingen over namen van gegevenssets:**
* De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
* Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
* Het is beste praktijken om extra informatie over de dataset te verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst differentiëren.

Als de gegevensset een naam en een beschrijving heeft, selecteert u **[!UICONTROL Finish]**.

![Gegevensset configureren](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Gegevensactiviteit

Zodra de dataset wordt gecreeerd, wordt u gebracht de activiteitenpagina voor die dataset. U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

De juiste spoorlijn bevat informatie met betrekking tot uw nieuwe dataset zoals dataset ID, naam, beschrijving, schema, en meer. Noteer **[!UICONTROL Dataset ID]**, omdat deze waarde is vereist om de workflow voor het exporteren van het publiekssegment te voltooien.

![Gegevensactiviteit](../images/tutorials/segment-export-dataset/activity.png)

## Volgende stappen

Nu u een dataset hebt gecreeerd die op [!DNL XDM Individual Profile Union Schema] wordt gebaseerd, kunt u datasetidentiteitskaart gebruiken om [het evalueren en tot segmentresultaten](./evaluate-a-segment.md) leerprogramma voort te zetten.

Op dit ogenblik, gelieve terug te keren naar de evaluerende zelfstudie van segmentresultaten en van [het produceren van profielen voor publieksleden ](./evaluate-a-segment.md#generate-profiles) stap van het uitvoeren van een segmentwerkschema op te halen.
