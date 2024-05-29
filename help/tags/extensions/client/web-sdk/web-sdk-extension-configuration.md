---
title: De web SDK-tagextensie configureren
description: Leer hoe te om de de markeringsuitbreiding van SDK van het Web van het Experience Platform in de UI van Markeringen te vormen.
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: 1d1bb754769defd122faaa2160e06671bf02c974
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 0%

---

# De webSDK-tagextensie configureren

De [!DNL Web SDK] de markeringsuitbreiding verzendt gegevens naar Adobe Experience Cloud van Web-eigenschappen door de Edge Network van het Experience Platform.

Met de extensie kunt u gegevens streamen naar Platform, identiteiten synchroniseren, de toestemmingssignalen van de klant verwerken en automatisch contextgegevens verzamelen.

In dit document wordt uitgelegd hoe u de tagextensie configureert in de gebruikersinterface voor tags.

## De extensie van de Web SDK-tag installeren {#install}

De de markeringsuitbreiding van SDK van het Web moet een bezit worden geïnstalleerd. Als u dit nog niet hebt gedaan, raadpleegt u de documentatie op [een tag-eigenschap maken](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Nadat u een eigenschap hebt gemaakt, opent u de eigenschap en selecteert u de **[!UICONTROL Extensions]** op de linkerzijbalk.

Selecteer de **[!UICONTROL Catalog]** tab. Zoek in de lijst met beschikbare extensies naar de [!DNL Web SDK] en selecteert u **[!UICONTROL Install]**.

![Afbeelding die de interface Tags weergeeft terwijl de Web SDK-extensie is geselecteerd](assets/web-sdk-install.png)

Na het selecteren **[!UICONTROL Install]**, moet u de de markeringsuitbreiding van SDK van het Web vormen en de configuratie opslaan.

>[!NOTE]
>
>De tagextensie wordt alleen geïnstalleerd nadat de configuratie is opgeslagen. Zie de volgende secties om te leren hoe te om de markeringsuitbreiding te vormen.

## Instantie-instellingen configureren {#general}

De configuratieopties boven aan de pagina vertellen Adobe Experience Platform waar de gegevens moeten worden gerouteerd en welke configuraties op de server moeten worden gebruikt.

![Afbeelding die de algemene instellingen van de extensie van de Web SDK-tag in de gebruikersinterface voor tags weergeeft](assets/web-sdk-ext-general.png)

* **[!UICONTROL Name]**: De extensie Adobe Experience Platform Web SDK ondersteunt meerdere exemplaren op de pagina. De naam wordt gebruikt om gegevens naar veelvoudige organisaties met een markeringsconfiguratie te verzenden. De instantienaam is standaard ingesteld op `alloy`. U kunt de instantienaam echter wijzigen in elke geldige naam voor een JavaScript-object.
* **[!UICONTROL IMS organization ID]**: De id van de organisatie waarnaar u de gegevens bij Adobe wilt verzenden. Meestal gebruikt u de standaardwaarde die automatisch wordt ingevuld. Wanneer u meerdere exemplaren op de pagina hebt, vult u dit veld met de waarde van de tweede organisatie waarnaar u gegevens wilt verzenden.
* **[!UICONTROL Edge domain]**: Het domein waarvan de extensie gegevens verzendt en ontvangt. De Adobe adviseert gebruikend een 1st-partijdomein (CNAME) voor deze uitbreiding. Het standaard domein van derden werkt voor ontwikkelomgevingen, maar is niet geschikt voor productieomgevingen. Instructies over hoe te opstelling een eerste-partij CNAME zijn vermeld [hier](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

## Gegevensstroominstellingen configureren {#datastreams}

Deze sectie staat u toe om de gegevensstromen te selecteren die voor elk van de drie beschikbare milieu&#39;s (productie, het opvoeren, en ontwikkeling) zouden moeten worden gebruikt.

Wanneer een verzoek naar de Edge Network wordt verzonden, wordt een gegevensstroom ID gebruikt om naar de server-zijconfiguratie te verwijzen. U kunt de configuratie bijwerken zonder dat u codewijzigingen op uw website hoeft aan te brengen.

Zie de handleiding op [datastreams](../../../../datastreams/overview.md) leren hoe u een gegevensstroom kunt configureren.

U kunt een gegevensstroom kiezen in de beschikbare vervolgkeuzemenu&#39;s of **[!UICONTROL Enter values]** en voer een aangepaste gegevensstroom-id in voor elke omgeving.

![Afbeelding die de gegevensstreaminstellingen van de Web SDK-tagextensie in de gebruikersinterface voor tags weergeeft](assets/web-sdk-ext-datastreams.png)

## Privacy-instellingen configureren {#privacy}

Deze sectie staat u toe om te vormen hoe de SDK van het Web de signalen van de gebruikerstoestemming van uw website behandelt. Met name kunt u het standaardniveau van toestemming selecteren dat wordt aangenomen door een gebruiker als er geen andere voorkeur voor expliciete toestemming is opgegeven.

Het standaard toestemmingsniveau wordt niet bewaard aan het gebruikersprofiel.

![Afbeelding die de privacy-instellingen van de Web SDK-tagextensie in de gebruikersinterface van Tags weergeeft](assets/web-sdk-ext-privacy.png)

| [!UICONTROL Default consent level] | Beschrijving |
| --- | --- |
| [!UICONTROL In] | Verzamel gebeurtenissen die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft. |
| [!UICONTROL Out] | Gebeurtenissen negeren die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft. |
| [!UICONTROL Pending] | Wachtrij-gebeurtenissen die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft. Als er voorkeuren voor toestemming zijn opgegeven, worden de gebeurtenissen verzameld of genegeerd, afhankelijk van de opgegeven voorkeuren. |
| [!UICONTROL Provided by data element] | Het standaard toestemmingsniveau wordt bepaald door een afzonderlijk gegevenselement dat u bepaalt. Wanneer u deze optie gebruikt, moet u het gegevenselement opgeven met behulp van het opgegeven vervolgkeuzemenu. |

>[!TIP]
>
>Gebruiken **[!UICONTROL Out]** of **[!UICONTROL Pending]** als u expliciete gebruikerstoestemming voor uw bedrijfsverrichtingen vereist.

## Identiteitsinstellingen configureren {#identity}

Deze sectie staat u toe om het gedrag van SDK van het Web te bepalen wanneer het over de behandeling van gebruikersidentificatie komt.

![Afbeelding met de identiteitsinstellingen van de extensie van de Web SDK-tag in de gebruikersinterface voor tags](assets/web-sdk-ext-identity.png)

* **[!UICONTROL Migrate ECID from VisitorAPI]**: Deze optie is standaard ingeschakeld. Wanneer deze functie is ingeschakeld, kan de SDK de `AMCV` en `s_ecid` cookies en stel de `AMCV` cookie gebruikt door [!DNL Visitor.js]. Deze eigenschap is belangrijk wanneer het migreren aan Web SDK, aangezien sommige pagina&#39;s nog kunnen gebruiken [!DNL Visitor.js]. Met deze optie kan de SDK hetzelfde blijven gebruiken [!DNL ECID] zodat gebruikers niet als twee afzonderlijke gebruikers worden geïdentificeerd.
* **[!UICONTROL Use third-party cookies]**: Wanneer deze optie wordt toegelaten, probeert SDK van het Web om een gebruikersherkenningsteken in een derdekoekje op te slaan. Als dit gelukt is, wordt de gebruiker geïdentificeerd als één gebruiker terwijl deze in meerdere domeinen navigeert en niet als een afzonderlijke gebruiker op elk domein wordt geïdentificeerd. Als deze optie is ingeschakeld, kan de SDK de gebruikersnaam nog steeds niet opslaan in een cookie van een andere fabrikant als de browser cookies van derden niet ondersteunt of door de gebruiker is geconfigureerd om cookies van derden niet toe te staan. In dit geval slaat de SDK alleen de id op in het domein van de eerste partij.

  >[!IMPORTANT]
  >>Cookies van derden zijn niet compatibel met de [apparaat-id van eerste partij](../../../../web-sdk/identity/first-party-device-ids.md) functionaliteit in Web SDK.
U kunt apparaat-id&#39;s van andere leveranciers gebruiken of cookies van andere leveranciers, maar u kunt beide functies niet tegelijkertijd gebruiken.
  >
## Aanpassingsinstellingen configureren {#personalization}

In deze sectie kunt u configureren hoe u bepaalde delen van een pagina wilt verbergen terwijl gepersonaliseerde inhoud wordt geladen. Zo weet u zeker dat uw bezoekers alleen de gepersonaliseerde pagina zien.

![Afbeelding die de verpersoonlijkingsinstellingen van de Web SDK-tagextensie in de gebruikersinterface van Tags weergeeft](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL Migrate Target from at.js to the Web SDK]**: Gebruik deze optie om in te schakelen [!DNL Web SDK] lezen en schrijven van de nalatenschap `mbox` en `mboxEdgeCluster` cookies die worden gebruikt door at.js `1.x` of `2.x` bibliotheken. Dit helpt u het bezoekersprofiel te houden terwijl het bewegen van een pagina die SDK van het Web aan een pagina gebruikt die at.js gebruikt `1.x` of `2.x` en omgekeerd.

### Stijl vooraf verbergen {#prehiding-style}

Met de preHide style editor kunt u aangepaste CSS-regels definiëren om specifieke secties van een pagina te verbergen. Wanneer de pagina wordt geladen, gebruikt SDK van het Web deze stijl om de secties te verbergen die moeten worden gepersonaliseerd, wint de verpersoonlijking terug, dan unhides de gepersonaliseerde paginagedeelten. Op deze manier zien uw bezoekers de reeds gepersonaliseerde pagina&#39;s, zonder het proces van de personalisatieherwinning te zien.

### Fragment vooraf verbergen {#prehiding-snippet}

Het voorbeeldfragment is handig wanneer de Web SDK-bibliotheek asynchroon wordt geladen. In deze situatie, om het flikkeren te vermijden, adviseren wij het verbergen van de inhoud alvorens de bibliotheek van SDK van het Web wordt geladen.

Als u het voorverborgen fragment wilt gebruiken, kopieert en plakt u het in het dialoogvenster `<head>` -element van uw pagina.

>[!IMPORTANT]
>
Als u het voorverborgen fragment gebruikt, wordt u aangeraden het zelfde fragment te gebruiken [!DNL CSS] als de regel die wordt gebruikt door de [stijl voorverbergen](#prehiding-style).

## Instellingen voor gegevensverzameling configureren {#data-collection}

![Afbeelding met de instellingen voor gegevensverzameling voor de extensie van de Web SDK-tag in de gebruikersinterface Codes](assets/web-sdk-ext-collection.png)

* **[!UICONTROL Callback function]**: De callback-functie die in de extensie wordt opgegeven, wordt ook wel de [`onBeforeEventSend` function](/help/web-sdk/commands/configure/onbeforeeventsend.md) in de bibliotheek. Met deze functie kunt u gebeurtenissen globaal wijzigen voordat ze naar de Edge Network worden verzonden.
* **[!UICONTROL Enable click data collection]**: De SDK van het Web kan verbindingsklikinformatie voor u automatisch verzamelen. Deze functie is standaard ingeschakeld, maar kan met deze optie worden uitgeschakeld. Koppelingen worden ook gemarkeerd als downloadkoppelingen als ze een van de downloadexpressies bevatten die in het dialoogvenster [!UICONTROL Download Link Qualifier] textbox. Adobe voorziet u van sommige standaardbepalende eigenschappen van de downloadverbinding. U kunt deze naar wens bewerken.
* **[!UICONTROL Automatically collected context data]**: Door gebrek, verzamelt het Web SDK bepaalde contextgegevens betreffende apparaat, Web, milieu, en plaatcontext. Als u deze gegevens niet wilt verzamelen of alleen bepaalde categorieën gegevens wilt verzamelen, selecteert u **[!UICONTROL Specific context information]** en selecteer de gegevens die u wilt verzamelen. Zie [`context`](/help/web-sdk/commands/configure/context.md) voor meer informatie .

## Instellingen voor mediaverzamelingen configureren {#media-collection}

Met de functie voor het verzamelen van media kunt u gegevens verzamelen die betrekking hebben op mediasessies op uw website.

De verzamelde gegevens kunnen informatie over media playbacks, pauzes, voltooiing, en andere verwante gebeurtenissen omvatten. Nadat deze gegevens zijn verzameld, kunt u deze naar Adobe Experience Platform en/of Adobe Analytics verzenden om rapporten te genereren. Deze functie biedt een uitgebreide oplossing voor het bijhouden en begrijpen van het gedrag van het mediaconsumptie op uw website.

![Afbeelding die de instellingen van de mediagroep van de Web SDK-tagextensie in de gebruikersinterface Tags weergeeft](assets/media-collection.png)


* **[!UICONTROL Channel]**: De naam van het kanaal waar de media inzameling voorkomt. Voorbeeld: `Video channel`.
* **[!UICONTROL Player Name]**: De naam van de mediaspeler.
* **[!UICONTROL Application Version]**: De versie van de toepassing Media Player.
* **[!UICONTROL Main ping interval]**: Frequentie van pingelt voor hoofdinhoud, in seconden. De standaardwaarde is `10`. Waarden kunnen variëren van `10` tot `50` seconden.  Als er geen waarde is opgegeven, wordt de standaardwaarde gebruikt bij het gebruik [automatisch bijgehouden sessies](../../../../web-sdk/commands/createmediasession.md#automatic).
* **[!UICONTROL Ad ping interval]**: Frequentie van pingelt voor advertentie-inhoud, in seconden. De standaardwaarde is `10`. Waarden kunnen variëren van `1` tot `10` seconden. Als er geen waarde is opgegeven, wordt de standaardwaarde gebruikt bij het gebruik [automatisch bijgehouden sessies](../../../../web-sdk/commands/createmediasession.md#automatic)

## Gegevensstroomoverschrijvingen configureren {#datastream-overrides}

Met overschrijvingen van gegevensstroom kunt u aanvullende configuraties voor uw gegevensstreams definiëren. Deze configuraties worden via de SDK van het web doorgegeven aan de Edge Network.

Dit helpt u verschillend gegevensstroomgedrag dan de standaarddegenen teweegbrengen, zonder het creëren van een nieuwe gegevensstroom of het wijzigen van uw bestaande montages.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst moet u de configuratie van uw gegevensstroom overschrijven in het dialoogvenster [configuratiepagina gegevensstroom](/help/datastreams/configure.md).
2. Dan, moet u de met voeten treden naar de Edge Network of via een bevel van SDK van het Web, of door de de markeringsuitbreiding van SDK van het Web te gebruiken.

Zie de gegevensstroom [documentatie bij overschrijvingen van configuratie](/help/datastreams/overrides.md) voor gedetailleerde instructies op hoe te om configuraties met betrekking tot gegevensstroom met voeten te treden.

Als alternatief voor het overgaan van de met voeten treedt door een bevel van SDK van het Web, kunt u de met voeten treden in het scherm van de markeringsuitbreiding vormen hieronder wordt getoond die.

>[!IMPORTANT]
>
DataStream-overschrijvingen moeten per omgeving worden geconfigureerd. De ontwikkelings-, staging- en productieomgevingen hebben allemaal verschillende overschrijvingen. U kunt de instellingen tussen de instellingen kopiëren met behulp van de speciale opties die in het onderstaande scherm worden weergegeven.

![Afbeelding die de configuratie van de gegevensstroom beschrijft, overschrijft deze met de webpagina voor de tagextensie SDK.](assets/datastream-overrides.png)

## Geavanceerde instellingen configureren

Gebruik de **[!UICONTROL Edge base path]** veld als u het basispad moet wijzigen dat wordt gebruikt voor interactie met de Edge Network. Dit zou niet het bijwerken moeten vereisen, maar in het geval dat u aan bèta of alpha deelneemt, zou de Adobe u kunnen vragen om dit gebied te veranderen.

![Afbeelding die de geavanceerde instellingen weergeeft met de webpagina voor de tagextensie SDK.](assets/advanced-settings.png)
