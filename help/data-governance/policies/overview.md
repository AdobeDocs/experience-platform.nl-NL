---
keywords: Experience Platform;thuis;populaire onderwerpen;module;DULE
solution: Experience Platform
title: Overzicht van beleidsregels voor gegevensgebruik
topic: policies
description: Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen het Experience Platform, of dat u er een beperking voor hebt.
translation-type: tm+mt
source-git-commit: 2dbd92efbd992b70f4f750b09e9d2e0626e71315
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

---


# Overzicht van beleidsregels voor gegevensgebruik

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen [!DNL Experience Platform].

Dit document biedt een overzicht op hoog niveau van het beleid voor gegevensgebruik en bevat koppelingen naar verdere documentatie voor het werken met het beleid in de gebruikersinterface of de API.

## Handelingen voor marketing {#marketing-actions}

Marketing-acties (ook wel marketinggebruiksgevallen genoemd) in het kader van het gegevensbeheerkader zijn acties die een [!DNL Experience Platform] gegevensconsument kan uitvoeren en waarvoor uw organisatie het gegevensgebruik wil beperken. Daarom wordt een beleid voor gegevensgebruik als volgt gedefinieerd:

1. Een specifieke marketingactie
2. De labels voor gegevensgebruik waarvoor de handeling niet kan worden uitgevoerd

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid is dat zegt dat de specifieke types van gegevens (zoals Persoonlijk identificeerbare Informatie (PII)) niet kunnen worden uitgevoerd, en u probeert om een dataset uit te voeren die een &quot;I&quot;etiket (de Gegevens van de Identiteit) bevat, zult u een reactie van [!DNL Policy Service] ontvangen die u vertelt dat een beleid van het gegevensgebruik is geschonden.

>[!NOTE]
>
>Handelingen voor het in de handel brengen zelf beperken het gegevensgebruik niet. Ze moeten worden opgenomen in beleid voor ingeschakeld gegevensgebruik om ervoor te zorgen dat deze acties worden geëvalueerd op beleidsovertredingen.

Wanneer het gegevensgebruik in de dienst van uw organisatie gebeurt, zouden de relevante marketing acties moeten worden vermeld zodat om het even welke beleidsschendingen kunnen worden geïdentificeerd. U kunt [Beleidsdienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) dan gebruiken om op beleidsschendingen in uw integratie te controleren.

>[!NOTE]
>
>Als u [!DNL Real-time Customer Data Platform] gebruikt, kunt u opstellings marketing gebruiksgevallen op bestemmingen om beleidshandhaving te automatiseren. Zie het document over [Gegevensbeheer in real time CDP](../../rtcdp/privacy/data-governance-overview.md) voor meer informatie.

Zie de bijlage bij dit document voor een lijst van [beschikbare Adobe-bepaalde marketing acties](#core-actions). U kunt ook uw eigen aangepaste marketingacties definiëren met de [!DNL Policy Service]-API of de [!DNL Experience Platform ]gebruikersinterface. In de volgende sectie vindt u meer informatie over het werken met marketingacties en -beleid.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Beleid voor gegevensgebruik beheren {#manage}

Zodra de etiketten van het gegevensgebruik zijn toegepast, kunnen de gegevensstewards API [!DNL Policy Service] of [!DNL Experience Platform] UI gebruiken om beleid met betrekking tot marketingacties te beheren en te evalueren die op gegevens worden genomen die de etiketten van het gegevensgebruik bevatten. U kunt beleid tot stand brengen en bijwerken, de status van een beleid bepalen, en met marketing acties werken om te evalueren of een specifieke actie een beleid van het gegevensgebruik schendt.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten door API of UI.

Voor geleidelijke instructies over het werken met marketing acties en het beleid van het gegevensgebruik in API, zie de zelfstudie over [het creëren van en het evalueren van het beleid van het gegevensgebruik](create.md). Voor meer informatie de belangrijkste verrichtingen die door [!DNL Policy Service] API worden verstrekt, zie [de gids van de ontwikkelaar van de Dienst van het Beleid](../api/getting-started.md).

Voor informatie over hoe te met marketing acties en beleid in [!DNL Platform] UI te werken, zie [de gebruikersgids ](./user-guide.md) van het beleid van het gegevensgebruik.

## Volgende stappen

Dit document bevat een inleiding op het beleid voor gegevensgebruik binnen het [!DNL Data Governance]-framework. U kunt nu de procesdocumentatie blijven lezen met betrekking tot deze gids voor meer informatie over hoe te met beleid in API en UI te werken.

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
| Combineren met PII | Een handeling waarbij alle PII&#39;s (Personal Identified Information) worden gecombineerd met anonieme gegevens. Contracten voor gegevens die afkomstig zijn van advertentienetwerken, servers en derde gegevensleveranciers bevatten vaak specifieke contractuele verbodsbepalingen inzake het gebruik van dergelijke gegevens met rechtstreeks identificeerbare gegevens. |
| Secundaire doelen voor meerdere sites | Een handeling die gegevens gebruikt voor verwijzing naar andere sites. De combinatie van gegevens van verschillende sites, waaronder een combinatie van gegevens ter plaatse en gegevens buiten de locatie of een combinatie van gegevens van verschillende bronnen buiten de locatie, wordt ook wel gegevens over andere locaties genoemd. Gegevens over andere sites worden doorgaans verzameld en verwerkt om conclusies te trekken over de belangen van gebruikers. |
| Gegevenswetenschap | Een handeling die gegevens gebruikt voor workflows voor gegevenswetenschap. Sommige contracten bevatten expliciete verbodsbepalingen voor het gebruik van gegevens voor gegevenswetenschap. Soms worden deze termen gedefinieerd in termen die het gebruik van gegevens voor kunstmatige intelligentie (AI), machinaal leren (ML) of modellering verbieden. |
| E-maildoelen | Een handeling die gegevens gebruikt in campagnes voor het aanwijzen van e-mail. |
| Exporteren naar derde partij | Een handeling die gegevens exporteert naar processors en entiteiten die geen directe relatie hebben met klanten. Veel gegevensleveranciers hebben bedingen in de contracten die de uitvoer van gegevens van waar het oorspronkelijk werd verzameld verbieden. Sociale netwerkcontracten beperken bijvoorbeeld vaak de overdracht van gegevens die u van hen ontvangt. |
| Onsite reclame | Een handeling die gegevens gebruikt voor onsite advertenties, waaronder de selectie en levering van advertenties op de websites of apps van uw organisatie, of om de levering en doeltreffendheid van dergelijke advertenties te meten. |
| Onsite personalisatie | Een actie die gegevens voor onsite inhoudpersonalisatie gebruikt. De verpersoonlijking op locatie is om het even welke gegevens die worden gebruikt om gevolgtrekkingen over gebruikersbelangen te maken, en gebruikt om te selecteren welke inhoud of advertenties op die gevolgtrekkingen worden gediend. |
| Eén identiteit aanpassen | Een handeling die vereist dat één identiteit wordt gebruikt voor verpersoonlijkingsdoeleinden in plaats van dat identiteiten uit meerdere bronnen worden gekoppeld. |
