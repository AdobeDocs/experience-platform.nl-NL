---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van beleidsregels voor gegevensgebruik
topic: policies
translation-type: tm+mt
source-git-commit: 92092620a7ba9129eef4bde852b1e0afc6612d74
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---


# Overzicht van beleidsregels voor gegevensgebruik

Om gegevensgebruikslabels effectief te steunen gegevensnaleving, moet het beleid van het gegevensgebruik worden uitgevoerd. Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen het Experience Platform, of dat u er een beperking voor hebt.

Dit document biedt een overzicht op hoog niveau van het beleid voor gegevensgebruik en bevat koppelingen naar verdere documentatie voor het werken met het beleid in de gebruikersinterface of de API.

## Marketingacties {#marketing-actions}

**Marketing-acties**(ook wel **marketinggebruiksgevallen** genoemd) in het kader van het gegevensbeheerkader zijn acties die een gebruiker van gegevens in een Experience Platform kan ondernemen en waarvoor uw organisatie het gegevensgebruik wil beperken. Daarom wordt een beleid voor gegevensgebruik als volgt gedefinieerd:

1. Een specifieke marketingactie
2. De labels voor gegevensgebruik waarvoor de handeling niet kan worden uitgevoerd

Een voorbeeld van een marketing actie zou de wens kunnen zijn om een dataset naar een derdedienst uit te voeren. Als er een beleid is dat zegt dat de specifieke types van gegevens (zoals Persoonlijk Identificeerbare Informatie (PII)) niet kunnen worden uitgevoerd, en u probeert om een dataset uit te voeren die een &quot;I&quot;etiket (de Gegevens van de Identiteit) bevat, zult u een reactie van de Dienst van het Beleid ontvangen die u vertelt dat een beleid van het gegevensgebruik is geschonden.

>[!NOTE] Handelingen voor het in de handel brengen zelf beperken het gegevensgebruik niet. Ze moeten worden opgenomen in beleid voor ingeschakeld gegevensgebruik om ervoor te zorgen dat deze acties worden geëvalueerd op beleidsovertredingen.

Wanneer het gegevensgebruik in de dienst van uw organisatie gebeurt, zouden de relevante marketing acties moeten worden vermeld zodat om het even welke beleidsschendingen kunnen worden geïdentificeerd. Vervolgens kunt u de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE Policy Service gebruiken om te controleren op beleidsovertredingen in uw integratie.

>[!NOTE] Als u het Platform van Gegevens van de Klant in real time gebruikt, kunt u de gevallen van het plaatsingsgebruik op bestemmingen plaatsen om beleidshandhaving te automatiseren. Zie het document over [Gegevensbeheer in real time CDP](../../rtcdp/privacy/data-governance-overview.md) voor meer informatie.

Zie de bijlage bij dit document voor een lijst met [beschikbare door Adobe gedefinieerde marketingacties](#core-actions). U kunt ook uw eigen aangepaste marketingacties definiëren met de DULE Policy Service API of de gebruikersinterface van het Experience Platform. In de volgende sectie vindt u meer informatie over het werken met marketingacties en -beleid.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Beleid voor gegevensgebruik beheren {#manage}

Zodra de etiketten van het gegevensgebruik zijn toegepast, kunnen de gegevensstewards de Dienst API van het Beleid DULE of UI van het Experience Platform gebruiken om beleid met betrekking tot marketingacties te beheren en te evalueren die op gegevens worden genomen die de etiketten van het gegevensgebruik bevatten. U kunt beleid tot stand brengen en bijwerken, de status van een beleid bepalen, en met marketing acties werken om te evalueren of een specifieke actie een beleid van het gegevensgebruik schendt.

>[!IMPORTANT] Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten door API of UI.

Zie de zelfstudie over het [maken en evalueren van beleid](create.md)voor gegevensgebruik voor stapsgewijze instructies over het werken met marketingacties en het beleid voor gegevensgebruik in de API. Voor meer informatie zien de belangrijkste verrichtingen die door de Dienst API van het Beleid worden verstrekt, de de ontwikkelaarsgids [van de Dienst van het](../api/getting-started.md)Beleid.

Voor informatie over hoe te met marketing acties en beleid in het Platform UI te werken, zie de de gebruikersgids [van het](./user-guide.md)gegevensgebruiksbeleid.

## Volgende stappen

Dit document gaf een inleiding op het beleid voor gegevensgebruik binnen het DULE-kader. U kunt nu de procesdocumentatie blijven lezen met betrekking tot deze gids voor meer informatie over hoe te met beleid in API en UI te werken.

## Aanhangsel

De volgende sectie verstrekt extra informatie over het beleid van het gegevensgebruik.

### Door Adobe gedefinieerde marketingacties {#core-actions}

In de onderstaande tabel worden de belangrijkste marketingacties beschreven die Adobe u buiten de verpakking biedt.

>[!NOTE] De belangrijkste marketingacties moeten worden beschouwd als een uitgangspunt om u te helpen bepalen welk gebruiksbeleid u moet maken en controleren op overtredingen. De definities en hoe deze worden geïnterpreteerd, zijn afhankelijk van de behoeften en het beleid van uw organisatie.

| Handeling | Beschrijving |
| --- | --- |
| Analytics | Een handeling die gegevens gebruikt voor analytische doeleinden, zoals het meten, analyseren en rapporteren van het gebruik van de sites of apps van uw organisatie door klanten. |
| Combineren met PII | Een handeling waarbij alle PII&#39;s (Personal Identified Information) worden gecombineerd met anonieme gegevens. Contracten voor gegevens die afkomstig zijn van advertentienetwerken, servers en derde gegevensleveranciers bevatten vaak specifieke contractuele verbodsbepalingen inzake het gebruik van dergelijke gegevens met rechtstreeks identificeerbare gegevens. |
| Secundaire doelen voor meerdere sites | Een handeling die gegevens gebruikt voor verwijzing naar andere sites. De combinatie van gegevens van verschillende sites, waaronder een combinatie van gegevens ter plaatse en gegevens buiten de locatie of een combinatie van gegevens van verschillende bronnen buiten de locatie, wordt ook wel gegevens over andere locaties genoemd. Gegevens over andere sites worden doorgaans verzameld en verwerkt om conclusies te trekken over de belangen van gebruikers. |
| Gegevenswetenschap | Een handeling die gegevens gebruikt voor workflows voor gegevenswetenschap. Sommige contracten bevatten expliciete verbodsbepalingen voor het gebruik van gegevens voor gegevenswetenschap. Soms worden deze termen gedefinieerd in termen die het gebruik van gegevens voor kunstmatige intelligentie (AI), machinaal leren (ML) of modellering verbieden. |
| E-maildoelen | Een handeling die gegevens gebruikt in campagnes voor het aanwijzen van e-mail. |
| Exporteren naar derde partij | Een handeling die gegevens exporteert naar processors en entiteiten die geen directe relatie hebben met klanten. Veel gegevensleveranciers hebben bedingen in de contracten die de uitvoer van gegevens van waar het oorspronkelijk werd verzameld verbieden. Sociale netwerkcontracten beperken bijvoorbeeld vaak de overdracht van gegevens die u van hen ontvangt. |
| Onsite reclame | Een handeling die gegevens gebruikt voor onsite advertenties, waaronder de selectie en levering van advertenties op de websites of apps van uw organisatie, of om de levering en doeltreffendheid van dergelijke advertenties te meten. |
| Onsite personalisatie | Een actie die gegevens voor onsite inhoudpersonalisatie gebruikt. De verpersoonlijking onsite is om het even welke gegevens die worden gebruikt om gevolgtrekkingen over gebruikersbelangen te maken, en gebruikt om te selecteren welke inhoud of advertenties op die gevolgtrekkingen worden gediend. |
| Eén identiteit aanpassen | Een handeling die vereist dat één identiteit wordt gebruikt voor verpersoonlijkingsdoeleinden in plaats van dat identiteiten uit meerdere bronnen worden gekoppeld. |