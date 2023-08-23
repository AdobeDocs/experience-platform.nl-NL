---
title: De extensie Adobe Experience Platform Web SDK configureren
description: Hoe te om de de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform in UI te vormen.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: 97b435b9bcaf20be0e41150b6a7a408e083fbd61
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---


# De extensie van de Adobe Experience Platform Web SDK-tag configureren

Met de tagextensie Adobe Experience Platform Web SDK worden gegevens vanuit wegeigenschappen via het Adobe Experience Platform Edge Network verzonden naar Adobe Experience Cloud. Met de extensie kunt u gegevens streamen naar Platform, identiteiten synchroniseren, de toestemmingssignalen van de klant verwerken en automatisch contextgegevens verzamelen.

Dit document behandelt hoe te om de uitbreiding in UI te vormen.

## Aan de slag

Als de uitbreiding van SDK van het Web van het Platform reeds voor een bezit is geïnstalleerd, open het bezit in UI en selecteer **[!UICONTROL Extensions]** tab. Selecteer onder de SDK van het Web Platform **[!UICONTROL Configure]**.

![](assets/configure.png)

Als u de extensie nog niet hebt geïnstalleerd, selecteert u de **[!UICONTROL Catalog]** tab. Van de lijst van beschikbare uitbreidingen, vind de uitbreiding van SDK van het Web van het Platform en selecteer **[!UICONTROL Install]**.

![](assets/install.png)

In beide gevallen, komt u bij de configuratiepagina voor het Web SDK van het Platform aan. In de volgende secties worden de configuratieopties van de extensie uitgelegd.

![](assets/config-screen.png)

## Algemene configuratieopties

De configuratieopties boven aan de pagina vertellen Adobe Experience Platform waar de gegevens moeten worden gerouteerd en welke configuraties op de server moeten worden gebruikt.

### [!UICONTROL Name]

De extensie Adobe Experience Platform Web SDK ondersteunt meerdere exemplaren op de pagina. De naam wordt gebruikt om gegevens naar veelvoudige organisaties met een markeringsconfiguratie te verzenden.

De naam van de extensie wordt standaard ingesteld op &quot;[!DNL alloy]&quot;. U kunt de instantienaam echter wijzigen in elke geldige naam voor een JavaScript-object.

### **[!UICONTROL IMS Organization ID]**

De [!UICONTROL IMS Organization ID] Dit is de organisatie waarnaar u de gegevens wilt verzenden bij de Adobe. Meestal gebruikt u de standaardwaarde die automatisch wordt ingevuld. Wanneer u meerdere exemplaren op de pagina hebt, vult u dit veld met de waarde van de tweede organisatie waarnaar u gegevens wilt verzenden.

### **[!UICONTROL Edge Domain]**

De [!UICONTROL Edge Domain] is het domein waarvan de extensie Adobe Experience Platform gegevens verzendt en ontvangt. De Adobe adviseert gebruikend een 1st-partijdomein (CNAME) voor deze uitbreiding. Het standaard domein van derden werkt voor ontwikkelomgevingen, maar is niet geschikt voor productieomgevingen. Instructies over hoe te opstelling een eerste-partij CNAME zijn vermeld [hier](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Datastreams]

Wanneer een aanvraag naar het Adobe Experience Platform Edge-netwerk wordt verzonden, wordt een gegevensstroom-id gebruikt om naar de serverconfiguratie te verwijzen. U kunt de configuratie bijwerken zonder dat u codewijzigingen op uw website hoeft aan te brengen.

Zie de handleiding op [datastreams](../../../../datastreams/overview.md) voor meer informatie .


## [!UICONTROL Privacy]

![](assets/privacy.png)

De [!UICONTROL Privacy] kunt u configureren hoe de SDK de signalen van uw website voor gebruikerstoestemming verwerkt. Met name kunt u het standaardniveau van toestemming selecteren dat wordt aangenomen door een gebruiker als er geen andere voorkeur voor expliciete toestemming is opgegeven. Het standaard toestemmingsniveau wordt niet bewaard aan het profiel van de gebruiker. In de volgende tabel wordt aangegeven wat elke optie inhoudt:

| [!UICONTROL Default Consent Level] | Beschrijving |
| --- | --- |
| [!UICONTROL In] | Verzamel gebeurtenissen die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft. |
| [!UICONTROL Out] | Gebeurtenissen negeren die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft. |
| [!UICONTROL Pending] | Wachtrij-gebeurtenissen die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft. Als er voorkeuren voor toestemming zijn opgegeven, worden de gebeurtenissen verzameld of genegeerd, afhankelijk van de opgegeven voorkeuren. |
| [!UICONTROL Provided by data element] | Het standaard toestemmingsniveau wordt bepaald door een afzonderlijk gegevenselement dat u bepaalt. Wanneer u deze optie gebruikt, moet u het gegevenselement opgeven met behulp van het opgegeven vervolgkeuzemenu. |

Gebruik uit of in afwachting als u expliciete gebruikerstoestemming voor uw bedrijfsverrichtingen vereist.

## [!UICONTROL Identity]

![](assets/identity.png)

### [!UICONTROL Migrate ECID from VisitorAPI]

Deze optie is standaard ingeschakeld. Als deze functie is ingeschakeld, kan de SDK de cookies AMCV en s_ecid lezen en de door Visitor.js gebruikte AMCV-cookie instellen. Deze functie is belangrijk wanneer u naar SDK van Adobe Experience Platform Web migreert, omdat sommige pagina&#39;s wellicht nog steeds Visitor.js gebruiken. Hierdoor kan de SDK dezelfde ECID blijven gebruiken, zodat gebruikers niet als twee aparte gebruikers worden geïdentificeerd.

### [!UICONTROL Use third-party cookies]

Met deze optie kan de SDK proberen een gebruikers-id op te slaan in een cookie van een andere fabrikant. Als dit gelukt is, wordt de gebruiker geïdentificeerd als één gebruiker terwijl deze in meerdere domeinen navigeert en niet als een afzonderlijke gebruiker op elk domein wordt geïdentificeerd. Als deze optie is ingeschakeld, kan de SDK de gebruikersnaam nog steeds niet opslaan in een cookie van een andere fabrikant als de browser cookies van derden niet ondersteunt of door de gebruiker is geconfigureerd om cookies van derden niet toe te staan. In dit geval slaat de SDK alleen de id op in het domein van de eerste partij.

## [!UICONTROL Personalization]

![](assets/personalization.png)

Als u bepaalde onderdelen wilt verbergen als uw site wordt geladen terwijl er gepersonaliseerde inhoud is geladen, kunt u de elementen opgeven die u wilt verbergen in de voorverborgen stijleditor. Vervolgens kunt u het standaard voorverborgen fragment dat u wordt aangeboden, kopiëren en in het deelvenster `<head>`-element van uw HTML-site.

## [!UICONTROL Data Collection]

![](assets/data-collection.png)

### [!UICONTROL Callback function]

De callback-functie die in de extensie wordt opgegeven, wordt ook [`onBeforeEventSend` function](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) in de bibliotheek. Met deze functie kunt u gebeurtenissen globaal wijzigen voordat ze naar Adobe Edge Network worden verzonden. Meer gedetailleerde informatie over het gebruik van deze functie vindt u [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Click data collection]

De SDK kan automatisch koppelingsklikgegevens voor u verzamelen. Deze functie is standaard ingeschakeld, maar kan met deze optie worden uitgeschakeld. Koppelingen worden ook gemarkeerd als downloadkoppelingen als ze een van de downloadexpressies bevatten die in het dialoogvenster [!UICONTROL Download Link Qualifier] textbox. Adobe biedt u enkele standaardkwalificatietekens voor downloadkoppelingen, maar deze kunnen op elk gewenst moment worden bewerkt.

### [!UICONTROL Automatically collected context data]

Door gebrek, verzamelt SDK bepaalde contextgegevens betreffende apparaat, Web, milieu, en plaatcontext. Als u een lijst van de informatie wilt zien Adobe verzamelt, kunt u het vinden [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Als u deze gegevens niet wilt verzamelen of slechts bepaalde categorieën gegevens wilt verzamelen, kunt u deze opties veranderen.

## [!UICONTROL Datastream Configuration Overrides]

Met de gegevensstroom overschrijft kunt u aanvullende configuraties voor uw gegevensstromen definiëren. Deze configuraties worden via de SDK van het Web doorgegeven aan het Edge-netwerk.

Dit helpt u verschillend gegevensstroomgedrag dan de standaarddegenen teweegbrengen, zonder het creëren van een nieuwe gegevensstroom of het wijzigen van uw bestaande montages.

De configuratieopheffing van gegevensstroom is een proces in twee stappen:

1. Eerst moet u de configuratie van uw gegevensstroom overschrijven in het dialoogvenster [configuratiepagina gegevensstroom](../../../../datastreams/configure.md).
2. Dan, moet u de met voeten treden naar het Netwerk van de Rand of via een bevel van SDK van het Web, of door de de markeringsuitbreiding van SDK van het Web te gebruiken.

Zie de gegevensstroom [documentatie bij overschrijvingen van configuratie](../../../../datastreams/overrides.md) voor gedetailleerde instructies op hoe te om configuraties met betrekking tot gegevensstroom met voeten te treden.

Als alternatief voor het overgaan van de met voeten treedt door een bevel van SDK van het Web, kunt u de met voeten treden in het scherm van de markeringsuitbreiding vormen hieronder wordt getoond die.

>[!IMPORTANT]
>
> DataStream-overschrijvingen moeten per omgeving worden geconfigureerd. De ontwikkelings-, staging- en productieomgevingen hebben allemaal verschillende overschrijvingen. U kunt de instellingen tussen de instellingen kopiëren met behulp van de speciale opties die in het onderstaande scherm worden weergegeven.

![Afbeelding die de configuratie van de gegevensstroom overschrijft in de webSDK-tagextensiepagina.](assets/datastream-overrides.png)

## [!UICONTROL Advanced Settings]

![](assets/advanced-settings.png)

### [!UICONTROL Edge base path]

Gebruik dit veld als u het basispad moet wijzigen dat wordt gebruikt voor interactie met Adobe Edge Network. Dit zou niet het bijwerken moeten vereisen, maar in het geval dat u aan bèta of alpha deelneemt, zou de Adobe u kunnen vragen om dit gebied te veranderen.
