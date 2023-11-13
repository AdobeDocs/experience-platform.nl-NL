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

[!DNL Adobe Experience Platform] staat u toe om klantenprofielen in publiek te segmenteren dat op specifieke attributen wordt gebaseerd. Zodra een segmentdefinitie wordt gecreeerd, kunt u het resulterende publiek naar een dataset uitvoeren waar het kan worden betreden en op gehandeld. Opdat de uitvoer succesvol is, moet de dataset behoorlijk worden gevormd.

Dit leerprogramma loopt door de stappen worden vereist om een dataset tot stand te brengen die kan worden gebruikt om een publiek uit te voeren gebruikend [!DNL Experience Platform] UI.

Deze zelfstudie houdt rechtstreeks verband met de stappen die worden beschreven in de zelfstudie over [segmentatieresultaten evalueren en openen](./evaluate-a-segment.md). De de evaluatiedeszelfstudie van de segmentdefinitie verstrekt stappen voor het creëren van een dataset gebruikend [!DNL Catalog Service] API, terwijl deze zelfstudie stappen beschrijft om een dataset tot stand te brengen gebruikend [!DNL Experience Platform] UI.

## Aan de slag

Om een publiek uit te voeren, moet de dataset op [!DNL XDM Individual Profile Union Schema]. Een verenigingsschema is een systeem-geproduceerd, read-only schema dat de gebieden van alle schema&#39;s samenvoegt die de zelfde klasse delen. Raadpleeg de handleiding voor meer informatie over samenvoegingsschema&#39;s [de grondbeginselen van de schemacompositie](../../xdm/schema/composition.md#union).

Om verenigingsschema&#39;s in UI te bekijken, selecteer **[!UICONTROL Profiles]** in de linkernavigatie, dan selecteren **[!UICONTROL Union Schema]** zoals hieronder weergegeven.

![Het tabblad Verenigingsschema wordt gemarkeerd.](../images/tutorials/segment-export-dataset/union.png)

## Werkruimte Gegevensbestanden

De [!UICONTROL Datasets] De werkruimte staat u toe om alle datasets voor uw organisatie te bekijken en te beheren.

Selecteren **[!UICONTROL Datasets]** in de linkernavigatie om tot de werkruimte toegang te hebben, dan selecteren **[!UICONTROL Browse]**. Dit lusje toont een lijst van datasets en hun details. Afhankelijk van de breedte van elke kolom moet u mogelijk naar links of rechts schuiven om alle kolommen weer te geven.

>[!NOTE]
>
>Selecteer het filterpictogram naast de zoekbalk om filtermogelijkheden te gebruiken om alleen die datasets weer te geven die zijn ingeschakeld voor [!DNL Real-Time Customer Profile].

![De werkruimte van datasets wordt getoond.](../images/tutorials/segment-export-dataset/browse.png)

## Een gegevensset maken

Als u een gegevensset wilt maken, selecteert u **[!UICONTROL Create Dataset]**.

![De knop Gegevensset maken is gemarkeerd.](../images/tutorials/segment-export-dataset/create-dataset.png)

Selecteer in het volgende scherm de optie **[!UICONTROL Create Dataset from Schema]**.

![De optie Gegevensset maken van schema is gemarkeerd.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## XDM Individueel profiel verenigingsschema selecteren

Als u de optie [!DNL XDM Individual Profile Union Schema] voor gebruik in uw dataset, vind &quot;[!UICONTROL XDM Individual Profile]&quot; schema op de **[!UICONTROL Select Schema]** scherm. Zodra u het schema selecteert, kunt u bevestigen of het het verenigingsschema onder is **[!UICONTROL API Usage]** in het rechterspoor. Als de [!UICONTROL Schema] paden eindigen met `_union`, het is een samenvoegingsschema.

>[!NOTE]
>
>Ondanks het feit dat de verenigingsschema&#39;s aan het Profiel van de Klant in real time door definitie deelnemen, zijn zij vermeld als &quot;Niet toegelaten&quot;wegens het feit dat zij niet voor Profiel op de zelfde manier zoals traditionele schema&#39;s worden toegelaten.

Selecteer het keuzerondje naast **[!UICONTROL XDM Individual Profile]** selecteert u vervolgens **[!UICONTROL Next]**.

![Het schema van het Individuele Profiel XDM wordt benadrukt.](../images/tutorials/segment-export-dataset/select-schema.png)

## Gegevensset configureren

Op het volgende scherm, moet u uw dataset een naam geven. U kunt ook een optionele beschrijving toevoegen.

**Opmerkingen over namen van gegevenssets:**

* De namen van gegevenssets moeten kort en beschrijvend zijn, zodat de gegevensset later gemakkelijk in de bibliotheek kan worden gevonden.
* Dataset-namen moeten uniek zijn, wat betekent dat ze ook specifiek genoeg moeten zijn om in de toekomst niet opnieuw te worden gebruikt.
* U zou extra informatie over de dataset moeten verstrekken gebruikend het beschrijvingsgebied, aangezien het andere gebruikers kan helpen tussen datasets in de toekomst onderscheiden.

Als de gegevensset een naam en beschrijving heeft, selecteert u **[!UICONTROL Finish]**.

![De Configure datasetpagina wordt getoond. De configuratieopties worden gemarkeerd.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Gegevensactiviteit

Zodra de dataset wordt gecreeerd, wordt u gebracht de activiteitenpagina voor die dataset. U zou de naam van de dataset in de upper-left hoek van de werkruimte, samen met een bericht moeten zien dat &quot;Geen partijen zijn toegevoegd.&quot; Dit moet worden verwacht aangezien u nog geen partijen aan deze dataset hebt toegevoegd.

De juiste spoorlijn bevat informatie met betrekking tot uw nieuwe dataset zoals dataset ID, naam, beschrijving, schema, en meer. Noteer de **[!UICONTROL Dataset ID]**, omdat deze waarde vereist is om de workflow voor het exporteren van doelgroepen te voltooien.

![De pagina van de datasetactiviteit wordt getoond. De dataset-id wordt gemarkeerd, aangezien deze waarde moet worden genoteerd voor toekomstige stappen.](../images/tutorials/segment-export-dataset/activity.png)

## Volgende stappen

Nu u een dataset hebt gecreeerd die op [!DNL XDM Individual Profile Union Schema]kunt u de gegevensset-id gebruiken om door te gaan met de [evalueren van en tot de resultaten van de segmentdefinitie toegang hebben](./evaluate-a-segment.md) zelfstudie.

Ga op dit moment terug naar de zelfstudie over de evaluatieresultaten voor segmentdefinitie en vul de resultaten in van de [profielen genereren voor gehoorleden](./evaluate-a-segment.md#generate-profiles) stap van het exporteren van een publieksworkflow.
