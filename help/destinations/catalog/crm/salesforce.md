---
keywords: crm;CRM;crm bestemmingen;salesforce crm;salesforce crm bestemming
title: Salesforce CRM-verbinding
description: Met de Salesforce CRM-bestemming kunt u uw accountgegevens exporteren en deze activeren in Salesforce CRM voor uw zakelijke behoeften.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: 27f2b28d924fbd85eefbea5a65d1ee9249bafa87
workflow-type: tm+mt
source-wordcount: '2734'
ht-degree: 0%

---

# [!DNL Salesforce CRM]-verbinding

## Overzicht {#overview}

[[!DNL Salesforce CRM] ](https://www.salesforce.com/crm/) is een populair platform van het Beheer van de Verhouding van de Klant (CRM) en steunt de types van hieronder beschreven profielen:

* [ Leads ](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - een lood is de naam van een persoon of een bedrijf die (of niet) in de producten of de diensten kan geinteresseerd zijn u verkoopt.
* [ Contacten ](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - een contact is een individu met wie één van uw vertegenwoordigers een verhouding heeft gevestigd en als potentiële klant gekwalificeerd.

Dit [!DNL Adobe Experience Platform] [ doel ](/help/destinations/home.md) hefboomwerkingen [[!DNL Salesforce composite API] ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), die beide hierboven beschreven soorten profielen steunt.

Wanneer [ het activeren van segmenten ](#activate), kunt u tussen of lood of contacten en updatekenmerken en publieksgegevens in [!DNL Salesforce CRM] selecteren.

[!DNL Salesforce CRM] gebruikt OAuth 2 met de Verlening van het Wachtwoord als authentificatiemechanisme om met Salesforce REST API te communiceren. De instructies om aan uw [!DNL Salesforce CRM] instantie voor authentiek te verklaren zijn verder hieronder, in [ voor authentiek verklaren aan bestemmings ](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u uw gebruikers een persoonlijke ervaring bieden op basis van kenmerken uit hun Adobe Experience Platform-profielen. U kunt een publiek maken op basis van uw offlinegegevens en dit publiek naar Salesforce CRM sturen om het CRM-lidmaatschap bij te werken zodra het publiek en de profielen in Adobe Experience Platform zijn bijgewerkt.

## Vereisten {#prerequisites}

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Alvorens gegevens aan de bestemming van Salesforce CRM te activeren, moet u a [ schema ](/help/xdm/schema/composition.md), a [ dataset ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), en [ segmenten ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) hebben die in [!DNL Experience Platform] worden gecreeerd.

### Vereisten in [!DNL Salesforce CRM] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden in [!DNL Salesforce CRM] als u gegevens van Experience Platform naar uw Salesforce-account wilt exporteren:

#### U moet een [!DNL Salesforce] -account hebben {#prerequisites-account}

Ga naar de [!DNL Salesforce] [ proef ](https://www.salesforce.com/in/form/signup/freetrial-sales/) pagina om een [!DNL Salesforce] rekening te registreren en tot stand te brengen, als u niet reeds hebt.

#### Een verbonden app configureren binnen [!DNL Salesforce] {#prerequisites-connected-app}

Eerst, moet u a [[!DNL Salesforce]  verbonden app ](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&language=en_US&r=https%3A%2F%2Fhelp.salesforce.com%2F&type=5) binnen uw [!DNL Salesforce] rekening vormen, als u niet reeds hebt. [!DNL Salesforce CRM] gebruikt de verbonden toepassing om verbinding te maken met [!DNL Salesforce] .

Schakel vervolgens [!DNL OAuth Settings for API Integration] in voor de [!DNL Salesforce connected app] . Raadpleeg de [[!DNL Salesforce] ](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&type=5&language=en_US) documentatie voor hulp.

Ook, zorg ervoor dat het [ hieronder vermelde werkingsgebied ](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&type=5&language=en_US) voor [!DNL Salesforce connected app] wordt geselecteerd.

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

Tot slot moet u ervoor zorgen dat de `password` -subsidie is ingeschakeld binnen uw [!DNL Salesforce] -account. Verwijs naar [!DNL Salesforce] [ OAuth 2.0 de stroom van het gebruikerswachtwoord voor Speciale Scenario&#39;s ](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&type=5) als u begeleiding nodig hebt.

>[!IMPORTANT]
>
>Als uw [!DNL Salesforce] accountbeheerder toegang tot vertrouwde op IP waaiers heeft beperkt, moet u hen contacteren om [ Experience Platform IP ](/help/destinations/catalog/streaming/ip-address-allow-list.md) gevoegd op lijst van gewenste personen te krijgen. Verwijs naar [!DNL Salesforce] [ Beperk Toegang tot Vertrouwde IP Waaier voor een Verbonden App ](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) documentatie als u extra begeleiding nodig hebt.

#### Aangepaste velden maken binnen [!DNL Salesforce] {#prerequisites-custom-field}

Wanneer het activeren van publiek aan de [!DNL Salesforce CRM] bestemming, moet u een waarde op het **[!UICONTROL Mapping ID]** gebied voor elk geactiveerd publiek, in de **[planningsstap van het Publiek](#schedule-segment-export-example)** invoeren.

[!DNL Salesforce CRM] vereist deze waarde voor het correct lezen en interpreteren van soorten publiek die vanuit Experience Platform binnenkomen en voor het bijwerken van de status van hun publiek in [!DNL Salesforce] . Verwijs naar de documentatie van Experience Platform voor [ het schemagroep van de Details van het Lidmaatschap van de Publiek ](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatus nodig hebt.

Voor elk publiek dat u activeert van Experience Platform naar [!DNL Salesforce CRM], moet u een aangepast veld maken van het type `Text Area (Long)` within [!DNL Salesforce] . U kunt de veldtekenlengte van een willekeurige grootte tussen 256 en 131.072 tekens definiëren volgens uw zakelijke vereisten. Zie de [!DNL Salesforce] [ de documentatiepagina van de Types van Gebied van de Douane ](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&type=5) voor extra informatie over de types van douanegebied. Ook verwijs de [!DNL Salesforce] documentatie aan [ creeer douanegebieden ](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&type=5&language=en_US) als u hulp op gebiedsverwezenlijking nodig hebt.

>[!IMPORTANT]
>
>Plaats geen spatietekens in de veldnaam. Gebruik in plaats daarvan het onderstrepingsteken `(_)` als scheidingsteken.
>Binnen [!DNL Salesforce] moet u aangepaste velden maken met een **[!UICONTROL Field Name]** die exact overeenkomt met de waarde die binnen **[!UICONTROL Mapping ID]** is opgegeven voor elk geactiveerd Experience Platform-segment. In de onderstaande schermafbeelding ziet u bijvoorbeeld een aangepast veld met de naam `crm_2_seg` . Wanneer u een publiek activeert naar dit doel, voegt u `crm_2_seg` toe als **[!UICONTROL Mapping ID]** om het publiek van Experience Platform in dit aangepaste veld te vullen.

Een voorbeeld van de verwezenlijking van het douanegebied in [!DNL Salesforce], *Stap 1 - selecteer het gegevenstype*, wordt hieronder getoond:
![ het schermschot van Salesforce UI die de verwezenlijking van het douanegebied, Stap 1 toont - selecteer het gegevenstype.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Een voorbeeld van de verwezenlijking van het douanegebied in [!DNL Salesforce], *Stap 2 - ga de details voor het douanegebied* in, wordt hieronder getoond:
![ het schermschot van Salesforce UI die de verwezenlijking van het douanegebied toont, Stap 2 - ga de details voor het douanegebied in.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Als u onderscheid wilt maken tussen aangepaste velden die worden gebruikt voor Experience Platform-publiek en andere aangepaste velden binnen [!DNL Salesforce] , kunt u bij het maken van het aangepaste veld een herkenbaar voor- of achtervoegsel toevoegen. Gebruik bijvoorbeeld `test_segment` of `Adobe_test_segment` in plaats van `test_segment_Adobe` .
>* Als u al andere aangepaste velden hebt gemaakt in [!DNL Salesforce] , kunt u dezelfde naam gebruiken als het Experience Platform-segment om het publiek gemakkelijk te identificeren in [!DNL Salesforce] .

>[!NOTE]
>
>* De voorwerpen in Salesforce zijn beperkt tot 25 Externe gebieden, zie {de Attributen van het Gebied van 0} Douane [.](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5)
>* Deze beperking houdt in dat u op elk moment maximaal 25 Experience Platform-publieksleden actief kunt hebben.
>* Als u deze limiet in Salesforce hebt bereikt, moet u de aangepaste kenmerken uit Salesforce verwijderen die zijn gebruikt om de publieksstatus op te slaan tegen oudere gebruikers in Experience Platform voordat een nieuwe **[!UICONTROL Mapping ID]** kan worden gebruikt.

#### [!DNL Salesforce CRM] gebruikersgegevens verzamelen {#gather-credentials}

Noteer de onderstaande items voordat u de verificatie uitvoert naar het doel van [!DNL Salesforce CRM] :

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Username` | Uw [!DNL Salesforce] gebruikersnaam van de account. | |
| `Password` | Wachtwoord voor uw [!DNL Salesforce] account. | |
| `Security Token` | Uw [!DNL Salesforce] veiligheidstoken dat u later aan het eind van uw [!DNL Salesforce] Wachtwoord zult toevoegen om een samengevoegde koord tot stand te brengen dat als **[!UICONTROL Password]** moet worden gebruikt wanneer [ het voor authentiek verklaren aan de bestemming ](#authenticate).<br> Verwijs naar de [!DNL Salesforce] documentatie [ om uw veiligheidstoken ](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&type=5) terug te stellen leren hoe te om het van de [!DNL Salesforce] interface opnieuw te produceren als u niet het Symbolische van de Veiligheid hebt. |  |
| `Custom Domain` | Het domeinvoorvoegsel [!DNL Salesforce] . <br> Zie de [[!DNL Salesforce]  documentatie ](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&type=5) leren hoe te om deze waarde uit de [!DNL Salesforce] interface te verkrijgen. | Als uw [!DNL Salesforce] domein <br> is *`d5i000000isb4eak-dev-ed`.my.salesforce.com*, <br> u `d5i000000isb4eak-dev-ed` als waarde zult nodig hebben. |
| `Client ID` | Uw Salesforce `Consumer Key` . <br> verwijs naar de [[!DNL Salesforce]  documentatie ](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&type=5) om te leren hoe te om deze waarde uit de [!DNL Salesforce] interface te verkrijgen. | |
| `Client Secret` | Uw Salesforce `Consumer Secret` . <br> verwijs naar de [[!DNL Salesforce]  documentatie ](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&type=5) om te leren hoe te om deze waarde uit de [!DNL Salesforce] interface te verkrijgen. | |

### Guardrails {#guardrails}

In [!DNL Salesforce] worden transactieladingen in evenwicht gebracht door verzoek-, tarief- en time-outlimieten op te leggen. Verwijs naar de [ Limieten en Toewijzingen van het API- Verzoek ](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) voor details.

Als uw [!DNL Salesforce] rekeningsbeheerder IP beperkingen heeft afgedwongen, zult u [ Experience Platform IP adressen ](/help/destinations/catalog/streaming/ip-address-allow-list.md) aan uw [!DNL Salesforce] vertrouwde op IP waaiers van rekeningen moeten toevoegen. Verwijs naar [!DNL Salesforce] [ Beperk Toegang tot Vertrouwde IP Waaier voor een Verbonden App ](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) documentatie als u extra begeleiding nodig hebt.

>[!IMPORTANT]
>
>Wanneer [ het activeren van segmenten ](#activate) u tussen of *contact* of ** types van Lood moet selecteren. U moet ervoor zorgen dat uw publiek de juiste gegevenstoewijzing heeft op basis van het geselecteerde type.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Salesforce CRM] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| `SalesforceId` | De [!DNL Salesforce CRM]-id voor de contactpersoon of lead-id&#39;s die u exporteert of bijwerkt via uw segment. | Verplicht |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Elke publieksstatus in [!DNL Salesforce CRM] wordt bijgewerkt met de overeenkomstige publieksstatus van Experience Platform, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd tijdens de [ publiek die ](#schedule-segment-export-example) stap plannen.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Kies in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** Zoeken naar [!DNL Salesforce CRM] . U kunt de locatie ook in de categorie **[!UICONTROL CRM]** vinden.

### Verifiëren voor bestemming {#authenticate}

Als u voor verificatie bij het doel wilt zorgen, vult u de vereiste velden hieronder in en selecteert u **[!UICONTROL Connect to destination]** . Verwijs naar de [ Gather  [!DNL Salesforce CRM]  geloofsbrieven ](#gather-credentials) sectie voor om het even welke begeleiding.

| Credentials | Beschrijving |
| --- | --- |
| **[!UICONTROL Username]** | Uw [!DNL Salesforce] gebruikersnaam van de account. |
| **[!UICONTROL Password]** | Een samengevoegde tekenreeks die bestaat uit het wachtwoord voor uw [!DNL Salesforce] -account dat is toegevoegd met uw [!DNL Salesforce] beveiligingstoken.<br> de samengevoegde waarde neemt de vorm van `{PASSWORD}{TOKEN}`.<br> Opmerking: gebruik geen accolades of spaties.<br> Bijvoorbeeld als uw [!DNL Salesforce] Wachtwoord `MyPa$$w0rd123` is en [!DNL Salesforce] Beveiligingstoken `TOKEN12345....0000` is, is de samengevoegde waarde die u in het **[!UICONTROL Password]** veld zult gebruiken `MyPa$$w0rd123TOKEN12345....0000` . |
| **[!UICONTROL Custom Domain]** | Het domeinvoorvoegsel [!DNL Salesforce] . <br> Bijvoorbeeld als uw domein *`d5i000000isb4eak-dev-ed`.my.salesforce.com* is, moet u `d5i000000isb4eak-dev-ed` als waarde verstrekken. |
| **[!UICONTROL Client ID]** | De [!DNL Salesforce] verbonden app `Consumer Key` . |
| **[!UICONTROL Client Secret]** | De [!DNL Salesforce] verbonden app `Consumer Secret` . |

{het schermschot van 0} Experience Platform UI die toont hoe te voor authentiek te verklaren.![](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface een **[!UICONTROL Connected]** -status weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Salesforce ID Type]**:

   * Selecteer **[!UICONTROL Contact]** als de identiteiten u wilt uitvoeren of bijwerken van type *Contact* zijn.
   * Selecteer **[!UICONTROL Lead]** als de identiteiten u wilt uitvoeren of bijwerken van type *Lood* zijn.

{het schermschot van 0} Experience Platform UI die de bestemmingsdetails toont.![](../../assets/catalog/crm/salesforce/destination-details.png)

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [ het intekenen aan bestemmingsalarm gebruikend UI ](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [ toegangsbeheertoestemming ](/help/access-control/home.md#permissions) nodig. <br> ![ Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [ activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen ](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Salesforce CRM] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming.

Kenmerken die in de **[!UICONTROL Target field]** worden opgegeven, moeten een naam krijgen die exact overeenkomt met de beschrijving in de tabel met kenmerktoewijzingen, aangezien deze kenmerken de aanvraaginstantie vormen.

Kenmerken die in **[!UICONTROL Source field]** worden opgegeven, volgen een dergelijke beperking niet. U kunt het in kaart brengen gebaseerd op uw behoefte, echter verzekeren het formaat van de inputgegevens geldig volgens de [[!DNL Salesforce]  documentatie ](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5) is. Als de invoergegevens niet geldig zijn, mislukt de updateaanroep naar [!DNL Salesforce] en worden uw contactpersonen/leads niet bijgewerkt.

Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL (API) Salesforce CRM] -doelvelden:

1. In de stap **[!UICONTROL Mapping]** selecteert u **[!UICONTROL Add new mapping]** en ziet u een nieuwe toewijzingsrij op het scherm.
   ![ het schermschot van Experience Platform UI voor Add nieuwe afbeelding.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. Kies in het venster **[!UICONTROL Select target field]** de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** en selecteer een kenmerk of definieer een kenmerk met behulp van het veld **[!UICONTROL Attribute name]** . Verwijs naar de [[!DNL Salesforce CRM]  documentatie ](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&type=5) voor begeleiding op gesteunde attributen.
   * Herhaal deze stappen om de volgende toewijzingen tussen uw XDM-profielschema en [!DNL (API) Salesforce CRM] toe te voegen:

   **Werkend met Contacten**

   * Als u met *Contacten* binnen uw segment werkt, verwijs naar de Verwijzing van Objecten in Salesforce voor [ Contact ](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) om afbeeldingen voor de gebieden te bepalen die moeten worden bijgewerkt.
   * U kunt verplichte gebieden identificeren door naar het woord *Vereiste* te zoeken, dat in gebiedsbeschrijvingen in de verbinding hierboven wordt vermeld.
   * Afhankelijk van de velden die u wilt exporteren of bijwerken, voegt u toewijzingen toe tussen het XDM-profielschema en [!DNL (API) Salesforce CRM] :

     | Source-veld | Doelveld | Notities |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Achternaam van de contactpersoon mag maximaal 80 tekens bevatten. |
     | `xdm: person.name.firstName` | `Attribute: FirstName` | De voornaam van de contactpersoon mag maximaal 40 tekens bevatten. |
     | `xdm: personalEmail.address` | `Attribute: Email` | Het e-mailadres van de contactpersoon |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
     ![ Experience Platform UI het screenshot voorbeeld dat de afbeeldingen van het Doel toont.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Werkend met Leads**

   * Als u met *Leads* binnen uw segment werkt, verwijs naar de Verwijzing van Objecten in Salesforce voor [ Lood ](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) om afbeeldingen voor de gebieden te bepalen die moeten worden bijgewerkt.
   * U kunt verplichte gebieden identificeren door naar het woord *Vereiste* te zoeken, dat in gebiedsbeschrijvingen in de verbinding hierboven wordt vermeld.
   * Afhankelijk van de velden die u wilt exporteren of bijwerken, voegt u toewijzingen toe tussen het XDM-profielschema en [!DNL (API) Salesforce CRM] :

     | Source-veld | Doelveld | Notities |
     | --- | --- | --- |
     | `IdentityMap: crmID` | `Identity: SalesforceId` | `Mandatory` |
     | `xdm: person.name.lastName` | `Attribute: LastName` | `Mandatory`. Achternaam van de lead mag maximaal 80 tekens bevatten. |
     | `xdm: b2b.companyName` | `Attribute: Company` | `Mandatory`. Het bedrijf van de leider. |
     | `xdm: personalEmail.address` | `Attribute: Email` | Het e-mailadres van de lead. |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
     ![ Experience Platform UI het screenshot voorbeeld dat de afbeeldingen van het Doel toont.](../../assets/catalog/crm/salesforce/mappings-leads.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-segment-export-example}

Wanneer het uitvoeren van de [ stap van de de publieksuitvoer van het Programma ](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) u moet publiek manueel in kaart brengen dat van Experience Platform aan hun overeenkomstig douanegebied in [!DNL Salesforce] wordt geactiveerd.

Hiervoor selecteert u elk segment en voert u de aangepaste veldnaam in uit [!DNL Salesforce] in het veld [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** . Verwijs naar [ creeer douanegebieden binnen  [!DNL Salesforce]](#prerequisites-custom-field) sectie voor begeleiding en beste praktijken bij het creëren van douanegebieden in [!DNL Salesforce].

Als het aangepaste veld [!DNL Salesforce] bijvoorbeeld `crm_2_seg` is, geeft u deze waarde op in [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** om het publiek van Experience Platform in dit aangepaste veld te vullen.

Hieronder ziet u een voorbeeld van een aangepast veld uit [!DNL Salesforce] :
![[!DNL Salesforce] UI-schermafbeelding met aangepast veld. ](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Hieronder ziet u een voorbeeld van de locatie van [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** :
![ het schermschot van Experience Platform UI die het publiek van het Programma tonen uitvoer.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Zoals hierboven wordt weergegeven, komt [!DNL Salesforce] **[!UICONTROL Field Name]** exact overeen met de waarde die is opgegeven binnen [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** .

Afhankelijk van het gebruik dat u maakt, kunnen alle geactiveerde soorten publiek worden toegewezen aan hetzelfde [!DNL Salesforce] aangepaste veld of aan een ander **[!UICONTROL Field Name]** in [!DNL Salesforce CRM] . Een typisch voorbeeld op basis van de bovenstaande afbeelding zou kunnen zijn.

| [!DNL Salesforce CRM] segmentnaam | [!DNL Salesforce] **[!UICONTROL Field Name]** | [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** |
| --- | --- | --- |
| crm_1_seg | `crm_1_seg` | `crm_1_seg` |
| crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Herhaal deze sectie voor elk geactiveerd Experience Platform-segment.

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteer **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met doelen te navigeren.
   {het schermschot van 0} Experience Platform UI die Browse Doelen toont.![](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Selecteer het doel en bevestig dat de status **[!UICONTROL enabled]** is.
   ![ het schermschot van Experience Platform UI die de Looppas van Doelen Dataflow toont.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Ga naar het tabblad **[!UICONTROL Activation data]** en selecteer vervolgens een publieksnaam.
   ![ het schermschot van Experience Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Controleer het publieksoverzicht en zorg ervoor dat de telling van profielen aan de telling beantwoordt die binnen het segment wordt gecreeerd.
   ![ het schermschot van Experience Platform UI die Segment toont.](../../assets/catalog/crm/salesforce/segment.png)

1. Meld u ten slotte aan bij de Salesforce-website en bevestig of de profielen van het publiek zijn bijgewerkt.

   **Werkend met Contacten**

   * Als u *Contacten* binnen uw segment van Experience Platform hebt geselecteerd, navigeer aan **[!DNL Apps]** > **[!DNL Contacts]** pagina.
     ![ het schermschot van Salesforce CRM die de pagina van Contacten met de profielen van het segment tonen.](../../assets/catalog/crm/salesforce/contacts.png)

   * Selecteer a *Contact* en controleer als de gebieden worden bijgewerkt. U kunt zien dat elke publieksstatus in [!DNL Salesforce CRM] met de overeenkomstige publieksstatus van Experience Platform werd bijgewerkt, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd tijdens het [ publiek dat ](#schedule-segment-export-example) plant.
     ![ het schermschot van Salesforce CRM die de pagina van de Details van het Contact met bijgewerkte publieksstatussen tonen.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Werkend met Leads**

   * Als u *Leads* binnen uw segment van Experience Platform hebt geselecteerd, dan navigeer aan **[!DNL Apps]** > **[!DNL Leads]** pagina.
     ![ het schermschot van Salesforce CRM die de pagina van Leads met de profielen van het segment toont.](../../assets/catalog/crm/salesforce/leads.png)

   * Selecteer a *Lood* en controleer als de gebieden worden bijgewerkt. U kunt zien dat elke publieksstatus in [!DNL Salesforce CRM] met de overeenkomstige publieksstatus van Experience Platform werd bijgewerkt, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd tijdens het [ publiek dat ](#schedule-segment-export-example) plant.
     ![ het schermschot van CRM van Salesforce die de pagina van Details van het Lood met bijgewerkte publieksstatussen toont.](../../assets/catalog/crm/salesforce/lead-info.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het naar de bestemming duwen van gebeurtenissen {#unknown-errors}

* Bij het controleren van een gegevensstroomuitvoering kan het volgende foutbericht optreden: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  {het schermschot van 0} Experience Platform UI die fout toont.![](../../assets/catalog/crm/salesforce/error.png)

   * Om deze fout te corrigeren, controleert u of de **[!UICONTROL Mapping ID]** die u in de activeringsworkflow hebt opgegeven voor het [!DNL Salesforce CRM] -doel exact overeenkomt met de waarde van het aangepaste veldtype dat u in [!DNL Salesforce] hebt gemaakt. Verwijs naar [ creeer douanegebieden binnen  [!DNL Salesforce]](#prerequisites-custom-field) sectie voor begeleiding.

* Wanneer u een segment activeert, wordt mogelijk een foutbericht weergegeven: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Om deze fout te bevestigen, contacteer uw [!DNL Salesforce] rekeningsbeheerder om [ Experience Platform IP adressen ](/help/destinations/catalog/streaming/ip-address-allow-list.md) aan uw [!DNL Salesforce] vertrouwde op IP waaiers van rekeningen toe te voegen. Verwijs naar [!DNL Salesforce] [ Beperk Toegang tot Vertrouwde IP Waaier voor een Verbonden App ](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5) documentatie als u extra begeleiding nodig hebt.

## Aanvullende bronnen {#additional-resources}

De extra nuttige informatie van [ Salesforce ontwikkelaarsportaal ](https://developer.salesforce.com/) is hieronder:

* [ Snel Begin ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [ creeer een Verslag ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [ publiek van de Aanbeveling van de Douane ](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [ Gebruikend Samengestelde Middelen ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Deze bestemmingshefboomwerkingen [ upsert Veelvoudige Verslagen ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API in plaats van [ upsert Enige Opname ](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API vraag.
