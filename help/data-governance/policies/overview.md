---
keywords: Experience Platform;thuis;populaire onderwerpen;module;DULE
solution: Experience Platform
title: Overzicht van beleidsregels voor gegevensgebruik
topic-legacy: policies
description: Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen het Experience Platform, of dat u er een beperking voor hebt.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: c314cba6b822e12aa0367e1377ceb4f6c9d07ac2
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Overzicht van beleidsregels voor gegevensgebruik {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Gegevensgebruik beperken"
>abstract="Het beleidstype voor gegevensgebruik evalueert specifieke marketingacties die worden toegepast op labels voor gegevensbeheer om het gegevensgebruik voor marketingactiviteiten te beperken."

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen mag uitvoeren [!DNL Experience Platform].

Er zijn twee soorten beleid beschikbaar:

* **[!UICONTROL Data governance policy]**: Beperk de gegevensactivering op basis van de marketingactie die wordt uitgevoerd en de labels voor gegevensgebruik die door de betrokken gegevens worden meegevoerd.
* **[!UICONTROL Consent policy]**: De profielen filteren waarop kan worden geactiveerd [bestemmingen](../../destinations/home.md) op basis van de toestemming of voorkeuren van uw klanten

>[!NOTE]
>
>Beleid voor gegevensgebruik mag niet worden verward met [toegangsbeheerbeleid](../../access-control/abac/end-to-end-guide.md#policy), die bepalen of bepaalde gebruikers van het Platform in uw organisatie tot bepaalde gegevensgebieden kunnen toegang hebben, en gevormd door [!UICONTROL Permissions] tab.

Dit document biedt een overzicht op hoog niveau van het beleid voor gegevensgebruik en bevat koppelingen naar verdere documentatie voor het werken met het beleid in de gebruikersinterface of de API.

## Marketingacties {#marketing-actions}

Marketingacties (ook wel gevallen van marketinggebruik genoemd) in het kader van het gegevensbeheerkader zijn acties die [!DNL Experience Platform] gegevens kan de consument nemen, waarvoor uw organisatie gegevensgebruik wil beperken. Daarom wordt een beleid voor gegevensgebruik als volgt gedefinieerd:

1. Een specifieke marketingactie
2. De voorwaarden waaronder die handeling niet kan worden uitgevoerd

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid is dat zegt dat de specifieke types van gegevens (zoals Persoonlijk identificeerbare Informatie (PII)) niet kunnen worden uitgevoerd, en u probeert om een dataset uit te voeren die een &quot;I&quot;etiket (Gegevens van de Identiteit) bevat, zult u een reactie van het [!DNL Policy Service] u vertellen dat een beleid van het gegevensgebruik is geschonden.

>[!NOTE]
>
>Handelingen voor het in de handel brengen zelf beperken het gegevensgebruik niet. Ze moeten worden opgenomen in beleid voor ingeschakeld gegevensgebruik om ervoor te zorgen dat deze acties worden geëvalueerd op beleidsovertredingen.

Wanneer het gegevensgebruik in de dienst van uw organisatie gebeurt, zouden de relevante marketing acties moeten worden vermeld zodat om het even welke beleidsschendingen kunnen worden geïdentificeerd. U kunt dan de [Beleidsservice-API](https://www.adobe.io/experience-platform-apis/references/policy-service/) om te controleren op beleidsovertredingen in uw integratie.

>[!NOTE]
>
>U kunt de gevallen van het plaatsingsgebruik op bestemmingen plaatsen om beleidshandhaving te automatiseren. Zie de [documentatie voor doelen](../../destinations/home.md) voor meer informatie over de configuratieopties voor uw bepaalde bestemming.

Zie de bijlage bij dit document voor een lijst met [beschikbare door Adobe gedefinieerde marketingacties](#core-actions). U kunt ook uw eigen aangepaste marketingacties definiëren met de opdracht [!DNL Policy Service] API of de [!DNL Experience Platform] gebruikersinterface. In de volgende sectie vindt u meer informatie over het werken met marketingacties en -beleid.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Beleid voor gegevensgebruik beheren {#manage}

Zodra de etiketten van het gegevensgebruik zijn toegepast, kunnen de gegevens eerder gebruiken [!DNL Policy Service] API of de [!DNL Experience Platform] UI voor het beheren en evalueren van beleid met betrekking tot marketingacties die worden uitgevoerd op gegevens die labels voor gegevensgebruik bevatten. U kunt beleid tot stand brengen en bijwerken, de status van een beleid bepalen, en met marketing acties werken om te evalueren of een specifieke actie een beleid van het gegevensgebruik schendt.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten door API of UI.

Zie de zelfstudie voor stapsgewijze instructies voor het werken met marketingacties en het beleid voor gegevensgebruik in de API [beleid voor gegevensgebruik maken en evalueren](create.md). Voor meer informatie over de belangrijkste bewerkingen die door de [!DNL Policy Service] API, zie [Handleiding voor ontwikkelaars van beleidsservices](../api/getting-started.md).

Voor informatie over hoe u met marketingacties en -beleid kunt werken in de [!DNL Platform] UI, zie [gebruikershandleiding voor gegevensgebruiksbeleid](./user-guide.md).

## Volgende stappen

Dit document bevatte een inleiding op het beleid inzake gegevensgebruik binnen het kader voor gegevensbeheer. U kunt nu de procesdocumentatie blijven lezen met betrekking tot deze gids voor meer informatie over hoe te met beleid in API en UI te werken.

## Aanhangsel

De volgende sectie verstrekt extra informatie over het beleid van het gegevensgebruik.

### Door Adobe gedefinieerde marketingacties {#core-actions}

In de onderstaande tabel worden de belangrijkste marketingacties beschreven die door Adobe buiten de box worden geleverd.

>[!NOTE]
>
>De belangrijkste marketingacties moeten worden beschouwd als een uitgangspunt om u te helpen bepalen welk gebruiksbeleid u moet maken en controleren op overtredingen. De definities en hoe deze worden geïnterpreteerd, zijn afhankelijk van de behoeften en het beleid van uw organisatie.

| Handeling | Beschrijving |
| --- | --- |
| Analytics | Een handeling die gegevens gebruikt voor analytische doeleinden, zoals het meten, analyseren en rapporteren van het gebruik van de sites of apps van uw organisatie door klanten. |
| Combineren met rechtstreeks identificeerbare gegevens | Een handeling waarbij alle PII&#39;s (Personal Identified Information) worden gecombineerd met anonieme gegevens. Contracten voor gegevens die afkomstig zijn van advertentienetwerken, servers en derde gegevensleveranciers bevatten vaak specifieke contractuele verbodsbepalingen inzake het gebruik van dergelijke gegevens met rechtstreeks identificeerbare gegevens. |
| Secundaire doelen voor meerdere sites | Een handeling die gegevens gebruikt voor verwijzing naar andere sites. De combinatie van gegevens van verschillende sites, waaronder een combinatie van gegevens ter plaatse en gegevens buiten de locatie of een combinatie van gegevens van verschillende bronnen buiten de locatie, wordt ook wel gegevens over andere locaties genoemd. Gegevens over andere sites worden doorgaans verzameld en verwerkt om conclusies te trekken over de belangen van gebruikers. |
| Gegevenswetenschap | Een handeling die gegevens gebruikt voor workflows voor gegevenswetenschap. Sommige contracten bevatten expliciete verbodsbepalingen voor het gebruik van gegevens voor gegevenswetenschap. Soms worden deze termen gedefinieerd in termen die het gebruik van gegevens voor kunstmatige intelligentie (AI), machinaal leren (ML) of modellering verbieden. |
| E-maildoelen | Een handeling die gegevens gebruikt in campagnes voor het aanwijzen van e-mail. |
| Exporteren naar derde partij | Een handeling die gegevens exporteert naar processors en entiteiten die geen directe relatie hebben met klanten. Veel gegevensleveranciers hebben bedingen in de contracten die de uitvoer van gegevens van waar het oorspronkelijk werd verzameld verbieden. Sociale netwerkcontracten beperken bijvoorbeeld vaak de overdracht van gegevens die u van hen ontvangt. |
| Onsite reclame | Een handeling die gegevens gebruikt voor onsite advertenties, waaronder de selectie en levering van advertenties op de websites of apps van uw organisatie, of om de levering en doeltreffendheid van dergelijke advertenties te meten. |
| Onsite personalisatie | Een actie die gegevens voor onsite inhoudpersonalisatie gebruikt. De verpersoonlijking onsite is om het even welke gegevens die worden gebruikt om gevolgtrekkingen over gebruikersbelangen te maken, en gebruikt om te selecteren welke inhoud of advertenties op die gevolgtrekkingen worden gediend. |
| Segmentovereenkomst | Een actie die gegevens voor de Gelijke van het Segment van Adobe Experience Platform gebruikt, die voor twee of meer gebruikers van het Platform toestaat om segmentgegevens uit te wisselen. Door beleid in te schakelen dat naar deze handeling verwijst, kunt u beperken welke gegevens worden gebruikt voor Segment Match. Als het kernbeleid &#39;Gegevens delen beperken&#39; bijvoorbeeld is ingeschakeld, worden alle gegevens met een [C11-label](../labels/reference.md#c11) kan niet worden gebruikt voor Segment Match. |
| Eén identiteit aanpassen | Een handeling die vereist dat één identiteit wordt gebruikt voor verpersoonlijkingsdoeleinden in plaats van dat identiteiten uit meerdere bronnen worden gekoppeld. |
