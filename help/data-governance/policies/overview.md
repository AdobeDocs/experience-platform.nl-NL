---
keywords: Experience Platform;home;populaire onderwerpen;module;DULE
solution: Experience Platform
title: Overzicht van beleidsregels voor gegevensgebruik
description: Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens in Adobe Experience Platform of waarvan u een beperking hebt ingesteld.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---

# Overzicht van beleidsregels voor gegevensgebruik {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Gegevensgebruik beperken"
>abstract="Het beleidstype voor gegevensgebruik evalueert specifieke marketingacties die worden toegepast op labels voor gegevensbeheer om het gegevensgebruik voor marketingactiviteiten te beperken."

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen [!DNL Experience Platform] of dat u hierop beperkingen mag toepassen.

Er zijn twee soorten beleid beschikbaar:

* **[!UICONTROL Data governance policy]**: de activering van gegevens beperken op basis van de marketingactie die wordt uitgevoerd en de labels voor gegevensgebruik die door de gegevens in kwestie worden meegevoerd.
* **[!UICONTROL Consent policy]**: Filter de profielen die aan [&#x200B; bestemmingen &#x200B;](../../destinations/home.md) kunnen worden geactiveerd die op de toestemming of de voorkeur van uw klanten worden gebaseerd

>[!NOTE]
>
>Het beleid van het gegevensgebruik moet niet met [&#x200B; toegangsbeheerbeleid &#x200B;](../../access-control/abac/end-to-end-guide.md#policy) worden verward, dat bepaalt of bepaalde gebruikers van Experience Platform in uw organisatie tot bepaalde gegevensgebieden kunnen toegang hebben, en door het [!UICONTROL Permissions] lusje worden gevormd.

Dit document biedt een overzicht op hoog niveau van het beleid voor gegevensgebruik en bevat koppelingen naar verdere documentatie voor het werken met het beleid in de gebruikersinterface of de API.

## Marketingacties {#marketing-actions}

Marketing-acties (ook wel marketinggebruiksgevallen genoemd) in het kader van het gegevensbeheerkader zijn acties die een [!DNL Experience Platform] gegevensconsument kan ondernemen en waarvoor uw organisatie het gegevensgebruik wil beperken. Daarom wordt een beleid voor gegevensgebruik als volgt gedefinieerd:

1. Een specifieke marketingactie
2. De voorwaarden waaronder die handeling niet kan worden uitgevoerd

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid bestaat dat zegt dat specifieke types van gegevens (zoals Persoonlijk Identificeerbare Informatie (PII)) niet kunnen worden uitgevoerd, en u probeert om een dataset uit te voeren die een &quot;I&quot;etiket (Gegevens van de Identiteit) bevat, zult u een antwoord van [!DNL Policy Service] ontvangen die u vertelt dat een beleid van het gegevensgebruik is geschonden.

>[!NOTE]
>
>Handelingen voor het in de handel brengen zelf beperken het gegevensgebruik niet. Ze moeten worden opgenomen in beleid voor ingeschakeld gegevensgebruik om ervoor te zorgen dat deze acties worden geëvalueerd op beleidsovertredingen.

Wanneer het gegevensgebruik in de dienst van uw organisatie gebeurt, zouden de relevante marketing acties moeten worden vermeld zodat om het even welke beleidsschendingen kunnen worden geïdentificeerd. U kunt de [&#x200B; Dienst API van het Beleid &#x200B;](https://www.adobe.io/experience-platform-apis/references/policy-service/) dan gebruiken om beleidsschendingen in uw integratie te controleren.

>[!NOTE]
>
>U kunt de gevallen van het gebruiksgebruik van de opstelling op bestemmingen om beleidshandhaving te automatiseren. Zie de [&#x200B; documentatie van bestemmingen &#x200B;](../../destinations/home.md) voor meer informatie over de configuratieopties voor uw bijzondere bestemming.

Zie het bijlage aan dit document voor een lijst van [&#x200B; beschikbare Adobe-bepaalde marketing acties &#x200B;](#core-actions). U kunt ook uw eigen aangepaste marketingacties definiëren met de [!DNL Policy Service] API of de [!DNL Experience Platform] -gebruikersinterface. In de volgende sectie vindt u meer informatie over het werken met marketingacties en -beleid.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share audiences with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager audiences are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Experience Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=nl-NL).
-->

## Beleid voor gegevensgebruik beheren {#manage}

Nadat labels voor gegevensgebruik zijn toegepast, kunnen gegevensbeheerders de [!DNL Policy Service] API of de [!DNL Experience Platform] UI gebruiken voor het beheren en evalueren van beleid dat betrekking heeft op marketingacties die worden uitgevoerd op gegevens die labels voor gegevensgebruik bevatten. U kunt beleid tot stand brengen en bijwerken, de status van een beleid bepalen, en met marketing acties werken om te evalueren of een specifieke actie een beleid van het gegevensgebruik schendt.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief basisbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten door API of UI.

Voor geleidelijke instructies bij het werken met marketing acties en het beleid van het gegevensgebruik in API, zie het leerprogramma op [&#x200B; het creëren van en het evalueren van het beleid van het gegevensgebruik &#x200B;](create.md). Voor meer informatie zien de belangrijkste verrichtingen die door [!DNL Policy Service] API worden verstrekt, de [&#x200B; gids van de ontwikkelaar van de Dienst van het Beleid &#x200B;](../api/getting-started.md).

Voor informatie over hoe te met marketing acties en beleid in [!DNL Experience Platform] UI te werken, zie de [&#x200B; gebruikersgids van het gegevensgebruiksbeleid &#x200B;](./user-guide.md).

## Volgende stappen

Dit document bevatte een inleiding op het beleid inzake gegevensgebruik binnen het kader voor gegevensbeheer. U kunt nu de procesdocumentatie blijven lezen met betrekking tot deze gids voor meer informatie over hoe te met beleid in API en UI te werken.

## Bijlage

In de volgende sectie vindt u aanvullende informatie over het beleid voor gegevensgebruik.

### Door Adobe gedefinieerde marketingacties {#core-actions}

In de onderstaande tabel worden de belangrijkste marketingacties beschreven die Adobe van de verpakking heeft voorzien.

>[!NOTE]
>
>De belangrijkste marketingacties moeten worden beschouwd als een uitgangspunt om u te helpen bepalen welk gebruiksbeleid u moet maken en controleren op overtredingen. De definities en hoe deze worden geïnterpreteerd, zijn afhankelijk van de behoeften en het beleid van uw organisatie.

| Handeling | Beschrijving |
| --- | --- |
| Analytics | Een handeling die gegevens gebruikt voor analytische doeleinden, zoals het meten, analyseren en rapporteren van het gebruik van de sites of apps van uw organisatie door klanten. |
| Combineren met rechtstreeks identificeerbare gegevens | Een handeling waarbij alle PII&#39;s (Personal Identified Information) worden gecombineerd met anonieme gegevens. Contracten voor gegevens die afkomstig zijn van advertentienetwerken, servers en derde gegevensleveranciers bevatten vaak specifieke contractuele verbodsbepalingen inzake het gebruik van dergelijke gegevens met rechtstreeks identificeerbare gegevens. |
| Secundaire doelen voor meerdere sites | Een handeling die gegevens gebruikt voor verwijzing naar andere sites. De combinatie van gegevens van verschillende sites, waaronder een combinatie van gegevens ter plaatse en gegevens buiten de locatie of een combinatie van gegevens van verschillende bronnen buiten de locatie, wordt ook wel gegevens over andere locaties genoemd. Gegevens over andere sites worden doorgaans verzameld en verwerkt om conclusies te trekken over de belangen van gebruikers. |
| Gegevenswetenschap | Een handeling die gegevens gebruikt voor workflows voor gegevenswetenschap. Sommige contracten bevatten expliciete verbodsbepalingen voor het gebruik van gegevens voor gegevenswetenschap. Soms worden deze termen gedefinieerd in termen die het gebruik van gegevens voor kunstmatige intelligentie (AI), machinaal leren (ML) of modellering verbieden. |
| Gegevens exporteren | Een actie die gegevens naar om het even welke plaats of bestemming buiten de producten en de diensten van Adobe uitvoert. Bijvoorbeeld het downloaden van gegevens naar uw lokale computer, het kopiëren van gegevens van het scherm, het plannen van levering van gegevens aan een plaats buiten Adobe, Customer Journey Analytics Geplande Projecten, de Rapporten van de Download, Rapporterende API, etc. |
| E-maildoelen | Een handeling waarbij gegevens worden gebruikt in campagnes voor het aanwijzen van e-mail. |
| Exporteren naar derde partij | Een handeling die gegevens exporteert naar processors en entiteiten die geen directe relatie hebben met klanten. Veel gegevensleveranciers hebben bedingen in de contracten die de uitvoer van gegevens van waar het oorspronkelijk werd verzameld verbieden. Sociale netwerkcontracten beperken bijvoorbeeld vaak de overdracht van gegevens die u van hen ontvangt. |
| Onsite Advertising | Een handeling die gegevens gebruikt voor onsite advertenties, waaronder de selectie en levering van advertenties op de websites of apps van uw organisatie, of om de levering en doeltreffendheid van dergelijke advertenties te meten. |
| Onsite Personalization | Een actie die gegevens voor onsite inhoudpersonalisatie gebruikt. De verpersoonlijking op locatie is om het even welke gegevens die worden gebruikt om gevolgtrekkingen over gebruikersbelangen te maken, en gebruikt om te selecteren welke inhoud of advertenties op die gevolgtrekkingen worden gediend. |
| Segmentovereenkomst | Een actie die gegevens voor de Gelijke van het Segment van Adobe Experience Platform gebruikt, die voor twee of meer gebruikers van Experience Platform toestaat om publieksgegevens uit te wisselen. Door beleid in te schakelen dat naar deze handeling verwijst, kunt u beperken welke gegevens worden gebruikt voor Segment Match. Bijvoorbeeld, als het kernbeleid &quot;Gegevens beperken die&quot;wordt toegelaten, om het even welke gegevens met het etiket van a [&#x200B; C11 &#x200B;](../labels/reference.md#c11) kunnen niet voor de Overeenkomst van het Segment worden gebruikt. |
| Single Identity Personalization | Een handeling die vereist dat één identiteit wordt gebruikt voor verpersoonlijkingsdoeleinden in plaats van dat identiteiten uit meerdere bronnen worden gekoppeld. |
