---
keywords: Experience Platform;home;populaire onderwerpen;naamruimte voor identiteit;Naamruimte
solution: Experience Platform
title: Handleiding voor probleemoplossing voor identiteitsservice
topic: troubleshooting
description: Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform Identity Service en een gids voor probleemoplossing voor algemene fouten.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 0%

---


# Handleiding voor het oplossen van problemen met identiteitsservice

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Identity Service] en een gids voor probleemoplossing voor algemene fouten. Raadpleeg de [Adobe Experience Platform API-handleiding voor het oplossen van problemen](../landing/troubleshooting.md) voor vragen en het oplossen van problemen met betrekking tot [!DNL Platform] API&#39;s in het algemeen.

Gegevens die één enkele klant identificeren, worden vaak gefragmenteerd over de verschillende apparaten en systemen die zij gebruiken om met uw merk in contact te komen. [!DNL Identity Service] verzamelt deze gefragmenteerde identiteiten, zodat u een volledig inzicht in het gedrag van de klant krijgt zodat u in real-time een ongekende digitale ervaring kunt opdoen. Zie [Overzicht van identiteitsservice](./home.md) voor meer informatie.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over [!DNL Identity Service].

## Wat zijn identiteitsgegevens?

Identiteitsgegevens zijn alle gegevens die kunnen worden gebruikt om een individuele persoon te identificeren. Afhankelijk van de context van hoe de gegevens binnen uw organisatie worden gebruikt, kunnen de identiteitsgegevens gebruikersnamen, e-mailadressen, en identiteitskaart van de systemen van CRM omvatten. Identiteitsgegevens zijn niet beperkt tot geregistreerde gebruikers van uw website of service, omdat anonieme gebruikers ook kunnen worden geïdentificeerd door hun apparaat of cookie-id.

## Wat is het nut van het etiketteren van gegevensvelden als identiteiten?

Door bepaalde gegevensvelden als identiteiten te labelen in uw record- en tijdreeksgegevens kunt u identiteitsrelaties toewijzen binnen de natuurlijke structuur van uw gegevens en dubbele gegevenskanalen met elkaar in overeenstemming brengen. Zie [Overzicht van de Identiteitsservice](./home.md) voor meer informatie.

## Wat zijn bekende en anonieme identiteiten?

Een bekende identiteit verwijst naar een identiteitswaarde die zelfstandig of met andere informatie kan worden gebruikt om een individuele persoon te identificeren, te contacteren of te bepalen. Voorbeelden van bekende identiteiten zijn bijvoorbeeld e-mailadressen, telefoonnummers en CRM-id&#39;s.

Een anonieme identiteit verwijst naar een identiteitswaarde die niet zelfstandig of met andere informatie kan worden gebruikt om een individuele persoon (zoals een koekjesidentiteitskaart) te identificeren, te contacteren of de plaats te bepalen.

## Wat is een persoonlijke identiteitsgrafiek?

Een persoonlijke identiteitsgrafiek is een persoonlijke kaart van relaties tussen verbonden en verbonden identiteiten, die alleen zichtbaar is voor uw organisatie.

Wanneer meer dan één identiteit inbegrepen in om het even welke gegevens die van een het stromen eindpunt worden opgenomen of naar een dataset worden verzonden die voor [!DNL Identity Service] wordt toegelaten, zijn die identiteiten verbonden in de Privé Grafiek van de Identiteit. [!DNL Identity Service] gebruikt deze grafiek om een bepaalde consument of entiteit aan de genre identiteiten te helpen, waardoor identiteitsstitching en het samenvoegen van profielen mogelijk worden.

## Hoe maak ik veelvoudige identiteitsgebieden binnen een XDM schema?

[XDM-](../xdm/home.md) schema&#39;s (Experience Data Model) ondersteunen meerdere identiteitsvelden. Elk gegevensveld van het type `string` binnen een schema dat de klasse XDM Individual Profile of XDM ExperienceEvent implementeert, kan worden gelabeld als een identiteitsveld. Als deze velden zijn gelabeld, worden alle gegevens in deze velden toegevoegd aan het identiteitsoverzicht van het profiel.

Voor stappen op hoe te om een gebied XDM als identiteitsgebied te etiketteren gebruikend het gebruikersinterface, zie [de sectie van de Identiteit](../xdm/tutorials/create-schema-ui.md) in het leerprogramma van de Redacteur van het Schema. Als u API gebruikt, zie [de sectie van de Beschrijver van de Identiteit](../xdm/tutorials/create-schema-api.md) in de RegisterAPI van het Schema leerprogramma.

## Zijn er contexten waarin sommige gebieden niet als identiteiten zouden moeten worden geëtiketteerd?

Identiteitsvelden moeten worden gereserveerd voor waarden die uniek zijn voor elk individu. Bijvoorbeeld, overweeg een dataset voor een programma van de klantenloyaliteit. Het veld &quot;loyaliteitsniveau&quot; (goud, zilver, brons) zou geen nuttig identiteitsveld zijn, terwijl de loyaliteitsidentiteitskaart-unieke waarde-zou zijn.

Velden zoals ZIP-codes en IP-adressen mogen niet worden gelabeld als identiteiten voor personen, omdat deze waarden op meerdere personen van toepassing kunnen zijn. Deze soorten velden mogen alleen worden geëtiketteerd als identiteiten voor marketingstrategieën op huishoudelijk niveau.

## Waarom zijn mijn identiteitsvelden niet aan elkaar gekoppeld zoals ik verwacht?

Met het [`/cluster/members` eindpunt](./api/list-cluster-identites.md) in de Identiteitsdienst API, kunt u de bijbehorende identiteiten voor één of meerdere identiteitsgebieden bekijken. Als de reactie niet de verbonden identiteiten terugkeert u verwacht, zorg ervoor dat u de aangewezen identiteitsinformatie in uw XDM gegevens verstrekt. Zie de sectie over [het verstrekken van XDM gegevens aan de Dienst van de Identiteit](./home.md) in het overzicht van de Dienst van de Identiteit voor meer informatie.

## Wat is naamruimte voor identiteit?

Een identiteitsnaamruimte geeft context voor hoe identiteitsvelden betrekking hebben op de identiteit van een klant. Identiteitsvelden onder de naamruimte &quot;E-mail&quot; moeten bijvoorbeeld een standaard e-mailindeling hebben (naam<span>@emailprovider.com), terwijl velden die de naamruimte &quot;Telefoon&quot; gebruiken, moeten voldoen aan een standaardtelefoonnummer (zoals 987-555-1234 in Noord-Amerika).

Naamruimten maken onderscheid tussen vergelijkbare identiteitswaarden tussen verschillende CRM-systemen. Neem bijvoorbeeld een profiel dat een numerieke identificatie bevat die is gekoppeld aan het beloningsprogramma van uw bedrijf. Een naamruimte van &quot;Loyalty&quot; zou deze waarde scheiden van een vergelijkbare numerieke id voor uw eCommerce-systeem dat ook in hetzelfde profiel wordt weergegeven.

Zie [Naamruimte overzicht](./home.md) voor meer informatie.

## Hoe associeer ik een identiteit met een identiteitsnamespace?

Identiteitsvelden moeten worden gekoppeld aan een bestaande naamruimte voor identiteiten wanneer deze worden gemaakt. Nieuwe naamruimten moeten [gemaakt zijn met de API](#how-do-i-create-a-custom-namespace-for-my-organization) voordat ze aan identiteitsvelden kunnen worden gekoppeld.

Voor geleidelijke instructies voor het bepalen van namespace wanneer het creëren van een identiteitsbeschrijver gebruikend API, te zien gelieve de sectie op [creërend een beschrijver](../xdm/tutorials/create-schema-ui.md) in de de ontwikkelaarsgids van het Registratie van het Schema. Voor het merken van een schemagebied als identiteit in UI, volg de stappen in [de zelfstudie van de Redacteur van het Schema](../xdm/tutorials/create-schema-api.md).

## Wat zijn de standaardnaamruimten van Experience Platform? {#standard-namespaces}

Standaardnaamruimten zijn naamruimten die beschikbaar zijn voor alle organisaties. Zie [Overzicht van naamruimten voor identiteiten](./namespaces.md) voor een volledige lijst van beschikbare standaardnaamruimten.

## Waar kan ik de lijst van identiteitsnamespaces beschikbaar voor mijn organisatie vinden?

Met de [Identiteitsservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) kunt u alle beschikbare naamruimten voor uw organisatie weergeven door een GET-aanvraag in te dienen bij het `/idnamespace/identities`-eindpunt. Zie de sectie over [het vermelden van beschikbare naamruimten](./api/list-namespaces.md) in het overzicht van de Identiteitsservice API voor meer informatie.

## Hoe maak ik een aangepaste naamruimte voor mijn organisatie?

Met de [Identiteitsservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) kunt u een aangepaste naamruimte voor uw organisatie maken door een POST-aanvraag in te dienen bij het `/idnamespace/identities`-eindpunt. Zie de sectie over [het creëren van een douanenamespace](./api/create-custom-namespace.md) in het overzicht van de Dienst API van de Identiteit voor meer informatie.

## Wat zijn samengestelde identiteiten en XIDs?

In API-aanroepen wordt naar identiteiten verwezen door hun samengestelde identiteit of XID. Een samengestelde identiteit is een representatie van een identiteit die een id-waarde en een naamruimte bevat. Een XID is een single-value herkenningsteken die het zelfde concept zoals een samengestelde identiteit (identiteitskaart en een namespace) vertegenwoordigt, en automatisch toegewezen aan nieuwe identiteiten wanneer voortgeduurd door de Dienst van de Identiteit. Zie [Overzicht van de Identiteitsdienst API](./home.md) voor meer informatie.

## Hoe verwerkt de Identiteitsdienst persoonlijk identificeerbare informatie (PII)?

De Dienst van de identiteit leidt tot een sterke, unidirectionele cryptografische knoeiboel van PII voorafgaand aan het aanhouden van waarden. Identiteitsgegevens in de naamruimten &#39;Telefoon&#39; en &#39;E-mail&#39; worden automatisch gehasht met SHA-256, waarbij de waarden &#39;E-mail&#39; automatisch worden omgezet in kleine letters voordat er hashing optreedt.

## Moet ik alle PII versleutelen voordat ik naar Platform verstuur?

U hoeft de PII-gegevens niet handmatig te coderen voordat u deze in het Platform opneemt. Door het `I1` etiket van het gegevensgebruik op alle toepasselijke gegevensgebieden toe te passen, zet het Platform deze gebieden automatisch in gehakte waarden van identiteitskaart na opname om.

Zie de [zelfstudie over gegevensgebruikslabels voor informatie over het toepassen en beheren van labels voor gegevensgebruik](../data-governance/labels/user-guide.md).

## Zijn er overwegingen bij het hakken van op PII-Gebaseerde identiteiten?

Als u gehakte PII waarden naar de Dienst van de Identiteit verzendt, moet u de zelfde encryptiemethode over uw datasets gebruiken. Dit zorgt ervoor dat de zelfde identiteitswaarde over datasets de zelfde hashed waarden produceert en behoorlijk kan worden aangepast en in de identiteitsgrafiek worden verbonden.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Problemen oplossen

In de volgende sectie vindt u suggesties voor het oplossen van problemen voor specifieke foutcodes en voor onverwacht gedrag dat u kunt tegenkomen tijdens het werken met de API [!DNL Identity Service].

## [!DNL Identity Service] foutberichten

Hieronder volgt een lijst met foutberichten die kunnen optreden wanneer u de API [!DNL Identity Service] gebruikt.

### Vereiste queryparameter ontbreekt

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Deze fout wordt weergegeven wanneer een vereiste queryparameter niet is opgenomen in het aanvraagpad. `detail` van het foutbericht geeft de naam van de ontbrekende parameter. Variaties in dit foutbericht zijn:

- Ontbrekende vereiste queryparameter - nsId
- Vereiste queryparameter ontbreekt - id
- Ontbrekende vereiste queryparameter - xid of (nsid,id)
- Ontbrekende vereiste queryparameter - targetNs
- Ontbrekende vereiste queryparameter - xids of compoundXids

Controleer of u de opgegeven parameter correct in het aanvraagpad opneemt voordat u het opnieuw probeert.

### De tijdstempel moet in de afgelopen 180 dagen staan

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] zuivert gegevens ouder dan 180 dagen. Dit foutbericht wordt weergegeven wanneer u probeert toegang te krijgen tot gegevens die ouder zijn dan deze pagina.

### Er is een grens van 1000 XIDs in één enkele vraag

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Dit foutenbericht toont wanneer u probeert om identiteitsinformatie voor meer dan het maximumaantal [XIDs](#what-are-composite-identities-and-xids) terug te winnen toegelaten in één enkele API vraag. Verlaag het aantal XID&#39;s in uw verzoek tot onder de weergegeven limiet om dit probleem op te lossen.


### Er is een grens voor 1000 compoundXids in één enkele vraag

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Dit foutenbericht toont wanneer u probeert om identiteitsinformatie voor meer dan het maximumaantal [samengestelde identiteiten ](#what-are-composite-identities-and-xids) terug te winnen toegelaten in één enkele API vraag. Verlaag het aantal samengestelde identiteiten in uw verzoek tot onder de weergegeven limiet om dit probleem op te lossen.

### Het opgegeven grafiektype is ongeldig

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Dit foutenbericht toont wanneer een `graph-type` vraagparameter een ongeldige waarde in de verzoekweg wordt gegeven. Zie de sectie over [identiteitsgrafieken](./home.md) in [!DNL Identity Service] overzicht om te leren welke grafiek-types worden gesteund.

### Servicetoken heeft geen geldig bereik

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Dit foutbericht wordt weergegeven wanneer uw IMS-organisatie niet beschikt over de juiste machtigingen voor [!DNL Identity Service]. Neem contact op met de systeembeheerder om dit probleem op te lossen.

### Het de dienstteken van de gateway is niet geldig

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

In het geval van deze fout, is uw toegangstoken ongeldig. Toegangstokens verlopen elke 24 uur en moeten opnieuw worden gegenereerd om te kunnen doorgaan met het gebruik van [!DNL Platform] API&#39;s. Zie [authentificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voor instructies bij het produceren van nieuwe toegangstokens.

### Token voor machtigingsservice is niet geldig

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

In het geval van deze fout, is uw toegangstoken ongeldig. Toegangstokens verlopen elke 24 uur en moeten opnieuw worden gegenereerd om te kunnen doorgaan met het gebruik van [!DNL Platform] API&#39;s. Zie [authentificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voor instructies bij het produceren van nieuwe toegangstokens.

### Gebruikerstoken heeft geen geldige productcontext

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Dit foutenbericht toont wanneer uw toegangstoken niet uit een [!DNL Experience Platform] integratie is geproduceerd. Zie [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voor instructies over het genereren van nieuwe toegangstokens voor een [!DNL Experience Platform]-integratie.

### Interne fout bij ophalen van native XID uit identiteit- en naamruimtecode

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Wanneer [!DNL Identity Service] een identiteit voortduurt, wordt identiteitskaart van de identiteit en bijbehorende namespace identiteitskaart toegewezen een uniek herkenningsteken genoemd XID. Dit bericht wordt weergegeven wanneer een fout optreedt tijdens het zoeken naar de XID voor een bepaalde ID-waarde en -naamruimte.

### De IMS-organisatie is niet ingericht voor [!DNL Identity Service]-gebruik

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Dit foutbericht wordt weergegeven wanneer uw IMS-organisatie niet beschikt over de juiste machtigingen voor [!DNL Identity Service]. Neem contact op met de systeembeheerder om dit probleem op te lossen.

### Interne serverfout

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Deze fout toont wanneer een onverwachte uitzondering in de uitvoering van een [!DNL Platform] de dienstvraag voorkomt. De beste praktijken moeten uw geautomatiseerde vraag programmeren om hun verzoeken een paar keer bij een bepaald interval opnieuw te proberen wanneer het ontvangen van deze fout. Neem contact op met de systeembeheerder als het probleem zich blijft voordoen.

## Code voor de fout met de inname in de batch

[!DNL Identity Service] Neemt identiteitsgegevens uit verslag en tijdreeksgegevens op die aan het  [!DNL Platform] gebruiken van de Ingestie van de Partij worden geupload. Aangezien batch-opname een asynchroon proces is, moet u de details van een batch bekijken om fouten weer te geven. Fouten zullen zich ophopen aangezien de partij vordert tot de partij volledig is.

Hieronder volgt een lijst met foutberichten die betrekking hebben op [!DNL Identity Service] die u kunt tegenkomen bij het gebruik van de [API voor gegevensinname](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

### Onbekend XDM-schema

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] gebruikt alleen identiteiten voor record- of tijdreeksgegevens die respectievelijk overeenkomen met de  [!DNL Profile] of  [!DNL ExperienceEvent] klassen. Deze fout wordt veroorzaakt wanneer wordt geprobeerd gegevens in te voeren voor [!DNL Identity Service] die zich niet aan een van beide klassen houdt.

### Er waren 0 geldige identiteiten in de eerste 100 rijen van de verwerkte partij

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Deze fout wordt weergegeven wanneer de eerste 100 rijen van een batch geen id&#39;s bevatten. Deze fout geeft echter niet overtuigend aan dat er geen identiteiten zijn gevonden in volgende records.

### Overgeslagen records omdat ze slechts 1 identiteit per XDM-record hadden

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] Hiermee worden alleen id&#39;s gekoppeld wanneer één record twee of meer identiteitswaarden bevat. Dit foutbericht treedt één keer op voor elke opgenomen batch en geeft het aantal records weer waarin slechts één identiteit kan worden gevonden en waarbij de identiteitsgrafiek niet is gewijzigd.

### Naamruimtecode is niet geregistreerd voor deze IMS-organisatie

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Deze fout wordt weergegeven wanneer een opgenomen record een identiteit voorstelt waarvan de bijbehorende naamruimte niet bestaat of niet toegankelijk is voor uw IMS-organisatie.

### Het overslaan van batch-opname als IMS Org is niet voorzien voor Private Identity Graph

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Bij het opnemen van batchgegevens wordt dit foutbericht weergegeven wanneer uw IMS-organisatie niet beschikt over de juiste machtigingen voor [!DNL Identity Service]. Neem contact op met de systeembeheerder om dit probleem op te lossen.

### Interne fout

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Deze fout wordt weergegeven wanneer tijdens een batchopname een onverwachte uitzondering optreedt. De beste praktijken moeten uw geautomatiseerde vraag programmeren om hun verzoeken een paar keer bij een bepaald interval opnieuw te proberen wanneer het ontvangen van deze fout. Neem contact op met de systeembeheerder als het probleem zich blijft voordoen.
