---
title: (API) Salesforce Marketing Cloud-verbinding
description: Met de Salesforce Marketing Cloud-bestemming (voorheen ExactTarget genoemd) kunt u uw accountgegevens exporteren en deze activeren in Salesforce Marketing Cloud voor uw zakelijke behoeften.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2823'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud]-verbinding

## Overzicht {#overview}

[[!DNL (API) Salesforce Marketing Cloud] ](https://www.salesforce.com/products/marketing-cloud/engagement/) (voorheen bekend als [!DNL ExactTarget]) is een digitale marketingsuite waarmee u ritten kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

>[!IMPORTANT]
>
> Neem nota van het verschil tussen deze verbinding en andere [[!DNL Salesforce Marketing Cloud]  verbinding ](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) die binnen de E-mail marketing catalogussectie bestaat. Met de andere Salesforce Marketing Cloud-verbinding kunt u bestanden exporteren naar een opgegeven opslaglocatie, terwijl dit een op API gebaseerde streamingverbinding is.

Vergeleken met [!DNL Salesforce Marketing Cloud Account Engagement] die meer gericht op **B2B** marketing is, is de [!DNL (API) Salesforce Marketing Cloud] bestemming ideaal voor **B2C** gebruiksgevallen met kortere transactie besluitvormingscycli. U kunt grotere datasets consolideren die het gedrag van uw doelpubliek vertegenwoordigen om marketing campagnes aan te passen en te verbeteren door aan contacten voorrang te geven en te segmenteren, vooral van datasets buiten [!DNL Salesforce]. *Nota, heeft Experience Platform ook een verbinding voor [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Dit [!DNL Adobe Experience Platform] [ bestemming ](/help/destinations/home.md) gebruikt [!DNL Salesforce Marketing Cloud] [ updatecontacten ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, die u toestaat om **contacten toe te voegen en contactgegevens** voor uw bedrijfsbehoeften bij te werken na hen binnen een nieuw [!DNL Salesforce Marketing Cloud] segment te activeren.

[!DNL Salesforce Marketing Cloud] gebruikt OAuth 2 met Client Credentials als het verificatiemechanisme om te communiceren met de [!DNL Salesforce Marketing Cloud] API. De instructies om aan uw [!DNL Salesforce Marketing Cloud] instantie voor authentiek te verklaren zijn verder hieronder, in [ voor authentiek verklaren aan bestemmings ](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL (API) Salesforce Marketing Cloud] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De verkoopafdeling van een platform van de huishuur wil een marketing e-mail aan een gericht klantenpubliek uitzenden. Het marketing team van het platform kan nieuwe contacten toevoegen/bestaande contacten bijwerken *(en hun e-mailadressen)* door Adobe Experience Platform, publiek van hun eigen off-line gegevens bouwen, en deze publiek naar [!DNL Salesforce Marketing Cloud] verzenden, die dan kan worden gebruikt om de marketing campagne e-mail te verzenden.

## Vereisten {#prerequisites}

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL (API) Salesforce Marketing Cloud] bestemming te activeren, moet u a [ schema ](/help/xdm/schema/composition.md), a [ dataset ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) hebben, en [ segmenten ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) die in [!DNL Experience Platform] worden gecreeerd.

### Vereisten in [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Experience Platform naar uw [!DNL Salesforce Marketing Cloud] -account te exporteren:

#### U moet een [!DNL Salesforce Marketing Cloud] -account hebben {#prerequisites-account}

Een [!DNL Salesforce Marketing Cloud] rekening met een abonnement op het [[!DNL Marketing Cloud Engagement] ](https://www.salesforce.com/products/marketing-cloud/engagement/) product is verplicht te werk te gaan.

Bereik uit aan [[!DNL Salesforce]  Steun ](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) als u geen [!DNL Salesforce Marketing Cloud] rekening hebt of uw rekening het [!DNL Marketing Cloud Engagement] productabonnement mist.

#### Kenmerken maken binnen [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

Wanneer het activeren van publiek aan de [!DNL (API) Salesforce Marketing Cloud] bestemming, moet u een waarde op het **[!UICONTROL Mapping ID]** gebied voor elk geactiveerd publiek, in de **[planningsstap van het Publiek](#schedule-segment-export-example)** invoeren.

[!DNL Salesforce] vereist deze waarde voor het correct lezen en interpreteren van soorten publiek die vanuit Experience Platform binnenkomen en voor het bijwerken van de status van hun publiek in [!DNL Salesforce Marketing Cloud] . Verwijs naar de documentatie van Experience Platform voor [ het schemagroep van de Details van het Lidmaatschap van de Publiek ](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatus nodig hebt.

Voor elk publiek dat u activeert van Experience Platform naar [!DNL Salesforce] , moet u een kenmerk van het type `Text` hebben dat is gekoppeld aan de gegevensextensie [!DNL Email Demographics] in [!DNL Salesforce Marketing Cloud] . Gebruik [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] om kenmerken te maken. Verwijs naar de [!DNL Salesforce Marketing Cloud] documentatie om [ attributen ](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&type=5&language=en_US) tot stand te brengen als u begeleiding bij het creëren van attributen nodig hebt.

De namen van kenmerkvelden worden tijdens de [!DNL (API) Salesforce Marketing Cloud] -stap gebruikt voor het doelveld van **[!UICONTROL Mapping]** . U kunt het veldteken definiëren met maximaal 4000 tekens, afhankelijk van uw zakelijke vereisten. Zie de [!DNL Salesforce Marketing Cloud] [ de documentatiepagina van de Types van Gegevens van Uitbreidingen van Gegevens van Gegevens van de Uitbreidingen van Gegevens ](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&type=5) voor extra informatie over attributentypes.

Een voorbeeld van het scherm van de gegevensontwerper in [!DNL Salesforce Marketing Cloud], waarin u de attributen zult toevoegen wordt hieronder getoond:
![ Salesforce Marketing Cloud UI gegevensontwerper.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

Hieronder ziet u een weergave van een [!DNL Salesforce Marketing Cloud] [!DNL Email Data] -kenmerkgroep met kenmerken die overeenkomen met de publieksstatus in de [!DNL Email Demographics] -gegevensextensie:
![ Salesforce Marketing Cloud UI e-mailgegevenskenmerkgroep.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

De [!DNL (API) Salesforce Marketing Cloud] bestemming gebruikt [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [ API ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) om de gegevensuitbreidingen en hun verbonden die attributen dynamisch terug te winnen binnen [!DNL Salesforce Marketing Cloud] worden bepaald.

Deze worden getoond in het **[!UICONTROL Target field]** selectievenster wanneer u opstelling de [ afbeelding ](#mapping-considerations-example) in het werkschema om [ publiek aan de bestemming ](#activate) te activeren.

>[!IMPORTANT]
>
> Binnen [!DNL Salesforce Marketing Cloud] moet u kenmerken maken met een **[!UICONTROL FIELD NAME]** die exact overeenkomt met de waarde die binnen **[!UICONTROL Mapping ID]** is opgegeven voor elk geactiveerd Experience Platform-segment. In de onderstaande schermafbeelding ziet u bijvoorbeeld een kenmerk met de naam `salesforce_mc_segment_1` . Wanneer u een publiek activeert naar dit doel, voegt u `salesforce_mc_segment_1` toe als **[!UICONTROL Mapping ID]** om het publiek van Experience Platform in dit kenmerk te vullen.

Hieronder ziet u een voorbeeld van het maken van kenmerken in [!DNL Salesforce Marketing Cloud] :
![ Salesforce Marketing Cloud UI het schermschot die een attribuut tonen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * Neem bij het maken van het kenmerk geen spatietekens op in de veldnaam. Gebruik in plaats daarvan het onderstrepingsteken `(_)` als scheidingsteken.
> * Als u onderscheid wilt maken tussen kenmerken die worden gebruikt voor Experience Platform-publiek en andere kenmerken binnen [!DNL Salesforce Marketing Cloud] , kunt u een herkenbaar voor- of achtervoegsel opnemen voor de kenmerken die worden gebruikt voor Adobe-segmenten. Gebruik bijvoorbeeld `test_segment` of `Adobe_test_segment` in plaats van `test_segment_Adobe` .
> * Als u al andere kenmerken in [!DNL Salesforce Marketing Cloud] hebt gemaakt, kunt u dezelfde naam gebruiken als het Experience Platform-segment om het publiek gemakkelijk te identificeren in [!DNL Salesforce Marketing Cloud] .

#### Gebruikersrollen en machtigingen toewijzen binnen [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Aangezien [!DNL Salesforce Marketing Cloud] aangepaste rollen ondersteunt, afhankelijk van uw gebruikscase, moet aan uw gebruiker de relevante rollen worden toegewezen om uw kenmerken binnen [!DNL Salesforce Marketing Cloud] bij te werken. Hieronder ziet u een voorbeeld van rollen die aan een gebruiker zijn toegewezen:
![ Salesforce Marketing Cloud UI voor een geselecteerde gebruiker die hun toegewezen rollen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Afhankelijk van de rollen die de [!DNL Salesforce Marketing Cloud] -gebruiker heeft toegewezen, moet u ook machtigingen toewijzen aan de [!DNL Salesforce Marketing Cloud] -gegevensextensie die is gekoppeld aan de velden die u wilt bijwerken.

Aangezien deze bestemming toegang tot `[!DNL data extension]` vereist, moet u hen toestaan. Bijvoorbeeld voor `Email` [!DNL data extension] moet u toestaan zoals hieronder wordt getoond:

![ Salesforce Marketing Cloud UI die de uitbreiding van e-mailgegevens met toegestane toestemmingen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Om het niveau van toegang te beperken, kunt u individuele toegang ook met voeten treden door korrelige voorrechten te gebruiken.
![ Salesforce Marketing Cloud UI die de uitbreiding van e-mailgegevens met korrelige toestemmingen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Zie de [[!DNL Marketing Cloud Roles] ](https://help.salesforce.com/s/articleView?language=en_US&id=sf.mc_overview_marketing_cloud_roles.htm&type=5) en [[!DNL Marketing Cloud Roles and Permissions] ](https://help.salesforce.com/s/articleView?language=en_US&id=sf.mc_overview_roles.htm&type=5) pagina&#39;s voor gedetailleerde begeleiding.

#### [!DNL Salesforce Marketing Cloud] gebruikersgegevens verzamelen {#gather-credentials}

Noteer de onderstaande items voordat u de verificatie uitvoert naar de bestemming [!DNL (API) Salesforce Marketing Cloud] .

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Subdomein | Zie [[!DNL Salesforce Marketing Cloud domain prefix] ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) leren hoe te om deze waarde van de [!DNL Salesforce Marketing Cloud] interface te verkrijgen. | Als uw [!DNL Salesforce Marketing Cloud] domein <br> is *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> moet u `mcq4jrssqdlyc4lph19nnqgzzs84` als waarde verstrekken. |
| Client-id | Zie [!DNL Salesforce Marketing Cloud] [ documentatie ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) leren hoe te om deze waarde uit de [!DNL Salesforce Marketing Cloud] interface te verkrijgen. | r23kxxxxxx0z05xxxxxx |
| Clientgeheim | Zie [!DNL Salesforce Marketing Cloud] [ documentatie ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) leren hoe te om deze waarde uit de [!DNL Salesforce Marketing Cloud] interface te verkrijgen. | ipxxxxxxxxT4xxxxxxxx |

{style="table-layout:auto"}

### Guardrails {#guardrails}

* Salesforce legt bepaalde [ tariefgrenzen ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html) op.
   * Verwijs naar de [!DNL Salesforce Marketing Cloud] [ documentatie ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) om het even welke waarschijnlijke grenzen te richten die u fouten tijdens uitvoering zou kunnen ontmoeten en verminderen.
   * Verwijs naar de [[!DNL Salesforce Marketing Cloud]  Prijsstelling van de Betrokkenheid ](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pagina aan *Download de Volledige Grafiek van de Vergelijking van de Uitgave* als pdf die de grenzen door uw plan worden opgelegd detailleert.
   * Het [ API overzicht ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) paginadetails extra grenzen.
   * Verwijs [ hier ](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) voor een pagina die deze details sorteert.
* De telling van *douanegebieden toegestaan per voorwerp* varieert afhankelijk van uw Uitgave van Salesforce.
   * Verwijs naar de [!DNL Salesforce] [ documentatie ](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&type=5) voor extra begeleiding.
   * Als u de grens hebt bereikt die voor *wordt bepaald die douanegebieden per voorwerp* worden toegestaan binnen [!DNL Salesforce Marketing Cloud] u zult moeten
      * Verwijder oudere kenmerken voordat u nieuwe kenmerken toevoegt in [!DNL Salesforce Marketing Cloud] .
      * Werk of verwijder om het even welk geactiveerd publiek in de bestemmingen van Experience Platform die deze oudere attributennamen als waarde gebruiken die voor **[!UICONTROL Mapping ID]** tijdens de [ publiek wordt verstrekt die ](#schedule-segment-export-example) stap plannen.

## Ondersteunde identiteiten {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Contactsleutel. Verwijs naar de [!DNL Salesforce Marketing Cloud] [ documentatie ](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&type=5) als u extra begeleiding nodig hebt. | Verplicht |

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | X | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Elke segmentstatus in [!DNL Salesforce Marketing Cloud] wordt bijgewerkt met de overeenkomstige publieksstatus van Experience Platform, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd die tijdens de [ publiek wordt verstrekt die ](#schedule-segment-export-example) stap plant.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
> Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Zoek in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** naar [!DNL (API) Salesforce Marketing Cloud] . U kunt de locatie ook in de categorie **[!UICONTROL Email marketing]** vinden.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden hieronder in en selecteert u **[!UICONTROL Connect to destination]** . Verwijs naar de [ Gather  [!DNL Salesforce Marketing Cloud]  geloofsbrieven ](#gather-credentials) sectie voor om het even welke begeleiding.

| [!DNL (API) Salesforce Marketing Cloud]-bestemming | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Het domeinvoorvoegsel [!DNL Salesforce Marketing Cloud] . <br> Bijvoorbeeld als uw domein <br> is *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> u `mcq4jrssqdlyc4lph19nnqgzzs84` als waarde moet verstrekken. |
| **[!UICONTROL Client ID]** | Uw [!DNL Salesforce Marketing Cloud] `Client ID` . |
| **[!UICONTROL Client Secret]** | Uw [!DNL Salesforce Marketing Cloud] `Client Secret` . |

{het schermschot van 0} Experience Platform UI die tonen hoe te om aan Salesforce Marketing Cloud voor authentiek te verklaren.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface een **[!UICONTROL Connected]** -status weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
{het schermschot van 0} Experience Platform UI die de bestemmingsdetails toont.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
> * Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
> * Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL (API) Salesforce Marketing Cloud] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming.

Voer de onderstaande stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL (API) Salesforce Marketing Cloud] -doelvelden.

>[!IMPORTANT]
>
> * Hoewel de namen van uw kenmerken overeenkomen met die van uw [!DNL Salesforce Marketing Cloud] -account, zijn toewijzingen voor zowel `contactKey` als `personalEmail.address` verplicht.
>
> * Voor de integratie met de [!DNL Salesforce Marketing Cloud] API geldt een pagineringslimiet van het aantal kenmerken dat Experience Platform kan ophalen van Salesforce. Dit betekent dat tijdens de stap **[!UICONTROL Mapping]** het doelveldschema maximaal 2000 kenmerken van uw Salesforce-account kan weergeven.

1. Selecteer **[!UICONTROL Mapping]** in de stap **[!UICONTROL Add new mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.
   ![ het schermschot van Experience Platform UI voor Add nieuwe afbeelding.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. Kies in het venster **[!UICONTROL Select target field]** de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select attributes]** de categorie en selecteer een kenmerk uit de gegevensextensies die zo nodig worden weergegeven. De [!DNL (API) Salesforce Marketing Cloud] bestemming gebruikt [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [ API ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) om de gegevensuitbreidingen en hun verbonden die attributen dynamisch terug te winnen binnen [!DNL Salesforce Marketing Cloud] worden bepaald. Deze worden getoond in **[!UICONTROL Target field]** popup wanneer u opstelling de [ afbeelding ](#mapping-considerations-example) in [ activeert publiek werkschema ](#activate).

   * Herhaal deze stappen om de volgende toewijzingen tussen uw XDM-profielschema en [!DNL (API) Salesforce Marketing Cloud] toe te voegen:

     | Source-veld | Doelveld | Verplicht |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | `Attribute: Email Address` in de gegevensextensie [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses] . | `Mandatory` bij het toevoegen van nieuwe contactpersonen. |
     | `xdm: person.name.firstName` | `Attribute: First Name` uit de gewenste [!DNL Salesforce Marketing Cloud] -gegevensextensie. | - |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
     ![ Experience Platform UI het screenshot voorbeeld dat de afbeeldingen van het Doel toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-segment-export-example}

Wanneer het uitvoeren van de [ stap van de de publieksuitvoer van het Programma ](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling), moet u het publiek van Experience Platform aan de [ attributen ](#prerequisites-attribute) in kaart brengen [!DNL Salesforce Marketing Cloud].

Hiervoor selecteert u elk segment en voert u vervolgens een naam in van het kenmerk uit [!DNL Salesforce Marketing Cloud] in het veld [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** . Verwijs naar [ creeer attribuut binnen  [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) sectie voor begeleiding en beste praktijken bij het creëren van attributen in [!DNL Salesforce Marketing Cloud].

Als uw [!DNL Salesforce Marketing Cloud] -kenmerk bijvoorbeeld `salesforce_mc_segment_1` is, geeft u deze waarde op in [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** om het publiek van Experience Platform in dit kenmerk te vullen.

Hieronder ziet u een voorbeeldkenmerk van [!DNL Salesforce Marketing Cloud] :
![ Salesforce Marketing Cloud UI het schermschot die een attribuut tonen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Hieronder ziet u een voorbeeld van de locatie van [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** :

{het screenshot voorbeeld van 0} Experience Platform UI die het publiek van het Programma tonen uitvoer.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Zoals u ziet, moet [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** exact overeenkomen met de waarde die is opgegeven binnen [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** .

Herhaal deze sectie voor elk geactiveerd Experience Platform-segment.

Een typisch voorbeeld op basis van de bovenstaande afbeelding zou kunnen zijn.

| [!DNL (API) Salesforce Marketing Cloud] segmentnaam | [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** |
| --- | --- | --- |
| salesforce mc publiek 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` |
| salesforce mc publiek 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteer **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met doelen te navigeren.
   {het schermschot van 0} Experience Platform UI die Browse Doelen toont.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selecteer het doel en bevestig dat de status **[!UICONTROL enabled]** is.
   ![ het schermschot van Experience Platform UI die de Looppas van Doelen Dataflow toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Ga naar het tabblad **[!DNL Activation data]** en selecteer vervolgens een publieksnaam.
   ![ het schermschot van Experience Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Controleer het publieksoverzicht en zorg ervoor dat de telling van profielen aan de telling beantwoordt die binnen het segment wordt gecreeerd.
   ![ het schermschot van Experience Platform UI die Segment toont.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Meld u aan bij de [[!DNL Salesforce Marketing Cloud] ](https://mc.exacttarget.com/) -website. Navigeer vervolgens naar de pagina **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** en controleer of de profielen van het publiek zijn toegevoegd.
   ![ Salesforce Marketing Cloud UI het schermschot die de pagina van Contacten met profielen toont die in het segment worden gebruikt.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Als u wilt controleren of er profielen zijn bijgewerkt, navigeert u naar de pagina **[!UICONTROL Email]** en controleert u of de kenmerkwaarden voor het profiel van de doelgroep zijn bijgewerkt. Als succesvol, kunt u zien dat elke publieksstatus in [!DNL Salesforce Marketing Cloud] met de overeenkomstige publieksstatus van Experience Platform werd bijgewerkt, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd die in het [ publiek wordt verstrekt die ](#schedule-segment-export-example) stap plant.
   {het schermschot van 0} Salesforce Marketing Cloud UI die de geselecteerde E-mailpagina van Contacten met bijgewerkte publieksstatussen toont.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het verplaatsen van gebeurtenissen naar Salesforce Marketing Cloud {#unknown-errors}

* Bij het controleren van een gegevensstroomuitvoering kan het volgende foutbericht optreden: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  {het schermschot van 0} Experience Platform UI die fout toont.![](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Om deze fout te corrigeren, controleert u of de **[!UICONTROL Mapping ID]** die u in de activeringsworkflow hebt opgegeven voor het [!DNL (API) Salesforce Marketing Cloud] -doel exact overeenkomt met de naam van het kenmerk dat u in [!DNL Salesforce Marketing Cloud] hebt gemaakt. Verwijs naar [ creeer attribuut binnen  [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) sectie voor begeleiding.

* Wanneer u een segment activeert, wordt mogelijk een foutbericht weergegeven: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Om deze fout te bevestigen, contacteer uw [!DNL Salesforce Marketing Cloud] rekeningsbeheerder om [ Experience Platform IP adressen ](/help/destinations/catalog/streaming/ip-address-allow-list.md) aan uw [!DNL Salesforce Marketing Cloud] vertrouwde op IP waaiers van rekeningen toe te voegen. Verwijs naar de [!DNL Salesforce Marketing Cloud] [ IP Adressen voor Opname op Lijsten van gewenste personen in Marketing Cloud ](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&type=5) documentatie als u extra begeleiding nodig hebt.

## Aanvullende bronnen {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [ API ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [ documentatie ](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) verklarend hoe de contacten met de gespecificeerde informatie worden bijgewerkt.

### Changelog {#changelog}

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Oktober 2023 | Documentatie bijgewerkt | <ul><li>Wij hebben de [ Eerste vereisten in (API) sectie van Salesforce Marketing Cloud ](#prerequisites-destination) bijgewerkt en in het algemeen verwijderde onnodige verwijzingen naar attributengroepen over het document.</li> <li>Bijgewerkte documentatie die aangeeft dat kenmerken voor de publieksstatus alleen binnen [!DNL Salesforce Marketing Cloud] in de gegevensextensie [!DNL Email Demographics] moeten worden gemaakt.</li> <li>Wij hebben de mappingstabel binnen de [ Afbeeldingsoverwegingen en voorbeeld ](#mapping-considerations-example) sectie bijgewerkt, de afbeelding voor `Email Address` attributen binnen de `Email Addresses` gegevensuitbreiding duidelijk verplicht, werd dit vereiste vermeld in duidelijk BELANGRIJK callout maar werd weggelaten uit de lijst.</li></ul> |
| April 2023 | Documentatie bijgewerkt | <ul><li>Wij verbeterden een verklaring en verwijzingsverbinding in de [ Eerste vereisten in (API) Salesforce Marketing Cloud ](#prerequisites-destination) sectie om uit te roepen dat [!DNL Salesforce Marketing Cloud Engagement] een verplicht abonnement is om deze bestemming te gebruiken. De sectie riep eerder verkeerd uit dat de gebruikers een abonnement op de **Betrokkenheid van de Rekening van Marketing Cloud** nodig hebben om te werk te gaan.</li> <li>Wij hebben een sectie onder [ eerste vereisten ](#prerequisites) voor [ rollen en toestemmingen ](#prerequisites-roles-permissions) toegevoegd die aan de [!DNL Salesforce] gebruiker voor deze bestemming moeten worden toegewezen om te werken. (PLATIR-26299)</li></ul> |
| Februari 2023 | Documentatie bijgewerkt | Wij hebben de [ Eerste vereisten in (API) Salesforce Marketing Cloud ](#prerequisites-destination) sectie bijgewerkt om een verwijzingsverbinding te omvatten die aanroept dat [!DNL Salesforce Marketing Cloud Engagement] een verplicht abonnement is om deze bestemming te gebruiken. |
| Februari 2023 | Functionaliteitsupdate | We hebben een probleem opgelost waarbij een onjuiste configuratie in de bestemming ertoe leidde dat een verkeerd gevormde JSON naar Salesforce werd gestuurd. Dit heeft ertoe geleid dat sommige gebruikers hoge aantallen identiteiten ontbrak bij activering zagen. (PLATIR-26299) |
| Januari 2023 | Documentatie bijgewerkt | <ul><li>Wij hebben de [ Eerste vereisten in  [!DNL Salesforce]](#prerequisites-destination) sectie bijgewerkt om uit te roepen dat de attributen op de [!DNL Salesforce] kant moeten worden gecreeerd. Deze sectie bevat nu gedetailleerde instructies over hoe u dat kunt doen en aanbevolen procedures voor het benoemen van de kenmerken in [!DNL Salesforce] . (PLATIR-25602)</li><li>Wij toegevoegde duidelijke instructies op hoe te om identiteitskaart van de Afbeelding voor elk geactiveerd publiek in de [ publiek te gebruiken die ](#schedule-segment-export-example) stap plannen. (PLATIR-25602)</li></ul> |
| Oktober 2022 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++
