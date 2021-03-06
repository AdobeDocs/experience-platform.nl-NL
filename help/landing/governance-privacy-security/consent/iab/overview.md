---
keywords: Experience Platform;home;IAB;IAB 2.0;toestemming;toestemming
solution: Experience Platform
title: IAB TCF 2.0-ondersteuning in Experience Platform
topic-legacy: privacy events
description: Leer hoe te om uw gegevensverrichtingen en schema's te vormen om de keuzen van de klantentoestemming te brengen wanneer het activeren van segmenten aan bestemmingen in Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 0%

---

# IAB TCF 2.0-ondersteuning in Experience Platform

De [!DNL Transparency & Consent Framework] (TCF), zoals beschreven door de [!DNL Interactive Advertising Bureau] (IAB) is een open-standaard technisch kader dat organisaties in staat moet stellen toestemming van de consument voor de verwerking van hun persoonsgegevens te verkrijgen, te registreren en bij te werken, in overeenstemming met het [!DNL General Data Protection Regulation] (GDPR). De tweede iteratie van het framework, TCF 2.0, biedt meer flexibiliteit voor de manier waarop consumenten toestemming kunnen geven of weigeren, inclusief of en hoe leveranciers bepaalde functies van gegevensverwerking kunnen gebruiken, zoals exacte geolocatie.

>[!NOTE]
>
>Meer informatie over TCF 2.0 vindt u op de [IAB Europe-website](https://iabeurope.eu/tcf-2-0/), met inbegrip van ondersteunende materialen en technische specificaties.

Adobe Experience Platform maakt deel uit van de geregistreerde [IAB TCF 2.0 leverancierslijst](https://iabeurope.eu/vendor-list-tcf-v2-0/), onder de ID **565**. In overeenstemming met de TCF 2.0-vereisten, kunt u met Platform gegevens over toestemming van klanten verzamelen en deze integreren in uw opgeslagen klantprofielen. Deze toestemmingsgegevens kunnen dan in rekening worden gebracht of de profielen in uitgevoerde publiekssegmenten, afhankelijk van hun gebruiksgeval inbegrepen zijn.

>[!IMPORTANT]
>
>Platform kan alleen voldoen aan versie 2.0 van de TCF (of hoger). Eerdere versies van TCF worden niet ondersteund.

Dit document biedt een overzicht van hoe u uw gegevensbewerkingen en profielschema&#39;s kunt configureren om gegevens voor klanttoestemming te accepteren die door uw CMP worden gegenereerd, en hoe het Platform keuzes voor gebruikersmachtigingen laat zien bij het exporteren van segmenten.

## Vereisten

Om deze gids te volgen, moet u een Platform van het Beheer van de Toestemming (CMP), of commercieel of uw gebruiken, gebruiken die met IAB TCF wordt ge??ntegreerd en volgzaam is. Zie de [Lijst van conforme CMP&#39;s](https://iabeurope.eu/cmp-list/) voor meer informatie .

>[!IMPORTANT]
>
>Als de id van uw CMP ongeldig is, blijven de gegevens ongewijzigd door het Platform worden verwerkt. Om TCF 2.0 af te dwingen, moet u bevestigen dat uw CMP een geldige identiteitskaart heeft die met IAB TCF 2.0 is geregistreerd alvorens gegevens naar Platform te verzenden.

Deze gids vereist ook een werkend begrip van de volgende diensten van de Platform:

* [Experience Data Model (XDM)](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel in realtime](../../../../profile/home.md): Hefboomwerking [!DNL Identity Service] om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. [!DNL Real-time Customer Profile] trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Een JavaScript-bibliotheek aan de clientzijde waarmee u verschillende services voor Platforms kunt integreren in uw klantgerichte website.
   * [Opdrachten voor SDK-toestemming](../../../../edge/consent/supporting-consent.md): Een gebruiksscenario-overzicht van de toestemmingsgerelateerde bevelen van SDK in deze gids wordt getoond die.
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md): Hiermee kunt u delen [!DNL Real-time Customer Profile] gegevens in groepen personen die vergelijkbare kenmerken delen en op vergelijkbare wijze reageren als marketingstrategie??n.

Naast de hierboven vermelde diensten van het Platform, zou u ook vertrouwd moeten zijn met [bestemmingen](../../../../data-governance/home.md) en hun rol in het ecosysteem van de Platform.

## Overzicht van de instemmingsstroom van de klant {#summary}

De volgende secties beschrijven hoe de toestemmingsgegevens worden verzameld en afgedwongen nadat het systeem behoorlijk is gevormd.

### Goedgekeurde gegevensverzameling

Met het Platform kunt u gegevens over uw toestemming van klanten verzamelen via het volgende proces:

1. Een klant geeft via een dialoogvenster op uw website zijn voorkeuren voor het verzamelen van gegevens weer.
1. Uw CMP detecteert de wijziging van de voorkeur voor toestemming en genereert dienovereenkomstig TCF gegevens over toestemming.
1. Gebruikend het Web SDK van het Platform, worden de geproduceerde toestemmingsgegevens (die door CMP worden teruggegeven) verzonden naar Adobe Experience Platform.
1. De verzamelde toestemmingsgegevens worden opgenomen in een [!DNL Profile]-enabled dataset het waarvan schema TCF toestemmingsgebieden bevat.

Naast SDK-opdrachten die worden geactiveerd door de haken voor wijziging van de CMP-toestemming, kunnen toestemmingsgegevens ook in het Experience Platform stromen via door de klant gegenereerde XDM-gegevens die rechtstreeks naar een [!DNL Profile]-enabled dataset.

Alle segmenten die Adobe Audience Manager met Platform deelt (via de [!DNL Audience Manager] bronaansluiting of anderszins) kan ook toestemmingsgegevens bevatten, mits de desbetreffende velden op die segmenten zijn toegepast via [!DNL Experience Cloud Identity Service]. Voor meer informatie over het verzamelen van toestemmingsgegevens in [!DNL Audience Manager], zie het document op de [Adobe Audience Manager-insteekmodule voor IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Goedkeuring stroomafwaarts

Zodra TCF toestemmingsgegevens met succes is opgenomen, vinden de volgende processen in de stroomafwaartse diensten van het Platform plaats:

1. [!DNL Real-time Customer Profile] werkt de opgeslagen toestemmingsgegevens voor het profiel van die klant bij.
1. Het Platform verwerkt klant IDs slechts als de verkoperstoestemming voor Platform (565) voor elke identiteitskaart in een cluster wordt verstrekt.
1. Wanneer het uitvoeren van segmenten aan bestemmingen tot leden van de TCF 2.0 verkoperslijst behoort, omvat het Platform slechts profielen als de verkoperstoestemmingen voor beide Platform (565) *en* de individuele bestemming wordt verstrekt voor elke identiteitskaart in een cluster.

De rest van de secties in dit document verstrekken begeleiding op hoe te om Platform en uw gegevensverrichtingen te vormen om de inzameling en handhavingsvereisten te voldoen die hierboven worden beschreven.

## Bepalen hoe gegevens over klanttoestemming binnen uw CMP worden gegenereerd {#consent-data}

Aangezien elk CMP-systeem uniek is, moet u de beste manier bepalen om uw klanten toestemming te geven wanneer ze met uw service communiceren. Een gemeenschappelijke manier om dit te bereiken is door het gebruik van een dialoog van de koekjesinstemming, gelijkend op het volgende voorbeeld:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

In dit dialoogvenster moet de klant de mogelijkheid hebben om in of uit te gaan van het volgende:

| Goedkeuring, optie | Beschrijving |
| --- | --- |
| **Doelstellingen** | Doel bepaalt voor welke advertentietechnische doeleinden een merk de gegevens van een klant kan gebruiken. Het volgende doel moet worden gekozen opdat het Platform klant IDs verwerkt: <ul><li>**Doel 1**: Informatie opslaan en/of openen op een apparaat</li><li>**Doel 10**: Producten ontwikkelen en verbeteren</li></ul> |
| **Machtigingen leverancier** | Naast technische doeleinden moet de dialoog de klant ook de mogelijkheid bieden om ervoor te kiezen om hun gegevens te gebruiken door specifieke leveranciers, waaronder Adobe Experience Platform (565). |

### Constante tekenreeksen {#consent-strings}

Ongeacht de methode u gebruikt om de gegevens te verzamelen, is het doel een koordwaarde te produceren die op de toestemmingsopties wordt gebaseerd die door de klant worden gekozen, genoemd een toestemmingskoord.

In de TCF specificatie, worden de toestemmingskoorden gebruikt om relevante details over de toestemmingsmontages van een klant, in termen van specifieke marketing doeleinden te coderen zoals die door beleid en verkopers worden bepaald. Het Platform gebruikt deze koorden om de toestemmingsmontages voor elke klant op te slaan, en daarom moet een nieuwe toestemmingskoord worden geproduceerd telkens als die montages veranderen.

Constante tekenreeksen kunnen alleen worden gemaakt door een CMP die is geregistreerd bij de IAB TCF. Voor meer informatie over hoe u toestemmingsreeksen kunt genereren met behulp van uw specifieke CMP, raadpleegt u de [overzicht van tekenreeksindeling voor toestemming](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) in de IAB TCF GitHub repo.

## Gegevenssets maken met TCF-toestemmingsvelden {#datasets}

De gegevens van de toestemming van de klant moeten naar datasets worden verzonden waarvan de schema&#39;s TCF toestemmingsgebieden bevatten. Raadpleeg de zelfstudie op [gegevenssets maken voor het vastleggen van TCF 2.0-toestemming](./dataset.md) voor hoe te om de vereiste profieldataset (en een facultatieve dataset van de Gebeurtenis van de Ervaring) tot stand te brengen alvorens met deze gids verder te gaan.

## Bijwerken [!DNL Profile] beleid samenvoegen om toestemmingsgegevens op te nemen {#merge-policies}

Als u eenmaal een [!DNL Profile]- de toegelaten dataset voor het verzamelen van toestemmingsgegevens, moet u ervoor zorgen dat uw fusiebeleid is gevormd om TCF toestemmingsgebieden in uw klantenprofielen altijd te omvatten. Dit impliceert het plaatsen van datasetbelangrijkheid zodat uw toestemmingsdataset boven andere potentieel conflicterende datasets voorrang krijgt.

Raadpleeg voor meer informatie over het werken met samenvoegbeleid de [overzicht van samenvoegbeleid](../../../../profile/merge-policies/overview.md). Wanneer u het samenvoegbeleid instelt, moet u ervoor zorgen dat alle segmenten alle vereiste toestemmingskenmerken bevatten die door de [XDM-veldgroep met privacyschema](./dataset.md#privacy-field-group), zoals uiteengezet in de gids voor de opstelling van gegevensverzamelingen.

## Integreer de SDK van het Web van het Experience Platform om gegevens van de klantentoestemming te verzamelen {#sdk}

>[!NOTE]
>
>Het gebruik van de Web SDK van het Experience Platform wordt vereist om toestemmingsgegevens in Adobe Experience Platform direct te verwerken. [!DNL Experience Cloud Identity Service] wordt momenteel niet ondersteund.
>
>[!DNL Experience Cloud Identity Service] wordt echter nog steeds ondersteund voor de verwerking van toestemming in Adobe Audience Manager en naleving van TCF 2.0 vereist alleen dat de bibliotheek wordt bijgewerkt naar [versie 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Zodra u CMP hebt gevormd om toestemmingskoorden te produceren, moet u het Web SDK van het Experience Platform integreren om die koorden te verzamelen en hen te verzenden naar Platform. De Platform SDK verstrekt twee bevelen die kunnen worden gebruikt om TCF toestemmingsgegevens naar Platform (die in de hieronder subsecties worden verklaard) te verzenden, en zou moeten worden gebruikt wanneer een klant toestemmingsinformatie voor het eerst verstrekt, en om het even welk ogenblik dat de toestemming daarna verandert.

**De SDK interface niet met CMP&#39;s uit het vak**. Het is aan u om te bepalen hoe te om SDK in uw website te integreren, naar toestemmingsveranderingen in CMP te luisteren, en het aangewezen bevel te roepen.

### Een nieuwe gegevensstroom maken

SDK kan alleen gegevens naar Experience Platform verzenden als u eerst een nieuwe gegevensstroom voor Platform maakt in de gebruikersinterface voor gegevensverzameling. De specifieke stappen voor hoe te om een nieuwe gegevensstroom tot stand te brengen worden verstrekt in [SDK-documentatie](../../../../edge/datastreams/overview.md).

Nadat u een unieke naam voor de gegevensstroom hebt opgegeven, selecteert u de schakelknop naast **[!UICONTROL Adobe Experience Platform]**. Gebruik vervolgens de volgende waarden om de rest van het formulier in te vullen:

| Veld DataStream | Waarde |
| --- | --- |
| [!UICONTROL Sandbox] | De naam van het Platform [sandbox](../../../../sandboxes/home.md) die de vereiste het stromen verbinding en datasets aan opstelling de gegevensstroom bevat. |
| [!UICONTROL Streaming Inlet] | Een geldige streamingverbinding voor Experience Platform. Zie de zelfstudie aan [streaming verbinding maken](../../../../ingestion/tutorials/create-streaming-connection-ui.md) als u geen bestaande streaminginlaat hebt. |
| [!UICONTROL Event Dataset] | Selecteer [!DNL XDM ExperienceEvent] dataset die in [vorige stap](#datasets). Als u het [[!UICONTROL IAB TCF 2.0 Consent] veldgroep](../../../../xdm/field-groups/event/iab.md) in het schema van deze dataset, kunt u toestemming-verandering gebeurtenissen in tijd volgen gebruikend [`sendEvent`](#sendEvent) bevel, die dat gegevens in deze dataset opslaat. Houd er rekening mee dat de in deze gegevensset opgeslagen toestemmingswaarden **niet** gebruikt in automatische handhavingswerkstromen. |
| [!UICONTROL Profile Dataset] | Selecteer [!DNL XDM Individual Profile] dataset die in [vorige stap](#datasets). Wanneer wordt gereageerd op CMP visiewisselhaken met de [`setConsent`](#setConsent) bevel, zullen de verzamelde gegevens in deze dataset worden opgeslagen. Aangezien deze dataset profiel-toegelaten is, worden de toestemmingswaarden die in deze dataset worden opgeslagen gehouden tijdens automatische handhavingswerkschema&#39;s. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Als u klaar bent, selecteert u **[!UICONTROL Save]** onder aan het scherm en doorgaan met het volgen van eventuele extra vragen om de configuratie te voltooien.

### Opdrachten voor wijzigen van toestemming maken

Nadat u de in de vorige sectie beschreven gegevensstroom hebt gemaakt, kunt u beginnen met het gebruik van SDK-opdrachten om gegevens met toestemming naar het Platform te verzenden. De volgende secties verstrekken voorbeelden van hoe elk bevel van SDK in verschillende scenario&#39;s kan worden gebruikt.

>[!NOTE]
>
>Voor een inleiding aan de gemeenschappelijke syntaxis voor alle bevelen van SDK van het Platform, zie het document op [uitvoeren, opdrachten](../../../../edge/fundamentals/executing-commands.md).

#### Kantaarnhaken voor wijziging van CMP-toestemming gebruiken {#setConsent}

Vele CMPs verstrekt uit-van-de-doos haken die aan toestemmings-verandering gebeurtenissen luisteren. Wanneer deze gebeurtenissen zich voordoen, kunt u de opdracht `setConsent` gebruiken om de gegevens van de toestemming van die klant bij te werken.

De `setConsent` bevel verwacht twee argumenten: (1) een tekenreeks die het opdrachttype aangeeft (in dit geval &quot;setConsent&quot;) en (2) een payload die een `consent` array, die ten minste ????n object moet bevatten dat de vereiste toestemmingsvelden bevat, zoals hieronder wordt getoond:

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
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. Om TCF 2.0 voor deze klant te dwingen, moet de waarde worden geplaatst aan `true`. Standaardwaarden: `true` indien niet gedefinieerd. |

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

De `sendEvent` gebruiken als callback in de juiste gebeurtenislisteners op uw website. De opdracht verwacht twee argumenten: (1) een tekenreeks die het opdrachttype aangeeft (in dit geval: `sendEvent`), en (2) een lading die een `xdm` object dat de vereiste toestemmingsvelden als JSON biedt:

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
| `xdm.consentStrings` | Een array die ten minste ????n object moet bevatten dat de vereiste toestemmingsvelden bevat. |
| `consentStandard` | De gebruikte toestemmingsnorm. Deze waarde moet worden ingesteld op `IAB` voor TCF 2.0 toestemmingsverwerking. |
| `consentStandardVersion` | Het versienummer van de krachtens `standard`. Deze waarde moet worden ingesteld op `2.0` voor TCF 2.0 toestemmingsverwerking. |
| `consentStringValue` | De basis-64-gecodeerde toestemmingstekenreeks die door CMP wordt geproduceerd. |
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. Om TCF 2.0 voor deze klant te dwingen, moet de waarde worden geplaatst aan `true`. Standaardwaarden: `true` indien niet gedefinieerd. |

### Reacties in SDK verwerken

Alles [!DNL Platform SDK] de bevelen keren beloftes terug die erop wijzen of de vraag slaagde of ontbrak. U kunt deze reacties vervolgens gebruiken voor extra logica, zoals het weergeven van bevestigingsberichten aan de klant. Zie de sectie over [afhandeling gelukt of mislukt](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) in de handleiding voor het uitvoeren van SDK-opdrachten voor specifieke voorbeelden.

## Segmenten exporteren {#export}

>[!NOTE]
>
>Voordat u begint met het exporteren van segmenten, moet u ervoor zorgen dat uw segmenten alle vereiste machtigingsvelden bevatten. Zie de sectie over [samenvoegbeleid configureren](#merge-policies) voor meer informatie .

Zodra u de gegevens van de klantentoestemming hebt verzameld en publiekssegmenten gecreeerd die de vereiste toestemmingsattributen bevatten, kunt u TCF 2.0 naleving dan afdwingen wanneer het uitvoeren van die segmenten naar stroomafwaartse bestemmingen.

Op voorwaarde dat de toestemmingsbepaling `gdprApplies` is ingesteld op `true` voor een reeks klantprofielen, worden om het even welke gegevens van die profielen die naar stroomafwaartse bestemmingen worden uitgevoerd gefiltreerd gebaseerd op de toestemmingsvoorkeur TCF voor elk profiel. Elk profiel dat niet voldoet aan de vereiste voorkeuren voor toestemming wordt tijdens het exportproces overgeslagen.

Klanten moeten instemmen met de volgende doeleinden (zoals beschreven door [TCF 2.0-beleid](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) om hun profielen op te nemen in segmenten die naar bestemmingen worden uitgevoerd:

* **Doel 1**: Informatie opslaan en/of openen op een apparaat
* **Doel 10**: Producten ontwikkelen en verbeteren

TCF 2.0 vereist ook dat de bron van gegevens de de verkoperstoestemming van de bestemming moet controleren alvorens gegevens naar die bestemming te verzenden. Als dusdanig, controleert het Platform als de de verkoperstoestemming van de bestemming binnen aan voor alle IDs in de cluster alvorens gegevens te omvatten die aan die bestemming worden gebonden.

>[!NOTE]
>
>Om het even welke segmenten die met Adobe Audience Manager worden gedeeld zullen de zelfde TCF 2.0 toestemmingswaarden zoals hun Platform tegenhangers bevatten. Sinds [!DNL Audience Manager] deelt dezelfde leverancier-id als Platform (565), dezelfde doeleinden en machtiging van de leverancier zijn vereist. Zie het document op de [Adobe Audience Manager-insteekmodule voor IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) voor meer informatie .

## Implementatie testen {#test-implementation}

Zodra u uw implementatie TCF 2.0 hebt gevormd en segmenten naar bestemmingen uitgevoerd, zullen om het even welke gegevens die toestemmingsvereisten niet voldoen niet worden uitgevoerd. Nochtans, om te zien of de juiste klantenprofielen tijdens de uitvoer werden gefiltreerd, moet u de gegevensopslag op uw bestemmingen manueel controleren om te zien of werd de toestemming behoorlijk gehandhaafd.

Het is belangrijk om op te merken dat als veelvoudige IDs omhoog een cluster maken en TCF 2.0 van toepassing is, de volledige cluster zal worden uitgesloten als zelfs ????n enkele identiteitskaart niet de correcte doeleinden en verkoperstoestemmingen bevat.

## Volgende stappen

Dit document behandelde het proces om uw verrichtingen van de gegevens van het Platform te vormen om aan uw bedrijfsverplichtingen zoals die door TCF 2.0 worden geschetst te voldoen. Zie het overzicht op [bestuur, privacy en veiligheid](../../overview.md) voor meer informatie over de privacy-gerelateerde mogelijkheden van het Platform.
