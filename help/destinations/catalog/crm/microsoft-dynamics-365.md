---
keywords: crm;CRM;crm bestemmingen;Microsoft Dynamics 365;Microsoft Dynamics 365 crm bestemming
title: Microsoft Dynamics 365-verbinding
description: Met de bestemming Microsoft Dynamics 365 kunt u uw accountgegevens exporteren en activeren in Microsoft Dynamics 365 voor uw zakelijke behoeften.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 49bb5c95-f4b7-42e1-9aae-45143bbb1d73
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 0%

---

# [!DNL Microsoft Dynamics 365] verbinding

## Overzicht {#overview}

[[!DNL Microsoft Dynamics 365]](https://dynamics.microsoft.com/en-us/) is een bedrijfstoepassingsplatform in de cloud dat zowel Enterprise Resource Planning (ERP) als Customer Relationship Management (CRM) combineert met productiviteitstoepassingen en AI-tools, om end-to-end soepelere en meer gecontroleerde bewerkingen, een beter groeipotentieel en lagere kosten te realiseren.

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [[!DNL Contact Entity Reference API]](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1), waarmee u identiteiten binnen een publiek kunt bijwerken naar [!DNL Dynamics 365].

[!DNL Dynamics 365] gebruikt OAuth 2 met de Vergunning van de Vergunning als authentificatiemechanisme om met het te communiceren [!DNL Contact Entity Reference API]. Instructies voor verificatie aan uw [!DNL Dynamics 365] de instantie is verder onderaan, in de [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u uw gebruikers een persoonlijke ervaring bieden op basis van kenmerken uit hun Adobe Experience Platform-profielen. U kunt een publiek maken op basis van uw offline gegevens en deze soorten publiek verzenden naar [!DNL Dynamics 365], om in de feeds van de gebruikers weer te geven zodra het publiek en de profielen in Adobe Experience Platform zijn bijgewerkt.

## Vereisten {#prerequisites}

### Voorwaarden voor Experience Platforms {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL Dynamics 365] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html), en [publiek](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) gemaakt in [!DNL Experience Platform].

Raadpleeg de documentatie van de Adobe voor [Publiek Lidmaatschap Details schema groep](/help/xdm/field-groups/profile/segmentation.md) als u hulp over publieksstatus nodig hebt.

### [!DNL Microsoft Dynamics 365] voorwaarden {#prerequisites-destination}

Houd rekening met de volgende voorwaarden in [!DNL Dynamics 365]om gegevens van Platform naar uw [!DNL Dynamics 365] account:

#### U hebt een [!DNL Microsoft Dynamics 365] account {#prerequisites-account}

Ga naar de [!DNL Dynamics 365] [proefversie](https://dynamics.microsoft.com/en-us/dynamics-365-free-trial/) pagina om te registreren en een account te maken, als u er nog geen hebt.

#### Veld maken binnen [!DNL Dynamics 365] {#prerequisites-custom-field}

Het aangepaste tekstveld maken `Simple` met veldgegevenstype als `Single Line of Text` welk Experience Platform wordt gebruikt om de publieksstatus bij te werken binnen [!DNL Dynamics 365].

Zie de [!DNL Dynamics 365] [Een veld maken of bewerken (kenmerk)](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) documentatie als u extra begeleiding nodig hebt.

Schrijf de **[!UICONTROL Customization prefix]** van het aangepaste veld dat u maakt in [!DNL Dynamics 365]. U hebt dit voorvoegsel nodig tijdens het [Doelgegevens invullen](#destination-details) stap. Zie de [Velden maken en bewerken](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) van de [!DNL Dynamics 365] documentatie voor meer informatie.
![Dynamics 365 UI screenshot die het aanpassingsvoorvoegsel toont.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-customization-prefix.png)

Een voorbeeldinstelling binnen [!DNL Dynamics 365] wordt hieronder weergegeven:
![Dynamics 365 UI screenshot die de aangepaste velden weergeeft.](../../assets/catalog/crm/microsoft-dynamics-365/dynamics-365-fields.png)

#### Registreer een toepassing en toepassingsgebruiker binnen Azure Actieve Folder {#prerequisites-app-user}

Inschakelen [!DNL Dynamics 365] om tot middelen toegang te hebben zult u met uw moeten login [!DNL Azure Account] tot [[!DNL Azure Active Directory]](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#register-an-application-with-azure-ad-and-create-a-service-principal) en maak het volgende:
* An [!DNL Azure Active Directory] toepassing
* A Service principal
* Een toepassingsgeheim

U moet ook [een toepassingsgebruiker maken](https://docs.microsoft.com/en-us/power-platform/admin/manage-application-users#create-an-application-user) in [!DNL Azure Active Directory] en deze aan de nieuwe toepassing koppelen.

#### Gather [!DNL Dynamics 365] geloofsbrieven {#gather-credentials}

Noteer de onderstaande items voordat u deze verifieert voor de [!DNL Dynamics 365] CRM-bestemming:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Client ID` | De [!DNL Dynamics 365] Client-id voor uw [!DNL Azure Active Directory] toepassing. Zie de [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) ter begeleiding. | `ababbaba-abab-baba-acac-acacacacacac` |
| `Client Secret` | De [!DNL Dynamics 365] Clientgeheim voor uw [!DNL Azure Active Directory] toepassing. U gebruikt optie nr. 2 binnen [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#authentication-two-options). | `abcde~abcdefghijklmnopqrstuvwxyz12345678` ter begeleiding. |
| `Tenant ID` | De [!DNL Dynamics 365] Tenant ID voor uw [!DNL Azure Active Directory] toepassing. Zie de [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal#get-tenant-and-app-id-values-for-signing-in) ter begeleiding. | `1234567-aaaa-12ab-ba21-1234567890` |
| `Region` | Het Microsoft-gebied dat is gekoppeld aan de URL van de omgeving.<br> Zie de [[!DNL Dynamics 365] documentatie](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) ter begeleiding. | Als uw domein is zoals hieronder, moet u de benadrukte waarde voor het gebied van CRM in de dropdown selecteur verstrekken wanneer voor authentiek verklaard aan [doel](#authenticate).<br> *org5771b33.`crm`.dynamics.com*<br>  Als voorbeeld: Als uw bedrijf is ingericht in het gebied Noord-Amerika (NAM), is uw URL `crm.dynamics.com` en u moet selecteren `crm`. Als uw bedrijf is ingericht in het Canada-gebied (CAN), is uw URL `crm3.dynamics.com` en u moet selecteren `crm3`. |
| `Environment URL` | Zie de [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/org-service/discover-url-organization-organization-service?view=op-9-1) ter begeleiding. | Als uw [!DNL Dynamics 365] -domein is zoals hieronder aangegeven, hebt u de gemarkeerde waarde nodig.<br> *`org57771b33`.crm.dynamics.com* |

{style="table-layout:auto"}

## Guardrails {#guardrails}

De [Beperkingen en toewijzingen van verzoeken](https://docs.microsoft.com/en-us/power-platform/admin/api-request-limits-allocations) pagina bevat de details van [!DNL Dynamics 365] API-limieten die zijn gekoppeld aan uw [!DNL Dynamics 365] licentie. U moet ervoor zorgen dat uw gegevens en lading binnen deze beperkingen zijn.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Dynamics 365] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Voorbeeld | Beschrijving | Overwegingen |
|---|---|---|---|
| `contactid` | 7eb682f1-ca75-e511-80d4-00155d2a68d1 | Unieke id voor een contactpersoon. | **Verplicht**. Zie de [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1) voor nadere bijzonderheden. |

{style="table-layout:auto"}

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Deze bestemming steunt de activering van alle publiek dat door het Experience Platform wordt geproduceerd [Segmenteringsservice](../../../segmentation/home.md).

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)*, op basis van uw veldtoewijzing.</li><li> Elke publieksstatus in [!DNL Dynamics 365] wordt bijgewerkt met de corresponderende publieksstatus van Platform, gebaseerd op de **[!UICONTROL Mapping ID]** waarde die tijdens de [publieksplanning](#schedule-audience-export-example) stap.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** zoeken naar [!DNL Dynamics 365]. U kunt de locatie ook onder de **[!UICONTROL CRM]** categorie.

### Verifiëren voor bestemming {#authenticate}

Om voor authentiek te verklaren aan de bestemming, uitgezocht **[!UICONTROL Connect to destination]**.
![Schermopname van de gebruikersinterface van het platform waarin wordt getoond hoe te voor authentiek te verklaren.](../../assets/catalog/crm/microsoft-dynamics-365/authenticate-destination.png)

Vul de vereiste velden hieronder in. Zie de [Inloggegevens van Gather Dynamics 365](#gather-credentials) voor eventuele richtsnoeren.
* **[!UICONTROL Client ID]**: De [!DNL Dynamics 365] Client-id voor uw [!DNL Azure Active Directory] toepassing.
* **[!UICONTROL Tenant ID]**: De [!DNL Dynamics 365] Tenant ID voor uw [!DNL Azure Active Directory] toepassing.
* **[!UICONTROL Client Secret]**: De [!DNL Dynamics 365] Clientgeheim voor uw [!DNL Azure Active Directory] toepassing.
* **[!UICONTROL Region]**: Uw [[!DNL Dynamics 365]](https://learn.microsoft.com/en-us/power-platform/admin/new-datacenter-regions) Regio. Als voorbeeld: Als uw bedrijf is ingericht in het gebied Noord-Amerika (NAM), is uw URL `crm.dynamics.com` en u moet selecteren `crm`. Als uw bedrijf is ingericht in het Canada-gebied (CAN), is uw URL `crm3.dynamics.com` en u moet selecteren `crm3`.
* **[!UICONTROL Environment URL]**: Uw [!DNL Dynamics 365] Omgeving-URL.

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** status met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Platform UI het schermschot die de bestemmingsdetails tonen.](../../assets/catalog/crm/microsoft-dynamics-365/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst wilt herkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Customization Prefix]**: De `Customization prefix` van het aangepaste veld waarin u hebt gemaakt [!DNL Dynamics 365]. Zie de [Velden maken en bewerken](https://learn.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1#create-and-edit-fields) van de [!DNL Dynamics 365] documentatie voor meer informatie.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.
>* Om te exporteren *identiteiten*, hebt u de **[!UICONTROL View Identity Graph]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). <br> ![Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecteer naamruimte voor identiteit die in de workflow wordt gemarkeerd om het publiek naar bestemmingen te activeren."){width="100" zoomable="yes"}

Lezen [Profielen en doelgroepen activeren voor het streamen van doelgroepen voor het exporteren van bestanden](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Dynamics 365] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming. Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL Dynamics 365] doelvelden, voer de volgende stappen uit:

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
   ![Voorbeeld van screenshot van platforminterface voor nieuwe toewijzing toevoegen.](../../assets/catalog/crm/microsoft-dynamics-365/add-new-mapping.png)

1. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select identity namespace]** categorie en selecteer `contactid`.
   ![Voorbeeld van screenshot voor platform-UI voor brontoewijzing.](../../assets/catalog/crm/microsoft-dynamics-365/source-mapping.png)

1. In de **[!UICONTROL Select target field]** selecteert u het type doelveld waaraan u het bronveld wilt toewijzen.
   * **[!UICONTROL Select identity namespace]**: selecteer deze optie om het bronveld toe te wijzen aan een naamruimte in de lijst.
     ![Platform UI-screenshot met doeltoewijzing voor inhoud.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-contactid.png)

   * Voeg de volgende afbeelding toe tussen uw XDM-profielschema en uw [!DNL Dynamics 365] -instantie: |XDM-profielschema|[!DNL Dynamics 365] Instance| Verplicht| |—|—|—| |`contactid`|`contactid`| Ja |

   * **[!UICONTROL Select custom attributes]**: selecteer deze optie om het bronveld toe te wijzen aan een aangepast kenmerk dat u in het dialoogvenster **[!UICONTROL Attribute name]** veld. Zie [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/developer/entities/contact?view=op-9-1#entity-properties) voor een uitgebreide lijst met ondersteunde kenmerken.
     ![Platform UI-screenshot met doeltoewijzing voor e-mail.](../../assets/catalog/crm/microsoft-dynamics-365/target-mapping-email.png)

     >[!IMPORTANT]
     >
     > * Doelveldnamen moeten aanwezig zijn `lowercase`.
     > * Als u een datum- of tijdstempelbronveld hebt dat is toegewezen aan een [!DNL Dynamics 365] [datum of tijdstempel](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/reference/timestampdatemapping?view=dataverse-latest) doelveld, controleer of de toegewezen waarde niet leeg is. Als de geëxporteerde veldwaarde leeg is, treedt er een *`Bad request reported while pushing events to the destination. Please contact the administrator and try again.`* foutbericht en de gegevens worden niet bijgewerkt. Dit is een [!DNL Dynamics 365] beperking.

   * Afhankelijk van de waarden die u wilt bijwerken, voegt u bijvoorbeeld de volgende toewijzing toe tussen uw XDM-profielschema en uw [!DNL Dynamics 365] -instantie: |XDM-profielschema|[!DNL Dynamics 365] Instance| |—|—| |`person.name.firstName`|`firstname`| |`person.name.lastName`|`lastname`| |`personalEmail.address`|`emailaddress1`|

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
     ![Voorbeeld van schermopname van platformgebruikersinterface met doeltoewijzingen.](../../assets/catalog/crm/microsoft-dynamics-365/mappings.png)

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-audience-export-example}

In de [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) Als u een stap wilt zetten in de activeringsworkflow, moet u het publiek van het platform handmatig toewijzen aan het aangepaste veldkenmerk in [!DNL Dynamics 365].

Om dit te doen, selecteer elk publiek, dan ga het overeenkomstige attribuut van het douanegebied van in [!DNL Dynamics 365] in de **[!UICONTROL Mapping ID]** veld.

>[!IMPORTANT]
>
>De waarde die wordt gebruikt voor de **[!UICONTROL Mapping ID]** moet exact overeenkomen met de naam van het aangepaste veldkenmerk dat is gemaakt in [!DNL Dynamics 365]. Zie [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/dynamics365/customerengagement/on-premises/customize/create-edit-fields?view=op-9-1) als u hulp bij het vinden van uw attributen van het douanegebied nodig hebt.

Hieronder ziet u een voorbeeld:
![Voorbeeld van platformgebruikersinterface met een schermafbeelding waarin het publiek voor het programma wordt geëxporteerd.](../../assets/catalog/crm/microsoft-dynamics-365/schedule-segment-export.png)

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteren **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met bestemmingen te navigeren.
   ![Platform UI het schermschot die Browse Doelen toont.](../../assets/catalog/crm/microsoft-dynamics-365/browse-destinations.png)

1. Selecteer het doel en controleer of de status **[!UICONTROL enabled]**.
   ![Platform UI screenshot die de Looppas van Doelen Dataflow toont.](../../assets/catalog/crm/microsoft-dynamics-365/destination-dataflow-run.png)

1. Schakel over naar de **[!DNL Activation data]** en selecteert u vervolgens de naam van een publiek.
   ![Het het schermschot van het platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/crm/microsoft-dynamics-365/destinations-activation-data.png)

1. Controleer het overzicht van het publiek en zorg ervoor dat het aantal profielen overeenkomt met het aantal profielen dat in het publiek is gemaakt.
   ![Voorbeeld van publiek weergeven van platformgebruikersinterface-screenshot.](../../assets/catalog/crm/microsoft-dynamics-365/segment.png)

1. Aanmelden bij de [!DNL Dynamics 365] website, navigeer vervolgens naar de [!DNL Customers] > [!DNL Contacts] en controleer of de profielen van het publiek zijn toegevoegd. U kunt zien dat elke publieksstatus in [!DNL Dynamics 365] werd bijgewerkt met de overeenkomstige publieksstatus van Platform, gebaseerd op **[!UICONTROL Mapping ID]** waarde die tijdens de [publieksplanning](#schedule-audience-export-example) stap.
   ![De het schermschot van de dynamiek 365 UI die de pagina van Contacten met bijgewerkte publieksstatus toont.](../../assets/catalog/crm/microsoft-dynamics-365/contacts.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het naar bestemming duwen van gebeurtenissen {#unknown-errors}

Wanneer u een gegevensstroom controleert, als u het volgende foutbericht krijgt: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Schermopname van platforminterface met onjuiste aanvraagfout.](../../assets/catalog/crm/microsoft-dynamics-365/error.png)

Om deze fout te bevestigen, verifieer dat **[!UICONTROL Mapping ID]** u hebt opgegeven in [!DNL Dynamics 365] voor uw publiek van het Platform geldig is en binnen bestaat [!DNL Dynamics 365].

## Aanvullende bronnen {#additional-resources}

Aanvullende nuttige informatie uit de [[!DNL Dynamics 365] documentatie](https://docs.microsoft.com/en-us/dynamics365/) is lager dan:
* [Methode IOrganisationService.Update(Entiteit)](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dataverse-sdk-latest)
* [Tabelrijen bijwerken en verwijderen met de web-API](https://docs.microsoft.com/en-us/power-apps/developer/data-platform/webapi/update-delete-entities-using-web-api#basic-update)

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Oktober 2023 | Documentatie bijwerken | Bijgewerkte richtlijnen voor het aangeven van alle namen van doelkenmerken moeten in kleine letters worden weergegeven, in het gedeelte [Afbeeldingsoverwegingen en voorbeeld](#mapping-considerations-example) stap. |
| Augustus 2023 | Bijwerken van functionaliteit en documentatie | Extra ondersteuning voor [!DNL Dynamics 365] aangepaste veldvoorvoegsels voor aangepaste velden die niet zijn gemaakt binnen de standaardoplossing in [!DNL Dynamics 365]. Een nieuw invoerveld, **[!UICONTROL Customization Prefix]**, is toegevoegd aan de [Doelgegevens invullen](#destination-details) stap. (PLATIR-31602). |
| nov. 2022 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++