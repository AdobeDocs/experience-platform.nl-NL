---
title: HubSpot-verbinding
description: De bestemming HubSpot staat u toe om contactverslagen in uw rekening te beheren HubSpot.
last-substantial-update: 2023-09-28T00:00:00Z
exl-id: e2114bde-b7c3-43da-9f3a-919322000ef4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 0%

---

# [!DNL HubSpot] verbinding

[[!DNL HubSpot] &#x200B;](https://www.hubspot.com) is een platform van CRM met alle software, integratie, en middelen u marketing, verkoop, inhoudsbeheer, en de klantendienst moet verbinden. Het staat u toe om uw gegevens, teams, en klanten op één platform van CRM te verbinden.

Dit [!DNL Adobe Experience Platform] [&#x200B; bestemmings &#x200B;](/help/destinations/home.md) hefboomwerkingen [[!DNL HubSpot]  Contactpersonen API &#x200B;](https://developers.hubspot.com/docs/api/crm/contacts), om contacten binnen [!DNL HubSpot] van een bestaand publiek van Experience Platform na activering bij te werken.

De instructies om aan uw [!DNL HubSpot] instantie voor authentiek te verklaren zijn verder hieronder, in [&#x200B; voor authentiek verklaren aan bestemmings &#x200B;](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL HubSpot] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

[!DNL HubSpot] slaat informatie over de individuen op die met uw zaken in wisselwerking staan. Uw team gebruikt de contactpersonen in [!DNL HubSpot] om het Experience Platform-publiek op te bouwen. Nadat deze doelgroepen naar [!DNL HubSpot] zijn verzonden, worden hun gegevens bijgewerkt en wordt aan elke contactpersoon een eigenschap toegewezen met de waarde ervan als de publieksnaam die aangeeft tot welk publiek de contactpersoon behoort.

## Vereisten {#prerequisites}

Raadpleeg de onderstaande secties voor alle voorwaarden die u in Experience Platform en [!DNL HubSpot] moet instellen en voor informatie die u moet verzamelen voordat u met het [!DNL HubSpot] -doel kunt werken.

### Experience Platform-voorwaarden {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL HubSpot] bestemming te activeren, moet u a [&#x200B; schema &#x200B;](/help/xdm/schema/composition.md), a [&#x200B; dataset &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=nl-NL) hebben, en [&#x200B; publiek &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=nl-NL) dat in [!DNL Experience Platform] wordt gecreeerd.

Verwijs naar de documentatie van Experience Platform voor [&#x200B; het schemagroep van de Details van het Lidmaatschap van de Publiek &#x200B;](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatus nodig hebt.

### Vereisten voor het doel [!DNL HubSpot] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Experience Platform naar uw [!DNL HubSpot] -account te exporteren:

#### U moet een [!DNL HubSpot] -account hebben {#prerequisites-account}

Als u gegevens van Experience Platform naar uw [!DNL Hubspot] -account wilt exporteren, hebt u een [!DNL HubSpot] -account nodig. Als u niet reeds hebt, bezoek de [&#x200B; Opstelling uw HubSpot rekening &#x200B;](https://knowledge.hubspot.com/get-started/set-up-your-account) pagina en volg de begeleiding om uw rekening te registreren en te creëren.

#### Het toegangstoken voor de [!DNL HubSpot] persoonlijke app verzamelen {#gather-credentials}

U hebt uw [!DNL HubSpot] `Access token` nodig om de [!DNL HubSpot] -bestemming toe te staan API-aanroepen uit te voeren via uw [!DNL HubSpot] persoonlijke app in uw [!DNL HubSpot] -account. `Access token` dient als `Bearer token` wanneer u [&#x200B; de bestemming &#x200B;](#authenticate) voor authentiek verklaart.

Als u geen privé app hebt, volg de documentatie aan [&#x200B; creeer privé app in  [!DNL HubSpot] &#x200B;](https://developers.hubspot.com/docs/api/private-apps).

>[!IMPORTANT]
>
> Aan de persoonlijke app moeten de onderstaande bereiken worden toegewezen:
> `crm.objects.contacts.write`, `crm.objects.contacts.read`
> `crm.schemas.contacts.write`, `crm.schemas.contacts.read`

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Bearer token` | De `Access token` van uw [!DNL HubSpot] persoonlijke app. <br> om uw [!DNL HubSpot] te verkrijgen `Access token` volg de [!DNL HubSpot] documentatie om [&#x200B; API vraag met het toegangstoken van uw app &#x200B;](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token) te maken. | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## Guardrails {#guardrails}

[!DNL HubSpot] privé apps zijn onderworpen aan [&#x200B; Grenswaarden van het Tarief &#x200B;](https://developers.hubspot.com/docs/api/usage-details). Het aantal aanroepen dat uw persoonlijke app kan uitvoeren, is gebaseerd op uw accountabonnement van [!DNL HubSpot] en of u de API-invoegtoepassing hebt aangeschaft. Bovendien verwijs ook naar [&#x200B; Andere Beperkingen &#x200B;](https://developers.hubspot.com/docs/api/usage-details#other-limits).

## Ondersteunde identiteiten {#supported-identities}

[!DNL HubSpot] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Voorbeeld | Beschrijving | Overwegingen |
|---|---|---|---|
| `email` | `test@test.com` | E-mailadres van de contactpersoon. | Verplicht |

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Deze bestemming steunt de activering van alle die publiek door de Dienst van de Segmentatie van Experience Platform [&#x200B; wordt geproduceerd &#x200B;](../../../segmentation/home.md).

Deze bestemming ondersteunt ook de activering van het publiek dat in de onderstaande tabel wordt beschreven.

| Type publiek | Beschrijving |
|---------|----------|
| Aangepaste uploads | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Bovendien wordt in [!DNL HubSpot] een nieuwe eigenschap gemaakt met de naam van het publiek en heeft de waarde ervan de overeenkomende status van het publiek in Experience Platform voor elk geselecteerd publiek.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Kies in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** Zoeken naar [!DNL HubSpot] . U kunt de locatie ook in de categorie **[!UICONTROL CRM]** vinden.

### Verifiëren voor bestemming {#authenticate}

Vul de vereiste velden hieronder in. Verwijs naar [&#x200B; verzamelen de  [!DNL HubSpot]  privé app toegangstoken &#x200B;](#gather-credentials) sectie voor om het even welke begeleiding.
* **[!UICONTROL Bearer token]**: het toegangstoken voor uw [!DNL HubSpot] persoonlijke app.

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.
{het schermschot van 0} Experience Platform UI die toont hoe te voor authentiek te verklaren.![&#128279;](../../assets/catalog/crm/hubspot/authenticate-destination.png)

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
{het schermschot van 0} Experience Platform UI die de bestemmingsdetails toont.![&#128279;](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
>
>Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL HubSpot] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming.

Voer de onderstaande stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL HubSpot] -doelvelden:

#### De identiteit van `Email` toewijzen

De identiteit van `Email` is een verplichte toewijzing voor dit doel. Voer de onderstaande stappen uit om deze toe te wijzen:
1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . U ziet nu een nieuwe toewijzingsrij op het scherm.
   {het schermschot van 0} Experience Platform UI met toegevoegde nieuwe benadrukte toewijzingsknoop.![&#128279;](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Kies in het **[!UICONTROL Select source field]** -venster de **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
   {het schermschot van 0} Experience Platform UI die e-mail als bronattribuut selecteert om als identiteit in kaart te brengen.![&#128279;](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. Kies in het **[!UICONTROL Select target field]** -venster de **[!UICONTROL Select attributes]** en selecteer `email` .
   {het schermschot van 0} Experience Platform UI die e-mail als doelattribuut selecteert om als identiteit in kaart te brengen.![&#128279;](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| Source-veld | Doelveld | Verplicht |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | Ja |

Hieronder ziet u een voorbeeld met de identiteitstoewijzing:
![&#x200B; het schermschot van Experience Platform UI met e-mailidentiteitstoewijzing.](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### Het in kaart brengen **facultatieve** attributen

Als u andere kenmerken wilt toevoegen die u tussen het XDM-profielschema en uw [!DNL HubSpot] -account wilt bijwerken, herhaalt u de onderstaande stappen:
1. Selecteer **[!UICONTROL Add new mapping]** in de stap **[!UICONTROL Mapping]** . U ziet nu een nieuwe toewijzingsrij op het scherm.
   {het schermschot van 0} Experience Platform UI met toegevoegde nieuwe benadrukte toewijzingsknoop.![&#128279;](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk.
   ![&#x200B; het schermschot van Experience Platform UI die Voornaam als bronattribuut selecteert.](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. Kies in het venster **[!UICONTROL Select target field]** de categorie **[!UICONTROL Select attributes]** en selecteer een van de kenmerken die automatisch worden ingevuld in uw [!DNL HubSpot] -account. De bestemming gebruikt [[!DNL HubSpot]  Eigenschappen &#x200B;](https://developers.hubspot.com/docs/api/crm/properties) API om deze informatie terug te winnen. Zowel [!DNL HubSpot] [&#x200B; standaardeigenschappen &#x200B;](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties) als om het even welke douaneeigenschappen worden teruggewonnen voor selectie als doelgebieden.
   {het schermschot van 0} Experience Platform UI die Voornaam als doelattribuut selecteert.![&#128279;](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

Hieronder worden enkele beschikbare toewijzingen weergegeven tussen uw XDM-profielschema en [!DNL Hubspot] :

| Source-veld | Doelveld |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

Hieronder ziet u een voorbeeld waarin deze kenmerktoewijzingen worden gebruikt:
![&#x200B; het schermschot van Experience Platform UI met attributenafbeeldingen.](../../assets/catalog/crm/hubspot/mapping-attributes.png)

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Meld u aan bij de [!DNL HubSpot] -website en navigeer naar de **[!UICONTROL Contacts]** -pagina om de status van het publiek te controleren. Deze lijst kan worden gevormd om kolommen voor de douaneeigenschappen te tonen die met de publieksnaam met hun waarde worden gecreeerd de publieksstatus zijn.
   ![&#x200B; het schermschot van HubSpot UI die de pagina van Contacten met kolomkopballen toont die de publieksnaam en de statistieken van het celpubliek tonen &#x200B;](../../assets/catalog/crm/hubspot/contacts.png)

1. U kunt ook omlaag naar een afzonderlijke **[!UICONTROL Person]** -pagina gaan en naar de eigenschappen navigeren die de publieksnaam en de publieksstatus weergeven.
   ![&#x200B; HubSpot UI het schermschot die de pagina van het Contact met douaneeigenschappen toont die de publieksnaam en de publieksstatussen tonen.](../../assets/catalog/crm/hubspot/contact.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Hieronder vindt u aanvullende nuttige informatie uit de documentatie van [!DNL HubSpot] :
* [&#x200B; methodes van de Authentificatie op HubSpot &#x200B;](https://developers.hubspot.com/docs/api/intro-to-auth)
* [!DNL HubSpot] API verwijzingen voor de [&#x200B; Contacten &#x200B;](https://developers.hubspot.com/docs/api/crm/contacts) en [&#x200B; Eigenschappen &#x200B;](https://developers.hubspot.com/docs/api/crm/properties) APIs.

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| September 2023 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++
