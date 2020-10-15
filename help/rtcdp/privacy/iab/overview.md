---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consent
solution: Experience Platform
title: IAB TCF 2.0-ondersteuning in Real-time Customer Data Platform
topic: privacy events
translation-type: tm+mt
source-git-commit: b24c624df188be3cbe7f71dcdf8a23d2478c287c
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 1%

---


# IAB TCF 2.0-ondersteuning in [!DNL Real-time Customer Data Platform]

De [!DNL Transparency & Consent Framework] (TCF), zoals uiteengezet door de [!DNL Interactive Advertising Bureau] (IAB), is een open-standaard technisch kader dat organisaties in staat stelt om toestemming van de consument voor de verwerking van hun persoonsgegevens te verkrijgen, te registreren en bij te werken, in overeenstemming met de GDPR van de Europese Unie [!DNL General Data Protection Regulation] (EU). De tweede iteratie van het framework, TCF 2.0, biedt meer flexibiliteit voor de manier waarop consumenten toestemming kunnen geven of weigeren, inclusief of en hoe leveranciers bepaalde functies van gegevensverwerking kunnen gebruiken, zoals exacte geolocatie.

>[!NOTE]
>
>Meer informatie over TCF 2.0 is te vinden op de website [van](https://iabeurope.eu/tcf-2-0/)IAB Europe, met inbegrip van steunmaterialen en technische specificaties.

[!DNL Real-time Customer Data Platform (Real-time CDP)] maakt deel uit van de geregistreerde [IAB TCF 2.0 leverancierslijst](https://iabeurope.eu/vendor-list-tcf-v2-0/), onder identiteitskaart **565**. In overeenstemming met TCF 2.0 vereisten, [!DNL Real-time CDP] staat u toe om gegevens van de klantentoestemming te verzamelen en het in uw opgeslagen klantenprofielen te integreren. Deze toestemmingsgegevens kunnen dan in rekening worden gebracht of de profielen in uitgevoerde publiekssegmenten, afhankelijk van hun gebruiksgeval inbegrepen zijn.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] alleen kan voldoen aan versie 2.0 van de TCF (of hoger). Eerdere versies van TCF worden niet ondersteund.

Dit document biedt een overzicht van hoe u uw gegevensbewerkingen en profielschema&#39;s kunt configureren om gegevens voor klanttoestemming te accepteren die door uw CMP worden gegenereerd, en hoe u keuzes voor gebruikerstoestemming kunt [!DNL Real-time CDP] overbrengen bij het exporteren van segmenten.

## Vereisten

Om deze gids te volgen, moet u een Platform van het Beheer van de Toestemming (CMP), of commercieel of uw gebruiken, gebruiken die met IAB TCF wordt geïntegreerd en volgzaam is. Zie de [lijst van conforme CMP](https://iabeurope.eu/cmp-list/) &#39;s voor meer informatie.

>[!IMPORTANT]
>
>Als de id van uw CMP ongeldig is, [!DNL Real-time CDP] blijven uw gegevens ongewijzigd verwerken. Om TCF 2.0 af te dwingen, moet u bevestigen dat uw CMP een geldige identiteitskaart heeft die met IAB TCF 2.0 is geregistreerd alvorens gegevens naar te verzenden [!DNL Experience Platform].

Deze handleiding vereist ook een goed begrip van de volgende Adobe Experience Platform-services:

* [XDM (Experience Data Model)](../../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
* [Adobe Experience Platform Identity Service](../../../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel](../../../profile/home.md)in realtime: Hefboomwerkingen [!DNL Identity Service] om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. [!DNL Real-time Customer Profile] trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Een JavaScript-bibliotheek aan de clientzijde waarmee u verschillende [!DNL Platform] services kunt integreren in uw klantgerichte website.
   * [Opdrachten](../../../edge/consent/supporting-consent.md)voor SDK-toestemming: Een gebruiksscenario-overzicht van de toestemmingsgerelateerde bevelen van SDK in deze gids wordt getoond die.
* [Adobe Experience Platform Segmentation Service](../../../segmentation/home.md): Hiermee kunt u [!DNL Real-time Customer Profile] gegevens opsplitsen in groepen van personen die vergelijkbare kenmerken delen en op vergelijkbare wijze reageren op marketingstrategieën.

Naast de hierboven vermelde [!DNL Platform] diensten, zou u ook met [bestemmingen](../../destinations/destinations-overview.md) en hun gebruik in moeten vertrouwd zijn [!DNL Real-time CDP].

## Overzicht van de instemmingsstroom van de klant {#summary}

De volgende secties beschrijven hoe de toestemmingsgegevens worden verzameld en afgedwongen nadat het systeem behoorlijk is gevormd.

### Goedgekeurde gegevensverzameling

[!DNL Real-time CDP] Hiermee kunt u gegevens over toestemming van klanten verzamelen via het volgende proces:

1. Een klant geeft via een dialoogvenster op uw website zijn voorkeuren voor het verzamelen van gegevens weer.
1. Uw CMP detecteert de wijziging van de voorkeur voor toestemming en genereert dienovereenkomstig gegevens over de IAB-toestemming.
1. Met behulp van het [!DNL Experience Platform Web SDK]formulier worden de gegevens over de gegenereerde toestemming (geretourneerd door het CMP) naar Adobe Experience Platform verzonden.
1. De verzamelde toestemmingsgegevens worden opgenomen in een [!DNL Profile]toegelaten dataset het waarvan schema IAB toestemmingsgebieden bevat.

Naast SDK-opdrachten die worden geactiveerd door de haken voor wijziging van de CMP-toestemming, kunnen gegevens over de toestemming ook worden doorgegeven [!DNL Experience Platform] via door de klant gegenereerde XDM-gegevens die rechtstreeks naar een [!DNL Profile]ingeschakelde gegevensset worden geüpload.

Alle segmenten die door Adobe Audience Manager (via de [!DNL Platform] bronconnector of anderszins) worden gedeeld, kunnen ook toestemmingsgegevens bevatten, mits de desbetreffende velden op die segmenten zijn toegepast [!DNL Audience Manager] [!DNL Experience Cloud Identity Service]. Raadpleeg het document over de insteekmodule [!DNL Audience Manager]Adobe Audience Manager voor IAB TCF voor meer informatie over het verzamelen van gegevens over toestemming in [](https://docs.adobe.com/help/nl-NL/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Goedkeuring stroomafwaarts

Zodra de gegevens van de IAB-toestemming met succes zijn opgenomen, vinden de volgende processen plaats in stroomafwaartse [!DNL Real-time CDP] diensten:

1. [!DNL Real-time Customer Profile] werkt de opgeslagen toestemmingsgegevens voor het profiel van die klant bij.
1. [!DNL Real-time CDP] verwerkt klant IDs slechts als de verkoperstoestemming voor [!DNL Real-time CDP] (565) voor elke identiteitskaart in een cluster wordt verstrekt.
1. Wanneer het uitvoeren van segmenten aan bestemmingen tot leden van de TCF 2.0 verkoperslijst behoort, omvat [!DNL Real-time CDP] slechts profielen als de verkoperstoestemmingen voor zowel [!DNL Real-time CDP] (565) *als* de bestemming voor elke identiteitskaart in een cluster wordt verstrekt.

De rest van de secties in dit document geven richtlijnen voor het configureren [!DNL Real-time CDP] en uitvoeren van gegevensbewerkingen om te voldoen aan de hierboven beschreven vereisten voor verzameling en handhaving.

## Bepalen hoe gegevens over klanttoestemming binnen uw CMP worden gegenereerd {#consent-data}

Aangezien elk CMP-systeem uniek is, moet u de beste manier bepalen om uw klanten toestemming te geven wanneer ze met uw service communiceren. Een gemeenschappelijke manier om dit te bereiken is door het gebruik van een dialoog van de koekjesinstemming, gelijkend op het volgende voorbeeld:

![](../assets/iab/cmp-dialog.png)

In dit dialoogvenster moet de klant de mogelijkheid hebben om in of uit te gaan van het volgende:

| Goedkeuring, optie | Beschrijving |
| --- | --- |
| **Doelstellingen** | Doel bepaalt voor welke advertentietechnische doeleinden een merk de gegevens van een klant kan gebruiken. U moet kiezen voor de volgende doeleinden om de id&#39;s van de klant [!DNL Real-time CDP] te kunnen verwerken: <ul><li>**Doel 1**: Informatie opslaan en/of openen op een apparaat</li><li>**Doel 10**: Producten ontwikkelen en verbeteren</li></ul> |
| **Machtigingen leverancier** | Naast technische doeleinden moet de dialoog de klant ook de mogelijkheid bieden om ervoor te kiezen om hun gegevens te gebruiken door specifieke leveranciers, waaronder [!DNL  Real-time CDP] (565). |

### Constante tekenreeksen {#consent-strings}

Ongeacht de methode u gebruikt om de gegevens te verzamelen, is het doel een koordwaarde te produceren die op de toestemmingsopties wordt gebaseerd die door de klant worden gekozen, genoemd een toestemmingskoord.

In de TCF specificatie, worden de toestemmingskoorden gebruikt om relevante details over de toestemmingsmontages van een klant, in termen van specifieke marketing doeleinden te coderen zoals die door beleid en verkopers worden bepaald. [!DNL Real-time CDP] gebruikt deze tekenreeksen om de toestemmingsmontages voor elke klant op te slaan, en daarom moet een nieuwe toestemmingskoord worden geproduceerd telkens als die montages veranderen.

Constante tekenreeksen kunnen alleen worden gemaakt door een CMP die is geregistreerd bij de IAB TCF. Voor meer informatie over hoe te om toestemmingskoorden te produceren gebruikend uw bepaald CMP, verwijs naar de het formatteren van het [toestemmingstekengids](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) in het IAB TCF rapport GitHub.

## Gegevenssets maken met IAB-toestemmingsvelden {#datasets}

De gegevens van de toestemming van de klant moeten naar een datasets worden verzonden het waarvan schema IAB toestemmingsgebieden bevat. Raadpleeg de zelfstudie over het [maken van gegevenssets voor het vastleggen van TCF 2.0-toestemming](./dataset-preparation.md) voor het maken van de twee vereiste gegevenssets voordat u verdergaat met deze handleiding.

## Samenvoegbeleid bijwerken [!DNL Profile] en gegevens voor toestemming opnemen {#merge-policies}

Zodra u een [!DNL Profile]-Toegelaten dataset voor het verzamelen van toestemmingsgegevens hebt gecreeerd, moet u ervoor zorgen dat uw fusiebeleid is gevormd om IAB toestemmingsgebieden in uw klantenprofielen altijd te omvatten. Dit impliceert het plaatsen van datasetbelangrijkheid zodat uw toestemmingsdataset boven andere potentieel conflicterende datasets voorrang krijgt.

Voor meer informatie over hoe te met fusiebeleid te werken, verwijs naar de de gebruikersgids [van het](../../../profile/ui/merge-policies.md)fusiebeleid. Bij het opzetten van uw samenvoegbeleid, moet u ervoor zorgen dat uw segmenten alle vereiste toestemmingsattributen omvatten die door de [privacymixin](./dataset-preparation.md#privacy-mixin)XDM worden verstrekt, zoals die in de gids over datasetvoorbereiding worden geschetst.

## Integreer SDK van het [!DNL Experience Platform] Web om de gegevens van de klantentoestemming te verzamelen {#sdk}

>[!NOTE]
>
>Het gebruik van de [!DNL Experience Platform] Web SDK wordt vereist om toestemmingsgegevens in Adobe Experience Platform direct te verwerken. [!DNL Experience Cloud Identity Service] wordt momenteel niet ondersteund.
>
>[!DNL Experience Cloud Identity Service] wordt echter nog steeds ondersteund voor het verwerken van toestemming in Adobe Audience Manager en naleving van TCF 2.0 vereist alleen dat de bibliotheek wordt bijgewerkt naar [versie 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Zodra u CMP hebt gevormd om toestemmingskoorden te produceren, moet u SDK van het [!DNL Experience Platform] Web integreren om die koorden te verzamelen en hen te verzenden naar [!DNL Platform]. De [!DNL Platform] SDK biedt twee opdrachten die kunnen worden gebruikt om gegevens over IAB-toestemmingen naar het Platform te verzenden (zie de onderstaande subsecties). Deze opdrachten dienen te worden gebruikt wanneer een klant voor het eerst informatie over toestemming verstrekt en op elk moment dat de toestemming daarna verandert.

**De SDK interface niet met CMP&#39;s uit het vak**. Het is aan u om te bepalen hoe te om SDK in uw website te integreren, naar toestemmingsveranderingen in CMP te luisteren, en het aangewezen bevel te roepen.

### Een nieuwe randconfiguratie maken

De SDK kan alleen gegevens verzenden naar [!DNL Experience Platform]als u eerst een nieuwe randconfiguratie maakt voor [!DNL Platform] in [!DNL Adobe Experience Platform Launch]. De specifieke stappen voor hoe te om een nieuwe configuratie tot stand te brengen worden verstrekt in de documentatie [van](../../../edge/fundamentals/edge-configuration.md)SDK.

Nadat u een unieke naam voor de configuratie hebt opgegeven, selecteert u de schakelknop naast **[!UICONTROL Adobe Experience Platform]**. Gebruik vervolgens de volgende waarden om de rest van het formulier in te vullen:

| Edge-configuratieveld | Waarde |
| --- | --- |
| [!UICONTROL Sandbox] | De naam van de [!DNL Platform] zandbak [](../../../sandboxes/home.md) die de vereiste het stromen verbinding en datasets aan opstelling de randconfiguratie bevat. |
| [!UICONTROL Streaming-ingang] | Een geldige streamingverbinding voor [!DNL Experience Platform]. Zie de zelfstudie over het [maken van een streamingverbinding](../../../ingestion/tutorials/create-streaming-connection-ui.md) als u geen bestaande streamingingang hebt. |
| [!UICONTROL Gebeurtenisgegevens] | Selecteer de [!DNL XDM ExperienceEvent] dataset die in de [vorige stap](#datasets)wordt gecreeerd. |
| [!UICONTROL Profielgegevens] | Selecteer de [!DNL XDM Individual Profile] dataset die in de [vorige stap](#datasets)wordt gecreeerd. |

![](../assets/iab/edge-config.png)

Als u klaar bent, klikt u op **[!UICONTROL Opslaan]** onder aan het scherm en gaat u verder met het volgen van eventuele extra aanwijzingen om de configuratie te voltooien.

### Opdrachten voor wijzigen van toestemming maken

Zodra u de randconfiguratie hebt gecreeerd die in de vorige sectie wordt beschreven, kunt u beginnen SDK bevelen te gebruiken om toestemmingsgegevens naar te verzenden [!DNL Platform]. De volgende secties verstrekken voorbeelden van hoe elk bevel van SDK in verschillende scenario&#39;s kan worden gebruikt.

>[!NOTE]
>
>Voor een inleiding aan de gemeenschappelijke syntaxis voor alle bevelen [!DNL Platform] SDK, zie het document over het [uitvoeren van bevelen](../../../edge/fundamentals/executing-commands.md).

#### Kantaarnhaken voor wijziging van CMP-toestemming gebruiken

Vele CMPs verstrekt uit-van-de-doos haken die aan toestemmings-verandering gebeurtenissen luisteren. Wanneer deze gebeurtenissen voorkomen, kunt u het `setConsent` bevel gebruiken om de toestemmingsgegevens van die klant bij te werken.

De `setConsent` opdracht verwacht twee argumenten: (1) een tekenreeks die het opdrachttype aangeeft (in dit geval &quot;setConsent&quot;) en (2) een payload die een `consent` array bevat, die ten minste één object moet bevatten dat de vereiste toestemmingsvelden bevat, zoals hieronder wordt getoond:

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
| `standard` | De gebruikte toestemmingsnorm. Deze waarde moet aan &quot;IAB&quot;voor TCF 2.0 toestemmingsverwerking worden geplaatst. |
| `version` | Het versienummer van de goedkeuringsnorm die onder `standard`dit artikel wordt vermeld. Deze waarde moet worden ingesteld op &quot;2.0&quot; voor verwerking van TCF 2.0-toestemming. |
| `value` | De basis-64-gecodeerde toestemmingstekenreeks die door CMP wordt geproduceerd. |
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. Om TCF 2.0 voor deze klant te dwingen, moet de waarde aan &quot;waar&quot;worden geplaatst. |

De `setConsent` opdracht moet worden gebruikt als onderdeel van een CMP-haak die wijzigingen in de toestemmingsinstellingen detecteert. In het volgende JavaScript ziet u hoe de `setConsent` opdracht kan worden gebruikt voor de `OnConsentChanged` haak van OneTrust:

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

#### Gebeurtenissen gebruiken

U kunt TCF 2.0 toestemmingsgegevens over elke gebeurtenis ook verzamelen binnen teweeggebracht [!DNL Platform] door het `sendEvent` bevel te gebruiken.

>[!NOTE]
>
>Als u deze methode wilt gebruiken, moet u het bestand [!DNL Experience Event Privacy mixin] aan het [!DNL Profile]ingeschakelde [!DNL XDM ExperienceEvent] schema hebben toegevoegd. Zie de sectie bij het [bijwerken van het schema](./dataset-preparation.md#event-schema) ExperienceEvent in de gids van de datasetvoorbereiding voor stappen op hoe te om dit te vormen.

Het `sendEvent` bevel zou als callback in aangewezen gebeurtenisluisteraars op uw website moeten worden gebruikt. De opdracht verwacht twee argumenten: (1) een tekenreeks die het opdrachttype aangeeft (in dit geval &quot;sendEvent&quot;) en (2) een payload die een `xdm` object bevat dat de vereiste toestemmingsvelden bevat als JSON:

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
| `consentStandard` | De gebruikte toestemmingsnorm. Deze waarde moet aan &quot;IAB&quot;voor TCF 2.0 toestemmingsverwerking worden geplaatst. |
| `consentStandardVersion` | Het versienummer van de goedkeuringsnorm die onder `standard`dit artikel wordt vermeld. Deze waarde moet worden ingesteld op &quot;2.0&quot; voor verwerking van TCF 2.0-toestemming. |
| `consentStringValue` | De basis-64-gecodeerde toestemmingstekenreeks die door CMP wordt geproduceerd. |
| `gdprApplies` | Een waarde Van Boole die erop wijst of GDPR op de momenteel het programma geopende klant van toepassing is. Om TCF 2.0 voor deze klant te dwingen, moet de waarde aan &quot;waar&quot;worden geplaatst. |

### Reacties in SDK verwerken

Alle [!DNL Platform SDK] bevelen keren beloftes terug die erop wijzen of de vraag slaagde of ontbrak. U kunt deze reacties vervolgens gebruiken voor extra logica, zoals het weergeven van bevestigingsberichten aan de klant. Zie de sectie over het [afhandelen van succes of mislukking](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) in de handleiding over het uitvoeren van SDK-opdrachten voor specifieke voorbeelden.

## Segmenten exporteren {#export}

>[!NOTE]
>
>Voordat u begint met het exporteren van segmenten, moet u ervoor zorgen dat uw segmenten alle vereiste machtigingsvelden bevatten. Zie de sectie over het [configureren van samenvoegingsbeleid](#merge-policies) voor meer informatie.

Zodra u de gegevens van de klantentoestemming hebt verzameld en publiekssegmenten gecreeerd die de vereiste toestemmingsattributen bevatten, kunt u TCF 2.0 naleving dan afdwingen wanneer het uitvoeren van die segmenten naar stroomafwaartse bestemmingen.

Mits de instelling van de toestemming `gdprApplies` is ingesteld op `true` voor een reeks klantprofielen, worden alle gegevens van die profielen die naar downstreambestemmingen worden geëxporteerd, gefilterd op basis van de voorkeuren voor de toestemming voor elk profiel. Elk profiel dat niet voldoet aan de vereiste voorkeuren voor toestemming wordt tijdens het exportproces overgeslagen.

De klanten moeten met de volgende doeleinden (zoals die door [TCF 2.0 beleid](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)worden geschetst) instemmen opdat hun profielen in segmenten worden omvat die naar bestemmingen worden uitgevoerd:

* **Doel 1**: Informatie opslaan en/of openen op een apparaat
* **Doel 10**: Producten ontwikkelen en verbeteren

TCF 2.0 vereist ook dat de bron van gegevens de de verkoperstoestemming van de bestemming moet controleren alvorens gegevens naar die bestemming te verzenden. Als dusdanig, [!DNL Real-time CDP] controleert als de de verkoperstoestemming van de bestemming binnen aan voor alle IDs in de cluster alvorens gegevens te omvatten die aan die bestemming worden gebonden.

>[!NOTE]
>
>Om het even welke segmenten die met Adobe Audience Manager worden gedeeld zullen de zelfde TCF 2.0 toestemmingswaarden zoals hun [!DNL Platform] tegenhangers bevatten. Aangezien [!DNL Audience Manager] dezelfde leverancier-id wordt gedeeld als [!DNL Real-time CDP] (565), zijn dezelfde doeleinden en machtiging van de leverancier vereist. Raadpleeg het document over de plug-in [Adobe Audience Manager voor IAB TCF](https://docs.adobe.com/help/nl-NL/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) voor meer informatie.

## Test your implementation {#test-implementation}

Zodra u uw implementatie TCF 2.0 hebt gevormd en segmenten naar bestemmingen uitgevoerd, zullen om het even welke gegevens die toestemmingsvereisten niet voldoen niet worden uitgevoerd. Nochtans, om te zien of de juiste klantenprofielen tijdens de uitvoer werden gefiltreerd, moet u de gegevensopslag op uw bestemmingen manueel controleren om te zien of werd de toestemming behoorlijk gehandhaafd.

Het is belangrijk om op te merken dat als veelvoudige IDs omhoog een cluster maken en TCF 2.0 van toepassing is, de volledige cluster zal worden uitgesloten als zelfs één enkele identiteitskaart niet de correcte doeleinden en verkoperstoestemmingen bevat.

## Volgende stappen

In dit document wordt beschreven hoe u uw gegevensbewerkingen configureert om compatibel [!DNL Real-time CDP] te zijn met TCF 2.0. Raadpleeg de volgende documentatie voor meer informatie over de andere mogelijkheden op het gebied van privacy die worden geboden [!DNL Real-time CDP]door:

* [Privacy in real time CDP](../privacy-overview.md)
* [Gegevensbeheer in real time CDP](../data-governance-overview.md)