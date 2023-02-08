---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;salesforce;api salesforce marketing cloudbestemming
title: (API) Verbinding met Salesforce-Marketing Cloud
description: Met de Salesforce-Marketing Cloud (voorheen ExactTarget genoemd) kunt u uw accountgegevens exporteren en activeren binnen de Salesforce-Marketing Cloud voor uw zakelijke behoeften.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: d75c272b3c86e25d3f162c630963c10e8206bd9d
workflow-type: tm+mt
source-wordcount: '2342'
ht-degree: 0%

---

# [!DNL (API) Salesforce Marketing Cloud] verbinding

## Overzicht {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (voorheen bekend als [!DNL ExactTarget]) is een digitale marketingsuite waarmee u reizen kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

>[!IMPORTANT]
>
>Let op het verschil tussen deze verbinding en de andere [[!DNL Salesforce Marketing Cloud] verbinding](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) bestaat in de sectie E-mailmarketingcatalogus. Met de andere verbinding met de Salesforce-Marketing Cloud kunt u bestanden exporteren naar een opgegeven opslaglocatie, terwijl dit een op API gebaseerde streamingverbinding is.

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [!DNL Salesforce Marketing Cloud] [update contacten](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, die u toestaat om contacten toe te voegen/contactgegevens voor uw bedrijfsbehoeften bij te werken na het activeren van hen binnen een nieuwe [!DNL Salesforce Marketing Cloud] segment.

[!DNL Salesforce Marketing Cloud] gebruikt OAuth 2 met de Referenties van de Cliënt als authentificatiemechanisme om met te communiceren [!DNL Salesforce Marketing Cloud] API. Instructies voor verificatie aan uw [!DNL Salesforce Marketing Cloud] de instantie is verder onderaan, in de [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL (API) Salesforce Marketing Cloud] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De verkoopafdeling van een platform van de huishuur wil een marketing e-mail aan een gericht klantenpubliek uitzenden. Het marketing team van het platform kan nieuwe contacten toevoegen/bestaande contacten bijwerken *(en hun e-mailadres)* door Adobe Experience Platform, bouwt segmenten van hun eigen off-line gegevens, en verzendt deze segmenten naar [!DNL Salesforce Marketing Cloud], die vervolgens kan worden gebruikt om de marketingcampagne per e-mail te verzenden.

## Vereisten {#prerequisites}

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL (API) Salesforce Marketing Cloud] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) gemaakt in [!DNL Experience Platform].

### Vereisten in [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Platform naar uw [!DNL Salesforce Marketing Cloud] account:

#### U hebt een [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

Bereik uit naar uw [!DNL Salesforce Account Executive] om zich te abonneren op de [!DNL Salesforce Marketing Cloud Account Engagement] product als u dit nog niet hebt.

#### Kenmerken maken binnen [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Bij het activeren van segmenten op de [!DNL (API) Salesforce Marketing Cloud] doel, moet u een waarde in invoeren **[!UICONTROL Mapping ID]** veld voor elk geactiveerd segment, in het **[Segmentatieschema](#schedule-segment-export-example)** stap.

[!DNL Salesforce] vereist deze waarde om segmenten die vanuit het Experience Platform binnenkomen correct te lezen en te interpreteren en hun segmentstatus binnen bij te werken [!DNL Salesforce Marketing Cloud]. Raadpleeg de documentatie bij het Experience Platform voor [Segment Membership Details schema groep](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op segmentstatussen nodig hebt.

Voor elk segment dat u activeert van Platform tot [!DNL Salesforce Marketing Cloud]moet u een kenmerk van het type maken `Text` binnen [!DNL Salesforce]. Gebruik de [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] om kenmerken te maken. De namen van kenmerkvelden worden gebruikt voor de [!DNL (API) Salesforce Marketing Cloud] doelveld en moet worden gemaakt onder het `[!DNL Email Demographics system attribute-set]`. U kunt het veldteken definiëren met maximaal 4000 tekens, afhankelijk van uw zakelijke vereisten. Zie de [!DNL Salesforce Marketing Cloud] [Gegevenstypen gegevensextensies](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) Documentatiepagina voor aanvullende informatie over kenmerktypen.

Zie de [!DNL Salesforce Marketing Cloud] documentatie aan [kenmerken maken](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) als u richtlijnen nodig hebt voor het maken van kenmerken.

Een voorbeeld van het scherm van de gegevensontwerper in [!DNL Salesforce Marketing Cloud], waarin u het kenmerk wilt toevoegen, wordt hieronder weergegeven:
![Salesforce Marketing Cloud UI data designer.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Een weergave van de [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] attribute-set wordt hieronder getoond:
![Kenmerk-set voor demografische kenmerken van de Salesforce-Marketing Cloud UI-e-mail.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

De [!DNL (API) Salesforce Marketing Cloud] doel gebruikt [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) om de attributen en hun Attribuut-Reeksen dynamisch terug te winnen die binnen worden bepaald [!DNL Salesforce Marketing Cloud].

Deze worden weergegeven in het dialoogvenster **[!UICONTROL Target field]** selectievenster wanneer u de [toewijzing](#mapping-considerations-example) in de workflow naar [segmenten activeren naar het doel](#activate). Let op: alleen toewijzingen voor de kenmerken die zijn gedefinieerd in het dialoogvenster [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` attribute-set worden ondersteund.

>[!IMPORTANT]
>
>Within [!DNL Salesforce Marketing Cloud]moet u kenmerken maken met een **[!UICONTROL FIELD NAME]** die exact overeenkomt met de waarde die is opgegeven binnen **[!UICONTROL Mapping ID]** voor elk geactiveerd Platform. In de onderstaande schermafbeelding ziet u bijvoorbeeld een kenmerk met de naam `salesforce_mc_segment_1`. Wanneer het activeren van een segment aan deze bestemming, voeg toe `salesforce_mc_segment_1` als **[!UICONTROL Mapping ID]** om segmentpubliek van Experience Platform in deze eigenschap te bevolken.

Een voorbeeld van het maken van kenmerken in [!DNL Salesforce Marketing Cloud], wordt hieronder weergegeven:
![Schermafbeelding van de Salesforce-Marketing Cloud met een kenmerk.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* Neem bij het maken van het kenmerk geen spatietekens op in de veldnaam. Gebruik in plaats daarvan het onderstrepingsteken `(_)` als scheidingsteken.
>* Een onderscheid maken tussen kenmerken die worden gebruikt voor Platform-segmenten en andere kenmerken binnen [!DNL Salesforce Marketing Cloud]kunt u een herkenbaar voor- of achtervoegsel opnemen voor de kenmerken die worden gebruikt voor Adobe-segmenten. In plaats van `test_segment`, gebruik `Adobe_test_segment` of `test_segment_Adobe`.
>* Als u al andere kenmerken hebt gemaakt in [!DNL Salesforce Marketing Cloud], kunt u de zelfde naam gebruiken zoals het segment van het Platform, om het segment in gemakkelijk te identificeren [!DNL Salesforce Marketing Cloud].


#### Gather [!DNL Salesforce Marketing Cloud] geloofsbrieven {#gather-credentials}

Noteer de onderstaande items voordat u deze verifieert voor de [!DNL (API) Salesforce Marketing Cloud] bestemming.

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Subdomein | Zie [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) om te leren hoe u deze waarde kunt verkrijgen via de [!DNL Salesforce Marketing Cloud] interface. | Als uw [!DNL Salesforce Marketing Cloud] domain is<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>u moet verstrekken `mcq4jrssqdlyc4lph19nnqgzzs84` als de waarde. |
| Client-id | Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om te leren hoe u deze waarde kunt verkrijgen via de [!DNL Salesforce Marketing Cloud] interface. | r23kxxxxxxxx0z05xxxxxx |
| Clientgeheim | Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om te leren hoe u deze waarde kunt verkrijgen via de [!DNL Salesforce Marketing Cloud] interface. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style=&quot;table-layout:auto&quot;}

### Guardrails {#guardrails}

* Salesforce stelt bepaalde [tarieflimieten](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) om eventuele limieten aan te pakken die u tijdens de uitvoering kunt tegenkomen en fouten te reduceren.
   * Zie de [[!DNL Salesforce Marketing Cloud] Prijs voor betrokkenheid](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pagina naar *Download de vergelijkingstabel van de Volledige Uitgave* als een pdf waarin de limieten worden uiteengezet die in uw plan worden opgelegd.
   * De [API-overzicht](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) pagina details extra limieten.
   * Vernieuwen [hier](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) voor een pagina waarop deze gegevens worden gesorteerd.
* Het aantal *aangepaste velden toegestaan per object* varieert afhankelijk van uw Salesforce Edition.
   * Zie de [!DNL Salesforce] [documentatie](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) voor aanvullende richtsnoeren.
   * Als u de limiet hebt bereikt voor *aangepaste velden toegestaan per object* binnen [!DNL Salesforce Marketing Cloud] u zult moeten
      * Oudere kenmerken verwijderen voordat u nieuwe kenmerken toevoegt in [!DNL Salesforce Marketing Cloud].
      * Werk of verwijder om het even welke geactiveerde segmenten in de bestemmingen van het Platform die deze oudere attributennamen als waarde gebruiken voor **[!UICONTROL Mapping ID]** tijdens de [segment plannen](#schedule-segment-export-example) stap.

## Ondersteunde identiteiten {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Contactsleutel. Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) als u aanvullende instructies nodig hebt. | Verplicht |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)*, op basis van uw veldtoewijzing.</li><li> Elke segmentstatus in [!DNL Salesforce Marketing Cloud] wordt bijgewerkt met de corresponderende segmentstatus van het Platform, gebaseerd op de **[!UICONTROL Mapping ID]** waarde die tijdens de [segment plannen](#schedule-segment-export-example) stap.</li></ul> |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, zoeken naar [!DNL (API) Salesforce Marketing Cloud]. U kunt de locatie ook onder de **[!UICONTROL Email marketing]** categorie.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden hieronder in en selecteert u **[!UICONTROL Connect to destination]**. Zie de [Gather [!DNL Salesforce Marketing Cloud] geloofsbrieven](#gather-credentials) voor eventuele richtsnoeren.

| [!DNL (API) Salesforce Marketing Cloud] doel | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Uw [!DNL Salesforce Marketing Cloud] domeinvoorvoegsel. <br>Als uw domein bijvoorbeeld <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> u moet verstrekken `mcq4jrssqdlyc4lph19nnqgzzs84` als de waarde. |
| **[!UICONTROL Client ID]** | Uw [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Client Secret]** | Uw [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Het schermschot van het Platform UI die toont hoe te om aan Marketing Cloud Salesforce voor authentiek te verklaren.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** Als u een groene markering hebt, kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Het schermschot van het Platform UI die de bestemmingsdetails toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL (API) Salesforce Marketing Cloud] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL (API) Salesforce Marketing Cloud] de bestemmingsgebieden, volg de hieronder stappen.

>[!IMPORTANT]
>
>Hoewel de namen van uw kenmerken overeenkomen [!DNL Salesforce Marketing Cloud] account, de toewijzingen voor beide `contactKey` en `personalEmail.address` zijn verplicht. Bij het toewijzen van kenmerken, alleen kenmerken van het Experience Platform `Email Demographics` attribute-set moet binnen de doelvelden worden gebruikt.

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
   ![Voorbeeld van schermafbeelding van gebruikersinterface van Platform voor Nieuwe toewijzing toevoegen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. In de **[!UICONTROL Select target field]** venster, kiest u de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** en selecteer een kenmerk in het menu `Email Demographics` worden weergegeven. De [!DNL (API) Salesforce Marketing Cloud] doel gebruikt [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) om de attributen en hun kenmerkreeksen dynamisch terug te winnen die binnen worden bepaald [!DNL Salesforce Marketing Cloud]. Deze worden weergegeven in het dialoogvenster **[!UICONTROL Target field]** popup wanneer u opstelling [toewijzing](#mapping-considerations-example) in de [segmenten activeren naar workflow](#activate). Opmerking: alleen toewijzingen voor de kenmerken die zijn gedefinieerd in het dialoogvenster [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` kenmerkenset wordt ondersteund.

   * Herhaal deze stappen om de volgende toewijzingen tussen uw XDM-profielschema en [!DNL (API) Salesforce Marketing Cloud]: |Bronveld|Doelveld| Verplicht| |—|—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - |
|`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
      ![Voorbeeld van schermafbeelding van gebruikersinterface van Platform met doeltoewijzingen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

### De segmentuitvoer van het programma en voorbeeld {#schedule-segment-export-example}

Bij het uitvoeren van de [Segmentexport plannen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u de segmenten van het Platform aan de [attributes](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

Om dit te doen, selecteer elk segment, dan ga naam van de attributen van in [!DNL Salesforce Marketing Cloud] in de [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** veld. Zie de [Kenmerk maken binnen [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) voor begeleiding en beste praktijken bij het maken van kenmerken in [!DNL Salesforce Marketing Cloud].

Als uw [!DNL Salesforce Marketing Cloud] kenmerk is `salesforce_mc_segment_1`geeft u deze waarde op in het dialoogvenster [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** om segmentpubliek van Experience Platform in deze eigenschap te bevolken.

Een voorbeeldkenmerk van [!DNL Salesforce Marketing Cloud] wordt hieronder weergegeven:
![Het schermschot van de Marketing Cloud van Salesforce  UI die een attribuut toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Een voorbeeld dat de plaats van wijst [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** wordt hieronder weergegeven:
![Het het schermschot van het Platform UI die de segmentuitvoer van het Programma toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Zoals getoond de [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** moet exact overeenkomen met de waarde die is opgegeven binnen [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]**.

Herhaal deze sectie voor elk geactiveerd segment van het Platform.

Afhankelijk van uw gebruikscase kunnen alle geactiveerde segmenten worden toegewezen aan hetzelfde [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** of naar een andere **[!UICONTROL FIELD NAME]** in [!DNL (API) Salesforce Marketing Cloud]. Een typisch voorbeeld op basis van de hierboven getoonde afbeelding zou kunnen zijn.
| [!DNL (API) Salesforce Marketing Cloud] segmentnaam | [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** | | — | — | — | | Salesforce mc segment 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | Salesforce mc Segment 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteren **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met bestemmingen te navigeren.
   ![Het schermschot van het Platform UI die Browse Doelen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selecteer het doel en controleer of de status **[!UICONTROL enabled]**.
   ![Platform UI screenshot die de Looppas van Doelen Dataflow toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Naar de **[!DNL Activation data]** selecteert u vervolgens een segmentnaam.
   ![Het het schermschot van het Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Controleer de samenvatting van het segment en zorg ervoor dat de telling van profielen aan de telling beantwoordt die binnen het segment wordt gecreeerd.
   ![Platform UI-screenshot voorbeeld met segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Aanmelden bij de [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) website. Navigeer vervolgens naar de **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** en controleer of de profielen van het segment zijn toegevoegd.
   ![De het schermschot van de Marketing Cloud van Salesforce UI die de pagina van Contacten met profielen toont in het segment worden gebruikt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Als u wilt controleren of profielen zijn bijgewerkt, navigeert u naar de **[!UICONTROL Email]** en controleert u of de kenmerkwaarden voor het profiel van het segment zijn bijgewerkt. Indien succesvol, kunt u zien dat elk segmentstatus in [!DNL Salesforce Marketing Cloud] werd bijgewerkt met de overeenkomstige segmentstatus van Platform, gebaseerd op **[!UICONTROL Mapping ID]** de waarde die in de [segment plannen](#schedule-segment-export-example) stap.
   ![De het schermschot van de Marketing Cloud van Salesforce UI die de geselecteerde pagina van E-mail van Contacten met bijgewerkte segmentstatussen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het verplaatsen van gebeurtenissen naar de Salesforce-Marketing Cloud {#unknown-errors}

* Bij het controleren van een gegevensstroomuitvoering kan het volgende foutbericht optreden: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Fout in schermopname van Platform-interface.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Om deze fout te bevestigen, verifieer dat **[!UICONTROL Mapping ID]** die u in de activeringsworkflow aan de [!DNL (API) Salesforce Marketing Cloud] doel komt exact overeen met de naam van het kenmerk dat u hebt gemaakt in [!DNL Salesforce Marketing Cloud]. Zie de [Kenmerk maken binnen [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) voor richtsnoeren.

* Wanneer u een segment activeert, wordt mogelijk een foutbericht weergegeven: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Neem contact op met uw [!DNL Salesforce Marketing Cloud] accountbeheerder om toe te voegen [IP-adressen Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) aan uw [!DNL Salesforce Marketing Cloud] de vertrouwde op IP van rekeningen waaiers. Zie de [!DNL Salesforce Marketing Cloud] [IP Adressen voor Opname op Lijsten van gewenste personen in Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) documentatie als u extra begeleiding nodig hebt.

## Aanvullende bronnen {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) verklaren hoe de contacten met de gespecificeerde informatie in de gespecificeerde attributengroepen worden bijgewerkt.