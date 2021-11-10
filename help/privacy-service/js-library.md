---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Overzicht van Adobe Privacy JavaScript-bibliotheek
topic-legacy: overview
description: Met de Adobe Privacy JavaScript-bibliotheek kunt u gegevenssubject-id's ophalen voor gebruik in Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: 7f3a0594147a8cea292263f60aa45dc5ebb8484e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# Overzicht van Adobe Privacy JavaScript-bibliotheek

Als gegevensverwerker verwerkt Adobe persoonlijke gegevens volgens de toestemming en instructies van uw bedrijf. Als datacontroller bepaalt u welke persoonlijke data Adobe namens u verwerkt en opslaat. Afhankelijk van de informatie die u kiest om via Adobe Experience Cloud-oplossingen te verzenden, kan Adobe persoonlijke informatie opslaan die van toepassing is op privacyregels zoals de [!DNL General Data Protection Regulation] (GDPR) en [!DNL California Consumer Privacy Act] (CCPA). Document weergeven op [privacy in Adobe Experience Cloud](https://www.adobe.com/nl/privacy/marketing-cloud.html) voor meer informatie over hoe de oplossingen van de Experience Cloud privé gegevens verzamelen.

De **Adobe Privacy JavaScript-bibliotheek** staat gegevensverwerkingsverantwoordelijken toe om de terugwinning van alle gegevenssubject identiteiten te automatiseren die door [!DNL Experience Cloud] oplossingen voor een specifiek domein. De API van [Adobe Experience Platform Privacy Service](home.md)Deze identiteiten kunnen vervolgens worden gebruikt om toegang te verkrijgen tot en verzoeken te verwijderen voor privégegevens van deze betrokkenen.

>[!NOTE]
>
>De [!DNL Privacy JS Library] hoeft gewoonlijk alleen op privacygerelateerde pagina&#39;s te worden geïnstalleerd en hoeft niet op alle pagina&#39;s van een website of domein te worden geïnstalleerd.

## Functies

De [!DNL Privacy JS Library] biedt verschillende functies voor het beheren van identiteiten in [!DNL Privacy Service]. Deze functies kunnen alleen worden gebruikt om de identiteiten te beheren die in de browser voor een specifieke bezoeker zijn opgeslagen. Zij kunnen niet worden gebruikt om informatie aan [!DNL Experience Cloud Central Service] rechtstreeks.

In de volgende tabel worden de verschillende functies beschreven die door de bibliotheek worden geboden:

| -functie | Beschrijving |
| --- | --- |
| `retrieveIdentities` | Retourneert een array van overeenkomende identiteiten (`validIds`) die zijn opgehaald van [!DNL Privacy Service]en een array met identiteiten die niet zijn gevonden (`failedIds`). |
| `removeIdentities` | Hiermee verwijdert u elke overeenkomende (geldige) identiteit uit de browser. Retourneert een array van overeenkomende identiteiten (`validIds`), waarbij elke identiteit een `isDeletedClientSide` Boolean die aangeeft of deze id is verwijderd. |
| `retrieveThenRemoveIdentities` | Hiermee wordt een array van overeenkomende identiteiten opgehaald (`validIds`), en verwijdert dan die identiteiten uit browser. Hoewel deze functie vergelijkbaar is met `removeIdentities`, wordt het best gebruikt wanneer de oplossing van de Adobe u gebruikt vereist een toegangsverzoek alvorens schrapping mogelijk is (zoals wanneer een uniek herkenningsteken moet worden teruggewonnen alvorens het in een schrappingsverzoek te verstrekken). |

>[!NOTE]
>
>`removeIdentities` en `retrieveThenRemoveIdentities` verwijder alleen identiteiten uit de browser voor specifieke Adobe-oplossingen die deze ondersteunen. Adobe Audience Manager verwijdert bijvoorbeeld de index-id&#39;s die zijn opgeslagen in cookies van derden niet, terwijl Adobe Target alle cookies verwijdert waarin de id&#39;s zijn opgeslagen.

Aangezien alle drie functies asynchrone processen vertegenwoordigen, moeten om het even welke teruggewonnen identiteiten worden behandeld gebruikend callbacks of beloftes.


## Installatie

Als u het dialoogvenster [!DNL Privacy JS Library], moet u het op uw computer installeren gebruikend één van de volgende methodes:

* Installeer met npm door de volgende opdracht uit te voeren: `npm install @adobe/adobe-privacy`
* Downloaden vanaf de [Experience Cloud GitHub-opslagplaats](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

U kunt de bibliotheek ook installeren via een tagextensie in de gebruikersinterface voor gegevensverzameling. Zie het overzicht op de [Adobe Privacy-tagextensie](../tags/extensions/web/privacy/overview.md) voor meer informatie .

## Instantiëren van de [!DNL Privacy JS Library]

Alle apps die gebruikmaken van de [!DNL Privacy JS Library] moet een nieuw `AdobePrivacy` -object, dat moet worden geconfigureerd voor een specifieke Adobe-oplossing. Een instantie voor Adobe Analytics ziet er bijvoorbeeld ongeveer als volgt uit:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Voor een volledige lijst van gesteunde parameters voor verschillende oplossingen van Adobe, zie de bijlage sectie over gesteund [Adobe-configuratieparameters voor oplossing](#adobe-solution-configuration-parameters).

## Codevoorbeelden {#samples}

De volgende codesteekproeven tonen aan hoe te om het [!DNL Privacy JS Library] voor verschillende algemene scenario&#39;s, op voorwaarde dat u geen labels gebruikt.

### Identiteiten ophalen

In dit voorbeeld wordt getoond hoe u een lijst met identiteiten ophaalt uit [!DNL Experience Cloud].

#### JavaScript

De volgende code definieert een functie. `handleRetrievedIDs`, te gebruiken als callback of belofte om de identiteiten te behandelen die door worden teruggewonnen `retrieveIdentities`.

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
| `failedIDs` | Een JSON-object dat alle id&#39;s bevat die niet zijn opgehaald uit [!DNL Privacy Service], of anders niet gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, `validIDs` wordt gevuld met een lijst met opgehaalde identiteiten.

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

De volgende code definieert een functie. `handleRemovedIDs`, te gebruiken als callback of belofte om de identiteiten te behandelen die door worden teruggewonnen `removeIdentities` nadat ze uit de browser zijn verwijderd.

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
| `failedIDs` | Een JSON-object dat alle id&#39;s bevat die niet zijn opgehaald uit [!DNL Privacy Service], of anders niet gevonden. |

#### Resultaat

Als de code met succes wordt uitgevoerd, `validIDs` wordt gevuld met een lijst met opgehaalde identiteiten.

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

Door dit document te lezen, hebt u de kernfuncties van de [!DNL Privacy JS Library]. Nadat u de bibliotheek hebt gebruikt om een lijst met identiteiten op te halen, kunt u die identiteiten gebruiken om toegang tot gegevens te maken en verzoeken te verwijderen voor de [!DNL Privacy Service] API. Zie de [Handleiding Privacy Service-API](api/overview.md) voor meer informatie .

## Aanhangsel

Deze sectie bevat aanvullende informatie voor het gebruik van de [!DNL Privacy JS Library].

### Adobe-configuratieparameters voor oplossing {#config-params}

Hieronder volgt een lijst met de geaccepteerde configuratieparameters voor ondersteunde Adobe-oplossingen die worden gebruikt wanneer [een AdobePrivacy-object instantiëren](#instantiate-the-privacy-js-library).

**Alle oplossingen**

| Parameter | Beschrijving |
| --- | --- |
| `key` | Een unieke id die de gebruiker of het gegevenssubject identificeert. Deze eigenschap is bedoeld voor gebruik voor uw eigen interne traceringsdoeleinden en wordt niet gebruikt door Adobe. |

**Adobe Analytics**

| Parameter | Beschrijving |
| --- | --- |
| `cookieDomainPeriods` | Het aantal punten in een domein dat wordt gebruikt voor het bijhouden van cookies (standaard ingesteld op `2`, bijvoorbeeld `.domain.com`). Definieer deze hier niet, tenzij anders aangegeven in uw JavaScript-webbaken. |
| `dataCenter` | Het datacenter van de gegevensverzameling Adobe. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. Mogelijke waarden zijn: <ul><li>`d1`: San Jose datacenter</li><li>`d2`: Dallas, datacenter</li></ul> |
| `reportSuite` | De rapportsuite-id zoals opgegeven in uw JavaScript-webbaken (bijvoorbeeld `s_code.js` of `dtm`). |
| `trackingServer` | Een niet-SSL-gegevensverzamelingsdomein. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |
| `trackingServerSecure` | Een SSL-gegevensverzamelingsdomein. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |
| `visitorNamespace` | De naamruimte die wordt gebruikt om bezoekers te groeperen. Deze mag alleen worden opgenomen als deze is opgegeven in uw JavaScript-webbaken. |

**Adobe Audience Manager**

| Parameter | Beschrijving |
| --- | --- |
| `aamUUIDCookieName` | Naam van de cookie van de eerste partij met de unieke gebruikersnaam die door Adobe Audience Manager is geretourneerd. |

**Adobe Experience Cloud Identity Service (ECID)**

| Parameter | Beschrijving |
| --- | --- |
| `imsOrgID` | Uw IMS-organisatie-id. |

**Adobe Target**

| Parameter | Beschrijving |
| --- | --- |
| `clientCode` | Clientcode die een client in Adobe Target System identificeert. |
