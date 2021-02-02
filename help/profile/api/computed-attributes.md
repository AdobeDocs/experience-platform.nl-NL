---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Computed Attributes API Endpoint
topic: guide
type: Documentation
description: 'Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op gegevens van het Profiel van de Klant in real time, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen die in Adobe Experience Platform worden opgeslagen. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 0%

---


# (Alpha) Berekend kenmerkeindpunt

>[!IMPORTANT]
>
>De berekende kenmerkfunctionaliteit die in dit document wordt beschreven, bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op het profielniveau, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen.

Elk berekend kenmerk bevat een expressie, of &#39;regel&#39;, die binnenkomende gegevens evalueert en de resulterende waarde opslaat in een profielkenmerk of in een gebeurtenis. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren.

Deze gids zal u helpen om gegevens verwerkte attributen binnen Adobe Experience Platform beter te begrijpen en omvat steekproefAPI vraag voor het uitvoeren van basisbewerkingen CRUD gebruikend het `/config/computedAttributes` eindpunt.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [Real-time het Profiel van de Klant API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een [!DNL Experience Platform]-API te voltooien.

## Berekende kenmerken begrijpen

Met Adobe Experience Platform kunt u eenvoudig gegevens uit meerdere bronnen importeren en samenvoegen om [!DNL Real-time Customer Profiles] te genereren. Elk profiel bevat belangrijke informatie met betrekking tot een persoon, zoals zijn contactgegevens, voorkeuren en aankoopgeschiedenis, die een 360 graden mening van de klant verstrekken.

Een deel van de informatie die in het profiel wordt verzameld, is gemakkelijk te begrijpen wanneer de gegevensvelden rechtstreeks worden gelezen (bijvoorbeeld &quot;voornaam&quot;), terwijl andere gegevens meerdere berekeningen vereisen of op andere velden en waarden vertrouwen om de informatie te genereren (bijvoorbeeld &quot;totaal voor levenslange aanschaf&quot;). Om deze gegevens in één oogopslag begrijpelijker te maken, kunt u met [!DNL Platform] berekende kenmerken maken die deze verwijzingen en berekeningen automatisch uitvoeren en de waarde in het juiste veld retourneren.

De berekende attributen omvatten het creëren van een uitdrukking, of &quot;regel&quot;, die op inkomende gegevens werkt en de resulterende waarde in een profielattribuut of een gebeurtenis opslaat. Expressies kunnen op meerdere verschillende manieren worden gedefinieerd, zodat u kunt opgeven dat een regel alleen binnenkomende gebeurtenissen, binnenkomende gebeurtenis- en profielgegevens of binnenkomende gebeurtenissen, profielgegevens en historische gebeurtenissen evalueert.

### Gebruiksscenario’s

Bij gebruik van berekende kenmerken kan het gaan om eenvoudige berekeningen tot zeer complexe verwijzingen. Hier volgen een paar voorbeelden van gebruiksscenario&#39;s voor berekende kenmerken:

1. **[!UICONTROL Percentages]:** Een eenvoudig berekend kenmerk kan het opnemen van twee numerieke velden in een record omvatten en het splitsen van deze velden om een percentage te maken. U kunt bijvoorbeeld het totale aantal e-mails dat naar een individu is verzonden, opsplitsen in het aantal e-mails dat de persoon opent. Als u het resulterende berekende kenmerkveld bekijkt, wordt snel het percentage weergegeven van het totale aantal e-mails dat door het individu wordt geopend.
1. **[!UICONTROL Toepassingsgebruik]: in** een ander voorbeeld kunt u het aantal keren samenvoegen dat een gebruiker de toepassing opent. Door het totale aantal geopende toepassingen te volgen, op basis van afzonderlijke open gebeurtenissen, kunt u speciale aanbiedingen of berichten aan gebruikers aanbieden op hun 100e open, waardoor u een diepere betrokkenheid bij uw merk aanmoedigt.
1. **[!UICONTROL Levenstijdwaarden]:Het** verzamelen van lopende totalen, zoals een levenslange aankoopwaarde voor een klant, kan zeer moeilijk zijn. Dit vereist het bijwerken van het historische totaal telkens wanneer een nieuwe aankoopgebeurtenis plaatsvindt. Een gegevens verwerkt attribuut staat u toe om dit veel gemakkelijker te doen door de levenwaarde op één enkel gebied te handhaven dat automatisch na elke succesvolle koopgebeurtenis met betrekking tot de klant wordt bijgewerkt.

## Een berekend kenmerk configureren

Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit veld kan worden gemaakt met een mix om het veld toe te voegen aan een bestaand schema of door een veld te selecteren dat u al in een schema hebt gedefinieerd.

>[!NOTE]
>
>Berekende kenmerken kunnen niet worden toegevoegd aan velden binnen door Adobe gedefinieerde combinaties. Het veld moet zich binnen de naamruimte `tenant` bevinden. Dit betekent dat het een veld moet zijn dat u definieert en toevoegt aan een schema.

Om een gegevens verwerkt attributengebied met succes te bepalen, moet het schema voor [!DNL Profile] worden toegelaten en als deel van het verenigingsschema voor de klasse verschijnen waarop het schema wordt gebaseerd. Voor meer informatie over [!DNL Profile]-Toegelaten schema&#39;s en vakbonden, te herzien gelieve de sectie van de [!DNL Schema Registry] sectie van de ontwikkelaarsgids op [toelatend een schema voor Profiel en het bekijken verenigingsschema&#39;s](../../xdm/api/getting-started.md). Het wordt ook geadviseerd om de [sectie over union](../../xdm/schema/composition.md) in de documentatie van de schemacompositie te herzien basiscs.

Het werkschema in deze zelfstudie gebruikt een [!DNL Profile]-Toegelaten schema en volgt de stappen voor het bepalen van een nieuwe mengeling die het gegevens verwerkte attributengebied bevat en ervoor zorgt dat het correcte namespace is. Als u reeds een gebied hebt dat in correcte namespace binnen een profiel-toegelaten schema is, kunt u aan de stap voor [het creëren van een gegevens verwerkt attribuut](#create-a-computed-attribute) direct te werk gaan.

### Een schema weergeven

De stappen die volgen gebruiken het gebruikersinterface van Adobe Experience Platform om van een schema de plaats te bepalen, een mengeling toe te voegen, en een gebied te bepalen. Als u liever de [!DNL Schema Registry] API gebruikt, raadpleegt u de [Handleiding voor ontwikkelaars van het schemeregister](../../xdm/api/getting-started.md) voor stappen over hoe u een mix maakt, een mix aan een schema toevoegt en een schema voor gebruik met [!DNL Real-time Customer Profile] inschakelt.

Klik in de gebruikersinterface op **[!UICONTROL Schema&#39;s]** in het linkerspoor en gebruik de zoekbalk op het tabblad **[!UICONTROL Bladeren]** om snel het schema te zoeken dat u wilt bijwerken.

![](../images/computed-attributes/Schemas-Browse.png)

Zodra u het schema hebt gevestigd, klik zijn naam om [!DNL Schema Editor] te openen waar u uitgeeft aan het schema kunt maken.

![](../images/computed-attributes/Schema-Editor.png)

### Een mix maken

Als u een nieuwe mix wilt maken, klikt u op **[!UICONTROL Toevoegen]** naast **[!UICONTROL Mixins]** in de sectie **[!UICONTROL Compositie]** aan de linkerkant van de editor. Dit opent **[!UICONTROL Add mixin]** dialoog waar u bestaande mengen kunt zien. Klik op het keuzerondje voor **[!UICONTROL Nieuwe mix maken]** om de nieuwe mix te definiëren.

Geef de mixin een naam en een beschrijving, en klik **[!UICONTROL Add mixin]** wanneer volledig.

![](../images/computed-attributes/Add-mixin.png)

### Een veld voor berekende kenmerken toevoegen aan het schema

Uw nieuwe mix moet nu worden weergegeven in de sectie &quot;[!UICONTROL Mixins]&quot; onder &quot;[!UICONTROL Compositie]&quot;. Klik op de naam van de mixin en de veelvoudige **[!UICONTROL voegt gebied]** knopen in **[!UICONTROL Structuur]** sectie van de redacteur zal verschijnen.

Selecteer **[!UICONTROL Veld toevoegen]** naast de naam van het schema om een veld op hoofdniveau toe te voegen, of u kunt selecteren om het veld toe te voegen binnen het schema dat u wilt gebruiken.

Nadat u op **[!UICONTROL Veld toevoegen]** hebt geklikt, wordt een nieuw object geopend dat voor uw huurder-id is benoemd en waaruit blijkt dat het veld zich in de juiste naamruimte bevindt. Binnen dat object wordt een **[!UICONTROL Nieuw veld]** weergegeven. Dit als het veld waarin u het berekende kenmerk wilt definiëren.

![](../images/computed-attributes/New-field.png)

### Het veld configureren

Met de sectie **[!UICONTROL Veldeigenschappen]** aan de rechterkant van de editor geeft u de benodigde informatie voor het nieuwe veld op, zoals de naam, weergavenaam en het type.

>[!NOTE]
>
>Het type voor het veld moet van hetzelfde type zijn als de berekende kenmerkwaarde. Als de berekende kenmerkwaarde bijvoorbeeld een tekenreeks is, moet het veld dat in het schema wordt gedefinieerd, een tekenreeks zijn.

Wanneer gedaan, klik **[!UICONTROL toepassen]** en de naam van het gebied, evenals zijn type zal in de **[!UICONTROL sectie van de Structuur]** van de redacteur verschijnen.

![](../images/computed-attributes/Apply.png)

### Schema inschakelen voor [!DNL Profile]

Controleer voordat u doorgaat of het schema is ingeschakeld voor [!DNL Profile]. Klik op de schemanaam in **[!UICONTROL de sectie van de Structuur]** van de redacteur zodat **[!UICONTROL de Eigenschappen van het Schema]** tabel verschijnt. Als de schuifregelaar **[!UICONTROL Profiel]** blauw is, is het schema ingeschakeld voor [!DNL Profile].

>[!NOTE]
>
>Het toelaten van een schema voor [!DNL Profile] kan niet ongedaan worden gemaakt, zodat als u op de schuif klikt zodra het is toegelaten, moet u het risico niet het onbruikbaar maken.

![](../images/computed-attributes/Profile.png)

U kunt nu **[!UICONTROL Save]** klikken om het bijgewerkte schema op te slaan en verder te gaan met de rest van de zelfstudie met behulp van de API.

### Een berekend kenmerk maken {#create-a-computed-attribute}

Met uw gegevens verwerkte kenmerkgebied geïdentificeerd, en bevestiging dat het schema voor [!DNL Profile] wordt toegelaten, kunt u een gegevens verwerkt attribuut nu vormen.

Begin door een verzoek van de POST aan het `/config/computedAttributes` eindpunt met een verzoeklichaam te doen dat de details van de gegevens verwerkte attributen bevat die u wenst om tot stand te brengen.

**API-indeling**

```http
POST /config/computedAttributes
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Eigenschap | Beschrijving |
|---|---|
| `name` | De naam van het berekende kenmerkveld, als een tekenreeks. |
| `path` | Het pad naar het veld met het berekende kenmerk. Dit pad wordt gevonden in het `properties`-kenmerk van het schema en mag NIET de veldnaam in het pad opnemen. Laat bij het schrijven van het pad de verschillende niveaus van `properties`-kenmerken weg. |
| `{TENANT_ID}` | Als u niet vertrouwd met uw huurdersidentiteitskaart bent, gelieve te verwijzen naar de stappen voor het vinden van uw huurdersidentiteitskaart in [de ontwikkelaarsgids van de Registratie van het Schema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Een beschrijving van het berekende kenmerk. Dit is vooral handig als er meerdere berekende kenmerken zijn gedefinieerd, omdat hierdoor anderen binnen uw IMS-organisatie kunnen bepalen welk kenmerk correct moet worden berekend. |
| `expression.value` | Een geldige [!DNL Profile Query Language] (PQL)-expressie. Voor meer informatie over PQL en verbindingen aan gesteunde vragen, gelieve te lezen [PQL overzicht](../../segmentation/pql/overview.md). |
| `schema.name` | De klasse waarop het schema met het berekende kenmerkveld is gebaseerd. Voorbeeld: `_xdm.context.experienceevent` voor een schema dat op de klasse XDM ExperienceEvent wordt gebaseerd. |

**Antwoord**

Een met succes gecreeerd gegevens verwerkt attribuut keert de Status 200 van HTTP (O.K.) en een reactielichaam terug die de details van het onlangs gecreeerde gegevens verwerkte attribuut bevatten. Deze details omvatten een uniek, read-only, systeem-geproduceerd `id` die voor het van verwijzingen voorzien van het gegevens verwerkte attribuut tijdens andere API verrichtingen kunnen worden gebruikt.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | Een unieke, alleen-lezen, door het systeem gegenereerde id die kan worden gebruikt voor het verwijzen naar het berekende kenmerk tijdens andere API-bewerkingen. |
| `imsOrgId` | De IMS-organisatie die betrekking heeft op het berekende kenmerk, moet overeenkomen met de waarde die in de aanvraag is verzonden. |
| `sandbox` | Het sandboxobject bevat details van de sandbox waarin het berekende kenmerk is geconfigureerd. Deze informatie wordt getekend vanuit de sandboxheader die in de aanvraag wordt verzonden. Zie het [sandboxoverzicht](../../sandboxes/home.md) voor meer informatie. |
| `positionPath` | Een array met de gedeconstrueerde `path` naar het veld dat in de aanvraag is verzonden. |
| `returnSchema.meta:xdmType` | Het type veld waarin het berekende kenmerk wordt opgeslagen. |
| `definedOn` | Een array die de samenvoegingsschema&#39;s weergeeft waarop het berekende kenmerk is gedefinieerd. Bevat één object per samenvoegingsschema. Dit houdt in dat er meerdere objecten in de array kunnen zijn als het berekende kenmerk aan meerdere schema&#39;s is toegevoegd op basis van verschillende klassen. |
| `active` | Een booleaanse waarde die weergeeft of het berekende kenmerk actief is of niet. De standaardwaarde is `true`. |
| `type` | Het type van gecreeerde bron, in dit geval &quot;ComputedAttribute&quot;is de standaardwaarde. |
| `createEpoch` en `updateEpoch` | De tijd waarop het berekende attribuut werd gecreeerd en het laatst bijgewerkt, respectievelijk. |


## Toegang krijgen tot berekende kenmerken

Wanneer u werkt met berekende kenmerken met behulp van de API, hebt u twee opties voor toegang tot berekende kenmerken die door uw organisatie zijn gedefinieerd. Ten eerste moeten alle berekende kenmerken worden vermeld. Ten tweede moet een specifiek berekend kenmerk worden weergegeven op basis van het unieke `id`.

De stappen voor zowel het vermelden van alle gegevens verwerkte attributen als het bekijken van een specifiek gegevens verwerkt attribuut worden geschetst in de secties die volgen.

### Berekende kenmerken {#list-computed-attributes} weergeven

Uw IMS Organisatie kan veelvoudige gegevens verwerkte attributen tot stand brengen, en het uitvoeren van een verzoek van de GET aan het `/config/computedAttributes` eindpunt staat u toe om van alle bestaande gegevens verwerkte attributen voor uw organisatie een lijst te maken.

**API-indeling**

```http
GET /config/computedAttributes
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvol antwoord omvat een `_page` attribuut dat het totale aantal gegevens verwerkte attributen (`totalCount`) en het aantal gegevens verwerkte attributen op de pagina (`pageSize`) verstrekt.

De reactie bevat ook een `children`-array die bestaat uit een of meer objecten, die elk de details van één berekend kenmerk bevatten. Als uw organisatie geen berekende kenmerken heeft, zijn `totalCount` en `pageSize` 0 (nul) en is `children` array leeg.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Eigenschap | Beschrijving |
|---|---|
| `_page.totalCount` | Het totale aantal berekende kenmerken dat door uw IMS-organisatie is gedefinieerd. |
| `_page.pageSize` | Het aantal berekende kenmerken dat op deze resultatenpagina wordt geretourneerd. Als `pageSize` gelijk is aan `totalCount`, betekent dit dat er slechts één pagina met resultaten is en alle berekende kenmerken zijn geretourneerd. Als deze niet gelijk zijn, zijn er extra pagina&#39;s met resultaten die kunnen worden geopend. Zie `_links.next` voor meer informatie. |
| `children` | Een array die bestaat uit een of meer objecten, die elk de details van één berekend kenmerk bevatten. Als er geen berekende kenmerken zijn gedefinieerd, is de `children`-array leeg. |
| `id` | Een unieke, alleen-lezen, door het systeem gegenereerde waarde die automatisch wordt toegewezen aan een berekend kenmerk wanneer dit wordt gemaakt. Voor meer informatie over de componenten van een gegevens verwerkt attribuut voorwerp, te zien gelieve de sectie over [het creëren van een gegevens verwerkt attribuut](#create-a-computed-attribute) vroeger in deze zelfstudie. |
| `_links.next` | Als één pagina met berekende kenmerken wordt geretourneerd, is `_links.next` een leeg object, zoals in de voorbeeldreactie hierboven wordt getoond. Als uw organisatie veel berekende kenmerken heeft, worden deze geretourneerd op meerdere pagina&#39;s die u kunt openen door een GET-aanvraag in te dienen bij de waarde `_links.next`. |

### Een berekend kenmerk {#view-a-computed-attribute} weergeven

U kunt een specifiek gegevens verwerkt attribuut ook bekijken door een verzoek van de GET aan het `/config/computedAttributes` eindpunt en met inbegrip van gegevens verwerkte kenmerkidentiteitskaart in de verzoekweg te richten.

**API-indeling**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{ATTRIBUTE_ID}` | De id van het berekende kenmerk dat u wilt weergeven. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Een berekend kenmerk bijwerken

Mocht u vinden dat u een bestaand gegevens verwerkt attribuut moet bijwerken, kan dit worden gedaan door een verzoek van PATCH aan het `/config/computedAttributes` eindpunt en met inbegrip van identiteitskaart van berekende toegeschreven die u in de verzoekweg wenst bij te werken.

**API-indeling**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{ATTRIBUTE_ID}` | De id van het berekende kenmerk dat u wilt bijwerken. |

**Verzoek**

In dit verzoek wordt [JSON-patchopmaak](http://jsonpatch.com/) gebruikt om de &quot;waarde&quot; van het veld &quot;expression&quot; bij te werken.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Eigenschap | Beschrijving |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Een geldige [!DNL Profile Query Language] (PQL)-expressie. Voor meer informatie over PQL en verbindingen aan gesteunde vragen, gelieve te lezen [PQL overzicht](../../segmentation/pql/overview.md). |

**Antwoord**

Een geslaagde update retourneert HTTP Status 204 (Geen inhoud) en een lege antwoordinstantie. Als u wilt bevestigen dat de update succesvol was, kunt u een verzoek van de GET uitvoeren om het gegevens verwerkte attribuut door zijn identiteitskaart te bekijken.

## Een berekend kenmerk verwijderen

Het is ook mogelijk om een berekend attribuut te schrappen gebruikend API. Dit wordt gedaan door een verzoek van DELETE aan het `/config/computedAttributes` eindpunt en met inbegrip van identiteitskaart van de gegevens verwerkte attributen te doen die u wenst om in de verzoekweg te schrappen.

>[!NOTE]
>
>Wees voorzichtig bij het verwijderen van een kenmerk dat u hebt berekend, omdat het in meerdere schema&#39;s wordt gebruikt en de bewerking DELETE niet ongedaan kan worden gemaakt.

**API-indeling**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschrijving |
|---|---|
| `{ATTRIBUTE_ID}` | De id van het berekende kenmerk dat u wilt verwijderen. |

**Verzoek**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Antwoord**

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. Om de schrapping te bevestigen succesvol was, kunt u een verzoek van de GET om het gegevens verwerkte attribuut door zijn identiteitskaart uit te voeren. Als het kenmerk is verwijderd, ontvangt u een HTTP Status 404 (Not Found)-fout.

## Volgende stappen

Nu u de grondbeginselen van berekende attributen hebt geleerd, bent u klaar om te beginnen bepalend hen voor uw organisatie.