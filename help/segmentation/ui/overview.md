---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;realized;existing;exiting;
solution: Experience Platform
title: Gebruikershandleiding voor segmentatieservice
topic: ui guide
description: Adobe Experience Platform Segmentation Service biedt een gebruikersinterface voor het maken en beheren van segmentdefinities.
translation-type: tm+mt
source-git-commit: 3e83215cc24b32b7fe9486c6faf455f247b6c922
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 0%

---


# Handleiding voor segmentatieservice

[!DNL Adobe Experience Platform Segmentation Service] biedt een gebruikersinterface voor het maken en beheren van segmentdefinities.

## Aan de slag

Het werken met segmentdefinities vereist een begrip van de diverse [!DNL Experience Platform] diensten betrokken bij segmentatie. Lees de documentatie voor de volgende services voordat u deze gebruikershandleiding leest:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] staat u toe om gegevens te verdelen in [!DNL Experience Platform] die op individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) betrekking hebben in kleinere groepen.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Maakt het mogelijk om klantprofielen te maken door identiteiten te overbruggen van verschillende gegevensbronnen waarin ze worden opgenomen [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Platform] georganiseerd.

Het is ook belangrijk om twee belangrijke termen te kennen die in dit document worden gebruikt en het verschil tussen hen te begrijpen:
- **Segmentdefinitie**: De regelreeks die wordt gebruikt om zeer belangrijke eigenschappen of gedrag van een doelpubliek te beschrijven.
- **Publiek**: De resulterende set profielen die voldoen aan de criteria van een segmentdefinitie.

## Overzicht

In [[!DNL Experience Platform] UI](http://platform.adobe.com/), uitgezochte **[!UICONTROL Segmenten]** in de linkernavigatie om het **[!UICONTROL Overzicht]** tabel te openen. Dit tabblad bevat koppelingen naar documentatie en video&#39;s waarmee u segmenten kunt begrijpen en bewerken.

![](../images/ui/overview/segment-overview.png)

## Bladeren

Selecteer het tabblad **[!UICONTROL Bladeren]** om een lijst met alle segmentdefinities voor uw IMS-organisatie weer te geven.

![](../images/ui/overview/segment-browse-all.png)

Deze mening maakt een lijst van informatie over de segmentdefinitie met inbegrip van de uitsplitsing, de koeling, de profieltelling, de evaluatiemethode, gecreeerd datum, en laatst gewijzigde datum.

De uitsplitsing toont een staafgrafiek die het percentage van profielen schetst die tot elk van de volgende statussen behoren: [!UICONTROL Ingegaan], [!UICONTROL Gelaliseerd], en [!UICONTROL Beëindigen].

![](../images/ui/overview/segment-browse-breakdown.png)

| Status | Beschrijving |
| ------ | ----------- |
| Ingegaan | Een nieuw profiel binnen het segment. |
| Gerealiseerd | Een bestaand profiel dat binnen het segment is gebleven. |
| Afsluiten | Een bestaand profiel dat het segment verlaat. |

De kolom vertegenwoordigt het percentage profielen die binnen een segmentdefinitie in vergelijking met de laatste tijd veranderen de segmentbaan liep, terwijl de profieltelling het totale aantal profielen vertegenwoordigt die voor het segment kwalificeren.

De evaluatiemethode kan streaming of batch zijn. Streaming segmenten worden voortdurend geëvalueerd terwijl gegevens in het systeem worden ingevoerd. De segmenten van de partij worden geëvalueerd volgens een vastgesteld programma.

![](../images/ui/overview/segment-browse-segments.png)

Boven aan de pagina staan opties voor het toevoegen van alle segmenten aan een schema en het maken van een nieuw segment.

Als u schakelt **[!UICONTROL Alle segmenten aan schema]** toevoegen, wordt de geplande segmentatie ingeschakeld. Meer informatie over geplande segmentatie kan in de [geplande segmenteringssectie van deze gebruikersgids](#scheduled-segmentation)worden gevonden.

Als u Segment **** maken selecteert, gaat u naar de Segment Builder. Lees voor meer informatie over het maken van segmenten de sectie over het [maken van een segment in de gebruikershandleiding](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

De rechterzijbalk bevat informatie over alle segmenten binnen de IMS-organisatie, met een overzicht van het totale aantal segmenten, de laatste evaluatiedatum, de volgende evaluatiedatum en een uitsplitsing van de segmenten naar evaluatiemethode.

![](../images/ui/overview/segment-browse-segment-info.png)

Het selecteren van de rij van de segmentdefinitie verstrekt een samenvatting van de segmentdefinitie, met inbegrip van opties om of het segment uit te geven of te schrappen, het gekwalificeerde publiek voor het segment, de totale publieksgrootte, naast de naam van het segment, beschrijving, evaluatiemethode, gecreeerd datum, en laatst gewijzigde datum.

![](../images/ui/overview/segment-browse-details.png)

## Segmentdefinitiedetails {#segment-details}

Om meer details over een specifieke segmentdefinitie te zien, selecteer de naam van een segment binnen het **[!UICONTROL Browse]** lusje.

De pagina met segmentdetails wordt weergegeven. Bovenaan, is er een samenvatting van de segmentdefinitie, informatie over de gekwalificeerde publieksgrootte, evenals bestemmingen het segment voor wordt geactiveerd.

![](../images/ui/overview/segment-details-summary.png)

### Overzicht van segment

De overzichtssectie **[!UICONTROL Segment]** bevat informatie zoals de id, naam, beschrijving en details van de kenmerken.

Bovendien kunt u het segment bewerken. Als u Segment **** bewerken selecteert, komt u naar de [!DNL Segment Builder]gewenste locatie. Lees voor meer informatie over het gebruik van de [!DNL Segment Builder] werkruimte de [[!DNL Segment Builder] gebruikershandleiding](./segment-builder.md).

### Totaal aantal deelnemers in segment

Het **[!UICONTROL totale publiek in segmentsectie]** toont het totale aantal profielen dat voor het segment kwalificeert.

Schattingen worden gegenereerd door gebruik te maken van een steekproefgrootte van de voorbeeldgegevens van die dag. Als uw profielarchief minder dan 1 miljoen entiteiten bevat, wordt de volledige gegevensset gebruikt. voor tussen 1 en 20 miljoen entiteiten worden 1 miljoen entiteiten gebruikt; en voor meer dan 20 miljoen entiteiten wordt 5 % van de totale entiteiten gebruikt . Meer informatie over het produceren van segmentramingen kan in de sectie [van de de](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) schattingsproductie van de sectievan de segmentverwezenlijking worden gevonden.

### Geactiveerde doelen

De **[!UICONTROL Geactiveerde bestemmingssectie]** toont de bestemmingen waarvoor dit segment wordt geactiveerd.

>[!NOTE]
>
> Doelen zijn een functie die beschikbaar is bij [!DNL Real-time Customer Data Platform]en waarmee u gegevens kunt exporteren naar externe platforms. Voor meer informatie over bestemmingen, gelieve het overzicht [van](../../destinations/home.md)bestemmingen te lezen. Leer hoe te om een segment aan een bestemming te activeren, te lezen gelieve de [gids bij het activeren van segmenten aan een bestemming](../../destinations/ui/activate-destinations.md).

### Profielvoorbeelden

Hieronder ziet u een voorbeeld van profielen die in aanmerking komen voor het segment, met gedetailleerde informatie zoals de [!DNL Profile] id, voornaam, achternaam en persoonlijke e-mail.

De manier waarop gegevensbemonstering wordt geactiveerd, is afhankelijk van de innamemethode.

Voor batch-opname wordt de profielopslag automatisch elke 15 minuten gescand om te zien of een nieuwe batch is opgenomen sinds de laatste samplingtaak is uitgevoerd. Als dat het geval is, wordt de profielopslag gescand om te zien of is er minstens een 5% verandering in het aantal verslagen. Als aan deze voorwaarden wordt voldaan, wordt een nieuwe steekproefbaan teweeggebracht.

Voor het stromen opname, wordt de profielopslag automatisch gescand elk uur om te zien of is er minstens een 5% verandering in het aantal verslagen geweest. Als aan deze voorwaarde wordt voldaan, wordt een nieuwe steekproefbaan teweeggebracht.

De voorbeeldgrootte van de scan is afhankelijk van het totale aantal entiteiten in de profielopslag. Deze steekproefgrootte wordt vertegenwoordigd in de volgende lijst:

| Entiteiten in profielopslag | Voorbeeldformaat |
| ------------------------- | ----------- |
| Minder dan 1 miljoen | Volledige gegevensset |
| 1 tot 20 miljoen | 1 miljoen |
| Meer dan 20 miljoen | 5% van het totaal |

Meer gedetailleerde informatie over elk [!DNL Profile] [!DNL Profile] kan worden gezien door identiteitskaart te selecteren. Lees de [[!DNL Real-time Customer Profile] gebruikershandleiding](../../profile/ui/user-guide.md#profile-detail)voor meer informatie over de details van een profiel.

![](../images/ui/overview/segment-details-profiles.png)

## Segment maken {#create-segment}

Als u Segment **** maken in de rechterbovenhoek selecteert, wordt de [!DNL Segment Builder] werkruimte geopend waarin u een segmentdefinitie kunt maken.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] werkruimte

[!DNL Segment Builder] biedt een rijke werkruimte waarmee u kunt werken met [!DNL Profile] gegevenselementen. De werkruimte biedt intuïtieve besturingselementen voor het maken en bewerken van regels, zoals tegels voor slepen en neerzetten die worden gebruikt om gegevenseigenschappen te vertegenwoordigen.

Lees voor meer informatie over het gebruik van de [!DNL Segment Builder] werkruimte de [[!DNL Segment Builder] gebruikershandleiding](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Geplande segmentatie {#scheduled-segmentation}

Zodra de segmentdefinities zijn gecreeerd, kunt u hen door op bestelling of geplande (ononderbroken) evaluatie dan evalueren. Evaluatie houdt in dat [!DNL Real-time Customer Profile] gegevens door segmentdefinities worden verplaatst om het overeenkomstige publiek te bereiken. Nadat het publiek is gemaakt, wordt het opgeslagen en opgeslagen zodat het kan worden geëxporteerd met [!DNL Experience Platform] API&#39;s.

De evaluatie op bestelling impliceert het gebruiken van API om evaluatie uit te voeren en publiek te bouwen zoals nodig, terwijl de geplande evaluatie (die ook als &quot;geplande segmentatie&quot;wordt bekend) u toestaat om een terugkerend programma tot stand te brengen om segmentdefinities op een specifieke tijd (bij een maximum, eenmaal per dag) te evalueren.

### Geplande segmentatie inschakelen {#enable-scheduled-segmentation}

Het toelaten van uw segmentdefinities voor geplande evaluatie kan worden gedaan gebruikend UI of API. In UI, terugkeer naar het **[!UICONTROL Browse]** lusje binnen **[!UICONTROL Segmenten]** en knevel op **[!UICONTROL Add alle segmenten aan programma]**. Dit zal ertoe leiden dat alle segmenten worden geëvalueerd gebaseerd op het programma dat door uw organisatie wordt geplaatst.

>[!NOTE]
>
>De geplande evaluatie kan voor zandbakken met een maximum van vijf (5) fusiebeleid voor worden toegelaten [!DNL XDM Individual Profile]. Als uw organisatie meer dan vijf samenvoegingsbeleid voor [!DNL XDM Individual Profile] binnen één enkele zandbakmilieu heeft, zult u geen geplande evaluatie kunnen gebruiken.

Planningen kunnen momenteel alleen worden gemaakt met behulp van de API. Voor gedetailleerde stappen bij het creëren van, het uitgeven van, en het werken met programma&#39;s die API gebruiken, te volgen gelieve de leerprogramma&#39;s voor het evalueren van en de toegang tot van segmentresultaten, specifiek de sectie over [geplande evaluatie gebruikend API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Streaming segmentering {#streaming-segmentation}

Streaming segmentatie is de mogelijkheid om segmentatie uit te voeren [!DNL Platform] in bijna real-time, terwijl de nadruk ligt op gegevensrijkheid. Met het stromen segmentatie, gebeurt de segmentkwalificatie nu aangezien de gegevens in landen [!DNL Platform], die de behoefte verlichten om segmentatietaken te plannen en in werking te stellen.

Meer informatie over streamingsegmentatie vindt u in de gebruikershandleiding voor [streamingsegmentatie](./streaming-segmentation.md).

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor meer informatie over het inschakelen van geplande segmentatie raadpleegt u [de sectie streamingsegmentatie in deze gebruikershandleiding](#scheduled-segmentation).

## Beleidsovertredingen

>[!NOTE]
>
>Beleidsovertredingen zijn alleen van toepassing als u een segment maakt dat aan een doel is toegewezen.

Als u klaar bent met het maken van uw segment, wordt het segment geanalyseerd door Adobe Experience Platform Data Governance om ervoor te zorgen dat er geen beleidsovertredingen binnen het segment plaatsvinden. Zie het [[!DNL Data Governance] overzicht](../../data-governance/home.md) voor meer informatie.

![](../images/ui/overview/segment-dule-policy-violations.png)

## Volgende stappen en extra bronnen {#next-steps}

De [!DNL Segmentation Service] interface biedt een rijke workflow waarmee u verhandelbare doelgroepen kunt isoleren van [!DNL Real-time Customer Profile] gegevens.

Lees de documentatie voor meer informatie [!DNL Segmentation Service]. Lees voor meer informatie over het gebruik van de [!DNL Segmentation Service] API de handleiding voor [[!DNL Segmentation Service] ontwikkelaars](../api/overview.md).
