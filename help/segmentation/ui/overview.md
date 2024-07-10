---
solution: Experience Platform
title: UI-gids voor segmentatieservice
description: Leer hoe u publiek- en segmentdefinities kunt maken en beheren in de gebruikersinterface van Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: acfe91144175e136955ffd9f0cdae2c351217c16
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Handleiding voor segmentatieservice

[!DNL Adobe Experience Platform Segmentation Service] biedt een gebruikersinterface voor het maken en beheren van publiek- en segmentdefinities.

## Aan de slag

Om met het publiek en de segmentdefinities te kunnen werken, is een goed begrip van de verschillende [!DNL Experience Platform] diensten in verband met segmentatie. Lees de documentatie voor de volgende services voordat u deze gebruikershandleiding leest:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] dat betrekking heeft op individuen (zoals klanten, vooruitzichten, gebruikers, of organisaties) in kleinere groepen.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Schakelt het maken van klantprofielen in door identiteiten te overbruggen van verschillende gegevensbronnen waarin deze worden opgenomen [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring. Als u de segmentatie het beste wilt gebruiken, moet u ervoor zorgen dat uw gegevens als profielen en gebeurtenissen worden opgenomen volgens de [best practices voor gegevensmodellering](../../xdm/schema/best-practices.md).

U moet ook de volgende belangrijke termen begrijpen die in dit document worden gebruikt en het verschil tussen deze termen begrijpen:

- **Publiek**: Een verzameling personen die vergelijkbare gedragingen en/of kenmerken delen. Deze inzameling van mensen kan of door Adobe Experience Platform worden geproduceerd gebruikend segmentdefinities (Platform-geproduceerde publiek), publiekssamenstelling, of uit externe bronnen zoals douane uploads (extern geproduceerd publiek).
- **Segmentdefinitie**: De regels die Adobe Experience Platform gebruikt om sleutelkenmerken of gedrag van een doelpubliek te beschrijven.
- **Segment**: Het scheiden van profielen in publiek.

## Overzicht

Selecteer in de gebruikersinterface van het Experience Platform de optie **[!UICONTROL Audiences]** in de linkernavigatie om de **[!UICONTROL Overview]** tabblad met het tabblad [!UICONTROL Audiences] dashboard.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog geen actieve datasets van het Profiel of gecreeerd samenvoegbeleid heeft, [!UICONTROL Audiences] het dashboard is niet zichtbaar. In plaats daarvan [!UICONTROL Overview] op het tabblad vindt u koppelingen en documentatie waarmee u aan de slag kunt gaan met het publiek.

### [!UICONTROL Audiences] dashboard {#segments-dashboard}

De **[!UICONTROL Audiences]** het dashboard schetst belangrijke metriek met betrekking tot de publieksgegevens van uw organisatie.

Ga voor meer informatie naar de [gebruikershandleiding in dashboard](../../dashboards/guides/audiences.md).

![Het doeldashboard wordt weergegeven. Er worden verschillende widgets weergegeven, zoals de omvang van het publiek, profielen op basis van identiteit, identiteitsoverlapping en de trend om de omvang van het publiek te wijzigen.](../../dashboards/images/segments/dashboard-overview.png)

## Bladeren {#browse}

Selecteer de **[!UICONTROL Browse]** om het Poort van het Publiek te zien. Het Portaal van de Publiek verstrekt een lijst van alle publiek dat tot uw organisatie en zandbak behoort, en omvat details zoals het profielaantal, de oorsprong, de gecreeerde datum, de laatst gewijzigde datum, de markeringen, en de mislukking.

Daarnaast kunt u met Poort publiek nieuwe doelgroepen maken met Segment Builder of Audience Composition en extern gegenereerde doelgroepen importeren in Platform.

Voor meer informatie over de portal Poorten publiek, lees de [Overzicht van het portal Publiek](./audience-portal.md).

## Composities {#compositions}

Selecteer de **[!UICONTROL Compositions]** om een lijst van alle publiek te zien dat door de Samenstelling van het Publiek voor uw organisatie wordt geproduceerd.

![Een lijst van publiek dat in de Samenstelling van het Publiek voor uw organisatie wordt gecreeerd.](../images/ui/overview/compositions.png)

Standaard wordt in deze weergave informatie weergegeven over het publiek, zoals de naam, status, gemaakte datum, gemaakt op, laatst bijgewerkte datum en laatst bijgewerkt op.

Naast elk publiek bevindt zich een ellipspictogram. Als u deze optie selecteert, wordt een lijst weergegeven met beschikbare snelle acties voor de doelgroep.

| Actie | Beschrijving |
| ------ | ----------- |
| Dupliceren | Kopieert het geselecteerde publiek. |
| Toegang beheren | Beheert de toegangslabels die bij het publiek horen. Voor meer informatie over toegangslabels, te lezen gelieve de documentatie over [beheren, labels](../../access-control/abac/ui/labels.md). |
| Verwijderen | Hiermee verwijdert u het geselecteerde publiek. Soorten publiek dat wordt gebruikt in downstreambestemmingen of dat afhankelijk is van ander publiek **kan** worden geschrapt. Lees voor meer informatie over het verwijderen van het publiek de [Veelgestelde vragen over segmentatie](../faq.md#lifecycle-states). |

U kunt de ![Tabel aanpassen](../images/ui/overview/customize-table.png) om te wijzigen welke velden worden weergegeven.

![De knop Tabel aanpassen is gemarkeerd. Als u deze knop selecteert, kunt u de velden aanpassen die op de pagina Soorten publiek worden weergegeven.](../images/ui/overview/compositions-select-customize-table.png)

Er wordt een pop-up weergegeven met alle velden die in de tabel kunnen worden weergegeven.

![De kenmerken die kunnen worden weergegeven voor de sectie Compositie.](../images/ui/overview/compositions-customize-table.png)

| Veld | Beschrijving |
| ----- | ----------- | 
| [!UICONTROL Name] | De naam van het publiek. |
| [!UICONTROL Status] | De status van het publiek. Mogelijke waarden voor dit veld zijn `Draft`, `Inactive`, en `Published`. |
| [!UICONTROL Created] | De tijd en datum waarop het publiek is gemaakt. |
| [!UICONTROL Created by] | De naam van de persoon die het publiek heeft gemaakt. |
| [!UICONTROL Updated] | De tijd en datum waarop het publiek voor het laatst is bijgewerkt. |
| [!UICONTROL Updated by] | De naam van de persoon die het publiek het laatst heeft bijgewerkt. |

Als u wilt zien hoe het publiek wordt samengesteld, selecteert u de naam van een publiek in het dialoogvenster [!UICONTROL Audiences] tab.

De pagina van de Samenstelling van het Publiek verschijnt met de bouwstenen die uw publiek vormen. Voor meer informatie over het gebruik van Audience Composition raadpleegt u de [Handleiding voor compositie van publiek](./audience-composition.md).

## Streaming segmentering {#streaming-segmentation}

Streaming segmentatie is de mogelijkheid om segmentatie uit te voeren op [!DNL Platform] in bijna real time, terwijl het concentreren op gegevensrijkdom. Met streamingsegmentatie gebeurt kwalificatie voor segmentatie nu als gegevens binnenkomen [!DNL Platform], om de noodzaak om segmentatietaken te plannen en uit te voeren te verlichten.

Meer informatie over streamingsegmentatie vindt u in het gedeelte [gebruikershandleiding voor streamingsegmentatie](./streaming-segmentation.md).

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Raadpleeg voor meer informatie over het inschakelen van geplande segmentatie [het gedeelte voor streamingsegmentatie in deze gebruikershandleiding](#scheduled-segmentation).

## Edge-segmentatie {#edge-segmentation}

Edge-segmentatie is de mogelijkheid om het publiek in Platform ogenblikkelijk aan de rand te evalueren, zodat dezelfde pagina en de volgende pagina-personalisatie gebruikstoepassingen mogelijk maken.

Meer informatie over de segmentatie van de randen vindt u in de [gebruikersgids voor randsegmentatie](./edge-segmentation.md)

## Beleidsovertredingen

>[!NOTE]
>
>Beleidsovertredingen zijn alleen van toepassing als u een publiek maakt dat aan een doel is toegewezen.

Als u klaar bent met het maken van uw publiek, wordt het publiek geanalyseerd door Adobe Experience Platform Data Governance om ervoor te zorgen dat er geen beleidsovertredingen binnen het publiek plaatsvinden. Zie de [Overzicht van gegevensbeheer](../../data-governance/home.md) voor meer informatie .

![De beleidsovertredingen voor het publiek worden weergegeven.](../images/ui/overview/audience-dule-policy-violations.png)

## Volgende stappen en extra bronnen {#next-steps}

De [!DNL Segmentation Service] UI verstrekt een rijk werkschema dat u toestaat om verhandelbare soorten publiek van te creëren [!DNL Real-Time Customer Profile] gegevens.

Meer informatie over [!DNL Segmentation Service], doorgaat u met het lezen van de documentatie. Leren hoe u de [!DNL Segmentation Service] API, lees de [[!DNL Segmentation Service] ontwikkelaarsgids](../api/overview.md).
