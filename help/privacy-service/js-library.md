---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van de Adobe Privacy JavaScript-bibliotheek
topic: overview
translation-type: tm+mt
source-git-commit: 3b916ac5529db6ca383bf8bad56961bb1b8a0b0c

---


# Overzicht van de Adobe Privacy JavaScript-bibliotheek

Als gegevensverwerker verwerkt Adobe persoonlijke gegevens volgens de toestemming en instructies van uw bedrijf. Als de gegevenscontroller bepaalt u de persoonlijke gegevens die Adobe voor u verwerkt en opslaat. Afhankelijk van de informatie die u via de oplossingen van de Wolk van de Ervaring van Adobe wilt verzenden, kan Adobe persoonlijke informatie opslaan die van toepassing is op privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) en de Wet van de Consumeprivacydienst van Californië (CCPA). Raadpleeg het document over [privacy in Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) voor meer informatie over hoe Experience Cloud-oplossingen persoonlijke gegevens verzamelen.

Met de **Adobe Privacy JavaScript-bibliotheek** kunnen gegevenscontrollers het ophalen van alle gegevensonderwerpidentiteiten die zijn gegenereerd door Experience Cloud-oplossingen voor een bepaald domein automatiseren. Met behulp van de API die door de [Adobe Experience Platform Privacy Service](home.md)wordt aangeboden, kunnen deze identiteiten vervolgens worden gebruikt om aanvragen voor toegang tot en verwijdering van persoonlijke gegevens van die betrokkenen te maken.

>[!NOTE] De Privacy JS Library hoeft gewoonlijk alleen op privacygerelateerde pagina&#39;s te worden geïnstalleerd en hoeft niet op alle pagina&#39;s van een website of domein te worden geïnstalleerd.

## Functies

De Privacy JS Library biedt verschillende functies voor het beheer van identiteiten in de Privacy Service. Deze functies kunnen alleen worden gebruikt om de identiteiten te beheren die in de browser voor een specifieke bezoeker zijn opgeslagen. Ze kunnen niet worden gebruikt om informatie rechtstreeks naar de Experience Cloud Central Service te verzenden.

In de volgende tabel worden de verschillende functies beschreven die door de bibliotheek worden geboden:

| -functie | Beschrijving |
| --- | --- |
| `retrieveIdentities` | Retourneert een array van overeenkomende identiteiten (`validIds`) die zijn opgehaald van de Privacy Service en een array van identiteiten die niet zijn gevonden (`failedIds`). |
| `removeIdentities` | Hiermee verwijdert u elke overeenkomende (geldige) identiteit uit de browser. Retourneert een array van overeenkomende identiteiten (`validIds`), met elke identiteit die een `isDeleteClientSide` booleaanse id bevat die aangeeft of deze id is verwijderd. |
| `retrieveThenRemoveIdentities` | Haalt een array van overeenkomende identiteiten (`validIds`) op en verwijdert deze identiteiten vervolgens uit de browser. Hoewel deze functie vergelijkbaar is met `removeIdentities`, wordt deze het best gebruikt wanneer voor de Adobe-oplossing die u gebruikt een toegangsverzoek is vereist voordat verwijdering mogelijk is (bijvoorbeeld wanneer een unieke id moet worden opgehaald voordat deze in een verwijderingsaanvraag wordt opgegeven). |

>[!NOTE] en verwijder `removeIdentities` `retrieveThenRemoveIdentities` alleen identiteiten uit de browser voor specifieke Adobe-oplossingen die deze ondersteunen. Adobe Audience Manager verwijdert bijvoorbeeld niet de index-id&#39;s die zijn opgeslagen in cookies van derden, terwijl Adobe Target alle cookies verwijdert waarin de id&#39;s zijn opgeslagen.

Aangezien alle drie functies asynchrone processen vertegenwoordigen, moeten om het even welke teruggewonnen identiteiten worden behandeld gebruikend callbacks of beloftes.


## Installatie

Als u de Privacy JS Library wilt gaan gebruiken, moet u deze op een van de volgende manieren op uw computer installeren:

* Installeer met npm door de volgende opdracht uit te voeren: `npm install @adobe/adobe-privacy`
* Adobe Launch Extension onder de naam gebruiken `AdobePrivacy`
* Downloaden vanaf [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instantiëren van de Privacy JS Library

Alle toepassingen die gebruikmaken van de Privacy JS Library moeten een nieuw `AdobePrivacy` object instantiëren, dat moet worden geconfigureerd voor een specifieke Adobe-oplossing. Een instantie voor Adobe Analytics ziet er bijvoorbeeld ongeveer als volgt uit:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Voor een volledige lijst van gesteunde parameters voor verschillende oplossingen van Adobe, zie de bijlage sectie over gesteunde de configuratieparameters [van de](#adobe-solution-configuration-parameters)oplossing van Adobe.

## Codevoorbeelden

De volgende codesteekproeven tonen aan hoe te om de Bibliotheek van Privacy JS voor verscheidene gemeenschappelijke scenario&#39;s te gebruiken, op voorwaarde dat u geen Lancering of DTM gebruikt.

### Identiteiten ophalen

In dit voorbeeld wordt getoond hoe u een lijst met identiteiten ophaalt uit Experience Cloud.

#### JavaScript

De volgende code definieert een functie, `handleRetrievedIDs`, die moet worden gebruikt als callback of promise om de identiteiten af te handelen die door `retrieveIdentities`.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variabele | Beschrijving |
| --- | --- |
| `validIds` | Een JSON-object dat alle id&#39;s bevat die met succes zijn opgehaald. |
| `failedIDs` | Een JSON-object met alle id&#39;s die niet van de privacyservice zijn opgehaald of die op een andere manier niet zijn gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, `validIDs` wordt gevuld met een lijst van opgehaalde identiteiten.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Identiteiten verwijderen

In dit voorbeeld wordt getoond hoe u een lijst met identiteiten uit de browser kunt verwijderen.

#### JavaScript

De volgende code definieert een functie, `handleRemovedIDs`, die moet worden gebruikt als callback of promise voor het afhandelen van de identiteiten die zijn opgehaald `removeIdentities` nadat deze uit de browser zijn verwijderd.

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variabele | Beschrijving |
| --- | --- |
| `validIds` | Een JSON-object dat alle id&#39;s bevat die met succes zijn opgehaald. |
| `failedIDs` | Een JSON-object met alle id&#39;s die niet van de privacyservice zijn opgehaald of die op een andere manier niet zijn gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, `validIDs` wordt gevuld met een lijst van opgehaalde identiteiten.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de kernfuncties van de Privacy JS Library. Nadat u de bibliotheek hebt gebruikt om een lijst met identiteiten op te halen, kunt u die identiteiten gebruiken om gegevenstoegang te maken en aanvragen naar de API van de privacydienst te verwijderen. Zie de [de ontwikkelaarsgids](api/getting-started.md) van de Dienst van de Privacy voor meer informatie.

## Aanhangsel

Deze sectie bevat aanvullende informatie voor het gebruik van de Privacy JS Library.

### Configuratieparameters van de Adobe-oplossing

Hieronder volgt een lijst met de geaccepteerde configuratieparameters voor ondersteunde Adobe-oplossingen die worden gebruikt bij het [instantiëren van een AdobePrivacy-object](#instantiate-the-privacy-js-library).

**Adobe Analytics**

| Parameter | Beschrijving |
| --- | --- |
| `cookieDomainPeriods` | De numerieke punten in een domein voor het bijhouden van cookies (standaard is 2). |
| `dataCenter` | Adobe-datacenter voor gegevensverzameling. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. Mogelijke waarden zijn: <ul><li>&quot;d1&quot;: San Jose datacenter.</li><li>&quot;d2&quot;: Dallas datacenter.</li></ul> |
| `reportSuite` | ID van de Reeks van het rapport zoals gespecificeerd in uw JavaScript Webbaken (bijvoorbeeld, &quot;s_code.js&quot;of &quot;dtm&quot;). |
| `trackingServer` | Domein voor gegevensverzameling (niet-SSL). Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |
| `trackingServerSecure` | Domein voor gegevensverzameling (SSL). Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |
| `visitorNamespace` | Naamruimte die wordt gebruikt om bezoekers te groeperen. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |

**Adobe-doel**

| Parameter | Beschrijving |
| --- | --- |
| `clientCode` | Clientcode die een client identificeert in Adobe Target System. |

**Adobe Audience Manager**

| Parameter | Beschrijving |
| --- | --- |
| `aamUUIDCookieName` | Naam van het cookie van de eerste partij met de unieke gebruikers-id die door Adobe Audience Manager is geretourneerd. |

**Adobe-id-service (ECID)**

| Parameter | Beschrijving |
| --- | --- |
| `imsOrgID` | Uw IMS-organisatie-id. |