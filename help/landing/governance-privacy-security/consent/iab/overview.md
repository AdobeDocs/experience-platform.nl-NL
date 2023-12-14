---
keywords: Experience Platform;home;IAB;IAB 2.0;toestemming;toestemming
solution: Experience Platform
title: IAB TCF 2.0-ondersteuning in Experience Platform
description: Leer hoe te om uw gegevensverrichtingen en schema's te vormen om de keuzen van de klantentoestemming te brengen wanneer het activeren van segmenten aan bestemmingen in Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: 43b3b79a4d24fd92c7afbf9ca9c83b0cbf80e2c2
workflow-type: tm+mt
source-wordcount: '2505'
ht-degree: 0%

---

# IAB TCF 2.0-ondersteuning in Experience Platform

De [!DNL Transparency & Consent Framework] (TCF), zoals beschreven door [!DNL Interactive Advertising Bureau] (IAB) is een open-standaard technisch kader dat organisaties in staat moet stellen toestemming van de consument voor de verwerking van hun persoonsgegevens te verkrijgen, te registreren en bij te werken, in overeenstemming met het [!DNL General Data Protection Regulation] (GDPR). De tweede iteratie van het framework, TCF 2.0, biedt meer flexibiliteit voor de manier waarop consumenten toestemming kunnen geven of weigeren, inclusief of en hoe leveranciers bepaalde functies van gegevensverwerking kunnen gebruiken, zoals exacte geolocatie.

>[!NOTE]
>
>Meer informatie over TCF 2.0 vindt u op de [IAB Europe-website](https://iabeurope.eu/), met inbegrip van ondersteunende materialen en technische specificaties.

Adobe Experience Platform maakt deel uit van de geregistreerde [IAB TCF 2.0 leverancierslijst](https://iabeurope.eu/vendor-list-tcf/), onder de ID **565**. In overeenstemming met de TCF 2.0-vereisten, kunt u met Platform gegevens voor klanttoestemming verzamelen en deze integreren in uw opgeslagen klantprofielen. Deze toestemmingsgegevens kunnen dan in rekening worden gebracht of de profielen in uitgevoerde publiekssegmenten, afhankelijk van hun gebruiksgeval inbegrepen zijn.

>[!IMPORTANT]
>
>Platform kan slechts aan versie 2.0 van TCF (of groter) voldoen. Eerdere versies van TCF worden niet ondersteund.

Dit document biedt een overzicht van hoe u uw gegevensbewerkingen en profielschema&#39;s kunt configureren voor het accepteren van gegevens voor toestemming van klanten die zijn gegenereerd door uw CMP (Consent Management Platform). Ook wordt uitgelegd hoe Platform keuzes voor gebruikerstoestemming overbrengt bij het exporteren van segmenten.

## Vereisten

Om deze gids te volgen, moet u CMP, of commercieel of uw gebruiken, die geïntegreerd en volgzaam met IAB TCF is. Zie de [Lijst van conforme CMP&#39;s](https://iabeurope.eu/cmp-list/) voor meer informatie .

>[!IMPORTANT]
>
>Als de id van uw CMP ongeldig is, verwerkt Platform uw gegevens ongewijzigd. Om TCF 2.0 af te dwingen, moet u bevestigen dat uw CMP een geldige identiteitskaart heeft die met IAB TCF 2.0 is geregistreerd alvorens gegevens naar Platform te verzenden.

Deze gids vereist ook een werkend inzicht in de volgende diensten van het Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel in realtime](../../../../profile/home.md): Gebruikt [!DNL Identity Service] om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. [!DNL Real-Time Customer Profile] trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Een JavaScript-bibliotheek aan de clientzijde waarmee u verschillende platformservices kunt integreren in uw klantgerichte website.
   * [Opdrachten voor SDK-toestemming](../../../../edge/consent/supporting-consent.md): Een gebruiksscenario-overzicht van de toestemmingsgerelateerde SDK-opdrachten die in deze handleiding worden getoond.
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md): Hiermee kunt u delen [!DNL Real-Time Customer Profile] gegevens in groepen personen die vergelijkbare kenmerken delen en op vergelijkbare wijze reageren op marketingstrategieën.

Naast de hierboven vermelde diensten van het Platform, zou u ook vertrouwd moeten zijn met [bestemmingen](../../../../data-governance/home.md) en hun rol in het ecosysteem van het platform.

## Overzicht van de toestemmingsstroom voor klanten {#summary}

De volgende secties beschrijven hoe de toestemmingsgegevens worden verzameld en afgedwongen nadat het systeem behoorlijk is gevormd.

### Goedgekeurde gegevensverzameling

Het platform staat u toe om de gegevens van de klantentoestemming door het volgende proces te verzamelen:

1. Een klant geeft via een dialoogvenster op uw website zijn voorkeuren voor het verzamelen van gegevens weer.
1. Uw CMP detecteert de wijziging van de voorkeur voor toestemming en genereert dienovereenkomstig TCF gegevens over toestemming.
1. Met behulp van de Platform Web SDK worden de gegenereerde toestemmingsgegevens (geretourneerd door het CMP) verzonden naar Adobe Experience Platform.
1. De verzamelde toestemmingsgegevens worden opgenomen in een [!DNL Profile]-enabled dataset het waarvan schema TCF toestemmingsgebieden bevat.

Naast SDK-opdrachten die worden geactiveerd door de haken voor wijziging van de CMP-toestemming, kunnen toestemmingsgegevens ook in het Experience Platform stromen via door de klant gegenereerde XDM-gegevens die rechtstreeks naar een [!DNL Profile]-enabled dataset.

Alle segmenten die door Adobe Audience Manager met Platform worden gedeeld (via [!DNL Audience Manager] bronaansluiting of anderszins) kan ook toestemmingsgegevens bevatten indien de desbetreffende velden op die segmenten zijn toegepast via [!DNL Experience Cloud Identity Service]. Voor meer informatie over het verzamelen van toestemmingsgegevens in [!DNL Audience Manager], zie het document op de [Adobe Audience Manager-insteekmodule voor IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Goedkeuring stroomafwaarts

Zodra TCF toestemmingsgegevens met succes is opgenomen, vinden de volgende processen in de stroomafwaartse diensten van het Platform plaats:

1. [!DNL Real-Time Customer Profile] werkt de opgeslagen toestemmingsgegevens voor het profiel van die klant bij.
1. Het platform verwerkt klant-id&#39;s alleen als de toestemming van de leverancier voor Platform (565) voor elke id in een cluster is opgegeven.
1. Wanneer het uitvoeren van segmenten aan bestemmingen tot leden van de TCF 2.0 verkoperslijst behoort, omvat het Platform slechts profielen als de verkoperstoestemmingen voor beide Platform (565) *en* de individuele bestemming wordt verstrekt voor elke identiteitskaart in een cluster.

De rest van de secties in dit document verstrekken begeleiding op hoe te om Platform en uw gegevensverrichtingen te vormen om de inzameling en handhavingsvereisten te voldoen die hierboven worden beschreven.

## Bepalen hoe gegevens over klanttoestemming binnen uw CMP worden gegenereerd {#consent-data}

Aangezien elk CMP-systeem uniek is, moet u de beste manier bepalen om uw klanten toestemming te geven wanneer ze met uw service communiceren. Een dialoogvenster voor cookie-toestemming is een algemene manier om de instemming van de klant te verkrijgen. Hieronder ziet u een voorbeeld van een CMP-dialoogvenster.

![Een voorbeeld van het dialoogvenster Consent Management Platform.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

In dit dialoogvenster moet de klant de mogelijkheid hebben om in of uit te gaan van het volgende:

| Goedkeuring, optie | Beschrijving |
| --- | --- |
| **Doelstellingen** | Doel bepaalt voor welke advertentietechnische doeleinden een merk de gegevens van een klant kan gebruiken. Voor Platform moeten de volgende doeleinden worden gekozen om klant-id&#39;s te verwerken: <ul><li>**Doel 1**: Gegevens opslaan en/of openen op een apparaat</li><li>**Doel 10**: Producten ontwikkelen en verbeteren</li></ul> |
| **Machtigingen leverancier** | Naast technische doeleinden moet de dialoog de klant ook de mogelijkheid bieden om ervoor te kiezen om hun gegevens te gebruiken door specifieke leveranciers, waaronder Adobe Experience Platform (565). |

### Constante tekenreeksen {#consent-strings}

Ongeacht de methode u gebruikt om de gegevens te verzamelen, is het doel een koordwaarde te produceren die op de toestemmingsopties wordt gebaseerd die door de klant worden gekozen, genoemd een toestemmingskoord.

In de TCF specificatie, worden de toestemmingskoorden gebruikt om relevante details over de toestemmingsmontages van een klant, in termen van specifieke marketing doeleinden te coderen zoals die door beleid en verkopers worden bepaald. Het platform gebruikt deze koorden om de toestemmingsmontages voor elke klant op te slaan, en daarom moet een nieuwe toestemmingskoord worden geproduceerd telkens als die montages veranderen.

Constante tekenreeksen kunnen alleen worden gemaakt door een CMP die is geregistreerd bij de IAB TCF. Voor meer informatie over hoe u toestemmingsreeksen kunt genereren met behulp van uw specifieke CMP raadpleegt u de [overzicht van tekenreeksindeling voor toestemming](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) in de IAB TCF GitHub repo.

## Gegevenssets maken met TCF-toestemmingsvelden {#datasets}

De gegevens van de toestemming van de klant moeten naar datasets worden verzonden waarvan de schema&#39;s TCF toestemmingsgebieden bevatten. Raadpleeg de zelfstudie op [gegevenssets maken voor het vastleggen van TCF 2.0-toestemming](./dataset.md) voor hoe te om de vereiste profieldataset (en een facultatieve dataset van de Gebeurtenis van de Ervaring) tot stand te brengen alvorens met deze gids verder te gaan.

## Bijwerken [!DNL Profile] beleid samenvoegen om toestemmingsgegevens op te nemen {#merge-policies}

Als u eenmaal een [!DNL Profile]- de toegelaten dataset voor het verzamelen van toestemmingsgegevens, moet u ervoor zorgen dat uw fusiebeleid is gevormd om TCF toestemmingsgebieden in uw klantenprofielen altijd te omvatten. Dit impliceert het plaatsen van datasetbelangrijkheid zodat uw toestemmingsdataset boven andere potentieel conflicterende datasets voorrang krijgt.

Raadpleeg voor meer informatie over het werken met samenvoegbeleid de [overzicht van samenvoegbeleid](../../../../profile/merge-policies/overview.md). Wanneer u het samenvoegbeleid instelt, moet u ervoor zorgen dat alle segmenten alle vereiste toestemmingskenmerken bevatten die door de [XDM-veldgroep met privacyschema](./dataset.md#privacy-field-group), zoals uiteengezet in de handleiding voor de opstelling van gegevensverzamelingen.

## Integreer de SDK van het Web van het Experience Platform om gegevens van de klantentoestemming te verzamelen {#sdk}

>[!NOTE]
>
>Het gebruik van het Web SDK van het Experience Platform wordt vereist om toestemmingsgegevens direct in Adobe Experience Platform te verwerken. [!DNL Experience Cloud Identity Service] wordt niet ondersteund.
>
>[!DNL Experience Cloud Identity Service] wordt echter nog steeds ondersteund voor de verwerking van toestemming in Adobe Audience Manager en naleving van TCF 2.0 vereist alleen dat de bibliotheek wordt bijgewerkt naar [versie 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Zodra u uw CMP hebt gevormd om toestemmingskoorden te produceren, moet u het Web SDK van het Experience Platform integreren om die koorden te verzamelen en hen te verzenden naar Platform. De Platform SDK verstrekt twee bevelen die kunnen worden gebruikt om TCF toestemmingsgegevens naar Platform (die in de hieronder subsecties worden verklaard) te verzenden. Deze bevelen zouden moeten worden gebruikt wanneer een klant toestemmingsinformatie voor het eerst verstrekt, en om het even welk ogenblik dat de toestemming daarna verandert.

**De SDK interface niet met CMP&#39;s uit het vak**. Het is aan u om te bepalen hoe te om SDK in uw website te integreren, naar toestemmingsveranderingen in CMP te luisteren, en het aangewezen bevel te roepen.

### Een gegevensstroom maken

SDK kan alleen gegevens naar Experience Platform verzenden als u eerst een gegevensstroom voor Platform maakt. De specifieke stappen voor hoe te om een gegevensstroom tot stand te brengen worden verstrekt in [SDK-documentatie](../../../../datastreams/overview.md).

Nadat u een unieke naam voor de gegevensstroom hebt opgegeven, selecteert u de schakelknop naast **[!UICONTROL Adobe Experience Platform]**. Gebruik vervolgens de volgende waarden om de rest van het formulier in te vullen:

| Veld DataStream | Waarde |
| --- | --- |
| [!UICONTROL Sandbox] | De naam van het platform [sandbox](../../../../sandboxes/home.md) die de vereiste het stromen verbinding en datasets aan opstelling de gegevensstroom bevat. |
| [!UICONTROL Streaming Inlet] | Een geldige streamingverbinding voor Experience Platform. Zie de zelfstudie aan [streaming verbinding maken](../../../../ingestion/tutorials/create-streaming-connection-ui.md) als u geen bestaande streaminginlaat hebt. |
| [!UICONTROL Event Dataset] | Selecteer de [!DNL XDM ExperienceEvent] dataset die in [vorige stap](#datasets). Als u het [[!UICONTROL IAB TCF 2.0 Consent] veldgroep](../../../../xdm/field-groups/event/iab.md) in het schema van deze dataset, kunt u toestemming-verandering gebeurtenissen in tijd volgen gebruikend [`sendEvent`](#sendEvent) bevel, die dat gegevens in deze dataset opslaat. Houd er rekening mee dat de in deze gegevensset opgeslagen toestemmingswaarden **niet** gebruikt in automatische handhavingswerkstromen. |
| [!UICONTROL Profile Dataset] | Selecteer de [!DNL XDM Individual Profile] dataset die in [vorige stap](#datasets). Wanneer wordt gereageerd op CMP visiewisselhaken met de functie [`setConsent`](#setConsent) bevel, worden de verzamelde gegevens opgeslagen in deze dataset. Aangezien deze dataset profiel-toegelaten is, worden de toestemmingswaarden die in deze dataset worden opgeslagen gehouden tijdens automatische handhavingswerkschema&#39;s. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Selecteer **[!UICONTROL Save]** onder aan het scherm en doorgaan met het volgen van eventuele extra vragen om de configuratie te voltooien.

### Opdrachten voor wijzigen van toestemming maken

Nadat u de in de vorige sectie beschreven gegevensstroom hebt gemaakt, kunt u beginnen met het gebruik van SDK-opdrachten voor het verzenden van toestemmingsgegevens naar Platform. De volgende secties verstrekken voorbeelden van hoe elk bevel van SDK in verschillende scenario&#39;s kan worden gebruikt.

>[!NOTE]
>
>Voor een inleiding aan de gemeenschappelijke syntaxis voor alle bevelen van SDK van het Platform, zie het document op [uitvoeren, opdrachten](../../../../edge/fundamentals/executing-commands.md).

#### Kantaarnhaken voor wijziging van CMP-toestemming gebruiken {#setConsent}

Vele CMPs verstrekt uit-van-de-doos haken die aan toestemmings-verandering gebeurtenissen luisteren. Wanneer deze gebeurtenissen zich voordoen, kunt u de opdracht `setConsent` gebruiken om de gegevens van de toestemming van die klant bij te werken.

De `setConsent` bevel verwacht twee argumenten:

1. Een tekenreeks die het opdrachttype aangeeft (in dit geval &quot;setConsent&quot;).
1. Een lading die een `consent` array. De array moet ten minste één object bevatten dat de vereiste toestemmingsvelden bevat.

De `setConsent` wordt hieronder weergegeven:

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
| `standard` | De gebruikte toestemmingsnorm. Deze waarde moet worden ingesteld op `IAB` voor TCF 2.0 toestemmingsverwerking. |
| `version` | Het versienummer van de krachtens `standard`. Deze waarde moet worden ingesteld op `2.0` voor TCF 2.0 toestemmingsverwerking. |
| `value` | De basis-64-gecodeerde toestemmingstekenreeks die door CMP wordt geproduceerd. |
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. Voor TCF 2.0 die voor deze klant moet worden afgedwongen, moet de waarde worden geplaatst aan `true`. Standaardwaarden: `true` indien niet gedefinieerd. |

De `setConsent` gebruiken als onderdeel van een CMP-haak die wijzigingen in de toestemmingsinstellingen detecteert. In het volgende JavaScript ziet u hoe het `setConsent` kan worden gebruikt voor OneTrust&#39;s `OnConsentChanged` haak:

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

U kunt TCF 2.0 toestemmingsgegevens over elke gebeurtenis ook verzamelen teweeggebracht in Platform door te gebruiken `sendEvent` gebruiken.

>[!NOTE]
>
>Als u deze methode wilt gebruiken, moet u de het gebiedsgroep van de Privacy van de Gebeurtenis van de Ervaring aan uw hebben toegevoegd [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] schema. Zie de sectie over [het bijwerken van het schema ExperienceEvent](./dataset.md#event-schema) in de de voorbereidingsgids van de dataset voor stappen op hoe te om dit te vormen.

De `sendEvent` moet worden gebruikt als een callback in de juiste gebeurtenislisteners op uw website. De opdracht verwacht twee argumenten: (1) een tekenreeks die het opdrachttype aangeeft (in dit geval: `sendEvent`), en (2) een lading die een `xdm` object dat de vereiste toestemmingsvelden als JSON biedt:

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
| `consentStandard` | De gebruikte toestemmingsnorm. Deze waarde moet worden ingesteld op `IAB` voor TCF 2.0 toestemmingsverwerking. |
| `consentStandardVersion` | Het versienummer van de krachtens `standard`. Deze waarde moet worden ingesteld op `2.0` voor TCF 2.0 toestemmingsverwerking. |
| `consentStringValue` | De basis-64-gecodeerde toestemmingstekenreeks die door CMP wordt geproduceerd. |
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. Voor TCF 2.0 die voor deze klant moet worden afgedwongen, moet de waarde worden geplaatst aan `true`. Standaardwaarden: `true` indien niet gedefinieerd. |

### Reacties in SDK verwerken

Alles [!DNL Platform SDK] de bevelen keren beloftes terug die erop wijzen of de vraag slaagde of ontbrak. U kunt deze reacties vervolgens gebruiken voor extra logica, zoals het weergeven van bevestigingsberichten aan de klant. Zie de sectie over [afhandeling gelukt of mislukt](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) in de handleiding voor het uitvoeren van SDK-opdrachten voor specifieke voorbeelden.

## Segmenten exporteren {#export}

>[!NOTE]
>
>Voordat u begint met het exporteren van segmenten, moet u ervoor zorgen dat uw segmenten alle vereiste machtigingsvelden bevatten. Zie de sectie over [samenvoegbeleid configureren](#merge-policies) voor meer informatie .

Zodra u de gegevens van de klantentoestemming hebt verzameld en publiekssegmenten gecreeerd die de vereiste toestemmingsattributen bevatten, kunt u TCF 2.0 naleving dan afdwingen wanneer het uitvoeren van die segmenten naar stroomafwaartse bestemmingen.

Indien de instelling van de toestemming `gdprApplies` is ingesteld op `true` voor een reeks klantprofielen, worden om het even welke gegevens van die profielen die naar stroomafwaartse bestemmingen worden uitgevoerd gefiltreerd gebaseerd op de toestemmingsvoorkeur TCF voor elk profiel. Elk profiel dat niet voldoet aan de vereiste voorkeuren voor toestemming wordt tijdens het exportproces overgeslagen.

Klanten moeten instemmen met de volgende doeleinden (zoals beschreven door [TCF 2.0-beleid](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) voor profielen die moeten worden opgenomen in segmenten die naar bestemmingen worden geëxporteerd:

* **Doel 1**: Gegevens opslaan en/of openen op een apparaat
* **Doel 10**: Producten ontwikkelen en verbeteren

TCF 2.0 vereist ook dat de bron van gegevens de de verkoperstoestemming van de bestemming moet controleren alvorens gegevens naar die bestemming te verzenden. Als dusdanig, controleert het Platform als de de verkoperstoestemming van de bestemming binnen aan voor alle IDs in de cluster alvorens gegevens te omvatten die aan die bestemming worden gebonden.

>[!NOTE]
>
>Om het even welke segmenten die met Adobe Audience Manager worden gedeeld bevatten de zelfde TCF 2.0 toestemmingswaarden zoals hun tegenhangers van het Platform. Sinds [!DNL Audience Manager] deelt dezelfde leverancier-id als Platform (565), dezelfde doeleinden en toestemming van de leverancier zijn vereist. Zie het document op de [Adobe Audience Manager-insteekmodule voor IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) voor meer informatie .

## Implementatie testen {#test-implementation}

Zodra u uw implementatie TCF 2.0 hebt gevormd en segmenten naar bestemmingen uitgevoerd, zullen om het even welke gegevens die toestemmingsvereisten niet voldoen niet worden uitgevoerd. Om te zien of de correcte klantenprofielen tijdens de uitvoer werden gefiltreerd, moet u de gegevensopslag op uw bestemmingen manueel controleren om te zien of werd de toestemming behoorlijk afgedwongen.

>[!IMPORTANT]
>
>Als meerdere id&#39;s een cluster vormen en TCF 2.0 van toepassing is, wordt de gehele cluster uitgesloten als zelfs één id niet de juiste doelen en machtigingen van de leverancier bevat.

## Volgende stappen

Dit document behandelde het proces om uw gegevensverrichtingen van het Platform te vormen om aan uw bedrijfsverplichtingen te voldoen zoals die door TCF 2.0 worden geschetst. Zie het overzicht op [bestuur, privacy en veiligheid](../../overview.md) voor meer informatie over de mogelijkheden van het platform op het gebied van privacy.
