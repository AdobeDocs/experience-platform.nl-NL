---
keywords: Experience Platform;home;IAB;IAB 2.0;toestemming;Toestemming
solution: Experience Platform
title: IAB TCF 2.0-ondersteuning in Experience Platform
description: Leer hoe te om uw gegevensverrichtingen en schema's te vormen om de keuzen van de klantentoestemming te brengen wanneer het activeren van segmenten aan bestemmingen in Adobe Experience Platform.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2509'
ht-degree: 0%

---

# IAB TCF 2.0-ondersteuning in Experience Platform

De [!DNL Transparency & Consent Framework] (TCF), zoals geschetst door [!DNL Interactive Advertising Bureau] (IAB), is een open-standaard technisch kader dat organisaties in staat stelt om toestemming van de consument voor de verwerking van hun persoonsgegevens te verkrijgen, te registreren en bij te werken, in overeenstemming met de [!DNL General Data Protection Regulation] -norm (GDPR) van de Europese Unie. De tweede iteratie van het framework, TCF 2.0, biedt meer flexibiliteit voor de manier waarop consumenten toestemming kunnen geven of weigeren, inclusief of en hoe leveranciers bepaalde functies van gegevensverwerking kunnen gebruiken, zoals exacte geolocatie.

>[!NOTE]
>
>Meer informatie over TCF 2.0 kan op de [ IAB Europa website ](https://iabeurope.eu/), met inbegrip van steunmaterialen en technische specificaties worden gevonden.

Adobe Experience Platform maakt deel uit van de geregistreerde [ IAB TCF 2.0 verkoperslijst ](https://iabeurope.eu/vendor-list-tcf/), onder identiteitskaart **565**. In overeenstemming met de TCF 2.0-vereisten kunt u met Experience Platform gegevens over toestemming van klanten verzamelen en deze integreren in uw opgeslagen klantprofielen. Deze toestemmingsgegevens kunnen dan in rekening worden gebracht of de profielen in uitgevoerde publiekssegmenten, afhankelijk van hun gebruiksgeval inbegrepen zijn.

>[!IMPORTANT]
>
>Experience Platform kan alleen voldoen aan versie 2.0 van de TCF (of hoger). Eerdere versies van TCF worden niet ondersteund.

Dit document biedt een overzicht van hoe u uw gegevensbewerkingen en profielschema&#39;s kunt configureren voor het accepteren van gegevens voor toestemming van klanten die zijn gegenereerd door uw CMP (Consent Management Platform). Het behandelt ook hoe Experience Platform keuzes voor gebruikersgoedkeuring bij het exporteren van segmenten overbrengt.

## Vereisten

Om deze gids te volgen, moet u CMP, of commercieel of uw gebruiken, die geïntegreerd en volgzaam met IAB TCF is. Zie de [ lijst van volgzame CMPs ](https://iabeurope.eu/cmp-list/) voor meer informatie.

>[!IMPORTANT]
>
>Als de id van uw CMP ongeldig is, verwerkt Experience Platform uw gegevens ongewijzigd. Om TCF 2.0 af te dwingen, moet u bevestigen dat uw CMP een geldige identiteitskaart heeft die met IAB TCF 2.0 is geregistreerd alvorens gegevens naar Experience Platform te verzenden.

Deze handleiding vereist ook een goed begrip van de volgende Experience Platform-services:

* [ Model van de Gegevens van de Ervaring (XDM) ](/help/xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
* [ de Dienst van de Identiteit van Adobe Experience Platform ](/help/identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [ Real-Time Profiel van de Klant ](/help/profile/home.md): Gebruik [!DNL Identity Service] om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. [!DNL Real-Time Customer Profile] haalt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [ Adobe Experience Platform Web SDK ](/help/web-sdk/home.md): Een cliënt-kant bibliotheek van JavaScript die u toestaat om diverse diensten van Experience Platform in uw klant-onder ogen ziet website te integreren.
   * [ de toestemmingsbevelen van SDK ](../../../../web-sdk/commands/setconsent.md): Een gebruik-geval overzicht van de toestemming-verwante bevelen van SDK die in deze gids worden getoond.
* [ de Dienst van de Segmentatie van Adobe Experience Platform ](/help/segmentation/home.md): Staat u toe om [!DNL Real-Time Customer Profile] gegevens in groepen individuen te verdelen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën antwoorden.

Naast de hierboven vermelde diensten van Experience Platform, zou u met [ bestemmingen ](/help/data-governance/home.md) en hun rol in het ecosysteem van Experience Platform ook vertrouwd moeten zijn.

## Overzicht van de toestemmingsstroom voor klanten {#summary}

De volgende secties beschrijven hoe de toestemmingsgegevens worden verzameld en afgedwongen nadat het systeem behoorlijk is gevormd.

### Goedgekeurde gegevensverzameling

Experience Platform biedt u de mogelijkheid om gegevens over uw toestemming te verzamelen via het volgende proces:

1. Een klant geeft via een dialoogvenster op uw website zijn voorkeuren voor het verzamelen van gegevens weer.
1. Uw CMP detecteert de wijziging van de voorkeur voor toestemming en genereert dienovereenkomstig TCF gegevens over toestemming.
1. Met behulp van de Experience Platform Web SDK worden de gegenereerde toestemmingsgegevens (die door het CMP worden geretourneerd) naar Adobe Experience Platform verzonden.
1. De verzamelde toestemmingsgegevens worden opgenomen in een [!DNL Profile]-Toegelaten dataset het waarvan schema TCF toestemmingsgebieden bevat.

Naast SDK-opdrachten die worden geactiveerd door de haken voor wijziging van de toestemming van CMP, kunnen toestemmingsgegevens ook naar Experience Platform stromen via door de klant gegenereerde XDM-gegevens die rechtstreeks naar een [!DNL Profile] -gegevensset worden geüpload.

Alle segmenten die Adobe Audience Manager met Experience Platform deelt (via de [!DNL Audience Manager] source connector of anderszins) kunnen ook gegevens over de toestemming bevatten als de desbetreffende velden op die segmenten zijn toegepast via [!DNL Experience Cloud Identity Service] . Voor meer informatie bij het verzamelen van toestemmingsgegevens in [!DNL Audience Manager], zie het document op het [ elektrische toestel van Adobe Audience Manager voor IAB TCF ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Goedkeuring stroomafwaarts

Zodra TCF toestemmingsgegevens met succes is opgenomen, vinden de volgende processen in stroomafwaartse diensten van Experience Platform plaats:

1. [!DNL Real-Time Customer Profile] werkt de opgeslagen toestemmingsgegevens voor het profiel van die klant bij.
1. Experience Platform verwerkt klant-id&#39;s alleen als de machtiging van de leverancier voor Experience Platform (565) is opgegeven voor elke id in een cluster.
1. Wanneer het uitvoeren van segmenten aan bestemmingen tot leden van de TCF 2.0 verkoperslijst behoren, omvat Experience Platform slechts profielen als de verkoperstoestemmingen voor zowel Experience Platform (565) *en* de individuele bestemming voor elke identiteitskaart in een cluster worden verstrekt.

De rest van de secties in dit document biedt richtlijnen voor het configureren van Experience Platform en uw gegevensbewerkingen om te voldoen aan de hierboven beschreven vereisten voor verzameling en handhaving.

## Bepalen hoe gegevens over klanttoestemming binnen uw CMP worden gegenereerd {#consent-data}

Aangezien elk CMP-systeem uniek is, moet u de beste manier bepalen om uw klanten toestemming te geven wanneer ze met uw service communiceren. Een dialoogvenster voor cookie-toestemming is een algemene manier om de instemming van de klant te verkrijgen. Hieronder ziet u een voorbeeld van een CMP-dialoogvenster.

![ een dialoog van het Platform van het Beheer van de voorbeeldgoedkeuring.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

In dit dialoogvenster moet de klant de mogelijkheid hebben om in of uit te gaan van het volgende:

| Goedkeuring, optie | Beschrijving |
| --- | --- |
| **Doelen** | Doel bepaalt voor welke advertentietechnische doeleinden een merk de gegevens van een klant kan gebruiken. Voor Experience Platform moet u de volgende doeleinden kiezen om de klant-id&#39;s te verwerken: <ul><li>**Doel 1**: Bewaar en/of toegangsinformatie over een apparaat</li><li>**Doel 10**: Ontwikkelen en verbeteren producten</li></ul> |
| **de toestemmingen van de Leverancier** | Naast technische doeleinden moet de dialoog de klant ook de mogelijkheid bieden om ervoor te kiezen om hun gegevens te gebruiken door specifieke leveranciers, waaronder Adobe Experience Platform (565). |

### Constante tekenreeksen {#consent-strings}

Ongeacht de methode u gebruikt om de gegevens te verzamelen, is het doel een koordwaarde te produceren die op de toestemmingsopties wordt gebaseerd die door de klant worden gekozen, genoemd een toestemmingskoord.

In de TCF specificatie, worden de toestemmingskoorden gebruikt om relevante details over de toestemmingsmontages van een klant, in termen van specifieke marketing doeleinden te coderen zoals die door beleid en verkopers worden bepaald. Experience Platform gebruikt deze tekenreeksen om de toestemmingsmontages voor elke klant op te slaan, en daarom moet een nieuwe toestemmingskoord worden geproduceerd telkens als die montages veranderen.

Constante tekenreeksen kunnen alleen worden gemaakt door een CMP die is geregistreerd bij de IAB TCF. Voor meer informatie over hoe te om toestemmingskoorden te produceren gebruikend uw bepaald CMP, verwijs naar het [ koord van de toestemming formatterende gids ](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) in de IAB TCF reactie GitHub.

## Gegevenssets maken met TCF-toestemmingsvelden {#datasets}

De gegevens van de toestemming van de klant moeten naar datasets worden verzonden waarvan de schema&#39;s TCF toestemmingsgebieden bevatten. Verwijs naar het leerprogramma op [ het creëren van datasets voor het vangen van de toestemming TCF 2.0 ](./dataset.md) voor hoe te om de vereiste profieldataset (en een facultatieve dataset van de Gebeurtenis van de Ervaring) tot stand te brengen alvorens met deze gids verder te gaan.

## Beleid voor samenvoegen van [!DNL Profile] bijwerken en gegevens over toestemming opnemen {#merge-policies}

Zodra u een [!DNL Profile]-Toegelaten dataset voor het verzamelen van toestemmingsgegevens hebt gecreeerd, moet u ervoor zorgen dat uw samenvoegingsbeleid is gevormd om TCF toestemmingsgebieden in uw klantenprofielen altijd te omvatten. Dit impliceert het plaatsen van datasetbelangrijkheid zodat uw toestemmingsdataset boven andere potentieel conflicterende datasets voorrang krijgt.

Voor meer informatie over hoe te met fusiebeleid te werken, verwijs naar het [ overzicht van het fusiebeleid ](/help/profile/merge-policies/overview.md). Wanneer vestiging moet uw samenvoegbeleid, u ervoor zorgen dat uw segmenten alle vereiste toestemmingsattributen omvatten die door de [ worden verstrekt de groep van het het privacyschemagebied van XDM ](./dataset.md#privacy-field-group), zoals die in de gids over datasetvoorbereiding wordt geschetst.

## Integreer de Experience Platform Web SDK om gegevens over klanttoestemming te verzamelen {#sdk}

>[!NOTE]
>
>Het gebruik van de Experience Platform Web SDK is vereist om toestemmingsgegevens direct in Adobe Experience Platform te verwerken. [!DNL Experience Cloud Identity Service] wordt niet ondersteund.
>
>[!DNL Experience Cloud Identity Service] wordt nog gesteund voor toestemmingsverwerking in Adobe Audience Manager, echter, en de naleving van TCF 2.0 vereist slechts dat de bibliotheek aan [ versie 5.0 ](https://github.com/Adobe-Marketing-Cloud/id-service/releases) wordt bijgewerkt.

Nadat u uw CMP hebt geconfigureerd voor het genereren van toestemmingstekenreeksen, moet u de Experience Platform Web SDK integreren om deze tekenreeksen te verzamelen en naar Experience Platform te verzenden. De Experience Platform SDK biedt twee opdrachten die kunnen worden gebruikt om TCF-gegevens voor toestemming naar Experience Platform te verzenden (zie de onderstaande subsecties). Deze bevelen zouden moeten worden gebruikt wanneer een klant toestemmingsinformatie voor het eerst verstrekt, en om het even welk ogenblik dat de toestemming daarna verandert.

**SDK interface niet met om het even welke CMPs uit de doos**. Het is aan u om te bepalen hoe te om de SDK in uw website te integreren, naar toestemmingsveranderingen in CMP te luisteren, en het aangewezen bevel te roepen.

### Een gegevensstroom maken

Als u wilt dat de SDK gegevens naar Experience Platform verzendt, moet u eerst een gegevensstroom voor Experience Platform maken. De specifieke stappen voor hoe te om tot een gegevensstroom te leiden worden verstrekt in de [ documentatie van SDK ](/help/datastreams/overview.md).

Nadat u een unieke naam voor de gegevensstroom hebt opgegeven, selecteert u de schakelknop naast **[!UICONTROL Adobe Experience Platform]** . Gebruik vervolgens de volgende waarden om de rest van het formulier in te vullen:

| Veld DataStream | Waarde |
| --- | --- |
| [!UICONTROL Sandbox] | De naam van de zandbak van Experience Platform [ ](/help/sandboxes/home.md) die de vereiste het stromen verbinding en datasets aan opstelling bevat de datastream. |
| [!UICONTROL Streaming Inlet] | Een geldige streamingverbinding voor Experience Platform. Zie het leerprogramma op [ het creëren van een het stromen verbinding ](/help/ingestion/tutorials/create-streaming-connection-ui.md) als u geen bestaande het stromen inlaat hebt. |
| [!UICONTROL Event Dataset] | Selecteer de [!DNL XDM ExperienceEvent] dataset die in de [ vorige stap ](#datasets) wordt gecreeerd. Als u de [[!UICONTROL IAB TCF 2.0 Consent] gebiedsgroep ](/help/xdm/field-groups/event/iab.md) in het schema van deze dataset omvatte, kunt u toestemming-verandering gebeurtenissen in tijd volgen gebruikend het [`sendEvent`](#sendEvent) bevel, die gegevens in deze dataset opslaan. Onthoud dat de toestemmingswaarden die in deze dataset worden opgeslagen **niet** worden gebruikt in automatische handhavingswerkschema&#39;s. |
| [!UICONTROL Profile Dataset] | Selecteer de [!DNL XDM Individual Profile] dataset die in de [ vorige stap ](#datasets) wordt gecreeerd. Wanneer wordt gereageerd op de koppeling voor het wijzigen van de toestemming van CMP met de opdracht [`setConsent`](#setConsent) , worden de verzamelde gegevens opgeslagen in deze gegevensset. Aangezien deze dataset profiel-toegelaten is, worden de toestemmingswaarden die in deze dataset worden opgeslagen gehouden tijdens automatische handhavingswerkschema&#39;s. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Als u klaar bent, selecteert u **[!UICONTROL Save]** onder aan het scherm en gaat u verder met het volgen van eventuele extra aanwijzingen om de configuratie te voltooien.

### Opdrachten voor wijzigen van toestemming maken

Nadat u de in de vorige sectie beschreven gegevensstroom hebt gemaakt, kunt u SDK-opdrachten gebruiken om gegevens over de toestemming naar Experience Platform te verzenden. In de onderstaande secties ziet u voorbeelden van de manier waarop elke SDK-opdracht in verschillende scenario&#39;s kan worden gebruikt.

#### Kantaarnhaken voor wijziging van CMP-toestemming gebruiken {#setConsent}

Vele CMPs verstrekt uit-van-de-doos haken die aan toestemmings-verandering gebeurtenissen luisteren. Wanneer deze gebeurtenissen zich voordoen, kunt u de opdracht [`setConsent`](/help/web-sdk/commands/setconsent.md) gebruiken om de gegevens voor toestemming van die klant bij te werken.

De opdracht `setConsent` verwacht twee argumenten:

1. Een tekenreeks die het opdrachttype aangeeft (in dit geval &quot;setConsent&quot;).
1. Een lading die een `consent` serie bevat. De array moet ten minste één object bevatten dat de vereiste toestemmingsvelden bevat.

De opdracht `setConsent` wordt hieronder weergegeven:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Payload, eigenschap | Beschrijving |
| --- | --- |
| `standard` | De gebruikte toestemmingsnorm. Deze waarde moet worden ingesteld op `IAB` voor verwerking van TCF 2.0-toestemming. |
| `version` | Het versienummer van de toestemmingsnorm die onder `standard` wordt vermeld. Deze waarde moet worden ingesteld op `2.0` voor verwerking van TCF 2.0-toestemming. |
| `value` | De basis-64-gecodeerde toestemmingstekenreeks die door CMP wordt geproduceerd. |
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. TCF 2.0 moet voor deze klant worden afgedwongen, de waarde aan `true` worden geplaatst. De standaardwaarde is `true` als deze niet is gedefinieerd. |

De opdracht `setConsent` moet worden gebruikt als onderdeel van een CMP-haak die wijzigingen in toestemmingsinstellingen detecteert. In de volgende JavaScript ziet u hoe de opdracht `setConsent` kan worden gebruikt voor de `OnConsentChanged` -haak van OneTrust:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Gebeurtenissen gebruiken {#sendEvent}

U kunt TCF 2.0 toestemmingsgegevens over elke gebeurtenis ook verzamelen die in Experience Platform door het `sendEvent` bevel wordt teweeggebracht te gebruiken.

>[!NOTE]
>
>Als u deze methode wilt gebruiken, moet u de het gebiedsgroep van de Privacy van de Gebeurtenis van de Ervaring aan uw [!DNL Profile] - toegelaten [!DNL XDM ExperienceEvent] schema hebben toegevoegd. Zie de sectie op [ het bijwerken van het schema ExperienceEvent ](./dataset.md#event-schema) in de gids van de datasetvoorbereiding voor stappen op hoe te om dit te vormen.

De opdracht `sendEvent` moet worden gebruikt als een callback in de juiste gebeurtenislisteners op uw website. De opdracht verwacht twee argumenten: (1) een tekenreeks die het opdrachttype aangeeft (in dit geval `sendEvent` ) en (2) een payload die een `xdm` -object bevat dat de vereiste toestemmingsvelden bevat als JSON:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Payload, eigenschap | Beschrijving |
| --- | --- |
| `xdm.consentStrings` | Een array die ten minste één object moet bevatten dat de vereiste toestemmingsvelden bevat. |
| `consentStandard` | De gebruikte toestemmingsnorm. Deze waarde moet worden ingesteld op `IAB` voor verwerking van TCF 2.0-toestemming. |
| `consentStandardVersion` | Het versienummer van de toestemmingsnorm die onder `standard` wordt vermeld. Deze waarde moet worden ingesteld op `2.0` voor verwerking van TCF 2.0-toestemming. |
| `consentStringValue` | De basis-64-gecodeerde toestemmingstekenreeks die door CMP wordt geproduceerd. |
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. TCF 2.0 moet voor deze klant worden afgedwongen, de waarde aan `true` worden geplaatst. De standaardwaarde is `true` als deze niet is gedefinieerd. |

### SDK-reacties verwerken

Vele bevelen van SDK van het Web keren beloftes terug die erop wijzen of de vraag slaagde of ontbrak. U kunt deze reacties vervolgens gebruiken voor extra logica, zoals het weergeven van bevestigingsberichten aan de klant. Zie [ reacties van het Bevel ](/help/web-sdk/commands/command-responses.md) voor meer informatie.

## Segmenten exporteren {#export}

>[!NOTE]
>
>Voordat u begint met het exporteren van segmenten, moet u ervoor zorgen dat uw segmenten alle vereiste machtigingsvelden bevatten. Zie de sectie over [ het vormen fusiebeleid ](#merge-policies) voor meer informatie.

Zodra u de gegevens van de klantentoestemming hebt verzameld en publiekssegmenten gecreeerd die de vereiste toestemmingsattributen bevatten, kunt u TCF 2.0 naleving dan afdwingen wanneer het uitvoeren van die segmenten naar stroomafwaartse bestemmingen.

Als de instelling voor toestemming `gdprApplies` is ingesteld op `true` voor een set klantprofielen, worden alle gegevens van die profielen die worden geëxporteerd naar downstreamdoelen, gefilterd op basis van de TCF-voorkeuren voor toestemming voor elk profiel. Elk profiel dat niet voldoet aan de vereiste voorkeuren voor toestemming wordt tijdens het exportproces overgeslagen.

De klanten moeten met de volgende doeleinden (zoals die door [ worden geschetst 2.0 beleid TCF ](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) voor hun profielen toestemming geven om in segmenten worden omvat die naar bestemmingen worden uitgevoerd:

* **Doel 1**: Bewaar en/of toegangsinformatie over een apparaat
* **Doel 10**: Ontwikkelen en verbeteren producten

TCF 2.0 vereist ook dat de bron van gegevens de de verkoperstoestemming van de bestemming moet controleren alvorens gegevens naar die bestemming te verzenden. Als dusdanig, controleert Experience Platform of de verkoperstoestemming van de bestemming binnen aan voor alle IDs in de cluster alvorens gegevens te omvatten die aan die bestemming worden gebonden.

>[!NOTE]
>
>Om het even welke segmenten die met Adobe Audience Manager worden gedeeld bevatten de zelfde TCF 2.0 toestemmingswaarden zoals hun Experience Platform tegenhangers. Aangezien [!DNL Audience Manager] dezelfde leverancier-id heeft als Experience Platform (565), zijn dezelfde doeleinden en machtiging van de leverancier vereist. Zie het document op het [ elektrische toestel van Adobe Audience Manager voor IAB TCF ](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) voor meer informatie.

## Implementatie testen {#test-implementation}

Zodra u uw implementatie TCF 2.0 hebt gevormd en segmenten naar bestemmingen uitgevoerd, zullen om het even welke gegevens die toestemmingsvereisten niet voldoen niet worden uitgevoerd. Om te zien of de correcte klantenprofielen tijdens de uitvoer werden gefiltreerd, moet u de gegevensopslag op uw bestemmingen manueel controleren om te zien of werd de toestemming behoorlijk afgedwongen.

>[!IMPORTANT]
>
>Als meerdere id&#39;s een cluster vormen en TCF 2.0 van toepassing is, wordt de gehele cluster uitgesloten als zelfs één id niet de juiste doelen en machtigingen van de leverancier bevat.

## Volgende stappen

In dit document wordt beschreven hoe u uw Experience Platform-gegevensbewerkingen configureert om aan uw zakelijke verplichtingen te voldoen, zoals beschreven in TCF 2.0. Zie het overzicht op [ bestuur, privacy, en veiligheid ](../../overview.md) voor meer informatie Experience Platform op privacy betrekking hebbende mogelijkheden.
