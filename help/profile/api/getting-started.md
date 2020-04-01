---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime

In real-time profiel voor klanten kunt u een holistische weergave van elk van uw individuele klanten bekijken in het Adobe Experience Platform. Het profiel staat u toe om verschillende klantengegevens van veelvoudige kanalen, zoals online, off-line, CRM, en derdegegevens, in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

## Getting started {#getting-started}

Met de Real-time API voor klantprofiel kunt u elementaire CRUD-bewerkingen uitvoeren op profielbronnen, zoals het configureren van berekende kenmerken, het openen van entiteiten, het exporteren van profielgegevens en het verwijderen van overbodige gegevenssets of batches.

Voor het gebruik van deze handleiding voor ontwikkelaars is een goed begrip vereist van de verschillende services van het Adobe Experience Platform die betrokken zijn bij het werken met profielgegevens. Lees de documentatie voor de volgende services voordat u begint te werken met de Real-time Customer Profile API:

* [Klantprofiel](../home.md)in realtime: Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Verbeter een beter beeld van uw klant en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [Adobe Experience Platform Segmentation Service](../../segmentation/home.md): Staat u toe om publiekssegmenten van de gegevens van het Profiel van de Klant in real time te bouwen.
* [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor Platform gegevens van de klantenervaring organiseert.
* [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de eindpunten van profiel API te maken.

### API-voorbeeldaanroepen lezen

De documentatie van de API van het Profiel van de Klant in real time verstrekt voorbeeld API vraag om aan te tonen hoe te behoorlijk verzoeken formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Vereiste koppen

De API documentatie vereist ook u om de [authentificatiezelfstudie](../../tutorials/authentication.md) te hebben voltooid om vraag aan de eindpunten van het Platform met succes te maken. Het voltooien van de authentificatiezelfstudie verstrekt de waarden voor elk van de vereiste kopballen in de vraag van API van het Platform van de Ervaring, zoals hieronder getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken aan platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken met een lading in het verzoeklichaam (zoals POST, GEPUT, en de vraag van de PATCH) moeten een `Content-Type` kopbal omvatten. De toegelaten waarden specifiek voor elke vraag worden verstrekt in de vraagparameters.

## (Alpha) Berekende kenmerken

>[!IMPORTANT]
>De functie voor berekende kenmerken staat in alfa en is niet beschikbaar voor alle gebruikers. Documentatie en functionaliteit kunnen worden gewijzigd.

Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op het profielniveau, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen.

Elk berekend kenmerk bevat een expressie, of &#39;regel&#39;, die binnenkomende gegevens evalueert en de resulterende waarde opslaat in een profielkenmerk of in een gebeurtenis. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren.

U kunt berekende kenmerken maken, weergeven, bewerken en verwijderen met de `config/computedAttributes` eindpunten. Meer informatie over het gebruik van deze eindpunten vindt u in de subhandleiding voor [berekende kenmerken](computed-attributes.md).

## Edge-prognoses

Met het Adobe Experience Platform kunnen de ervaringen van klanten in real time worden aangepast door gegevens gemakkelijk toegankelijk te maken op strategisch geplaatste servers, de zogenaamde &quot;randen&quot;. De Real-time API van het Profiel van de Klant verstrekt eindpunten voor het werken met randen door componenten genoemd &quot;projecties.&quot; Dit omvat projectieconfiguraties om te bepalen welke gegevens aan elke rand moeten worden geprojecteerd, evenals projectiebestemmingen om te bepalen waar te om een projectie te leiden.

Voor gedetailleerde informatie over het werken met randprojecties raadpleegt u de subgids voor [randprojecties](edge-projections.md).

## Entiteiten

Via het Adobe Experience Platform hebt u toegang tot gegevens van het Real-time klantprofiel met RESTful API&#39;s of de gebruikersinterface. Als u wilt leren hoe u met de API toegang krijgt tot entiteiten, beter bekend als &#39;profielen&#39;, volgt u de stappen in de subhandleiding voor [entiteiten](entities.md).

## Beleid samenvoegen

Wanneer het brengen van gegevens uit veelvoudige bronnen samen in het Platform van de Ervaring, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om individuele klantenprofielen tot stand te brengen.

Met behulp van de Real-Time Customer Profile API kunt u een nieuw samenvoegbeleid maken, bestaand beleid beheren en een standaardsamenvoegbeleid voor uw organisatie instellen. Meer informatie over het werken met samenvoegbeleid die API gebruiken, gelieve te bezoeken de subgids [van het](merge-policies.md)fusiebeleid.

Voor een gids aan het werken met samenvoegbeleid die de UI van het Platform gebruiken, te zien gelieve de de gebruikersgids [van het Beleid van de](../ui/merge-policies.md)Samenvoegen.

## Profielzoekopdracht

Het onderzoek van het profiel wordt gebruikt om configureerbare gebieden te zoeken en te indexeren die over diverse gegevensbronnen worden bevat en hen in bijna real time terug te keren. Zie de subhandleiding voor [zoekopdrachten voor informatie over het werken met het zoeken naar profielen](profile-search.md)

## Systeemtaken profiel

Gegevens die in Platform worden opgenomen, worden opgeslagen in het Data Lake en in de gegevensopslag van het Profiel van de Klant in real time. Soms kan het nodig zijn om een gegevensset of batch uit de profielopslag te verwijderen om gegevens te verwijderen die u niet meer nodig hebt of die in een fout zijn toegevoegd. Dit vereist het gebruiken van API om een Baan van het Systeem van het Profiel tot stand te brengen, die als &quot;schrappingsverzoek&quot;wordt bekend, die ook kan worden gewijzigd, worden gecontroleerd, of indien nodig worden geschrapt.

Als u wilt leren werken met verwijderingsaanvragen met de `/system/jobs` eindpunten in de Real-time Customer Profile API, volgt u de stappen die worden beschreven in de subhandleiding [voor](profile-system-jobs.md)profielsysteemtaken.

## Volgende stappen

Om beginnen het maken van vraag gebruikend Real-time het Profiel van de Klant API, selecteer één van subgidsen om te leren hoe te om specifieke op profiel betrekking hebbende eindpunten te gebruiken. Raadpleeg voor meer informatie over het werken met profielgegevens via de interface van het platform de gebruikershandleiding [van het profiel van de](../ui/user-guide.md)realtime klant.