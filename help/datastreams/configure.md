---
title: Gegevensstromen maken en configureren
description: Leer hoe te om uw cliënt-zijintegratie van SDK van het Web met andere producten van de Adobe en derdebestemmingen te verbinden.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: 370ab0b2a575cc2b5d17f3ae2b3b0b6a6999c462
workflow-type: tm+mt
source-wordcount: '2554'
ht-degree: 0%

---


# Gegevensstromen maken en configureren

In dit document worden de stappen beschreven voor het configureren van een [datastream](./overview.md) in de gebruikersinterface.

## Toegang krijgen tot de [!UICONTROL Datastreams] werkruimte

U kunt gegevensstromen in de UI van de Inzameling van Gegevens of UI van het Experience Platform tot stand brengen en beheren door te selecteren **[!UICONTROL Datastreams]** in de linkernavigatie.

![Gegevensstromen tabblad in de gebruikersinterface voor gegevensverzameling](assets/configure/datastreams-tab.png)

De **[!UICONTROL Datastreams]** wordt een lijst weergegeven met bestaande gegevensstromen, inclusief de vriendelijke naam, id en datum die als laatste is gewijzigd. Naar [Bekijk zijn details en vorm de diensten](#view-details)selecteert u de naam van een gegevensstroom.

Als u meer opties voor een bepaalde gegevensstroom wilt weergeven, selecteert u het pictogram Meer (**...**). Als u het dialoogvenster [basisconfiguratie](#configure) voor de gegevensstroom selecteert u **[!UICONTROL Edit]**. Als u de gegevensstroom wilt verwijderen, selecteert u **[!UICONTROL Delete]**.

![Opties voor het bewerken of verwijderen van een bestaande gegevensstroom](assets/configure/edit-datastream.png)

## Een gegevensstroom maken {#create}

Als u een gegevensstroom wilt maken, selecteert u **[!UICONTROL New Datastream]**.

![Nieuwe gegevensstroom selecteren](assets/configure/new-datastream-button.png)

De workflow voor het maken van de gegevensstroom wordt weergegeven, te beginnen bij de configuratiestap. Van hier, moet u een naam en een facultatieve beschrijving voor de gegevensstroom verstrekken.

Als u een gegevensstroom voor gebruik in Experience Platform vormt en u ook SDK van het Web gebruikt, moet u ook selecteren [op gebeurtenissen gebaseerd XDM-schema (Experience Data Model)](../xdm/classes/experienceevent.md) om de gegevens te vertegenwoordigen u bij het opnemen bent.

![Basisconfiguratie voor een gegevensstroom](assets/configure/configure.png)

### Geolocatie en netwerkopzoekhandeling configureren {#geolocation-network-lookup}

De montages van de geolocatie en van de netwerkraadpleging helpen u het niveau van granulariteit van de geografische en netwerk-vlakke gegevens bepalen die u wilt verzamelen.

Breid uit **[!UICONTROL Geolocation and network lookup]** om de hieronder beschreven instellingen te configureren.

![Het configuratiescherm van de gegevensstroom met de geolocatie en de montages van de netwerkraadpleging benadrukt.](assets/configure/geolookup.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Geo Lookup] | Hiermee schakelt u geolocatiezoekopdrachten voor de geselecteerde opties in op basis van het IP-adres van de bezoeker. Beschikbare opties zijn: <ul><li>**Land**: Populaten `xdm.placeContext.geo.countryCode`</li><li>**Postcode**: Populaten `xdm.placeContext.geo.postalCode`</li><li>**Staat/provincie**: Populaten `xdm.placeContext.geo.stateProvince`</li><li>**DMA**: Populaten `xdm.placeContext.geo.dmaID`</li><li>**Plaats**: Populaten `xdm.placeContext.geo.city`</li><li>**Breedte**: Populaten `xdm.placeContext.geo._schema.latitude`</li><li>**Lengtegraad**: Populaten `xdm.placeContext.geo._schema.longitude`</li></ul>Selecteren **[!UICONTROL City]**, **[!UICONTROL Latitude]**, of **[!UICONTROL Longitude]** biedt coördinaten tot twee decimale punten, ongeacht welke andere opties zijn geselecteerd. Dit wordt beschouwd als granulariteit op stadsniveau.<br> <br>Als u geen optie selecteert, worden geolocatieopzoekingen uitgeschakeld. Geolocatie gebeurt voor [!UICONTROL IP Obfuscation], hetgeen betekent dat de [!UICONTROL IP Obfuscation] instellen. |
| [!UICONTROL Network Lookup] | Laat netwerkraadplegingen voor de geselecteerde opties toe die op het IP van de bezoeker adres worden gebaseerd. Beschikbare opties zijn: <ul><li>**Vervoerder**: Populaten `xdm.environment.carrier`</li><li>**Domein**: Populaten `xdm.environment.domain`</li><li>**ISP**: Populaten `xdm.environment.ISP`</li></ul> |

Als u een van de bovenstaande velden inschakelt voor gegevensverzameling, moet u ervoor zorgen dat u de [`context`](/help/web-sdk/commands/configure/context.md) arraybezit wanneer het vormen van het Web SDK.

De opzoekvelden van Geolocatie gebruiken de `context` arraytekenreeks `"placeContext"`, terwijl de gebieden van de netwerkraadpleging gebruiken `context` arraytekenreeks `"environment"`.

Zorg er ook voor dat elk gewenst XDM-veld in uw schema voorkomt. Als dit niet het geval is, kunt u de meegeleverde Adobe toevoegen `Environment Details` veldgroep aan uw schema.

### Opzoeken van apparaat configureren {#geolocation-device-lookup}

De **[!UICONTROL Device Lookup]** Met instellingen kunt u apparaatspecifieke informatie selecteren die u wilt verzamelen.

Breid uit **[!UICONTROL Device Lookup]** om de hieronder beschreven instellingen te configureren.

![Het configuratiescherm van de gegevensstroom met de benadrukte montages van de apparatenraadpleging.](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>De instellingen in de onderstaande tabel sluiten elkaar uit. U kunt niet beide gebruikersagent-gegevens selecteren *en* de opzoekgegevens van het apparaat tegelijkertijd.

| Instelling | Beschrijving |
| --- | --- |
| **[!UICONTROL Keep user agent and client hints headers]** | Selecteer deze optie als u alleen de gegevens wilt verzamelen die in de userAgent-tekenreeks zijn opgeslagen. Deze instelling is standaard geselecteerd. Populaten `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL Use device lookup to collect the following information]** | Selecteer deze optie als u een of meer van de volgende apparaatspecifieke informatie wilt verzamelen: <ul><li>**[!UICONTROL Device]** informatie:<ul><li>**Apparaatfabrikant**: Populaten `xdm.device.manufacturer`</li><li>**Apparaatmodel**: Populaten `xdm.device.modelNumber`</li><li>**Marketingnaam**: Populaten `xdm.device.model`</li></ul></li><li>**[!UICONTROL Hardware]** informatie: <ul><li>**Type hardware**: Populaten `xdm.device.type`</li><li>**Weergavehoogte**: Populaten `xdm.device.screenHeight`</li><li>**Weergavebreedte**: Populaten `xdm.device.screenWidth`</li><li>**Kleurdiepte weergeven**: Populaten `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL Browser]** informatie: <ul><li>**Browserleverancier**: Populaten `xdm.environment.browserDetails.vendor`</li><li>**Browsernaam**: Populaten `xdm.environment.browserDetails.name`</li><li>**Browserversie**: Populaten `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL Operating system]** informatie: <ul><li>**OS-leverancier**: Populaten `xdm.environment.operatingSystemVendor`</li><li>**Naam besturingssysteem**: Populaten `xdm.environment.operatingSystem`</li><li>**Versie besturingssysteem**: Populaten `xdm.environment.operatingSystemVersion`</li></ul></li></ul>Opzoekgegevens van het apparaat kunnen niet samen met de gebruikersagent en de clienthints worden verzameld. Als u ervoor kiest apparaatinformatie te verzamelen, wordt de verzameling van gebruikersagent- en clienthints uitgeschakeld en andersom. |
| **[!UICONTROL Do not collect any device information]** | Selecteer deze optie als u geen informatie over het zoeken van apparaten wilt verzamelen. Er worden geen apparaat-, hardware-, browser-, besturingssysteem-, gebruikersagent- of clientgegevens verzameld. |

Als u een van de bovenstaande velden inschakelt voor gegevensverzameling, moet u ervoor zorgen dat u de [`context`](/help/web-sdk/commands/configure/context.md) arraybezit wanneer het vormen van het Web SDK.

Apparaat- en hardwaregegevens gebruiken de `context` arraytekenreeks `"device"`, terwijl de browser en besturingssysteeminformatie de `context` arraytekenreeks `"environment"`.

Zorg er ook voor dat elk gewenst XDM-veld in uw schema voorkomt. Als dit niet het geval is, kunt u de meegeleverde Adobe toevoegen `Environment Details` veldgroep aan uw schema.

### Geavanceerde opties configureren {#@advanced-options}

Selecteer **[!UICONTROL Advanced Options]**. Hier, kunt u extra gegevensstroommontages, zoals IP obfuscation, de koekjes van eerste identiteitskaart van de Partij, en meer vormen.

![Geavanceerde configuratieopties](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> U bent ervoor verantwoordelijk dat u alle benodigde machtigingen, toestemmingen, toestemmingen, toestemmingen, en toestemming hebt verkregen die krachtens de toepasselijke wetten en verordeningen vereist zijn voor het verzamelen, verwerken en verzenden van persoonlijke gegevens, met inbegrip van nauwkeurige geolocatiegegevens.
> 
> Uw IP selectie van de adresverwarring beïnvloedt niet het niveau van geolocatieinformatie die uit het IP adres wordt afgeleid en naar uw gevormde oplossingen van de Adobe wordt verzonden. Geolocation lookups moeten worden beperkt of afzonderlijk worden uitgeschakeld.

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL IP Obfuscation] | Geeft het type IP-verduistering aan dat op de gegevensstroom moet worden toegepast. Om het even welke verwerking die op klantIP wordt gebaseerd wordt beïnvloed door IP het obfuseren plaatsen. Dit omvat alle diensten van het Experience Cloud die gegevens van uw gegevensstroom ontvangen. <p>Beschikbare opties:</p> <ul><li>**[!UICONTROL None]**: Schakelt IP-verduistering uit. Het volledige gebruikersIP adres wordt verzonden via de datastream.</li><li>**[!UICONTROL Partial]**: Voor IPv4 adressen, verduistert het laatste octet van het gebruikersIP adres. Voor IPv6 adressen, verduistert de laatste 80 beetjes van het adres. <p>Voorbeelden:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Full]**: Verduistert het volledige IP adres. <p>Voorbeelden:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> Het effect van IP-verduistering op andere Adobe producten: <ul><li>**Adobe Target**: Het gegevensstroomniveau [!UICONTROL IP obfuscation] wordt toegepast vóór de [!UICONTROL IP obfuscation] uitgevoerd in Adobe Target, aan alle IP adressen aanwezig op het verzoek. Bijvoorbeeld wanneer het gegevensstroomniveau [!UICONTROL IP obfuscation] optie is ingesteld op **[!UICONTROL Full]** en de optie van de Verduistering van Adobe Target IP wordt geplaatst aan **[!UICONTROL Last octet obfuscation]** Adobe Target ontvangt een volledig verduisterde IP. Indien het gegevensstroomniveau [!UICONTROL IP obfuscation] optie is ingesteld op **[!UICONTROL Partial]** en de optie van de Verduistering van Adobe Target IP wordt geplaatst aan **[!UICONTROL Full]** Adobe Target ontvangt een gedeeltelijk verduisterde IP en past daarop de volledige verduistering toe. De verwarring van Adobe Target IP wordt beheerd onafhankelijk van datastream één. Zie de Adobe Target documentatie op [IP obfuscatie](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/privacy.html) en [geolocatie](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) voor meer informatie .</li><li>**Audience Manager**: Het gegevensstroomniveau [!UICONTROL IP obfuscation] instelling wordt toegepast vóór de instelling [!UICONTROL IP obfuscation] uitgevoerd in Audience Manager, aan alle IP adressen huidig in het verzoek. Elke opzoekhandeling van de geolocatie door de Audience Manager wordt beïnvloed door het niveau van de gegevensstroom [!UICONTROL IP obfuscation] -optie. Een opzoekhandeling naar een geolocatie in de Audience Manager, gebaseerd op een volledig verduisterde IP, resulteert in een onbekend gebied en alle segmenten op basis van de resulterende geolocatiegegevens worden niet uitgevoerd. Zie de documentatie van de Audience Manager op [IP obfuscatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html) voor meer informatie .</li><li>**Adobe Analytics**: Als IP-verduistering op gegevensstroomniveau wordt ingesteld op **[!UICONTROL Full]**, behandelt Adobe Analytics het IP-adres als leeg. Dit beïnvloedt om het even welke verwerking van Analytics die van IP adres, zoals geolocation raadplegingen en IP het filtreren afhangt. Voor Analytics om de onverduisterde of gedeeltelijk verduisterde IP adressen te ontvangen, plaats het IP verduisteren plaatsen aan **[!UICONTROL Partial]** of **[!UICONTROL None]**. Gedeeltelijk verduisterde en onverduisterde IP adressen kunnen verder worden verduisterd binnen Analytics. Zie de Adobe Analytics [documentatie](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html) voor details op hoe te om IP verwarring in Analytics toe te laten. Als het IP adres volledig verduisterd is en de paginaconte geen heeft [!DNL ECID] noch [!DNL VisitorID]En dan laat Analytics de hit vallen in plaats van een [Fallback-id](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html?lang=en), die gedeeltelijk op het IP-adres is gebaseerd.</li></ul> |
| [!UICONTROL First Party ID Cookie] | Als deze instelling is ingeschakeld, geeft de Edge Network de opdracht naar een opgegeven cookie te verwijzen wanneer een gebruiker een [apparaat-id van eerste partij](../web-sdk/identity/first-party-device-ids.md)in plaats van deze waarde op te zoeken in het identiteitsoverzicht.<br><br>Als u deze instelling inschakelt, moet u de naam opgeven van het cookie dat de id moet opslaan. |
| [!UICONTROL Third Party ID Sync] | De syncs van identiteitskaart kunnen in containers worden gegroepeerd om verschillende syncs van identiteitskaart toe te laten om op verschillende tijden worden in werking gesteld. Als deze instelling is ingeschakeld, kunt u opgeven welke container met id-syncs wordt uitgevoerd voor deze gegevensstroom. |
| [!UICONTROL Third Party ID Sync Container ID] | De numerieke id van de container die wordt gebruikt voor synchronisatie van externe id&#39;s. |
| [!UICONTROL Container ID Overrides] | In deze sectie kunt u aanvullende id&#39;s van de synchronisatiecontainer van derden definiëren waarmee u de standaard id&#39;s kunt overschrijven. |
| [!UICONTROL Access Type] | Bepaalt het authentificatietype dat de Edge Network voor de gegevensstroom goedkeurt. <ul><li>**[!UICONTROL Mixed Authentication]**: Als deze optie is ingeschakeld, accepteert de Edge Network zowel geverifieerde als niet-geverifieerde aanvragen. Selecteer deze optie als u de SDK van het Web wilt gebruiken of [Mobile SDK](https://developer.adobe.com/client-sdks/home/), samen met de [Server-API](../server-api/overview.md). </li><li>**[!UICONTROL Authenticated Only]**: Als deze optie is ingeschakeld, accepteert de Edge Network alleen geverifieerde aanvragen. Selecteer deze optie als u alleen de server-API wilt gebruiken en niet-geverifieerde aanvragen door de Edge Network moeten worden verwerkt.</li></ul> |
| [!UICONTROL Media Analytics] | Maakt verwerking van streaming tracking-gegevens voor Edge Network-integratie via Experience Platform SDK&#39;s of [Media Edge-API](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/getting-started/). Meer informatie over Media Analytics van de [documentatie](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html). |

Als u vanaf hier uw gegevensstroom configureert voor Experience Platform, volgt u de zelfstudie [Gegevensvoorvoegsel voor gegevensverzameling](./data-prep.md) om uw gegevens toe te wijzen aan een de gebeurtenisschema van het Platform alvorens aan deze gids terug te keren. Anders selecteert u **[!UICONTROL Save]** en ga verder met de volgende sectie.

## Gegevens gegevensstroom weergeven {#view-details}

Nadat u een nieuwe gegevensstroom hebt geconfigureerd of een bestaande gegevensstroom hebt geselecteerd, wordt de detailpagina voor die gegevensstroom weergegeven. Hier vindt u meer informatie over de gegevensstroom, inclusief de bijbehorende id.

![Detailpagina DataStream.](assets/configure/view-details.png)

Vanuit het scherm met gegevensstroomdetails kunt u [toevoegen, services](#add-services) om functies in te schakelen van de Adobe Experience Cloud-producten waartoe u toegang hebt. U kunt de gegevensstroom ook uitgeven [basisconfiguratie](#create), werkt de [toewijzingsregels](./data-prep.md), [de gegevensstroom kopiëren](#copy), of deze volledig verwijderen.

## Services toevoegen aan een gegevensstroom {#add-services}

Selecteer op de detailpagina van een gegevensstroom de optie **[!UICONTROL Add Service]** om de beschikbare services voor die gegevensstroom toe te voegen.

![Selecteer Service toevoegen om door te gaan.](assets/configure/add-service.png)

Voor het volgende scherm, gebruik dropdown menu om de dienst te selecteren voor deze gegevensstroom te vormen. Alleen de services waartoe u toegang hebt, worden in deze lijst weergegeven.

![Selecteer een service in de lijst.](assets/configure/service-selection.png)

Selecteer de gewenste service, vul de configuratieopties in die worden weergegeven en selecteer **[!UICONTROL Save]** om de dienst aan de datastream toe te voegen. Alle toegevoegde diensten verschijnen in de detailmening voor de gegevensstroom.

![Services die aan een gegevensstroom zijn toegevoegd](assets/configure/services-added.png)

In de onderstaande subsecties worden de configuratieopties voor elke service beschreven.

>[!NOTE]
>
>Elke de dienstconfiguratie bevat **[!UICONTROL Enabled]** schakelt die automatisch wordt geactiveerd wanneer de service wordt geselecteerd. Als u de geselecteerde service voor deze gegevensstroom wilt uitschakelen, selecteert u de **[!UICONTROL Enabled]** weer schakelen.

### Adobe Analytics-instellingen {#analytics}

Deze service bepaalt of en hoe gegevens naar Adobe Analytics worden verzonden. Zie [Gegevens verzenden naar Adobe Analytics](/help/web-sdk/use-cases/adobe-analytics.md).

![Adobe Analytics-gegevensstroominstellingen.](assets/configure/analytics-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Report Suite ID] | **(Vereist)** De id van de Analytics-rapportsuite waarnaar u gegevens wilt verzenden. Deze id is te vinden in de gebruikersinterface van Adobe Analytics onder [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Als de veelvoudige rapportreeksen worden gespecificeerd, dan worden de gegevens gekopieerd aan elke rapportreeks. |
| [!UICONTROL Visitor ID namespace] | (Optioneel) De naamruimte die u wilt gebruiken voor de Adobe Analytics [bezoekerID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html). Wanneer u een gebeurtenis verzendt met een waarde die voor deze naamruimte is opgegeven, wordt deze automatisch gebruikt als de `visitorID` in Analytics. |
| [!UICONTROL Report Suite Overrides] | In deze sectie, kunt u extra rapportreeks IDs toevoegen die u kunt gebruiken om het gebrek met voeten te treden. |

### Adobe Audience Manager-instellingen {#audience-manager}

Deze service bepaalt of en hoe gegevens naar Adobe Audience Manager worden verzonden. Alles wat nodig is om gegevens naar de Audience Manager te verzenden, moet deze sectie inschakelen. De andere instellingen zijn optioneel, maar worden wel aangemoedigd.

![Adobe publiek beheert gegevensstroominstellingen.](assets/configure/audience-manager-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Cookie Destinations Enabled] | Staat SDK toe om segmentinformatie via te delen [koekjesbestemmingen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) van [!DNL Audience Manager]. |
| [!UICONTROL URL Destinations Enabled] | Staat SDK toe om segmentinformatie via te delen [URL-doelen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html) van [!DNL Audience Manager]. |

### Adobe Experience Platform-instellingen {#aep}

>[!IMPORTANT]
>
>Wanneer het toelaten van een gegevensstroom voor Platform, neem nota van de zandbak van het Platform die u momenteel gebruikt, zoals getoond in het hoogste lint van UI.
>
>![Geselecteerde sandbox](assets/configure/platform-sandbox.png)
>
>Sandboxen zijn virtuele partities in Adobe Experience Platform waarmee u uw gegevens en implementaties kunt isoleren van die in uw organisatie. Wanneer een gegevensstroom is gemaakt, kan de sandbox niet meer worden gewijzigd. Zie voor meer informatie over de rol van sandboxen in het Experience Platform de klasse [sandboxdocumentatie](../sandboxes/home.md).

Deze service bepaalt of en hoe gegevens naar Adobe Experience Platform worden verzonden.

![Adobe Experience Platform-gegevensstroominstellingen.](assets/configure/platform-config.png)

| Instelling | Beschrijving |
|---| --- |
| [!UICONTROL Event Dataset] | **(Vereist)** Selecteer de dataset van het Platform dat de gegevens van de klantengebeurtenis zullen worden gestroomd aan. Dit schema moet de [XDM ExperienceEvent, klasse](../xdm/classes/experienceevent.md). Als u aanvullende gegevenssets wilt toevoegen, selecteert u **[!UICONTROL Add Event Dataset]**. |
| [!UICONTROL Profile Dataset] | Selecteer de dataset van het Platform dat de gegevens van de klantenattributen zullen worden verzonden naar. Dit schema moet de [Afzonderlijke XDM-profielklasse](../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Laat Offer decisioning voor de implementaties van SDK van het Web toe. Zie de handleiding op [het gebruiken van Offer decisioning met Web SDK](../web-sdk/personalization/offer-decisioning/offer-decisioning-overview.md) voor meer details over de implementatie.<br><br>Raadpleeg voor meer informatie over de mogelijkheden van Offer decisioning de [Adobe Journey Optimizer-documentatie](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html). |
| [!UICONTROL Edge Segmentation] | Inschakelen [randsegmentatie](../segmentation/ui/edge-segmentation.md) voor deze gegevensstroom. Wanneer de SDK gegevens via een voor edge-segmentatie ingeschakelde gegevensstroom verzendt, worden bijgewerkte segmentlidmaatschappen voor het profiel in kwestie teruggestuurd in de reactie.<br><br>Deze optie kan in combinatie met [!UICONTROL Personalization Destinations] for [gebruiksgevallen voor personalisatie op de volgende pagina](../destinations/ui/activate-edge-personalization-destinations.md). |
| [!UICONTROL Personalization Destinations] | Wanneer u deze optie inschakelt nadat u het [!UICONTROL Edge Segmentation] checkbox, staat deze optie de datastream toe om met verpersoonlijkingsbestemmingen, zoals te verbinden [Aangepaste personalisatie](../destinations/catalog/personalization/custom-personalization.md).<br><br>Raadpleeg de documentatie bij bestemmingen voor specifieke stappen over [het vormen verpersoonlijkingsbestemmingen](../destinations/ui/activate-edge-personalization-destinations.md). |
| [!UICONTROL Adobe Journey Optimizer] | Inschakelen [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) voor deze gegevensstroom. <br><br> Als u deze optie inschakelt, kan de gegevensstroom gepersonaliseerde inhoud van binnenkomende webcampagnes en op apps gebaseerde campagnes retourneren in [!DNL Adobe Journey Optimizer]. Deze optie is vereist [!UICONTROL Edge Segmentation] om actief te zijn. Indien [!UICONTROL Edge Segmentation] is uitgeschakeld, wordt deze optie grijs weergegeven. |

### Adobe Target-instellingen {#target}

Deze service bepaalt of en hoe gegevens naar Adobe Target worden verzonden.

![Adobe Target-gegevensstroominstellingen.](assets/configure/target-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Property Token] | [!DNL Target] staat klanten toe om toestemmingen te controleren door eigenschappen te gebruiken. Zie de handleiding voor meer informatie over eigenschappen [configureren van bedrijfsmachtigingen](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) in de [!DNL Target] documentatie.<br><br>Het eigenschapstoken vindt u in de gebruikersinterface van Adobe Target onder [!UICONTROL Setup] > [!UICONTROL Properties]. |
| [!UICONTROL Target Environment ID] | [Milieu in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) helpen u bij het beheren van uw implementatie in alle ontwikkelingsstadia. Deze instelling geeft aan welke omgeving u wilt gebruiken voor deze gegevensstroom.<br><br>De beste manier is om dit voor elk van uw `dev`, `stage`, en `prod` gegevensstroomomgevingen om dingen eenvoudig te houden. Als u echter al Adobe Target-omgevingen hebt gedefinieerd, kunt u deze gebruiken. |
| [!UICONTROL Target Third Party ID namespace] | De naamruimte voor de identiteit van de `mbox3rdPartyId` wilt gebruiken voor deze gegevensstroom. Zie de handleiding op [uitvoeren `mbox3rdPartyId` met de Web SDK](../web-sdk/personalization/adobe-target/using-mbox-3rdpartyid.md) voor meer informatie . |
| [!UICONTROL Property Token Overrides] | In deze sectie kunt u aanvullende eigenschapstokens definiëren die u kunt gebruiken om de standaardtokens te overschrijven. |

### [!UICONTROL Event Forwarding] instellingen

Deze service bepaalt of en hoe gegevens worden verzonden naar [gebeurtenis doorsturen](../tags/ui/event-forwarding/overview.md).

![Het door:sturen van de gebeurtenis sectie van het de configuratiescherm van de gegevensstroom.](assets/configure/event-forwarding-config.png)

| Instelling | Beschrijving |
| --- | --- |
| [!UICONTROL Launch Property] | **(Vereist)** De gebeurtenis die bezit door:sturen dat u gegevens naar wilt verzenden. |
| [!UICONTROL Launch Environment] | **(Vereist)** De omgeving binnen de geselecteerde eigenschap waarnaar u gegevens wilt verzenden. |

>[!NOTE]
>
>U kunt **[!UICONTROL Manually enter IDs]** om in de bezit en omgevingsnamen in plaats van het gebruiken van dropdown menu&#39;s te typen.

## Een gegevensstroom kopiëren {#copy}

U kunt een kopie van een bestaande gegevensstroom maken en de details ervan desgewenst wijzigen.

>[!NOTE]
>
>Gegevensstromen kunnen alleen worden gekopieerd binnen dezelfde map [sandbox](../sandboxes/home.md). Met andere woorden, u kunt geen gegevensstroom van één zandbak aan een andere kopiëren.

Vanaf de hoofdpagina in het dialoogvenster [!UICONTROL Datastreams] werkruimte, selecteert u de ellips (**...**) voor de gegevensstroom in kwestie, dan selecteren **[!UICONTROL Copy]**.

![Afbeelding die de optie Kopiëren weergeeft die wordt geselecteerd in de lijstweergave van de gegevensstroom.](assets/configure/copy-datastream-list.png)

U kunt ook **[!UICONTROL Copy Datastream]** in de detailweergave van een bepaalde gegevensstroom.

![De optie Kopiëren die wordt geselecteerd in de weergave met gegevensstroomdetails.](assets/configure/copy-datastream-details.png)

Er wordt een bevestigingsdialoogvenster weergegeven waarin u wordt gevraagd een unieke naam op te geven voor de nieuwe gegevensstroom die moet worden gemaakt, en waarin u informatie kunt vinden over de configuratieopties waarover u de gegevens wilt kopiëren. Indien klaar, selecteert u **[!UICONTROL Copy]**.

![Bevestigingsdialoogvenster voor het kopiëren van een gegevensstroom.](assets/configure/copy-datastream-confirm.png)

De hoofdpagina van de [!UICONTROL Datastreams] wordt de werkruimte opnieuw weergegeven met de nieuwe gegevensstroom die wordt weergegeven.

## Volgende stappen

Deze gids behandelde hoe te om gegevensstromen in de Inzameling van Gegevens UI te beheren. Voor meer informatie over om SDK van het Web na vestiging een gegevensstroom te installeren en te vormen, verwijs naar [E2E-handleiding voor gegevensverzameling](../collection/e2e.md#install).
