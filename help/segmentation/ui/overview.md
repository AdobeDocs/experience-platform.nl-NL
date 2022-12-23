---
keywords: Experience Platform;huis;populaire onderwerpen;de Dienst van de segmentatie;segmentatie;de segmenteringsdienst;gebruikersgids;ui gids;segmentation ui gids;segmentbouwer;Segmentbouwer;gerealiseerd;bestaand;het weggaan;
solution: Experience Platform
title: UI-gids voor segmentatieservice
topic-legacy: ui guide
description: Adobe Experience Platform Segmentation Service biedt een gebruikersinterface voor het maken en beheren van segmentdefinities.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '2566'
ht-degree: 0%

---

# Handleiding voor segmentatieservice

[!DNL Adobe Experience Platform Segmentation Service] biedt een gebruikersinterface voor het maken en beheren van segmentdefinities.

## Aan de slag

Het werken met segmentdefinities vereist een begrip van de diverse [!DNL Experience Platform] diensten in verband met segmentatie. Lees de documentatie voor de volgende services voordat u deze gebruikershandleiding leest:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] staat u toe om gegevens te verdelen die in worden opgeslagen [!DNL Experience Platform] dat betrekking heeft op individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) in kleinere groepen.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Laat de verwezenlijking van klantenprofielen toe door identiteiten van verschillende gegevensbronnen te overbruggen die in worden opgenomen [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Platform] organiseert de gegevens van de klantenervaring. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../../xdm/schema/best-practices.md).

Het is ook belangrijk om twee belangrijke termen te kennen die in dit document worden gebruikt en het verschil tussen hen te begrijpen:
- **Segmentdefinitie**: De regelreeks die wordt gebruikt om zeer belangrijke eigenschappen of gedrag van een doelpubliek te beschrijven.
- **Publiek**: De resulterende set profielen die voldoen aan de criteria van een segmentdefinitie. Dit kan worden gemaakt via Adobe Experience Platform (publiek dat door Platforms wordt gegenereerd) of via een externe bron (extern gegenereerd publiek).

## Overzicht

Selecteer in de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Segments]** in de linkernavigatie om de **[!UICONTROL Overview]** tabblad met het tabblad [!UICONTROL Segments] dashboard.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog niet de actieve datasets van het Profiel of gecreeerd verenigingsbeleid heeft, [!UICONTROL Segments] het dashboard is niet zichtbaar. In plaats daarvan [!UICONTROL Overview] het lusje toont verbindingen en documentatie om u te helpen met segmenten beginnen.

### [!UICONTROL Segments] dashboard {#segments-dashboard}

De **[!UICONTROL Segments]** het dashboard schetst zeer belangrijke metriek met betrekking tot de segmentgegevens van uw organisatie.

Ga voor meer informatie naar de [segmentdashboardhulplijn](../../dashboards/guides/segments.md).

![Het segmentdashboard wordt weergegeven. Er worden verschillende widgets weergegeven, zoals de omvang van het publiek, profielen op basis van identiteit, identiteitsbedekking en de trend om de omvang van het publiek te wijzigen.](../../dashboards/images/segments/dashboard-overview.png)

## Bladeren {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Churn"
>abstract="Het koord vertegenwoordigt het percentage profielen die binnen een segmentdefinitie in vergelijking met de laatste tijd veranderen de segmentbaan liep."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Evaluatiemethode"
>abstract="De methodes van de evaluatie voor segmenten omvatten partij, het stromen, en rand."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Alle segmenten aan schema toevoegen"
>abstract="Schakel deze optie in om alle batchevaluatiesegmenten op te nemen in de dagelijkse geplande update. Uitschakelen om alle segmenten uit de geplande update te verwijderen."

Selecteer **[!UICONTROL Browse]** om een lijst van alle segmentdefinities voor uw organisatie te zien.

![De segmenten bladeren het scherm wordt getoond. Een lijst van alle segmenten die tot de organisatie behoren wordt getoond.](../images/ui/overview/segment-browse-all.png)

Deze weergave bevat informatie over de segmentdefinitie, inclusief het aantal profielen, de datum waarop het segment is gemaakt en de datum waarop het laatst is gewijzigd.

U kunt extra velden aan deze weergave toevoegen door ![het pictogram van het filterkenmerk](../images/ui/overview/filter-attribute.png). Deze extra gebieden omvatten onderbreking, koor, evaluatiemethode, en baanidentiteitskaart

Als de indeling is geselecteerd, wordt in het scherm een staafgrafiek weergegeven met het percentage profielen dat tot elk van de volgende statussen behoort: [!UICONTROL Realized], [!UICONTROL Existing], en [!UICONTROL Exiting]. Daarnaast wordt de uitsplitsing in de [!UICONTROL Browse] tab is de nauwkeurigste uitsplitsing van de segmentstatus. Als dit getal afwijkt van wat staat vermeld op de knop [!UICONTROL Overview] gebruikt u de nummers op het tabblad [!UICONTROL Browse] als de juiste bron van informatie, aangezien [!UICONTROL Overview] tabnummers worden slechts eenmaal per dag bijgewerkt.

| Status | Beschrijving |
| ------ | ----------- |
| Gerealiseerd | Een nieuw profiel binnen het segment. |
| Bestaande | Een bestaand profiel dat binnen het segment is gebleven. |
| Afsluiten | Een bestaand profiel dat het segment verlaat. |

De kolom vertegenwoordigt het percentage profielen die binnen een segmentdefinitie in vergelijking met de laatste tijd veranderen de segmentbaan liep, terwijl de profieltelling het totale aantal profielen vertegenwoordigt die voor het segment kwalificeren.

De evaluatiemethode kan streaming, batch of edge zijn. Streaming segmenten worden voortdurend geëvalueerd terwijl gegevens in het systeem worden ingevoerd. De segmenten van de partij worden geëvalueerd volgens een vastgesteld programma. De segmenten van de rand worden geëvalueerd in real time, die voor de zelfde pagina en volgende het verpersoonlijkingsgebruiksgevallen van de paginagrootte toestaan.

![De segmenten binnen het segment doorbladeren pagina worden benadrukt.](../images/ui/overview/segment-browse-segments.png)

Boven aan de pagina staan opties voor het toevoegen van alle segmenten aan een schema en het maken van een nieuw segment.

Toggling **[!UICONTROL Add all segments to schedule]** zal geplande segmentatie toelaten. Meer informatie over geplande segmentatie vindt u in de [Gepland segmenteringsgedeelte van deze gebruikershandleiding](#scheduled-segmentation).

Selecteren **[!UICONTROL Create segment]** gaat u naar de Segment Builder. Voor meer informatie over het maken van segmenten leest u de sectie over [segment maken in de gebruikershandleiding](#create-segment).

![De hoogste navigatiebar op de segment doorbladert pagina wordt benadrukt. Deze bar bevat een knevel om alle segmenten aan een programma en een knoop toe te voegen om een segment tot stand te brengen.](../images/ui/overview/segment-browse-top.png)

De rechterzijbalk bevat informatie over alle segmenten binnen de organisatie, met een overzicht van het totale aantal segmenten, de laatste evaluatiedatum, de volgende evaluatiedatum en een uitsplitsing van de segmenten naar evaluatiemethode.

![De rechterzijbalk van de pagina Bladeren door segment wordt gemarkeerd. De informatie over de segmenten in de organisatie wordt getoond. Dit omvat informatie zoals het totale aantal segmenten, de laatste geëvalueerde tijd, de volgende geëvalueerde tijd, evenals een uitsplitsing van de verschillende segmenttypes.](../images/ui/overview/segment-browse-segment-info.png)

Het selecteren van de rij van de segmentdefinitie verstrekt een samenvatting van de segmentdefinitie, met inbegrip van opties om of het segment uit te geven of te schrappen, het segment aan een bestemming, het gekwalificeerde publiek voor het segment, de totale publieksgrootte, naast de naam van het segment, beschrijving, evaluatiemethode, gecreeerde datum, en laatst gewijzigde datum te activeren.

>[!NOTE]
>
> U zult **niet** kan een segment schrappen dat in een bestemmingsactivering wordt gebruikt.

![De details over het geselecteerde segment worden getoond. Dit omvat details over het aantal gekwalificeerde profielen, de procentuele uitsplitsing van gekwalificeerde profielen ten opzichte van het totaal van profielen, de laatste evaluatiedatum.](../images/ui/overview/segment-browse-details.png)

## Segmentdefinitiedetails {#segment-details}

Als u meer details wilt zien over een specifieke segmentdefinitie, selecteert u de naam van een segment in het dialoogvenster **[!UICONTROL Browse]** tab.

De pagina met segmentdetails wordt weergegeven. Bovenaan, is er een samenvatting van de segmentdefinitie, informatie over de gekwalificeerde publieksgrootte, evenals bestemmingen het segment voor wordt geactiveerd.

![De pagina met segmentdefinitiedetails wordt weergegeven. De segmentsamenvatting, het totale publiek in segment, en de geactiveerde bestemmingskaarten worden benadrukt.](../images/ui/overview/segment-details-summary.png)

### Overzicht van segment {#segment-summary}

De **[!UICONTROL Segment summary]** bevat informatie zoals de ID, naam, beschrijving en details van de kenmerken.

Bovendien, krijgt u de optie om of het segment aan een bestemming te activeren of het segment uit te geven. Selecteren **[!UICONTROL Activate to destination]** Hiermee kunt u het segment activeren naar een bestemming. Voor meer gedetailleerde informatie over het activeren van een segment naar een bestemming, gelieve te lezen [activeringsoverzicht](../../destinations/ui/activation-overview.md).

![De knop Activeren naar doel is gemarkeerd.](../images/ui/overview/segment-details-activate.png)

Selecteren **[!UICONTROL Edit segment]** brengt u naar de [!DNL Segment Builder]. Voor meer informatie over het gebruik van de [!DNL Segment Builder] werkruimte, lees de [[!DNL Segment Builder] gebruikershandleiding](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Totaal aantal deelnemers in segment

De **[!UICONTROL Total audience in segment]** wordt het totale aantal profielen weergegeven dat in aanmerking komt voor het segment.

Schattingen worden gegenereerd door gebruik te maken van een steekproefgrootte van de voorbeeldgegevens van die dag. Als uw profielarchief minder dan 1 miljoen entiteiten bevat, wordt de volledige gegevensset gebruikt. voor tussen 1 en 20 miljoen entiteiten worden 1 miljoen entiteiten gebruikt; en voor meer dan 20 miljoen entiteiten wordt 5 % van de totale entiteiten gebruikt . Meer informatie over het genereren van segmentramingen vindt u in het gedeelte [schatting van generatiesectie](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) van de zelfstudie voor het maken van segmenten.

### Geactiveerde doelen

De **[!UICONTROL Activated destinations]** toont de bestemmingen waarvoor dit segment wordt geactiveerd.

>[!NOTE]
>
> Doelen zijn een functie die beschikbaar is bij [!DNL Adobe Real-Time Customer Data Platform]en kunt u gegevens exporteren naar externe platforms. Lees voor meer informatie over bestemmingen de [Overzicht van doelen](../../destinations/home.md). Leren hoe te om een segment aan een bestemming te activeren, zie [activeringsoverzicht](../../destinations/ui/activation-overview.md).

### Profielvoorbeelden

Hieronder ziet u een voorbeeld van profielen die in aanmerking komen voor het segment, met gedetailleerde informatie zoals de [!DNL Profile] ID, voornaam, achternaam en persoonlijke e-mail.

De manier waarop gegevensbemonstering wordt geactiveerd, hangt af van de wijze van inname.

Voor batch-opname wordt de profielopslag automatisch elke 15 minuten gescand om te zien of een nieuwe batch is opgenomen sinds de laatste samplingtaak is uitgevoerd. Als dat het geval is, wordt de profielopslag gescand om te zien of is er minstens een 5% verandering in het aantal verslagen. Als aan deze voorwaarden wordt voldaan, wordt een nieuwe steekproefbaan teweeggebracht.

Voor het stromen opname, wordt de profielopslag automatisch gescand elk uur om te zien of is er minstens een 5% verandering in het aantal verslagen geweest. Als aan deze voorwaarde wordt voldaan, wordt een nieuwe steekproefbaan teweeggebracht.

De voorbeeldgrootte van de scan is afhankelijk van het totale aantal entiteiten in de profielopslag. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

Meer gedetailleerde informatie over elk [!DNL Profile] kunt u zien door de [!DNL Profile] ID. Als u meer wilt weten over de details van een profiel, leest u de [[!DNL Real-time Customer Profile] gebruikershandleiding](../../profile/ui/user-guide.md#profile-detail).

![De voorbeeldprofielen voor de segmentdefinitie worden gemarkeerd. Voorbeelden van profielgegevens zijn de profiel-id, de voornaam, de achternaam en het e-mailadres van de persoon.](../images/ui/overview/segment-details-profiles.png)

## Segment maken {#create-segment}

Selecteren **[!UICONTROL Create segment]** in de rechterbovenhoek de [!DNL Segment Builder] werkruimte, waarin u kunt beginnen met het maken van een segmentdefinitie.

![Op de doorbladerpagina van het Segment, wordt de Create segmentknoop benadrukt.](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] werkruimte

[!DNL Segment Builder] biedt een rijke werkruimte waarmee u kunt werken met [!DNL Profile] gegevenselementen. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.

Voor meer informatie over het gebruik van de [!DNL Segment Builder] werkruimte, lees de [[!DNL Segment Builder] gebruikershandleiding](./segment-builder.md).

![De werkruimte van de Bouwer van het Segment wordt getoond.](../images/ui/overview/segment-builder.png)

## Geplande segmentatie {#scheduled-segmentation}

Zodra de segmentdefinities zijn gecreeerd, kunt u hen door op bestelling of geplande (ononderbroken) evaluatie dan evalueren. Evaluatie betekent verplaatsen [!DNL Real-time Customer Profile] gegevens door segmentdefinities om het overeenkomstige publiek te bereiken. Nadat het publiek is gemaakt, wordt het opgeslagen en opgeslagen zodat het de doelgroep kan exporteren [!DNL Experience Platform] API&#39;s.

De evaluatie op bestelling impliceert het gebruiken van API om evaluatie uit te voeren en publiek te bouwen zoals nodig, terwijl de geplande evaluatie (die ook als &quot;geplande segmentatie&quot;wordt bekend) u toestaat om een terugkerend programma tot stand te brengen om segmentdefinities op een specifieke tijd (bij een maximum, eenmaal per dag) te evalueren.

### Geplande segmentatie inschakelen {#enable-scheduled-segmentation}

Het toelaten van uw segmentdefinities voor geplande evaluatie kan worden gedaan gebruikend UI of API. Ga in de gebruikersinterface terug naar de **[!UICONTROL Browse]** tab within **[!UICONTROL Segments]** en inschakelen **[!UICONTROL Add all segments to schedule]**. Dit zal ertoe leiden dat alle segmenten worden geëvalueerd gebaseerd op het programma dat door uw organisatie wordt geplaatst.

>[!NOTE]
>
>De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor worden toegelaten [!DNL XDM Individual Profile]. Als uw organisatie meer dan vijf samenvoegbeleidsregels heeft voor [!DNL XDM Individual Profile] binnen één sandboxomgeving kunt u geen geplande evaluatie gebruiken.

Planningen kunnen momenteel alleen worden gemaakt met behulp van de API. Voor gedetailleerde stappen bij het maken, bewerken en werken met planningen met behulp van de API, volgt u de zelfstudie voor het evalueren en benaderen van segmentresultaten, met name de sectie over [geplande evaluatie met behulp van de API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![De knevel om alle segmenten aan een programma toe te voegen wordt benadrukt op de Segmenten doorbladert pagina.](../images/ui/overview/segment-browse-scheduled.png)

## Doelgroepen {#audiences}

>[!IMPORTANT]
>
>De publieksfunctionaliteit is momenteel beperkt in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Selecteer **[!UICONTROL Audiences]** tabblad om een lijst weer te geven met alle soorten publiek voor uw organisatie.

![Een lijst met soorten publiek voor uw organisatie.](../images/ui/overview/list-audiences.png)

Standaard wordt in deze weergave informatie weergegeven over het publiek, zoals de naam, het aantal profielen, de oorsprong, de datum waarop het bestand is gemaakt en de datum waarop het laatst is gewijzigd.

U kunt de ![Tabel aanpassen](../images/ui/overview/customize-table.png) om te wijzigen welke velden worden weergegeven.

![De knop Tabel aanpassen is gemarkeerd. Als u deze knop selecteert, kunt u de velden aanpassen die op de pagina Soorten publiek worden weergegeven.](../images/ui/overview/select-customize-table.png)

Er wordt een pop-up weergegeven met alle velden die in de tabel kunnen worden weergegeven.

![De kenmerken die kunnen worden weergegeven voor de sectie Soorten publiek bladeren.](../images/ui/overview/customize-table-attributes.png)

| Veld | Beschrijving |
| ----- | ----------- | 
| [!UICONTROL Name] | De naam van het publiek. |
| [!UICONTROL Profile count] | Het totale aantal profielen dat voor het publiek in aanmerking komt. |
| [!UICONTROL Origin] | De oorsprong van het publiek. Als dit publiek Platform-geproduceerd was, zal het een oorsprong van de Dienst van de Segmentatie hebben. |
| [!UICONTROL Lifecycle status] | De status van het publiek. Mogelijke waarden voor dit veld zijn `Draft`, `Published`, en `Archived`. |
| [!UICONTROL Update frequency] | Een waarde die aangeeft hoe vaak de gegevens van het publiek worden bijgewerkt. Mogelijke waarden voor dit veld zijn `On Demand`, `Scheduled`, en `Continuous`. |
| [!UICONTROL Last updated by] | De naam van de persoon die het publiek het laatst heeft bijgewerkt. |
| [!UICONTROL Created] | De tijd en datum waarop het publiek is gemaakt. |
| [!UICONTROL Last updated] | De tijd en datum waarop het publiek voor het laatst is gemaakt. |
| [!UICONTROL Access labels] | De toegangslabels voor het publiek. De etiketten van de toegang staan u toe om datasets en gebieden volgens gebruiksbeleid te categoriseren dat op die gegevens van toepassing is. Deze labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. Voor meer informatie over toegangslabels, te lezen gelieve de documentatie over [beheren, labels](../../access-control/abac/ui/labels.md). |

U kunt **[!UICONTROL Create Audience]** om een publiek te maken.

![De knop voor een publiek maken is gemarkeerd en geeft aan waar u wilt selecteren om een publiek te maken.](../images/ui/overview/create-audience.png)

Er wordt een pop-up weergegeven, zodat u kunt kiezen tussen het samenstellen van een publiek of het samenstellen van regels.

![Een popover die de twee soorten publiek toont u kunt tot stand brengen.](../images/ui/overview/create-audience-type.png)

Selecteren **[!UICONTROL Compose Audiences]** neemt u aan de Bouwer van de Publiek. Lees voor meer informatie over het maken van soorten publiek de [Handleiding Audience Builder](./audience-builder.md).

Selecteren **[!UICONTROL Build Rule]** gaat u naar de Segment Builder. Voor meer informatie over het maken van segmenten leest u de [Handleiding Segment Builder](./segment-builder.md)

## Details publiek {#audience-details}

Als u meer details over een specifiek publiek wilt zien, selecteert u de naam van een publiek in het dialoogvenster [!UICONTROL Audiences] tab.

De pagina met publieksdetails wordt weergegeven. Deze pagina verschilt in details afhankelijk van het feit of het publiek is gegenereerd met Adobe Experience Platform of van een externe bron zoals Audience Orchestration.

### Door Platforms gegenereerd publiek

Lees voor meer informatie over publiek dat door Platforms wordt gegenereerd de [overzichtssectie segment](#segment-summary).

### Extern gegenereerd publiek

Boven aan de pagina met publieksdetails ziet u een overzicht van het publiek en details over de dataset waarin het publiek wordt opgeslagen.

![De verstrekte details voor een extern geproduceerd publiek.](../images/ui/overview/externally-generated-audience.png)

De **[!UICONTROL Audience summary]** bevat informatie zoals de ID, naam, beschrijving en details van de kenmerken.

De **[!UICONTROL Dataset details]** bevat informatie zoals de naam, beschrijving, tabelnaam, bron en schema. U kunt **[!UICONTROL View dataset]** voor meer informatie over de dataset.

| Veld | Beschrijving |
| ----- | ----------- |
| [!UICONTROL Name] | De naam van de gegevensset. |
| [!UICONTROL Description] | De beschrijving van de gegevensset. |
| [!UICONTROL Table name] | De tabelnaam van de gegevensset. |
| [!UICONTROL Source] | De bron van de gegevensset. Voor extern gegenereerde soorten publiek wordt deze waarde **Schema**. |
| [!UICONTROL Schema] | Het type van XDM schema dat de dataset aan beantwoordt. |

Voor meer informatie over gegevenssets leest u de [Overzicht van gegevenssets](../../catalog/datasets/overview.md).

## Streaming segmentering {#streaming-segmentation}

Streaming segmentatie is de mogelijkheid om segmentatie uit te voeren op [!DNL Platform] in bijna real time, terwijl het concentreren op gegevensrijkdom. Met streamingsegmentatie gebeurt segmentkwalificatie nu als gegevens doorlopen in [!DNL Platform], om de noodzaak om segmentatietaken te plannen en uit te voeren te verlichten.

Meer informatie over streamingsegmentatie vindt u in het gedeelte [gebruikershandleiding voor streamingsegmentatie](./streaming-segmentation.md).

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor meer informatie over het inschakelen van geplande segmentatie raadpleegt u [het gedeelte voor streamingsegmentatie in deze gebruikershandleiding](#scheduled-segmentation).

## Randsegmentatie {#edge-segmentation}

De segmentatie van de rand is de capaciteit om segmenten in Platform op de rand onmiddellijk te evalueren, toelatend de zelfde pagina en volgende de gebruikscituaties van de paginagrootte.

Meer informatie over de segmentatie van de randen vindt u in de [UI-hulplijn voor randsegmentatie](./edge-segmentation.md)

## Beleidsovertredingen

>[!NOTE]
>
>Beleidsovertredingen zijn alleen van toepassing als u een segment maakt dat aan een doel is toegewezen.

Als u klaar bent met het maken van uw segment, wordt het segment geanalyseerd door Adobe Experience Platform Data Governance om ervoor te zorgen dat er geen beleidsovertredingen binnen het segment plaatsvinden. Zie de [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie .

![De beleidsschendingen voor het segment worden getoond.](../images/ui/overview/segment-dule-policy-violations.png)

## Volgende stappen en extra bronnen {#next-steps}

De [!DNL Segmentation Service] UI verstrekt een rijk werkschema dat u toestaat om verhandelbare doelgroepen van te isoleren [!DNL Real-time Customer Profile] gegevens.

Meer informatie over [!DNL Segmentation Service], doorgaat u met het lezen van de documentatie. Leren hoe u de [!DNL Segmentation Service] API, lees de [[!DNL Segmentation Service] ontwikkelaarsgids](../api/overview.md).
