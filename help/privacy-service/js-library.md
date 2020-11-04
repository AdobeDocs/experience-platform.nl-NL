---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van Adobe Privacy JavaScript-bibliotheek
topic: overview
translation-type: tm+mt
source-git-commit: 6d706b33573e88b2f1ea9d386928dcfdb089a9c5
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 4%

---


# Overzicht van Adobe Privacy JavaScript-bibliotheek

Als gegevensverwerker verwerkt Adobe persoonlijke gegevens volgens de toestemming en instructies van uw bedrijf. Als datacontroller bepaalt u welke persoonlijke data Adobe namens u verwerkt en opslaat. Afhankelijk van de informatie die u kiest om via Adobe Experience Cloud-oplossingen te verzenden, kan Adobe persoonlijke informatie opslaan die van toepassing is op privacyregels zoals de [!DNL General Data Protection Regulation] (GDPR) en [!DNL California Consumer Privacy Act] (CCPA). Raadpleeg het document over [privacy in Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) voor meer informatie over hoe Experience Cloud-oplossingen privégegevens verzamelen.

Met de JavaScript-bibliotheek **** Adobe Privacy kunnen gegevenscontrollers het ophalen van alle gegevensonderwerpidentiteiten automatiseren die zijn gegenereerd door [!DNL Experience Cloud] oplossingen voor een bepaald domein. Met behulp van de API die door [Adobe Experience Platform Privacy Service](home.md)wordt aangeboden, kunnen deze identiteiten vervolgens worden gebruikt om toegang- en verwijderingsverzoeken te maken voor privégegevens die bij deze betrokkenen horen.

>[!NOTE]
>
>De code hoeft [!DNL Privacy JS Library] gewoonlijk alleen op privacygerelateerde pagina&#39;s te worden geïnstalleerd en hoeft niet op alle pagina&#39;s van een website of domein te worden geïnstalleerd.

## Functies

Het [!DNL Privacy JS Library] bevat verschillende functies voor het beheer van identiteiten in [!DNL Privacy Service]. Deze functies kunnen alleen worden gebruikt om de identiteiten te beheren die in de browser voor een specifieke bezoeker zijn opgeslagen. Ze kunnen niet worden gebruikt om informatie rechtstreeks aan de [!DNL Experience Cloud Central Service] Commissie voor te leggen.

In de volgende tabel worden de verschillende functies beschreven die door de bibliotheek worden geboden:

| -functie | Beschrijving |
| --- | --- |
| `retrieveIdentities` | Retourneert een array van overeenkomende identiteiten (`validIds`) die zijn opgehaald van [!DNL Privacy Service], en een array van identiteiten die niet zijn gevonden (`failedIds`). |
| `removeIdentities` | Hiermee verwijdert u elke overeenkomende (geldige) identiteit uit de browser. Retourneert een array van overeenkomende identiteiten (`validIds`), met elke identiteit die een `isDeletedClientSide` booleaanse id bevat die aangeeft of deze id is verwijderd. |
| `retrieveThenRemoveIdentities` | Haalt een array van overeenkomende identiteiten (`validIds`) op en verwijdert deze identiteiten vervolgens uit de browser. Terwijl deze functie aan gelijkaardig is, wordt het best gebruikt wanneer de oplossing van Adobe u gebruikt een toegangsverzoek vereist alvorens schrapping mogelijk is (zoals wanneer een uniek herkenningsteken moet worden teruggewonnen alvorens het in een schrappingsverzoek te verstrekken). `removeIdentities` |

>[!NOTE]
>
>`removeIdentities` en verwijder `retrieveThenRemoveIdentities` alleen identiteiten uit de browser voor specifieke Adobe-oplossingen die deze ondersteunen. Adobe Audience Manager verwijdert bijvoorbeeld de index-id&#39;s die zijn opgeslagen in cookies van derden niet, terwijl Adobe Target alle cookies verwijdert waarin de id&#39;s zijn opgeslagen.

Aangezien alle drie functies asynchrone processen vertegenwoordigen, moeten om het even welke teruggewonnen identiteiten worden behandeld gebruikend callbacks of beloftes.


## Installatie

Als u de toepassing wilt gaan gebruiken, moet u deze op een van de volgende manieren op de computer installeren: [!DNL Privacy JS Library]

* Installeer met npm door de volgende opdracht uit te voeren: `npm install @adobe/adobe-privacy`
* De extensie Adobe starten onder de naam `AdobePrivacy`
* Download van de [Experience Cloud GitHub-opslagplaats](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instantiëren van de [!DNL Privacy JS Library]

Alle apps die het gebruiken [!DNL Privacy JS Library] moeten een nieuw `AdobePrivacy` voorwerp concretiseren, dat aan een specifieke oplossing van de Adobe moet worden gevormd. Een instantie voor Adobe Analytics ziet er bijvoorbeeld ongeveer als volgt uit:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Voor een volledige lijst van gesteunde parameters voor verschillende oplossingen van Adobe, zie de bijlage sectie over gesteunde de configuratieparameters [van de oplossing van](#adobe-solution-configuration-parameters)Adobe.

## Codevoorbeelden

De volgende codesteekproeven tonen aan hoe te om [!DNL Privacy JS Library] voor verscheidene gemeenschappelijke scenario&#39;s te gebruiken, op voorwaarde dat u niet gebruikt [!DNL Launch] of DTM.

### Identiteiten ophalen

In dit voorbeeld wordt getoond hoe u een lijst met identiteiten ophaalt van [!DNL Experience Cloud].

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
| `failedIDs` | Een JSON-object dat alle id&#39;s bevat die niet zijn opgehaald van [!DNL Privacy Service]of die op een andere manier niet zijn gevonden. |

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
| `failedIDs` | Een JSON-object dat alle id&#39;s bevat die niet zijn opgehaald van [!DNL Privacy Service]of die op een andere manier niet zijn gevonden. |

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

Door dit document te lezen, bent u geïntroduceerd in de kernfuncties van het [!DNL Privacy JS Library]. Nadat u de bibliotheek hebt gebruikt om een lijst met identiteiten op te halen, kunt u deze identiteiten gebruiken om toegang tot gegevens te maken en aanvragen naar de [!DNL Privacy Service] API te verwijderen. Zie de [Privacy Service-ontwikkelaarsgids](api/getting-started.md) voor meer informatie.

## Aanhangsel

Deze sectie bevat aanvullende informatie voor het gebruik van de [!DNL Privacy JS Library]flacon.

### Adobe-configuratieparameters voor oplossing

Hieronder volgt een lijst met de geaccepteerde configuratieparameters voor ondersteunde Adobe-oplossingen die worden gebruikt bij het [instantiëren van een AdobePrivacy-object](#instantiate-the-privacy-js-library).

**Adobe Analytics**

| Parameter | Beschrijving |
| --- | --- |
| `cookieDomainPeriods` | De numerieke punten in een domein voor het bijhouden van cookies (standaard is 2). |
| `dataCenter` | Adobe gegevensverzamelingsdatacenter. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. Mogelijke waarden zijn: <ul><li>&quot;d1&quot;: San Jose datacenter.</li><li>&quot;d2&quot;: Dallas datacenter.</li></ul> |
| `reportSuite` | ID van de Reeks van het rapport zoals gespecificeerd in uw JavaScript Webbaken (bijvoorbeeld, &quot;s_code.js&quot;of &quot;dtm&quot;). |
| `trackingServer` | Domein voor gegevensverzameling (niet-SSL). Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |
| `trackingServerSecure` | Domein voor gegevensverzameling (SSL). Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |
| `visitorNamespace` | Naamruimte die wordt gebruikt om bezoekers te groeperen. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |

**Adobe Target**

| Parameter | Beschrijving |
| --- | --- |
| `clientCode` | Clientcode die een client in Adobe Target System identificeert. |

**Adobe Audience Manager**

| Parameter | Beschrijving |
| --- | --- |
| `aamUUIDCookieName` | Naam van de cookie van de eerste partij met de unieke gebruikersnaam die door Adobe Audience Manager is geretourneerd. |

**Adobe ID Service (ECID)**

| Parameter | Beschrijving |
| --- | --- |
| `imsOrgID` | Uw IMS-organisatie-id. |