---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;salesforce;api salesforce marketing cloudbestemming
title: (API) Verbinding met Salesforce-Marketing Cloud
description: Met de Salesforce-Marketing Cloud (voorheen ExactTarget genoemd) kunt u uw accountgegevens exporteren en activeren binnen de Salesforce-Marketing Cloud voor uw zakelijke behoeften.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 8e37ff057ec0fb750bc7b4b6f566f732d9fe5d68
workflow-type: tm+mt
source-wordcount: '2864'
ht-degree: 0%

---

# [!DNL (API) Salesforce Marketing Cloud] verbinding

## Overzicht {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (voorheen bekend als [!DNL ExactTarget]) is een digitale marketingsuite waarmee u reizen kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

>[!IMPORTANT]
>
>Let op het verschil tussen deze verbinding en de andere [[!DNL Salesforce Marketing Cloud] verbinding](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) bestaat in de sectie E-mailmarketingcatalogus. Met de andere verbinding met de Salesforce-Marketing Cloud kunt u bestanden exporteren naar een opgegeven opslaglocatie, terwijl dit een op API gebaseerde streamingverbinding is.

Vergeleken met [!DNL Salesforce Marketing Cloud Account Engagement] dat meer gericht is op **B2B** de [!DNL (API) Salesforce Marketing Cloud] doel is ideaal voor **B2C** gebruik van gevallen met kortere transactionele besluitvormingscycli. U kunt grotere datasets consolideren die het gedrag van uw doelpubliek vertegenwoordigen om marketing campagnes aan te passen en te verbeteren door contacten, vooral van datasets buiten voorrang te geven en te segmenteren [!DNL Salesforce]. *Opmerking: Experience Platform heeft ook een verbinding voor de [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [!DNL Salesforce Marketing Cloud] [update contacten](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, waarmee u **contactpersonen toevoegen en contactgegevens bijwerken** voor uw bedrijfsbehoeften na het activeren van hen binnen een nieuw [!DNL Salesforce Marketing Cloud] segment.

[!DNL Salesforce Marketing Cloud] gebruikt OAuth 2 met de Referenties van de Cliënt als authentificatiemechanisme om met te communiceren [!DNL Salesforce Marketing Cloud] API. Instructies voor verificatie aan uw [!DNL Salesforce Marketing Cloud] de instantie is verder onderaan, in de [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Om u te helpen beter begrijpen hoe en wanneer u het [!DNL (API) Salesforce Marketing Cloud] doel, hier is een geval van steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De verkoopafdeling van een platform van de huishuur wil een marketing e-mail aan een gericht klantenpubliek uitzenden. Het marketing team van het platform kan nieuwe contacten toevoegen/bestaande contacten bijwerken *(en hun e-mailadres)* door Adobe Experience Platform, bouwt publiek van hun eigen off-line gegevens en verzendt deze publiek naar [!DNL Salesforce Marketing Cloud], die vervolgens kan worden gebruikt om de marketingcampagne per e-mail te verzenden.

## Vereisten {#prerequisites}

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL (API) Salesforce Marketing Cloud] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) gemaakt in [!DNL Experience Platform].

### Vereisten in [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Platform naar uw [!DNL Salesforce Marketing Cloud] account:

#### U hebt een [!DNL Salesforce Marketing Cloud] account {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] account met een abonnement op de [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) Het product is verplicht verder te gaan.

Uitstrekken tot [[!DNL Salesforce] Ondersteuning](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) als u geen [!DNL Salesforce Marketing Cloud] -account of uw account ontbreekt het [!DNL Marketing Cloud Engagement] productabonnement.

#### Kenmerken maken binnen [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Wanneer het publiek wordt geactiveerd naar de [!DNL (API) Salesforce Marketing Cloud] doel, moet u een waarde in invoeren **[!UICONTROL Mapping ID]** veld voor elk geactiveerd publiek, in de **[Publiek schema](#schedule-segment-export-example)** stap.

[!DNL Salesforce] vereist deze waarde om het publiek dat vanuit het Experience Platform binnenkomt, correct te lezen en te interpreteren en zijn publieksstatus binnen bij te werken [!DNL Salesforce Marketing Cloud]. Raadpleeg de documentatie bij het Experience Platform voor [Publiek Lidmaatschap Details schema groep](/help/xdm/field-groups/profile/segmentation.md) als u hulp over publieksstatus nodig hebt.

Voor elk publiek dat u activeert van Platform tot [!DNL Salesforce Marketing Cloud]moet u een kenmerk van het type maken `Text` binnen [!DNL Salesforce]. Gebruik de [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] om kenmerken te maken. De namen van kenmerkvelden worden gebruikt voor de [!DNL (API) Salesforce Marketing Cloud] doelveld tijdens het **[!UICONTROL Mapping]** stap. U kunt het veldteken definiëren met maximaal 4000 tekens, afhankelijk van uw zakelijke vereisten. Zie de [!DNL Salesforce Marketing Cloud] [Gegevenstypen gegevensextensies](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) Documentatiepagina voor aanvullende informatie over kenmerktypen.

Zie de [!DNL Salesforce Marketing Cloud] documentatie aan [kenmerken maken](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) als u richtlijnen nodig hebt voor het maken van kenmerken.

Een voorbeeld van het scherm van de gegevensontwerper in [!DNL Salesforce Marketing Cloud], waarin u het kenmerk wilt toevoegen, wordt hieronder weergegeven:
![Salesforce Marketing Cloud UI data designer.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Een weergave van de [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] attribute-set wordt hieronder getoond:
![Kenmerk-set voor demografische kenmerken van de Salesforce-Marketing Cloud UI-e-mail.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

De [!DNL (API) Salesforce Marketing Cloud] doel gebruikt [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) om de attributen en hun Attribuut-Reeksen dynamisch terug te winnen die binnen worden bepaald [!DNL Salesforce Marketing Cloud].

Deze worden weergegeven in het dialoogvenster **[!UICONTROL Target field]** selectievenster wanneer u de [toewijzing](#mapping-considerations-example) in de workflow naar [publiek naar doel activeren](#activate).

>[!IMPORTANT]
>
>Within [!DNL Salesforce Marketing Cloud]moet u kenmerken maken met een **[!UICONTROL FIELD NAME]** die exact overeenkomt met de waarde die is opgegeven binnen **[!UICONTROL Mapping ID]** voor elk geactiveerd platformsegment. In de onderstaande schermafbeelding ziet u bijvoorbeeld een kenmerk met de naam `salesforce_mc_segment_1`. Wanneer u een publiek activeert naar deze bestemming, voegt u `salesforce_mc_segment_1` als **[!UICONTROL Mapping ID]** om het publiek te vullen van Experience Platform in dit kenmerk.

Een voorbeeld van het maken van kenmerken in [!DNL Salesforce Marketing Cloud], wordt hieronder weergegeven:
![Schermafbeelding van de Salesforce-Marketing Cloud met een kenmerk.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* Neem bij het maken van het kenmerk geen spatietekens op in de veldnaam. Gebruik in plaats daarvan het onderstrepingsteken `(_)` als scheidingsteken.
>* Een onderscheid maken tussen kenmerken die worden gebruikt voor het publiek van het platform en andere kenmerken binnen [!DNL Salesforce Marketing Cloud]kunt u een herkenbaar voor- of achtervoegsel opnemen voor de kenmerken die worden gebruikt voor Adobe-segmenten. In plaats van `test_segment`, gebruik `Adobe_test_segment` of `test_segment_Adobe`.
>* Als u al andere kenmerken hebt gemaakt in [!DNL Salesforce Marketing Cloud], kunt u de zelfde naam gebruiken zoals het segment van het Platform, om het publiek in gemakkelijk te identificeren [!DNL Salesforce Marketing Cloud].

#### Gebruikersrollen en machtigingen toewijzen binnen [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Als [!DNL Salesforce Marketing Cloud] steunt douanerollen afhankelijk van uw gebruik-geval, zou uw gebruiker de relevante rollen moeten worden toegewezen om uw attributen binnen uw bij te werken [!DNL Salesforce Marketing Cloud] kenmerksets. Hieronder ziet u een voorbeeld van rollen die aan een gebruiker zijn toegewezen:
![De Marketing Cloud UI van Salesforce voor een geselecteerde gebruiker die hun toegewezen rollen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Afhankelijk van welke rollen uw [!DNL Salesforce Marketing Cloud] gebruiker is toegewezen, zou u ook toestemmingen aan moeten toewijzen [!DNL Salesforce Marketing Cloud] kenmerksets die de velden bevatten die u wilt bijwerken.

Aangezien deze bestemming toegang tot vereist `[!DNL attribute-set]`, moet u ze toestaan. Bijvoorbeeld voor de `Email` [!DNL attribute-set] u moet toestaan zoals hieronder getoond:

![De gebruikersinterface van de Salesforce-Marketing Cloud geeft de kenmerkset van e-mail weer met toegestane machtigingen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Om het niveau van toegang te beperken, kunt u individuele toegang ook met voeten treden door korrelvoorrechten te gebruiken.
![De interface van de Marketing Cloud van Salesforce die e-mailattributen-reeks met korrelige toestemmingen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Zie de [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) en [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) pagina&#39;s voor gedetailleerde begeleiding.

#### Gather [!DNL Salesforce Marketing Cloud] geloofsbrieven {#gather-credentials}

Noteer de onderstaande items voordat u deze verifieert voor de [!DNL (API) Salesforce Marketing Cloud] bestemming.

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Subdomein | Zie [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) om te leren hoe u deze waarde kunt verkrijgen via de opdracht [!DNL Salesforce Marketing Cloud] interface. | Als uw [!DNL Salesforce Marketing Cloud] domain is<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>u moet verstrekken `mcq4jrssqdlyc4lph19nnqgzzs84` als de waarde. |
| Client-id | Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om te leren hoe u deze waarde kunt verkrijgen via de opdracht [!DNL Salesforce Marketing Cloud] interface. | r23kxxxxxxxx0z05xxxxxx |
| Clientgeheim | Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om te leren hoe u deze waarde kunt verkrijgen via de opdracht [!DNL Salesforce Marketing Cloud] interface. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### Guardrails {#guardrails}

* Salesforce stelt bepaalde [tarieflimieten](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) om eventuele limieten aan te pakken die u tijdens de uitvoering kunt tegenkomen en fouten te reduceren.
   * Zie de [[!DNL Salesforce Marketing Cloud] Prijs voor betrokkenheid](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pagina naar *Download de vergelijkingstabel van de Volledige Uitgave* als een pdf waarin de limieten worden beschreven die in uw plan worden opgelegd.
   * De [API-overzicht](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) pagina details extra limieten.
   * Vernieuwen [hier](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) voor een pagina waarop deze gegevens worden gesorteerd.
* Het aantal *aangepaste velden toegestaan per object* varieert afhankelijk van uw Salesforce Edition.
   * Zie de [!DNL Salesforce] [documentatie](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) voor aanvullende richtsnoeren.
   * Als u de limiet voor *aangepaste velden toegestaan per object* binnen [!DNL Salesforce Marketing Cloud] u zult moeten
      * Oudere kenmerken verwijderen voordat u nieuwe kenmerken toevoegt in [!DNL Salesforce Marketing Cloud].
      * Werk of verwijder om het even welk geactiveerd publiek in de bestemmingen van het Platform bij die deze oudere attributennamen als waarde gebruiken die voor **[!UICONTROL Mapping ID]** tijdens de [publieksplanning](#schedule-segment-export-example) stap.

## Ondersteunde identiteiten {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Contactsleutel. Zie de [!DNL Salesforce Marketing Cloud] [documentatie](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) als u aanvullende instructies nodig hebt. | Verplicht |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)*, op basis van uw veldtoewijzing.</li><li> Elke segmentstatus in [!DNL Salesforce Marketing Cloud] wordt bijgewerkt met de corresponderende publieksstatus van Platform, gebaseerd op de **[!UICONTROL Mapping ID]** waarde die tijdens de [publieksplanning](#schedule-segment-export-example) stap.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, zoeken naar [!DNL (API) Salesforce Marketing Cloud]. U kunt de locatie ook onder de **[!UICONTROL Email marketing]** categorie.

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden hieronder in en selecteert u **[!UICONTROL Connect to destination]**. Zie de [Gather [!DNL Salesforce Marketing Cloud] geloofsbrieven](#gather-credentials) voor eventuele richtsnoeren.

| [!DNL (API) Salesforce Marketing Cloud] doel | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Uw [!DNL Salesforce Marketing Cloud] domeinprefix. <br>Als uw domein bijvoorbeeld <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> u moet verstrekken `mcq4jrssqdlyc4lph19nnqgzzs84` als de waarde. |
| **[!UICONTROL Client ID]** | Uw [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Client Secret]** | Uw [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Platform UI het schermschot die tonen hoe te om aan Marketing Cloud Salesforce voor authentiek te verklaren.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** Als u een groene markering hebt, kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Platform UI het schermschot die de bestemmingsdetails tonen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL (API) Salesforce Marketing Cloud] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL (API) Salesforce Marketing Cloud] de bestemmingsgebieden, volg de hieronder stappen.

>[!IMPORTANT]
>
>* Hoewel de namen van uw kenmerken overeenkomen [!DNL Salesforce Marketing Cloud] account, de toewijzingen voor beide `contactKey` en `personalEmail.address` zijn verplicht.
>
>* De integratie met de [!DNL Salesforce Marketing Cloud] API is onderworpen aan een pagineringsgrens van hoeveel attributen Experience Platform van Salesforce kan terugwinnen. Dit betekent tijdens de **[!UICONTROL Mapping]** stap, kan het schema van het doelgebied een maximum van 2000 attributen van uw rekening Salesforce tonen.

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
   ![Voorbeeld van screenshot van platforminterface voor nieuwe toewijzing toevoegen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. In de **[!UICONTROL Select target field]** venster, kiest u de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select attributes]** en selecteer een kenmerk uit de kenmerksets die zo nodig worden weergegeven. De [!DNL (API) Salesforce Marketing Cloud] doel gebruikt [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) om de attributen en hun kenmerkreeksen dynamisch terug te winnen die binnen worden bepaald [!DNL Salesforce Marketing Cloud]. Deze worden weergegeven in het dialoogvenster **[!UICONTROL Target field]** popup wanneer u opstelling [toewijzing](#mapping-considerations-example) in de [publiek actief maken, workflow](#activate).

   * Herhaal deze stappen om de volgende toewijzingen tussen uw XDM-profielschema en [!DNL (API) Salesforce Marketing Cloud]:

     | Bronveld | Doelveld | Verplicht |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: person.name.firstName` | `Attribute: First Name` uit de gewenste kenmerkset. | - |
     | `xdm: personalEmail.address` | `Attribute: Email Address` uit de gewenste kenmerkset. | - |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
     ![Voorbeeld van schermopname van platformgebruikersinterface met doeltoewijzingen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-segment-export-example}

Bij het uitvoeren van de [Het exporteren van publiek plannen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) stap, moet u het publiek van het Platform aan de [attributes](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

Om dit te doen, selecteer elk segment, dan ga naam van de attributen van in [!DNL Salesforce Marketing Cloud] in de [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** veld. Zie de [Kenmerk maken binnen [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) voor begeleiding en beste praktijken bij het maken van kenmerken in [!DNL Salesforce Marketing Cloud].

Als uw [!DNL Salesforce Marketing Cloud] kenmerk is `salesforce_mc_segment_1`geeft u deze waarde op in het dialoogvenster [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** om het publiek te vullen van Experience Platform in dit kenmerk.

Een voorbeeldkenmerk van [!DNL Salesforce Marketing Cloud] wordt hieronder weergegeven:
![Het schermschot van de Marketing Cloud van Salesforce  UI die een attribuut toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Een voorbeeld dat de plaats van wijst [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** wordt hieronder weergegeven:
![Voorbeeld van platformgebruikersinterface met een schermafbeelding waarin het publiek voor het programma wordt geëxporteerd.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Zoals getoond de [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** moet exact overeenkomen met de waarde die is opgegeven binnen [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]**.

Herhaal deze sectie voor elk geactiveerd platformsegment.

Afhankelijk van uw gebruikscase kunnen alle geactiveerde doelgroepen aan hetzelfde worden toegewezen [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** of naar een andere **[!UICONTROL FIELD NAME]** in [!DNL (API) Salesforce Marketing Cloud]. Een typisch voorbeeld op basis van de bovenstaande afbeelding zou kunnen zijn.
| [!DNL (API) Salesforce Marketing Cloud] segmentnaam | [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** | | — | — | — | | Salesforce mc-publiek 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | Salesforce mc-publiek 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteren **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met bestemmingen te navigeren.
   ![Platform UI het schermschot die Browse Doelen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selecteer het doel en controleer of de status **[!UICONTROL enabled]**.
   ![Platform UI screenshot die de Looppas van Doelen Dataflow toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Schakel over naar de **[!DNL Activation data]** en selecteert u vervolgens de naam van een publiek.
   ![Het het schermschot van het platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Controleer het publieksoverzicht en zorg ervoor dat de telling van profielen aan de telling beantwoordt die binnen het segment wordt gecreeerd.
   ![Voorbeeld van schermopname van platform-UI met segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Aanmelden bij de [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) website. Navigeer vervolgens naar de **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** en controleer of de profielen van het publiek zijn toegevoegd.
   ![De het schermschot van de Marketing Cloud van Salesforce UI die de pagina van Contacten met profielen toont in het segment worden gebruikt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Navigeer naar de **[!UICONTROL Email]** en controleert u of de kenmerkwaarden voor het profiel van de doelgroep zijn bijgewerkt. Als dit lukt, kunt u zien dat elke publieksstatus in [!DNL Salesforce Marketing Cloud] werd bijgewerkt met de overeenkomstige publieksstatus van Platform, gebaseerd op **[!UICONTROL Mapping ID]** de waarde die in de [publieksplanning](#schedule-segment-export-example) stap.
   ![De het schermschot van de Marketing Cloud van Salesforce UI die de geselecteerde Pagina van Contacten e-mail met bijgewerkte publieksstatus toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het verplaatsen van gebeurtenissen naar de Salesforce-Marketing Cloud {#unknown-errors}

* Bij het controleren van een gegevensstroomuitvoering kan het volgende foutbericht optreden: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Fout in schermopname van platforminterface.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Om deze fout te bevestigen, verifieer dat **[!UICONTROL Mapping ID]** die u in de activeringsworkflow aan de [!DNL (API) Salesforce Marketing Cloud] doel komt exact overeen met de naam van het kenmerk dat u hebt gemaakt in [!DNL Salesforce Marketing Cloud]. Zie de [Kenmerk maken binnen [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) voor richtsnoeren.

* Wanneer u een segment activeert, wordt mogelijk een foutbericht weergegeven: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Neem contact op met uw [!DNL Salesforce Marketing Cloud] accountbeheerder om toe te voegen [IP-adressen van Experience Platforms](/help/destinations/catalog/streaming/ip-address-allow-list.md) aan uw [!DNL Salesforce Marketing Cloud] de vertrouwde op IP van rekeningen waaiers. Zie de [!DNL Salesforce Marketing Cloud] [IP Adressen voor Opname op Lijsten van gewenste personen in Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) documentatie als u extra begeleiding nodig hebt.

## Aanvullende bronnen {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) verklaren hoe de contacten met de gespecificeerde informatie in de gespecificeerde attributengroepen worden bijgewerkt.

### Changelog {#changelog}

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| April 2023 | Documentatie bijwerken | <ul><li>We hebben een verklaring en een verwijzing in de [Vereisten in (API) Salesforce-Marketing Cloud](#prerequisites-destination) deel uit te roepen dat [!DNL Salesforce Marketing Cloud Engagement] is een verplicht abonnement om deze bestemming te gebruiken. In de eerder genoemde sectie wordt ten onrechte aangegeven dat gebruikers een abonnement op de Marketing Cloud nodig hebben **Account** Betrokkenheid om door te gaan.</li> <li>We hebben een sectie toegevoegd onder [voorwaarden](#prerequisites) for [rollen en machtigingen](#prerequisites-roles-permissions) aan de [!DNL Salesforce] gebruiker voor deze bestemming aan het werk. (PLATIR-26299)</li></ul> |
| Februari 2023 | Documentatie bijwerken | We hebben de [Vereisten in (API) Salesforce-Marketing Cloud](#prerequisites-destination) om een verwijzingskoppeling op te nemen die [!DNL Salesforce Marketing Cloud Engagement] is een verplicht abonnement om deze bestemming te gebruiken. |
| Februari 2023 | Functionaliteitsupdate | We hebben een probleem opgelost waarbij een onjuiste configuratie in de bestemming ertoe leidde dat een verkeerd gevormde JSON naar Salesforce werd gestuurd. Dit heeft ertoe geleid dat sommige gebruikers hoge aantallen identiteiten ontbrak bij activering zagen. (PLATIR-26299) |
| Januari 2023 | Documentatie bijwerken | <ul><li>We hebben de [Vereisten in [!DNL Salesforce]](#prerequisites-destination) sectie om uit te roepen dat de attributen op moeten worden gecreeerd [!DNL Salesforce] zijde. Deze sectie bevat nu gedetailleerde instructies over hoe u dat kunt doen en aanbevolen procedures voor het benoemen van de kenmerken in [!DNL Salesforce]. (PLATIR-25602)</li><li>We hebben duidelijke instructies toegevoegd over het gebruik van de toewijzings-id voor elk geactiveerd publiek in het dialoogvenster [publieksplanning](#schedule-segment-export-example) stap. (PLATIR-25602)</li></ul> |
| Oktober 2022 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++
