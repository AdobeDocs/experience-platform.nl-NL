---
keywords: crm;CRM;crm bestemmingen;Microsoft Dynamics 365;Microsoft Dynamics 365 crm bestemming
title: Microsoft Dynamics 365-verbinding
description: Met de bestemming Microsoft Dynamics 365 kunt u uw accountgegevens exporteren en activeren in Microsoft Dynamics 365 voor uw zakelijke behoeften.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: 5aefa362d7a7d93c12f9997d56311127e548497e
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics 365] verbinding

## Overzicht {#overview}

[[!DNL Microsoft Dynamics 365] ](https://dynamics.microsoft.com/en-us/) is een op wolk-gebaseerd bedrijfstoepassingsplatform dat de Planning van het Middel van de Onderneming (ERP) en het Beheer van de Verhouding van de Klant samen met productiviteitstoepassingen en AI hulpmiddelen combineert, om van begin tot eind vlottere en meer gecontroleerde verrichtingen, beter groeipotentieel en lagere kosten te brengen.

Dit [!DNL Adobe Experience Platform] [ doel ](/help/destinations/home.md) hefboomwerkingen [[!DNL Contact Entity Reference API] ](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), die u toestaat om identiteiten binnen een publiek in [!DNL Dynamics 365] bij te werken.

[!DNL Dynamics 365] gebruikt OAuth 2 met de Vergunning verlenen als authentificatiemechanisme om met [!DNL Contact Entity Reference API] te communiceren. De instructies om aan uw [!DNL Dynamics 365] instantie voor authentiek te verklaren zijn verder hieronder, in [ voor authentiek verklaren aan bestemmings ](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u uw gebruikers een persoonlijke ervaring bieden op basis van kenmerken uit hun Adobe Experience Platform-profielen. U kunt publiek maken van uw offline gegevens en deze soorten publiek naar [!DNL Dynamics 365] sturen, zodat ze in de feeds van de gebruiker worden weergegeven zodra het publiek en de profielen in Adobe Experience Platform worden bijgewerkt.

## Vereisten {#prerequisites}

### Voorwaarden voor Experience Platforms {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL Dynamics 365] bestemming te activeren, moet u a [ schema ](/help/xdm/schema/composition.md), a [ dataset ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) hebben, en [ publiek ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) dat in [!DNL Experience Platform] wordt gecreeerd.

Verwijs naar de documentatie van de Adobe voor [ het schemagroep van de Details van het Lidmaatschap van de Publiek ](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatistieken nodig hebt.

### [!DNL Microsoft Dynamics 365] voorwaarden {#prerequisites-destination}

Als u gegevens wilt exporteren van Platform naar uw [!DNL Dynamics 365] -account, moet u rekening houden met de volgende voorwaarden in [!DNL Dynamics 365] :

#### U moet een [!DNL Microsoft Dynamics 365] -account hebben {#prerequisites-account}

Ga naar de [!DNL Dynamics 365] [ proefpagina ](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) om een rekening te registreren en tot stand te brengen, als u niet reeds hebt.

#### Veld maken binnen [!DNL Dynamics 365] {#prerequisites-custom-field}

Maak het aangepaste veld van het type `Simple` met het veldgegevenstype `Single Line of Text` dat Experience Platform gebruikt om de status van het publiek in [!DNL Dynamics 365] bij te werken.

Verwijs naar [!DNL Dynamics 365] [ creeer of geef een gebied (attribuut) uit ](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) documentatie als u extra begeleiding nodig hebt.

Schrijf de **[!UICONTROL Customization prefix]** op van het aangepaste veld dat u in [!DNL Dynamics 365] maakt. U zult dit voorvoegsel tijdens [ nodig hebben vult in bestemmingsdetails ](#destination-details) stap. Verwijs naar [ creeer en geef gebieden ](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) sectie van de [!DNL Dynamics 365] documentatie voor verdere details uit.
{de het schermschot van de Dynamiek 365 UI die van de aanpassingsprefix toont.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)![

Hieronder ziet u een voorbeeldinstelling in [!DNL Dynamics 365] :
![ Dynamiek 365 UI het schermschot die de douanegebieden tonen.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registreer een toepassing en toepassingsgebruiker binnen Azure Actieve Folder {#prerequisites-app-user}

Als u [!DNL Dynamics 365] toegang wilt geven tot bronnen, moet u zich aanmelden met uw [!DNL Azure Account] to [[!DNL Azure Active Directory] ](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) en het volgende maken:
* Een [!DNL Azure Active Directory] -toepassing
* A Service principal
* Een toepassingsgeheim

U zult ook [ een toepassingsgebruiker ](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) binnen [!DNL Azure Active Directory] moeten creëren en het met de pas gecreëerde toepassing associëren.

#### [!DNL Dynamics 365] gebruikersgegevens verzamelen {#gather-credentials}

Noteer de onderstaande items voordat u verifieert voor de bestemming [!DNL Dynamics 365] CRM:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Client ID` | De [!DNL Dynamics 365] client-id voor uw [!DNL Azure Active Directory] -toepassing. Verwijs naar de [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) voor begeleiding. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | Het [!DNL Dynamics 365] clientgeheim voor uw [!DNL Azure Active Directory] -toepassing. U zou optie #2 binnen de [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options) gebruiken. | `abcde~abcdefghijklmnopqrstuvwxyz12345678` voor hulp. |
| `Tenant ID` | De [!DNL Dynamics 365] Tenant ID voor uw [!DNL Azure Active Directory] -toepassing. Verwijs naar de [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) voor begeleiding. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | Het Microsoft-gebied dat is gekoppeld aan de URL van de omgeving.<br> verwijs naar de [[!DNL Dynamics 365]  documentatie ](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) voor begeleiding. | Als uw domein zoals hieronder is, moet u de benadrukte waarde voor het gebied van CRM in de dropdown selecteur verstrekken wanneer het voor authentiek verklaren aan de [ bestemming ](#authenticate).<br> *org57771b33.`crm` .dynamics.com*<br> Als voorbeeld: Als uw bedrijf provisioned in het gebied van Noord-Amerika (NAM) is, zou uw URL `crm.dynamics.com` zijn en u moet selecteren `crm`. Als uw bedrijf is ingericht in het Canada-gebied (CAN), is de URL `crm3.dynamics.com` en moet u `crm3` selecteren. |
| `Environment URL` | Verwijs naar de [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) voor begeleiding. | Als uw [!DNL Dynamics 365] domein hieronder is, hebt u de benadrukte waarde nodig.<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## Guardrails {#guardrails}

De [ grenzen en de toewijzingen van Verzoeken ](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) pagina details de [!DNL Dynamics 365] API grenzen verbonden aan uw [!DNL Dynamics 365] vergunning. U moet ervoor zorgen dat uw gegevens en lading binnen deze beperkingen zijn.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Dynamics 365] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Voorbeeld | Beschrijving | Overwegingen |
|---|---|---|---|
| `contactid` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Unieke id voor een contactpersoon. | **Verplicht**. Verwijs naar de [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) voor verdere details. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Deze bestemming steunt de activering van alle die publiek door de Dienst van de Segmentatie van het Experience Platform [ wordt geproduceerd ](../../../segmentation/home.md).

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Elke publieksstatus in [!DNL Dynamics 365] wordt bijgewerkt met de overeenkomstige publieksstatus van Platform, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd die tijdens de [ publiek wordt verstrekt die ](#schedule-audience-export-example) stap plant.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Kies in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** Zoeken naar [!DNL Dynamics 365] . U kunt de locatie ook in de categorie **[!UICONTROL CRM]** vinden.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.
{het schermschot van het platform UI die tonen hoe te voor authentiek te verklaren.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)![

Vul de vereiste velden hieronder in. Verwijs naar de [ Dynamica 365 van de Verzameling geloofsbrieven ](#gather-credentials) sectie voor om het even welke begeleiding.
* **[!UICONTROL Client ID]**: De [!DNL Dynamics 365] client-id voor uw [!DNL Azure Active Directory] -toepassing.
* **[!UICONTROL Tenant ID]**: De [!DNL Dynamics 365] Tenant-id voor uw [!DNL Azure Active Directory] -toepassing.
* **[!UICONTROL Client Secret]**: Het [!DNL Dynamics 365] clientgeheim voor uw [!DNL Azure Active Directory] -toepassing.
* **[!UICONTROL Region]**: Uw [[!DNL Dynamics 365] ](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) gebied. Als voorbeeld: Als uw bedrijf is ingericht in het gebied Noord-Amerika (NAM), is de URL `crm.dynamics.com` en moet u `crm` selecteren. Als uw bedrijf is ingericht in het Canada-gebied (CAN), is de URL `crm3.dynamics.com` en moet u `crm3` selecteren.
* **[!UICONTROL Environment URL]**: de URL van uw [!DNL Dynamics 365] omgeving.

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
{het schermschot van het platform UI die de bestemmingsdetails toont.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)![

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Customization Prefix]**: De `Customization prefix` van het aangepaste veld dat u hebt gemaakt in [!DNL Dynamics 365] . Verwijs naar [ creeer en geef gebieden ](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) sectie van de [!DNL Dynamics 365] documentatie voor verdere details uit.

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

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Dynamics 365] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming. Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Dynamics 365] -doelvelden:

1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.
   {het screenshot voorbeeld van het platform UI voor Add nieuwe afbeelding.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)![

1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select identity namespace]** en selecteer `contactid` .
   ![ het schermschot van het Platform UI voor het in kaart brengen van Source.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. Selecteer in het **[!UICONTROL Select target field]** -venster het type doelveld waaraan u het bronveld wilt toewijzen.
   * **[!UICONTROL Select identity namespace]**: selecteer deze optie om het bronveld toe te wijzen aan een naamruimte in de lijst.
     {het schermschot van het platform UI die van het Doel afbeelding voor contact tonen.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)![

   * Voeg de volgende toewijzing toe tussen uw XDM-profielschema en uw [!DNL Dynamics 365] -instantie:

     | XDM-profielschema | [!DNL Dynamics 365] Instantie | Verplicht |
     |---|---|---|
     | `contactid` | `contactid` | Ja |

   * **[!UICONTROL Select custom attributes]**: selecteer deze optie om het bronveld toe te wijzen aan een aangepast kenmerk dat u in het veld **[!UICONTROL Attribute name]** definieert. Verwijs naar [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) voor een uitvoerige lijst van gesteunde attributen.
     {het schermschot van het platform UI die van het Doel afbeelding voor e-mail toont.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-email.png)![

     >[!IMPORTANT]
     >
     > * Doelveldnamen moeten in `lowercase` staan.
     > * Bovendien, als u een datum of timestamp brongebied hebt dat aan a [!DNL Dynamics 365] [ datum of timestamp ](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) doelgebied in kaart wordt gebracht, zorg ervoor dat de in kaart gebrachte waarde niet leeg is. Als de geëxporteerde veldwaarde leeg is, wordt een *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* -foutbericht weergegeven en worden de gegevens niet bijgewerkt. Dit is een [!DNL Dynamics 365] -beperking.

   * Afhankelijk van de waarden die u wilt bijwerken, voegt u bijvoorbeeld de volgende toewijzing toe tussen uw XDM-profielschema en uw [!DNL Dynamics 365] -instantie:

     | XDM-profielschema | [!DNL Dynamics 365] Instantie |
     |---|---|
     | `person.name.firstName` | `firstname` |
     | `person.name.lastName` | `lastname` |
     | `personalEmail.address` | `emailaddress1` |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:

   ![ het schermschot van het Platform UI die de afbeeldingen van het Doel tonen.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-audience-export-example}

In de stap [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) van de activeringsworkflow moet u het publiek Platform handmatig toewijzen aan het aangepaste veldkenmerk in [!DNL Dynamics 365] .

U doet dit door elk publiek te selecteren en vervolgens het bijbehorende aangepaste veldkenmerk in te voeren vanuit [!DNL Dynamics 365] in het veld **[!UICONTROL Mapping ID]** .

>[!IMPORTANT]
>
>De waarde die voor de **[!UICONTROL Mapping ID]** wordt gebruikt, moet exact overeenkomen met de naam van het aangepaste veldkenmerk dat in [!DNL Dynamics 365] is gemaakt. Zie [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) als u begeleiding bij het vinden van uw attributen van het douanegebied nodig hebt.

Hieronder ziet u een voorbeeld:
{het screenshot voorbeeld van het Platform UI die het publiek van het Programma tonen uitvoer.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)![

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteer **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met doelen te navigeren.
   ![ het schermschot van het Platform UI die door Doelen toont.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Selecteer het doel en bevestig dat de status **[!UICONTROL enabled]** is.
   ![ het schermschot van het Platform UI die de Looppas van Doelen Dataflow toont.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Ga naar het tabblad **[!DNL Activation data]** en selecteer vervolgens een publieksnaam.
   ![ het schermschot van het Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Controleer het overzicht van het publiek en zorg ervoor dat het aantal profielen overeenkomt met het aantal profielen dat in het publiek is gemaakt.
   {het screenshot voorbeeld van het platform UI die publiek toont.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)![

1. Meld u aan bij de [!DNL Dynamics 365] -website, navigeer naar de pagina [!DNL Customers] > [!DNL Contacts] en controleer of de profielen van het publiek zijn toegevoegd. U kunt zien dat elke publieksstatus in [!DNL Dynamics 365] met de overeenkomstige publieksstatus van Platform werd bijgewerkt, dat op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd die tijdens de [ publiek wordt verstrekt die ](#schedule-audience-export-example) stap plant.
   {de het schermschot van de Dynamiek 365 UI die de pagina van Contacten met bijgewerkte publieksstatussen toont.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)![

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het naar bestemming duwen van gebeurtenissen {#unknown-errors}

Wanneer u een gegevensstroomuitvoering controleert, als u het volgende foutbericht krijgt: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

{het schermschot van 0} Platform UI die Onjuiste verzoekfout toont.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)![

U kunt deze fout verhelpen door te controleren of de **[!UICONTROL Mapping ID]** die u in [!DNL Dynamics 365] voor uw platformpubliek hebt opgegeven, geldig is en aanwezig is in [!DNL Dynamics 365] .

## Aanvullende bronnen {#additional-resources}

De extra nuttige informatie van de [[!DNL Dynamics 365]  documentatie ](https://docs.microsoft.com/en-us/dynamics365/) is hieronder:
* [ IOrganizationService.Update (Entiteit) Methode ](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [ Update en schrap lijstrijen gebruikend het Web API ](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Oktober 2023 | Documentatie bijwerken | De bijgewerkte begeleiding om op alle namen van doelattributen te wijzen zou in kleine letters, in de [ Afbeelding overwegingen en voorbeeld ](#mapping-considerations-example) stap moeten zijn. |
| Augustus 2023 | Bijwerken van functionaliteit en documentatie | Extra ondersteuning voor [!DNL Dynamics 365] aangepaste veldvoorvoegsels voor aangepaste velden die niet zijn gemaakt in de standaardoplossing van [!DNL Dynamics 365] . Een nieuw inputgebied, **[!UICONTROL Customization Prefix]**, is toegevoegd in [ Vul de stap van bestemmingsdetails ](#destination-details). (PLATIR-31602). |
| nov. 2022 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++