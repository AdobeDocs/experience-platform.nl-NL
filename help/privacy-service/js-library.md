---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Adobe Privacy JavaScript Library - Overzicht
description: Met de Adobe Privacy JavaScript Library kunt u de identiteit van de betrokkene ophalen voor gebruik in de Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 1%

---

# Overzicht Adobe Privacy JavaScript Library

Als gegevensverwerker verwerkt de Adobe persoonsgegevens volgens de toestemming en instructies van uw bedrijf. Als gegevenscontrolemechanisme, bepaalt u de persoonlijke gegevens die de Adobe verwerkt en namens u opslaat. Afhankelijk van de informatie die u kiest om via Adobe Experience Cloud-oplossingen te verzenden, kan Adobe persoonlijke informatie opslaan die van toepassing is op privacyregels zoals [!DNL General Data Protection Regulation] (GDPR) en [!DNL California Consumer Privacy Act] (CCPA). Zie het document over [ privacy in Adobe Experience Cloud ](https://www.adobe.com/nl/privacy/marketing-cloud.html) voor meer informatie over hoe de oplossingen van het Experience Cloud privé gegevens verzamelen.

De **Bibliotheek van JavaScript van de Privacy van de Adobe** staat gegevenscontrolemechanismen toe om de terugwinning van alle die gegevensonderwerpidentiteiten te automatiseren door [!DNL Experience Cloud] oplossingen voor een specifiek domein worden geproduceerd. Gebruikend API die door [ Adobe Experience Platform Privacy Service ](home.md) wordt verstrekt, kunnen deze identiteiten dan worden gebruikt om toegang tot en schrappingsverzoeken voor privé gegevens tot stand te brengen die tot die gegevenssubjecten behoren.

>[!NOTE]
>
>[!DNL Privacy JS Library] hoeft gewoonlijk alleen te worden geïnstalleerd op pagina&#39;s met betrekking tot privacy en hoeft niet op alle pagina&#39;s van een website of domein te worden geïnstalleerd.

## Functies

[!DNL Privacy JS Library] biedt verschillende functies voor het beheer van identiteiten in [!DNL Privacy Service] . Deze functies kunnen alleen worden gebruikt om de identiteiten te beheren die in de browser voor een specifieke bezoeker zijn opgeslagen. Ze kunnen niet worden gebruikt om informatie rechtstreeks naar [!DNL Experience Cloud Central Service] te verzenden.

In de volgende tabel worden de verschillende functies beschreven die door de bibliotheek worden geboden:

| Functie | Beschrijving |
| --- | --- |
| `retrieveIdentities` | Retourneert een array van overeenkomende identiteiten (`validIds`) die zijn opgehaald uit [!DNL Privacy Service] en een array van identiteiten die niet zijn gevonden (`failedIds`). |
| `removeIdentities` | Hiermee verwijdert u elke overeenkomende (geldige) identiteit uit de browser. Retourneert een array van overeenkomende identiteiten (`validIds`), met elke identiteit die een `isDeletedClientSide` boolean bevat die aangeeft of deze id is verwijderd. |
| `retrieveThenRemoveIdentities` | Haalt een serie van passende identiteiten (`validIds`) op, en verwijdert dan die identiteiten uit browser. Hoewel deze functie aan `removeIdentities` gelijkaardig is, wordt het best gebruikt wanneer de oplossing van de Adobe u gebruikt een toegangsverzoek vereist alvorens schrapping mogelijk is (zoals wanneer een uniek herkenningsteken moet worden teruggewonnen alvorens het in een schrappingsverzoek te verstrekken). |

>[!NOTE]
>
>`removeIdentities` en `retrieveThenRemoveIdentities` verwijderen alleen identiteiten uit de browser voor specifieke Adobe-oplossingen die deze ondersteunen. Adobe Audience Manager verwijdert bijvoorbeeld de index-id&#39;s die zijn opgeslagen in cookies van derden niet, terwijl Adobe Target alle cookies verwijdert waarin de id&#39;s zijn opgeslagen.

Aangezien alle drie functies asynchrone processen vertegenwoordigen, moeten om het even welke teruggewonnen identiteiten worden behandeld gebruikend callbacks of beloftes.


## Installatie

Als u [!DNL Privacy JS Library] wilt gaan gebruiken, moet u de toepassing op de computer installeren met een van de volgende methoden:

* Installeer met npm door de volgende opdracht uit te voeren: `npm install @adobe/adobe-privacy`
* Download van de [ bewaarplaats van GitHub van het Experience Cloud ](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

U kunt de bibliotheek ook installeren met een tagextensie. Zie het overzicht op de [ de markeringsuitbreiding van de Privacy van de Adobe ](../tags/extensions/client/privacy/overview.md) voor meer informatie.

## Instantiëren van de [!DNL Privacy JS Library]

Alle toepassingen die het [!DNL Privacy JS Library] gebruiken, moeten een nieuw `AdobePrivacy` -object instantiëren, dat moet worden geconfigureerd voor een specifieke Adobe. Een instantie voor Adobe Analytics ziet er bijvoorbeeld ongeveer als volgt uit:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Voor een volledige lijst van gesteunde parameters voor verschillende oplossingen van de Adobe, zie de bijlage sectie over gesteunde [ de configuratieparameters van de oplossing van de Adobe ](#adobe-solution-configuration-parameters).

## Codevoorbeelden {#samples}

In de volgende codevoorbeelden wordt getoond hoe u [!DNL Privacy JS Library] kunt gebruiken voor verschillende algemene scenario&#39;s, op voorwaarde dat u geen tags gebruikt.

### Identiteiten ophalen

In dit voorbeeld wordt getoond hoe u een lijst met identiteiten ophaalt uit [!DNL Experience Cloud] .

#### JavaScript

De volgende code definieert een functie, `handleRetrievedIDs` , die moet worden gebruikt als callback of promise voor het afhandelen van de identiteiten die door `retrieveIdentities` zijn opgehaald.

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
| `failedIDs` | Een JSON-object met alle id&#39;s die niet uit [!DNL Privacy Service] zijn opgehaald of die op een andere manier niet zijn gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, wordt `validIDs` gevuld met een lijst van opgehaalde identiteiten.

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

De volgende code definieert een functie, `handleRemovedIDs` , die als callback of promise moet worden gebruikt om de identiteiten af te handelen die `removeIdentities` heeft opgehaald nadat deze uit de browser zijn verwijderd.

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
| `failedIDs` | Een JSON-object met alle id&#39;s die niet uit [!DNL Privacy Service] zijn opgehaald of die op een andere manier niet zijn gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, wordt `validIDs` gevuld met een lijst van opgehaalde identiteiten.

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

Door dit document te lezen, hebt u de kernfuncties van de [!DNL Privacy JS Library] geïntroduceerd. Nadat u de bibliotheek hebt gebruikt om een lijst met identiteiten op te halen, kunt u deze identiteiten gebruiken om toegang tot gegevens te maken en aanvragen naar de API van [!DNL Privacy Service] te verwijderen. Zie de [ Privacy Service API gids ](api/overview.md) voor meer informatie.

## Bijlage

Deze sectie bevat aanvullende informatie voor het gebruik van [!DNL Privacy JS Library] .

### Configuratieparameters van de oplossing Adobe {#config-params}

Het volgende is een lijst van de toegelaten configuratieparameters voor gesteunde Adobe oplossingen, die worden gebruikt wanneer [ het concretiseren van een voorwerp AdobePrivacy ](#instantiate-the-privacy-js-library).

**Alle oplossingen**

| Parameter | Beschrijving |
| --- | --- |
| `key` | Een unieke id die de gebruiker of het gegevenssubject identificeert. Deze eigenschap is bedoeld voor gebruik voor uw eigen interne traceringsdoeleinden en wordt niet gebruikt door Adobe. |

**Adobe Analytics**

| Parameter | Beschrijving |
| --- | --- |
| `cookieDomainPeriods` | Het aantal punten in een domein dat wordt gebruikt voor het bijhouden van cookies (standaard ingesteld op `2`, bijvoorbeeld `.domain.com` ). Definieer deze hier niet, tenzij anders aangegeven in uw JavaScript-webbaken. |
| `dataCenter` | Het gegevensverzamelingsdatacenter van de Adobe. Deze mag alleen worden opgenomen als dit is opgegeven in uw JavaScript-webbaken. Mogelijke waarden zijn: <ul><li>`d1`: San Jose-datacenter</li><li>`d2`: Dallas-datacenter</li></ul> |
| `reportSuite` | De rapportsuite-id zoals opgegeven in de JavaScript-webbaken (bijvoorbeeld `s_code.js` of `dtm` ). |
| `trackingServer` | Een niet-SSL-gegevensverzamelingsdomein. Deze mag alleen worden opgenomen als dit is opgegeven in uw JavaScript-webbaken. |
| `trackingServerSecure` | Een SSL-gegevensverzamelingsdomein. Deze mag alleen worden opgenomen als dit is opgegeven in uw JavaScript-webbaken. |
| `visitorNamespace` | De naamruimte die wordt gebruikt om bezoekers te groeperen. Deze mag alleen worden opgenomen als dit is opgegeven in uw JavaScript-webbaken. |

**Adobe Audience Manager**

| Parameter | Beschrijving |
| --- | --- |
| `aamUUIDCookieName` | Naam van de cookie van de eerste partij met de unieke gebruikersnaam die door Adobe Audience Manager is geretourneerd. |

**Dienst van de Identiteit van Adobe Experience Cloud (ECID)**

| Parameter | Beschrijving |
| --- | --- |
| `imsOrgID` | Uw organisatie-id. |

**Adobe Target**

| Parameter | Beschrijving |
| --- | --- |
| `clientCode` | Clientcode die een client in Adobe Target System identificeert. |
