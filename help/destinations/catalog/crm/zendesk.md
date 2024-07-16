---
title: Zendesk-verbinding
description: Met de Zendesk-bestemming kunt u uw accountgegevens exporteren en activeren in Zendesk voor uw zakelijke behoeften.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: e7fcbbf4-5d6c-4abb-96cb-ea5b67a88711
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# [!DNL Zendesk] verbinding

[[!DNL Zendesk] ](https://www.zendesk.com) is een hulpmiddel van de klantendienst en verkoop.

Dit [!DNL Adobe Experience Platform] [ bestemmings ](/help/destinations/home.md) hefboomwerkingen [[!DNL Zendesk]  Contactpersonen API ](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), om **identiteiten** binnen een publiek tot stand te brengen en bij te werken zoals contacten binnen [!DNL Zendesk].

[!DNL Zendesk] gebruikt tokens aan toonder als verificatiemechanisme om te communiceren met de [!DNL Zendesk] Contactpersonen-API. De instructies om aan uw [!DNL Zendesk] instantie voor authentiek te verklaren zijn verder hieronder, in [ voor authentiek verklaren aan bestemmings ](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

De klantendienst van een multichannel B2C platform wil een naadloze gepersonaliseerde ervaring voor zijn klanten verzekeren. De afdeling kan een publiek maken op basis van hun eigen offline gegevens om nieuwe gebruikersprofielen te maken of bestaande profielgegevens bij te werken op basis van verschillende interacties (bijvoorbeeld aankopen, retourneren, enz.) en stuur deze soorten publiek van Adobe Experience Platform naar [!DNL Zendesk] . Als u de bijgewerkte informatie in [!DNL Zendesk] opgeeft, zorgt u ervoor dat de medewerker van de klantenservice de recente informatie van de klant direct beschikbaar heeft, zodat sneller kan worden gereageerd en de oplossing sneller verloopt.

## Vereisten {#prerequisites}

### Voorwaarden voor Experience Platforms {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL Zendesk] bestemming te activeren, moet u a [ schema ](/help/xdm/schema/composition.md), a [ dataset ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) hebben, en [ segmenten ](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) die in [!DNL Experience Platform] worden gecreeerd.

Verwijs naar de documentatie van het Experience Platform voor [ het schemagroep van de Details van het Lidmaatschap van de Publiek ](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatus nodig hebt.

### [!DNL Zendesk] voorwaarden {#prerequisites-destination}

Als u gegevens wilt exporteren van Platform naar uw [!DNL Zendesk] -account, hebt u een [!DNL Zendesk] -account nodig.

#### [!DNL Zendesk] gebruikersgegevens verzamelen {#gather-credentials}

Noteer de onderstaande items voordat u de verificatie uitvoert naar het doel van [!DNL Zendesk] :

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Bearer token` | Het toegangstoken dat u in uw [!DNL Zendesk] account hebt gegenereerd. <br> volg de documentatie aan [ produceren a  [!DNL Zendesk]  toegangstoken ](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) als u geen hebt. | `a0b1c2d3e4...v20w21x22y23z` |

## Guardrails {#guardrails}

De [ Prijsbepaling en van het Tarief Beperkingen ](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) pagina details de [!DNL Zendesk] API grenzen verbonden aan uw rekening. U moet ervoor zorgen dat uw gegevens en lading binnen deze beperkingen zijn.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Zendesk] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [ identiteiten ](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Voorbeeld | Beschrijving | Verplicht |
|---|---|---|---|
| `email` | `test@test.com` | E-mailadres van de contactpersoon. | Ja |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Elke segmentstatus in [!DNL Zendesk] wordt bijgewerkt met de overeenkomstige publieksstatus van Platform, die op de **[!UICONTROL Mapping ID]** waarde wordt gebaseerd die tijdens de [ publiek wordt verstrekt die ](#schedule-segment-export-example) stap plant.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [ leerprogramma van de bestemmingsconfiguratie ](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Kies in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** Zoeken naar [!DNL Zendesk] . U kunt de locatie ook in de categorie **[!UICONTROL CRM]** vinden.

### Verifiëren voor bestemming {#authenticate}

Vul de vereiste velden hieronder in. Verwijs naar de [ Gather  [!DNL Zendesk]  geloofsbrieven ](#gather-credentials) sectie voor om het even welke begeleiding.
* **[!UICONTROL Bearer Token]**: Het toegangstoken dat u in uw [!DNL Zendesk] -account hebt gegenereerd.

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.
{het schermschot van het platform UI die tonen hoe te voor authentiek te verklaren.](../../assets/catalog/crm/zendesk/authenticate-destination.png)![

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
{het schermschot van het platform UI die de bestemmingsdetails toont.](../../assets/catalog/crm/zendesk/destination-details.png)![

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

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

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Zendesk] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

Kenmerken die in de **[!UICONTROL Target field]** worden opgegeven, moeten een naam krijgen die exact overeenkomt met de beschrijving in de tabel met kenmerktoewijzingen, aangezien deze kenmerken de aanvraaginstantie vormen.

Kenmerken die in **[!UICONTROL Source field]** worden opgegeven, volgen een dergelijke beperking niet. U kunt deze toewijzen op basis van uw behoefte, maar als de gegevensindeling niet correct is wanneer u naar [!DNL Zendesk] wordt geduwd, resulteert dit in een fout.

Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL Zendesk] -doelvelden:

1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de categorie **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. Kies in het venster **[!UICONTROL Select target field]** de categorie **[!UICONTROL Select identity namespace]** en selecteer een doelidentiteit of kies de categorie **[!UICONTROL Select attributes]** en selecteer een van de ondersteunde schemakenmerken.
   * Herhaal deze stappen om de volgende verplichte toewijzingen toe te voegen, kunt u ook andere kenmerken toevoegen die u wilt bijwerken tussen het XDM-profielschema en uw [!DNL Zendesk] -instantie:
|Source-veld|Doelveld| Verplicht|
|—|—|—|
|`xdm: person.name.lastName`|`xdm: last_name`| Ja |
|`IdentityMap: Email`|`Identity: email`| Ja |
|`xdm: person.name.firstName`|`xdm: first_name`| |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
     ![ het schermschot van het Platform UI met attributenafbeeldingen.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>De doeltoewijzingen `Attribute: last_name` en `Identity: email` zijn verplicht voor dit doel. Als deze toewijzingen ontbreken, worden andere toewijzingen genegeerd en niet verzonden naar [!DNL Zendesk] .

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-segment-export-example}

In de stap [[!UICONTROL Schedule audience export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) van de activeringsworkflow moet u het publiek Platform handmatig toewijzen aan het aangepaste veldkenmerk in [!DNL Zendesk] .

Hiervoor selecteert u elk segment en voert u in [!DNL Zendesk] in het veld **[!UICONTROL Mapping ID]** het bijbehorende aangepaste veldkenmerk in.

Hieronder ziet u een voorbeeld:
{het screenshot voorbeeld van het Platform UI die het publiek van het Programma tonen uitvoer.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)![

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteer **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en navigeer naar de lijst met doelen.
1. Selecteer vervolgens het doel en schakel over naar het tabblad **[!UICONTROL Activation data]** en selecteer een publieksnaam.
   ![ het schermschot van het Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Controleer het publieksoverzicht en zorg ervoor dat de telling van profielen aan de telling binnen het segment beantwoordt.
   ![ het schermschot van het Platform UI die Segment toont.](../../assets/catalog/crm/zendesk/segment.png)

1. Meld u aan bij de [!DNL Zendesk] -website en navigeer naar de **[!UICONTROL Contacts]** -pagina om te controleren of de profielen van het publiek zijn toegevoegd. Deze lijst kan worden gevormd om kolommen voor de extra gebieden te tonen die met publiek* worden gecreeerd* [!UICONTROL Mapping ID]** en publieksstatus.
   {het schermschot van 0} Zendesk UI die de pagina van Contacten met de extra gebieden toont die met de publieksnaam worden gecreeerd.](../../assets/catalog/crm/zendesk/contacts.png)![

1. U kunt ook omlaag naar een afzonderlijke **[!UICONTROL Person]** -pagina gaan en de **[!UICONTROL Additional fields]** -sectie met de publieksnaam en de publieksstatus controleren.
   {het schermschot van 0} Zendesk UI die de pagina van de Persoon met de extra gebiedssectie toont die de publieksnaam en de publieksstatus toont.](../../assets/catalog/crm/zendesk/contact.png)![

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ overzicht van het Beleid van Gegevens ](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Hieronder vindt u aanvullende nuttige informatie uit de documentatie van [!DNL Zendesk] :
* [ Making van uw eerste vraag ](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [ de Gebieden van de Douane ](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| April 2023 | Documentatie bijwerken | <ul><li>Wij hebben de [ gebruik-gevallen ](#use-cases) sectie met een duidelijker voorbeeld bijgewerkt van wanneer de klanten van het gebruiken van deze bestemming zouden profiteren.</li> <li>Wij hebben de [ afbeelding ](#mapping-considerations-example) sectie bijgewerkt om op de correcte vereiste afbeeldingen te wijzen. De doeltoewijzingen `Attribute: last_name` en `Identity: email` zijn verplicht voor dit doel. Als deze toewijzingen ontbreken, worden andere toewijzingen genegeerd en niet verzonden naar [!DNL Zendesk] .</li> <li>Wij hebben de [ afbeelding ](#mapping-considerations-example) sectie met duidelijke voorbeelden van zowel verplichte als facultatieve afbeeldingen bijgewerkt.</li></ul> |
| Maart 2023 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++
