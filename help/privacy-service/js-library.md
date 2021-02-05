---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Overzicht van Adobe Privacy JavaScript-bibliotheek
topic: overview
description: Met de Adobe Privacy JavaScript-bibliotheek kunt u gegevenssubject-id's ophalen voor gebruik in Privacy Service.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 4%

---


# Overzicht van Adobe Privacy JavaScript-bibliotheek

Als gegevensverwerker verwerkt Adobe persoonlijke gegevens volgens de toestemming en instructies van uw bedrijf. Als datacontroller bepaalt u welke persoonlijke data Adobe namens u verwerkt en opslaat. Afhankelijk van de informatie die u kiest om via Adobe Experience Cloud-oplossingen te verzenden, kan Adobe persoonlijke informatie opslaan die van toepassing is op privacyregels zoals [!DNL General Data Protection Regulation] (GDPR) en [!DNL California Consumer Privacy Act] (CCPA). Zie het document over [privacy in Adobe Experience Cloud](https://www.adobe.com/privacy/marketing-cloud.html) voor meer informatie over hoe de oplossingen van de Experience Cloud privé gegevens verzamelen.

Met de **Adobe Privacy JavaScript Library** kunnen gegevenscontrollers het ophalen van alle gegevenssubject-id&#39;s automatiseren die worden gegenereerd door [!DNL Experience Cloud]-oplossingen voor een specifiek domein. Met behulp van de API van [Adobe Experience Platform Privacy Service](home.md), kunnen deze identiteiten dan worden gebruikt om toegang tot en schrappingsverzoeken voor privé gegevens tot stand te brengen die tot die betrokkenen behoren.

>[!NOTE]
>
>[!DNL Privacy JS Library] hoeft gewoonlijk alleen op pagina&#39;s met betrekking tot privacy te worden geïnstalleerd en hoeft niet op alle pagina&#39;s van een website of domein te worden geïnstalleerd.

## Functies

[!DNL Privacy JS Library] verstrekt verscheidene functies voor het beheren van identiteiten in [!DNL Privacy Service]. Deze functies kunnen alleen worden gebruikt om de identiteiten te beheren die in de browser voor een specifieke bezoeker zijn opgeslagen. Ze kunnen niet worden gebruikt om informatie rechtstreeks naar [!DNL Experience Cloud Central Service] te verzenden.

In de volgende tabel worden de verschillende functies beschreven die door de bibliotheek worden geboden:

| -functie | Beschrijving |
| --- | --- |
| `retrieveIdentities` | Retourneert een array van overeenkomende identiteiten (`validIds`) die zijn opgehaald van [!DNL Privacy Service], evenals een array van identiteiten die niet zijn gevonden (`failedIds`). |
| `removeIdentities` | Hiermee verwijdert u elke overeenkomende (geldige) identiteit uit de browser. Retourneert een array met overeenkomende identiteiten (`validIds`), waarbij elke identiteit een booleaanse waarde `isDeletedClientSide` bevat die aangeeft of deze id is verwijderd. |
| `retrieveThenRemoveIdentities` | Haalt een array van overeenkomende identiteiten (`validIds`) op en verwijdert deze identiteiten vervolgens uit de browser. Terwijl deze functie aan `removeIdentities` gelijkaardig is, wordt het best gebruikt wanneer de oplossing van Adobe u gebruikt een toegangsverzoek vereist alvorens schrapping mogelijk is (zoals wanneer een uniek herkenningsteken moet worden teruggewonnen alvorens het in een schrappingsverzoek te verstrekken). |

>[!NOTE]
>
>`removeIdentities` en verwijder  `retrieveThenRemoveIdentities` alleen identiteiten uit de browser voor specifieke Adobe-oplossingen die deze ondersteunen. Adobe Audience Manager verwijdert bijvoorbeeld de index-id&#39;s die zijn opgeslagen in cookies van derden niet, terwijl Adobe Target alle cookies verwijdert waarin de id&#39;s zijn opgeslagen.

Aangezien alle drie functies asynchrone processen vertegenwoordigen, moeten om het even welke teruggewonnen identiteiten worden behandeld gebruikend callbacks of beloftes.


## Installatie

Als u de [!DNL Privacy JS Library] wilt gaan gebruiken, moet u deze op een van de volgende manieren op uw computer installeren:

* Installeer met npm door de volgende opdracht uit te voeren: `npm install @adobe/adobe-privacy`
* De extensie Adobe starten gebruiken onder de naam `AdobePrivacy`
* Download van de [Experience Cloud GitHub-gegevensopslagruimte](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instantiëren van [!DNL Privacy JS Library]

Alle toepassingen die [!DNL Privacy JS Library] gebruiken moeten een nieuw `AdobePrivacy` voorwerp concretiseren, dat aan een specifieke oplossing van Adobe moet worden gevormd. Een instantie voor Adobe Analytics ziet er bijvoorbeeld ongeveer als volgt uit:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Voor een volledige lijst van gesteunde parameters voor verschillende oplossingen van de Adobe, zie de bijlage sectie over gesteunde [de configuratieparameters van de oplossing van de Adobe](#adobe-solution-configuration-parameters).

## Codevoorbeelden

De volgende codesteekproeven tonen aan hoe te om [!DNL Privacy JS Library] voor verscheidene gemeenschappelijke scenario&#39;s te gebruiken, op voorwaarde dat u [!DNL Launch] of DTM niet gebruikt.

### Identiteiten ophalen

In dit voorbeeld wordt getoond hoe u een lijst met identiteiten ophaalt uit [!DNL Experience Cloud].

#### JavaScript

De volgende code bepaalt een functie, `handleRetrievedIDs`, die als callback of belofte moet worden gebruikt om de identiteiten te behandelen die door `retrieveIdentities` worden teruggewonnen.

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
| `failedIDs` | Een JSON-object dat alle id&#39;s bevat die niet zijn opgehaald van [!DNL Privacy Service] of die op een andere manier niet zijn gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, wordt `validIDs` gevuld met een lijst van teruggewonnen identiteiten.

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

De volgende code definieert een functie, `handleRemovedIDs`, die als callback of promise moet worden gebruikt om de identiteiten af te handelen die door `removeIdentities` zijn opgehaald nadat deze uit de browser zijn verwijderd.

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
| `failedIDs` | Een JSON-object dat alle id&#39;s bevat die niet zijn opgehaald van [!DNL Privacy Service] of die op een andere manier niet zijn gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, wordt `validIDs` gevuld met een lijst van teruggewonnen identiteiten.

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

Door dit document te lezen, bent u geïntroduceerd in de kernfuncties van [!DNL Privacy JS Library]. Nadat u de bibliotheek hebt gebruikt om een lijst met identiteiten op te halen, kunt u die identiteiten gebruiken om gegevenstoegang te maken en aanvragen naar de [!DNL Privacy Service]-API te verwijderen. Zie [Privacy Service ontwikkelaarshandleiding](api/getting-started.md) voor meer informatie.

## Aanhangsel

Deze sectie bevat aanvullende informatie voor het gebruik van [!DNL Privacy JS Library].

### Adobe-configuratieparameters voor oplossing

Hieronder volgt een lijst met de geaccepteerde configuratieparameters voor ondersteunde Adobe-oplossingen die worden gebruikt wanneer [een AdobePrivacy-object](#instantiate-the-privacy-js-library) instantieert.

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