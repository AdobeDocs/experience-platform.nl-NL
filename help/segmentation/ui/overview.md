---
solution: Experience Platform
title: UI-gids voor segmentatieservice
description: Leer hoe u publiek- en segmentdefinities kunt maken en beheren in de gebruikersinterface van Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---

# Handleiding voor segmentatieservice

[!DNL Adobe Experience Platform Segmentation Service] biedt een gebruikersinterface voor het maken en beheren van publiek- en segmentdefinities.

## Aan de slag

Als u met doelgroepen en segmentdefinities werkt, hebt u inzicht nodig in de verschillende [!DNL Experience Platform] -services die met segmentatie te maken hebben. Lees de documentatie voor de volgende services voordat u deze gebruikershandleiding leest:

- [[!DNL Segmentation Service]](../home.md) [!DNL Segmentation Service] : hiermee kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, vooruitzichten, gebruikers of organisaties), segmenteren in kleinere groepen.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Schakelt het maken van klantprofielen in door identiteiten te overbruggen van verschillende gegevensbronnen die in [!DNL Experience Platform] worden opgenomen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt. Om het beste gebruik van Segmentatie te maken, gelieve te verzekeren uw gegevens als profielen en gebeurtenissen volgens de [ beste praktijken voor gegevens modellering ](../../xdm/schema/best-practices.md) worden opgenomen.

U moet ook de volgende belangrijke termen begrijpen die in dit document worden gebruikt en het verschil tussen deze termen begrijpen:

- **Publiek**: Een inzameling van mensen die gelijkaardig gedrag en/of kenmerken delen. Deze inzameling van mensen kan of door Adobe Experience Platform worden geproduceerd gebruikend segmentdefinities (Ervaring-Platform-geproduceerde publiek), publiekssamenstelling, of uit externe bronnen zoals douane uploads (extern geproduceerd publiek).
- **definitie van het Segment**: De regels Adobe Experience Platform gebruikt om zeer belangrijke kenmerken of gedrag van een doelpubliek te beschrijven.
- **Segment**: Het besluit om Profielen in publiek te scheiden.

## Overzicht

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Audiences]** in de linkernavigatie om het tabblad **[!UICONTROL Overview]** met het dashboard van [!UICONTROL Audiences] te openen.

>[!NOTE]
>
>Als uw organisatie nieuw is voor Experience Platform en nog geen actieve profielgegevenssets of samenvoegbeleid heeft gemaakt, is het dashboard van [!UICONTROL Audiences] niet zichtbaar. In plaats daarvan geeft het tabblad [!UICONTROL Overview] koppelingen en documentatie weer om u te helpen aan de slag te gaan met het publiek.

### [!UICONTROL Audiences] dashboard {#segments-dashboard}

Het dashboard van **[!UICONTROL Audiences]** beschrijft zeer belangrijke metriek met betrekking tot de publieksgegevens van uw organisatie.

Meer leren, bezoek de [ gids van het publiek dashboard ](../../dashboards/guides/audiences.md).

![ het publieksdashboard wordt getoond. Het toont diverse widgets, met inbegrip van de publieksgrootte, profielen door identiteit, identiteitsoverlapping, en de de veranderingstrend van de publieksgrootte.](../../dashboards/images/segments/dashboard-overview.png)

## Bladeren {#browse}

Selecteer het tabblad **[!UICONTROL Browse]** om de portal Poorten publiek weer te geven. Het Portaal van de Publiek verstrekt een lijst van alle publiek dat tot uw organisatie en zandbak behoort, en omvat details zoals het profielaantal, de oorsprong, de gecreeerde datum, de laatst gewijzigde datum, de markeringen, en de mislukking.

Daarnaast kunt u met Poortpubliek publiek nieuwe soorten publiek maken met Segment Builder of Audience Composition en extern gegenereerde soorten publiek importeren in Experience Platform.

Voor meer informatie over het Portaal van het Publiek, gelieve het [ Poortoverzicht van het Poortpubliek van het Publiek ](./audience-portal.md) te lezen.

## Composities {#compositions}

Selecteer het tabblad **[!UICONTROL Compositions]** om een lijst weer te geven met alle soorten publiek dat via Audience Composition voor uw organisatie wordt gegenereerd.

![ een lijst van publiek dat in de Samenstelling van het Publiek voor uw organisatie wordt gecreeerd.](../images/ui/overview/compositions.png)

Standaard wordt in deze weergave informatie weergegeven over het publiek, zoals de naam, status, gemaakte datum, gemaakt op, laatst bijgewerkte datum en laatst bijgewerkt op.

Naast elk publiek bevindt zich een ellipspictogram. Als u deze optie selecteert, wordt een lijst weergegeven met beschikbare snelle acties voor de doelgroep.

| Actie | Beschrijving |
| ------ | ----------- |
| Dupliceren | Kopieert het geselecteerde publiek. |
| Toegang beheren | Beheert de toegangslabels die bij het publiek horen. Voor meer informatie over toegangslabels, te lezen gelieve de documentatie over [ het leiden etiketten ](../../access-control/abac/ui/labels.md). |
| Verwijderen | Hiermee verwijdert u het geselecteerde publiek. Het publiek dat in stroomafwaartse bestemmingen wordt gebruikt of gebiedsdelen in andere soorten publiek **zijn kan** niet worden geschrapt. Voor meer informatie over publieksschrapping, te lezen gelieve [ segmentatie FAQ ](../faq.md#lifecycle-states). |

U kunt ![ selecteren past lijst ](/help/images/icons/column-settings.png) pictogram aan om te veranderen welke gebieden worden getoond.

![ de aanpasbare lijstknoop wordt benadrukt. Het selecteren van deze knoop staat u toe om de gebieden aan te passen die op de de samenstellingspagina van het publiek worden getoond.](../images/ui/overview/compositions-select-customize-table.png)

Er wordt een pop-up weergegeven met alle velden die in de tabel kunnen worden weergegeven.

![ de attributen die voor de sectie van de Samenstelling kunnen worden getoond.](../images/ui/overview/compositions-customize-table.png)

| Veld | Beschrijving |
| ----- | ----------- | 
| [!UICONTROL Name] | De naam van het publiek. |
| [!UICONTROL Status] | De status van het publiek. Mogelijke waarden voor dit veld zijn `Draft` , `Inactive` en `Published` . |
| [!UICONTROL Created] | De tijd en datum waarop het publiek is gemaakt. |
| [!UICONTROL Created by] | De naam van de persoon die het publiek heeft gemaakt. |
| [!UICONTROL Updated] | De tijd en datum waarop het publiek voor het laatst is bijgewerkt. |
| [!UICONTROL Updated by] | De naam van de persoon die het publiek het laatst heeft bijgewerkt. |

Als u wilt zien hoe de doelgroep wordt samengesteld, selecteert u de naam van een publiek in het tabblad [!UICONTROL Audiences] .

De pagina van de Samenstelling van het Publiek verschijnt met de bouwstenen die uw publiek vormen. Voor meer details over hoe te om de Samenstelling van het Publiek te gebruiken, te lezen gelieve de [ gids UI van de Samenstelling van het Publiek ](./audience-composition.md).

## Samenstelling van Federated-doelgroep {#fac}

Naast publiekssamenstellingen en segmentdefinities kunt u Adobe Federated Audience Composition gebruiken om nieuwe soorten publiek te maken van bedrijfsgegevenssets zonder onderliggende gegevens te kopiëren en die soorten publiek op te slaan in Adobe Experience Platform Audience Portal. U kunt bestaande soorten publiek in Adobe Experience Platform ook verrijken door samengestelde publieksgegevens te gebruiken die van het entrepot van ondernemingsgegevens zijn gefedereerd. Gelieve te lezen de gids op [ Federated de Samenstelling van het Publiek ](https://experienceleague.adobe.com/nl/docs/federated-audience-composition/using/home).

![ een lijst van publiek dat in Federatieve Samenstelling van het Publiek voor uw organisatie wordt gecreeerd.](../images/ui/overview/federated-audience-composition.png)

## Streaming segmentering {#streaming-segmentation}

Streaming segmentatie is de mogelijkheid om segmentatie uit te voeren op [!DNL Experience Platform] in bijna real-time, terwijl de nadruk ligt op gegevensrijkheid. Met streamingsegmentatie gebeurt er nu segmentering als gegevens in [!DNL Experience Platform] terechtkomen, waardoor de noodzaak om segmentatietaken te plannen en uit te voeren, wordt verminderd.

Meer informatie over het stromen segmentatie kan in de [ het stromen gebruikershandleiding van de segmentatie ](../methods/streaming-segmentation.md) worden gevonden.

>[!NOTE]
>
>Opdat het stromen segmentatie aan het werk is, zult u geplande segmentatie voor de organisatie moeten toelaten. Voor details bij het toelaten van geplande segmentatie, gelieve te verwijzen naar [ de het stromen segmentatiesectie in deze gebruikersgids ](#scheduled-segmentation).

## Edge-segmentatie {#edge-segmentation}

Edge-segmentatie is de mogelijkheid om het publiek in Experience Platform ogenblikkelijk aan de rand te evalueren, zodat dezelfde pagina en de volgende pagina kunnen worden gebruikt voor personalisatie.

Meer informatie over randsegmentatie kan in de [ gids van de randsegmentatie UI worden gevonden ](../methods/edge-segmentation.md)

## Beleidsovertredingen

>[!NOTE]
>
>Beleidsovertredingen zijn alleen van toepassing als u een publiek maakt dat aan een doel is toegewezen.

Als u klaar bent met het maken van uw publiek, wordt het publiek geanalyseerd door Adobe Experience Platform Data Governance om ervoor te zorgen dat er geen beleidsovertredingen binnen het publiek plaatsvinden. Zie het [ overzicht van het Beleid van Gegevens ](../../data-governance/home.md) voor meer informatie.

![ de beleidsschendingen voor het publiek worden getoond.](../images/ui/overview/audience-dule-policy-violations.png)

## Volgende stappen en extra bronnen {#next-steps}

De gebruikersinterface van [!DNL Segmentation Service] biedt een rijke workflow waarmee u commercieel publiek kunt maken op basis van [!DNL Real-Time Customer Profile] -gegevens.

Lees de documentatie voor meer informatie over [!DNL Segmentation Service] . Leren hoe te om [!DNL Segmentation Service] API te gebruiken, te lezen gelieve de [[!DNL Segmentation Service]  ontwikkelaarsgids ](../api/overview.md).
