---
keywords: crm;CRM;crm bestemmingen;Microsoft Dynamics 365;Microsoft Dynamics 365 crm bestemming
title: Microsoft Dynamics 365-verbinding
description: Met de Microsoft Dynamics 365-bestemming kunt u uw accountgegevens exporteren en activeren binnen Microsoft Dynamics 365 voor uw zakelijke behoeften.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics 365] verbinding

## Overzicht {#overview}

[[!DNL Microsoft Dynamics 365] &#x200B;](https://dynamics.microsoft.com/en-us/) is een op wolk-gebaseerd bedrijfstoepassingsplatform dat de Planning van het Middel van de Onderneming (ERP) en het Beheer van de Verhouding van de Klant samen met productiviteitstoepassingen en AI hulpmiddelen combineert, om van begin tot eind vlottere en meer gecontroleerde verrichtingen, beter groeipotentieel en lagere kosten te brengen.

Dit [!DNL Adobe Experience Platform] [&#x200B; doel &#x200B;](/help/destinations/home.md) hefboomwerkingen [[!DNL Contact Entity Reference API] &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), die u toestaat om identiteiten binnen een publiek in [!DNL Dynamics 365] bij te werken.

[!DNL Dynamics 365] gebruikt OAuth 2 met de Vergunning verlenen als authentificatiemechanisme om met [!DNL Contact Entity Reference API] te communiceren. De instructies om aan uw [!DNL Dynamics 365] instantie voor authentiek te verklaren zijn verder hieronder, in [&#x200B; voor authentiek verklaren aan bestemmings &#x200B;](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u uw gebruikers een persoonlijke ervaring bieden op basis van kenmerken uit hun Adobe Experience Platform-profielen. U kunt publiek maken van uw offline gegevens en deze soorten publiek naar [!DNL Dynamics 365] sturen, zodat ze in de feeds van de gebruiker worden weergegeven zodra het publiek en de profielen in Adobe Experience Platform worden bijgewerkt.

## Vereisten {#prerequisites}

### Experience Platform-voorwaarden {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL Dynamics 365] bestemming te activeren, moet u a [&#x200B; schema &#x200B;](/help/xdm/schema/composition.md), a [&#x200B; dataset &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=nl-NL) hebben, en [&#x200B; publiek &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=nl-NL) dat in [!DNL Experience Platform] wordt gecreeerd.

Verwijs naar de documentatie van Adobe voor [&#x200B; het schemagroep van de Details van het Lidmaatschap van het Publiek &#x200B;](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatistieken nodig hebt.

### [!DNL Microsoft Dynamics 365] voorwaarden {#prerequisites-destination}

Als u gegevens wilt exporteren van Experience Platform naar uw [!DNL Dynamics 365] -account, moet u rekening houden met de volgende voorwaarden in [!DNL Dynamics 365] :

#### U moet een [!DNL Microsoft Dynamics 365] -account hebben {#prerequisites-account}

Ga naar de [!DNL Dynamics 365] [&#x200B; proefpagina &#x200B;](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) om een rekening te registreren en tot stand te brengen, als u niet reeds hebt.

#### Veld maken binnen [!DNL Dynamics 365] {#prerequisites-custom-field}

Maak het aangepaste veld van het type `Simple` met het veldgegevenstype `Single Line of Text` dat Experience Platform gebruikt om de status van het publiek in [!DNL Dynamics 365] bij te werken.

Verwijs naar [!DNL Dynamics 365] [&#x200B; creeer of geef een gebied (attribuut) uit &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) documentatie als u extra begeleiding nodig hebt.

Schrijf de **[!UICONTROL Customization prefix]** op van het aangepaste veld dat u in [!DNL Dynamics 365] maakt. U zult dit voorvoegsel tijdens [&#x200B; nodig hebben vult in bestemmingsdetails &#x200B;](#destination-details) stap. Verwijs naar [&#x200B; creeer en geef gebieden &#x200B;](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) sectie van de [!DNL Dynamics 365] documentatie voor verdere details uit.
&lbrace;de het schermschot van de Dynamiek 365 UI die van de aanpassingsprefix toont.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)

Hieronder ziet u een voorbeeldinstelling in [!DNL Dynamics 365] :
![&#x200B; Dynamiek 365 UI het schermschot die de douanegebieden tonen.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registreer een toepassing en toepassingsgebruiker binnen Azure Actieve Folder {#prerequisites-app-user}

Als u [!DNL Dynamics 365] toegang wilt geven tot bronnen, moet u zich aanmelden met uw [!DNL Azure Account] to [[!DNL Azure Active Directory] &#x200B;](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) en het volgende maken:
* Een [!DNL Azure Active Directory] -toepassing
* A Service principal
* Een toepassingsgeheim

U zult ook [&#x200B; een toepassingsgebruiker &#x200B;](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) binnen [!DNL Azure Active Directory] moeten creëren en het met de pas gecreëerde toepassing associëren.

#### [!DNL Dynamics 365] gebruikersgegevens verzamelen {#gather-credentials}

Noteer de onderstaande items voordat u verifieert voor de bestemming [!DNL Dynamics 365] CRM:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Client ID` | De [!DNL Dynamics 365] client-id voor uw [!DNL Azure Active Directory] -toepassing. Verwijs naar de [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) voor begeleiding. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | Het [!DNL Dynamics 365] clientgeheim voor uw [!DNL Azure Active Directory] -toepassing. U zou optie #2 binnen de [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options) gebruiken. | `abcde~abcdefghijklmnopqrstuvwxyz12345678` voor hulp. |
| `Tenant ID` | De [!DNL Dynamics 365] Tenant ID voor uw [!DNL Azure Active Directory] -toepassing. Verwijs naar de [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) voor begeleiding. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | Het Microsoft-gebied dat is gekoppeld aan de URL van de omgeving.<br> verwijs naar de [[!DNL Dynamics 365]  documentatie &#x200B;](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) voor begeleiding. | Als uw domein zoals hieronder is, moet u de benadrukte waarde voor het gebied van CRM in de dropdown selecteur verstrekken wanneer het voor authentiek verklaren aan de [&#x200B; bestemming &#x200B;](#authenticate).<br> *org57771b33.`crm` .dynamics.com*<br> Als voorbeeld: Als uw bedrijf provisioned in het gebied van Noord-Amerika (NAM) is, zou uw URL `crm.dynamics.com` zijn en u moet selecteren `crm`. Als uw bedrijf is ingericht in het Canada-gebied (CAN), is de URL `crm3.dynamics.com` en moet u `crm3` selecteren. |
| `Environment URL` | Verwijs naar de [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) voor begeleiding. | Als uw [!DNL Dynamics 365] domein hieronder is, hebt u de benadrukte waarde nodig.<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## Guardrails {#guardrails}

De [&#x200B; grenzen en de toewijzingen van Verzoeken &#x200B;](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) pagina details de [!DNL Dynamics 365] API grenzen verbonden aan uw [!DNL Dynamics 365] vergunning. U moet ervoor zorgen dat uw gegevens en lading binnen deze beperkingen zijn.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Dynamics 365] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Voorbeeld | Beschrijving | Overwegingen |
|---|---|---|---|
| `contactid` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Unieke id voor een contactpersoon. | **Verplicht**. Verwijs naar de [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) voor verdere details. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Deze bestemming steunt de activering van alle die publiek door de Dienst van de Segmentatie van Experience Platform [&#x200B; wordt geproduceerd &#x200B;](../../../segmentation/home.md).

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Elke publieksstatus in [!DNL Dynamics 365] wordt bijgewerkt met de overeenkomstige publieksstatus van Experience Platform, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd tijdens de [&#x200B; publiek die &#x200B;](#schedule-audience-export-example) stap plannen.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Kies in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** Zoeken naar [!DNL Dynamics 365] . U kunt de locatie ook in de categorie **[!UICONTROL CRM]** vinden.

### Verifiëren voor bestemming {#authenticate}

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.
{het schermschot van 0} Experience Platform UI die toont hoe te voor authentiek te verklaren.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Vul de vereiste velden hieronder in. Verwijs naar de [&#x200B; Dynamica 365 van de Verzameling geloofsbrieven &#x200B;](#gather-credentials) sectie voor om het even welke begeleiding.
* **[!UICONTROL Client ID]**: De [!DNL Dynamics 365] client-id voor uw [!DNL Azure Active Directory] -toepassing.
* **[!UICONTROL Tenant ID]**: De [!DNL Dynamics 365] Tenant-id voor uw [!DNL Azure Active Directory] -toepassing.
* **[!UICONTROL Client Secret]**: Het [!DNL Dynamics 365] clientgeheim voor uw [!DNL Azure Active Directory] -toepassing.
* **[!UICONTROL Region]**: Uw [[!DNL Dynamics 365] &#x200B;](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) gebied. Als voorbeeld: Als uw bedrijf is ingericht in het gebied Noord-Amerika (NAM), is de URL `crm.dynamics.com` en moet u `crm` selecteren. Als uw bedrijf is ingericht in het Canada-gebied (CAN), is de URL `crm3.dynamics.com` en moet u `crm3` selecteren.
* **[!UICONTROL Environment URL]**: de URL van uw [!DNL Dynamics 365] omgeving.

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
{het schermschot van 0} Experience Platform UI die de bestemmingsdetails toont.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Customization Prefix]**: De `Customization prefix` van het aangepaste veld dat u hebt gemaakt in [!DNL Dynamics 365] . Verwijs naar [&#x200B; creeer en geef gebieden &#x200B;](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) sectie van de [!DNL Dynamics 365] documentatie voor verdere details uit.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Dynamics 365] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming. Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Dynamics 365] -doelvelden:

1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.
   ![&#x200B; het schermschot van Experience Platform UI voor Add nieuwe afbeelding.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select identity namespace]** en selecteer `contactid` .
   ![&#x200B; het schermschot van Experience Platform UI voor de afbeelding van Source.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. Selecteer in het **[!UICONTROL Select target field]** -venster het type doelveld waaraan u het bronveld wilt toewijzen.
   * **[!UICONTROL Select identity namespace]**: selecteer deze optie om het bronveld toe te wijzen aan een naamruimte in de lijst.

     ![&#x200B; het schermschot van Experience Platform UI die de afbeelding van het Doel voor contact tonen.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Voeg de volgende toewijzing toe tussen uw XDM-profielschema en uw [!DNL Dynamics 365] -instantie:

     | XDM-profielschema | [!DNL Dynamics 365] Instantie | Verplicht |
     |---|---|---|
     | `contactid` | `contactid` | Ja |

   * **[!UICONTROL Select custom attributes]**: selecteer deze optie om het bronveld toe te wijzen aan een aangepast kenmerk dat u in het veld **[!UICONTROL Attribute name]** definieert. Verwijs naar [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) voor een uitvoerige lijst van gesteunde attributen.

     {het schermschot van 0} Experience Platform UI die de afbeelding van het Doel voor e-mail toont.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-email.png)

     >[!IMPORTANT]
     >
     > * Doelveldnamen moeten in `lowercase` staan.
     > * Bovendien, als u een datum of timestamp brongebied hebt dat aan a [!DNL Dynamics 365] [&#x200B; datum of timestamp &#x200B;](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) doelgebied in kaart wordt gebracht, zorg ervoor dat de in kaart gebrachte waarde niet leeg is. Als de geëxporteerde veldwaarde leeg is, wordt een *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* -foutbericht weergegeven en worden de gegevens niet bijgewerkt. Dit is een [!DNL Dynamics 365] -beperking.

   * Afhankelijk van de waarden die u wilt bijwerken, voegt u bijvoorbeeld de volgende toewijzing toe tussen uw XDM-profielschema en uw [!DNL Dynamics 365] -instantie:

     | XDM-profielschema | [!DNL Dynamics 365] Instantie |
     |---|---|
     | `person.name.firstName` | `firstname` |
     | `person.name.lastName` | `lastname` |
     | `personalEmail.address` | `emailaddress1` |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:

   ![&#x200B; Experience Platform UI het screenshot voorbeeld dat de afbeeldingen van het Doel toont.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-audience-export-example}

In de stap [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) van de activeringsworkflow moet u Experience Platform-soorten publiek handmatig toewijzen aan het aangepaste veldkenmerk in [!DNL Dynamics 365] .

U doet dit door elk publiek te selecteren en vervolgens het bijbehorende aangepaste veldkenmerk in te voeren vanuit [!DNL Dynamics 365] in het veld **[!UICONTROL Mapping ID]** .

>[!IMPORTANT]
>
>De waarde die voor de **[!UICONTROL Mapping ID]** wordt gebruikt, moet exact overeenkomen met de naam van het aangepaste veldkenmerk dat in [!DNL Dynamics 365] is gemaakt. Zie [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) als u begeleiding bij het vinden van uw attributen van het douanegebied nodig hebt.

Hieronder ziet u een voorbeeld:
{het screenshot voorbeeld van 0} Experience Platform UI die het publiek van het Programma tonen uitvoer.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteer **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met doelen te navigeren.
   {het schermschot van 0} Experience Platform UI die Browse Doelen toont.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Selecteer het doel en bevestig dat de status **[!UICONTROL enabled]** is.
   ![&#x200B; het schermschot van Experience Platform UI die de Looppas van Doelen Dataflow toont.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Ga naar het tabblad **[!DNL Activation data]** en selecteer vervolgens een publieksnaam.
   ![&#x200B; het schermschot van Experience Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Controleer het overzicht van het publiek en zorg ervoor dat het aantal profielen overeenkomt met het aantal profielen dat in het publiek is gemaakt.
   {het schermschot van 0} Experience Platform UI die publiek toont.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Meld u aan bij de [!DNL Dynamics 365] -website, navigeer naar de pagina [!DNL Customers] > [!DNL Contacts] en controleer of de profielen van het publiek zijn toegevoegd. U kunt zien dat elke publieksstatus in [!DNL Dynamics 365] met de overeenkomstige publieksstatus van Experience Platform werd bijgewerkt, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd die tijdens de [&#x200B; publiek wordt verstrekt die &#x200B;](#schedule-audience-export-example) stap plant.
   &lbrace;de het schermschot van de Dynamiek 365 UI die de pagina van Contacten met bijgewerkte publieksstatussen toont.![&#128279;](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het naar bestemming duwen van gebeurtenissen {#unknown-errors}

Wanneer u een gegevensstroomuitvoering controleert, als u het volgende foutbericht krijgt: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![&#x200B; het schermschot van Experience Platform UI die Onjuiste verzoekfout toont.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Om deze fout te corrigeren, controleert u of de **[!UICONTROL Mapping ID]** die u in [!DNL Dynamics 365] voor uw Experience Platform-publiek hebt opgegeven, geldig is en bestaat binnen [!DNL Dynamics 365] .

## Aanvullende bronnen {#additional-resources}

De extra nuttige informatie van de [[!DNL Dynamics 365]  documentatie &#x200B;](https://docs.microsoft.com/en-us/dynamics365/) is hieronder:
* [&#x200B; IOrganizationService.Update (Entiteit) Methode &#x200B;](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [&#x200B; Update en schrap lijstrijen gebruikend het Web API &#x200B;](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Oktober 2023 | Documentatie bijgewerkt | De bijgewerkte begeleiding om op alle namen van doelattributen te wijzen zou in kleine letters, in de [&#x200B; Afbeelding overwegingen en voorbeeld &#x200B;](#mapping-considerations-example) stap moeten zijn. |
| Augustus 2023 | Bijwerken van functionaliteit en documentatie | Extra ondersteuning voor [!DNL Dynamics 365] aangepaste veldvoorvoegsels voor aangepaste velden die niet zijn gemaakt in de standaardoplossing van [!DNL Dynamics 365] . Een nieuw inputgebied, **[!UICONTROL Customization Prefix]**, is toegevoegd in [&#x200B; Vul de stap van bestemmingsdetails &#x200B;](#destination-details). (PLATIR-31602). |
| nov. 2022 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++