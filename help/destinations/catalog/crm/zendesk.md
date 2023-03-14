---
title: Zendesk-verbinding
description: Met de Zendesk-bestemming kunt u uw accountgegevens exporteren en activeren in Zendesk voor uw zakelijke behoeften.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 0%

---

# [!DNL Zendesk] verbinding

[[!DNL Zendesk]](https://www.zendesk.com) is een oplossing van de klantendienst en verkoophulpmiddel.

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [[!DNL Zendesk] Contactpersonen-API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/), om identiteiten binnen een segment als contacten binnen te creëren en bij te werken [!DNL Zendesk].

[!DNL Zendesk] gebruikt dragertokens als authentificatiemechanisme om met het [!DNL Zendesk] Contactpersonen-API. Instructies voor verificatie aan uw [!DNL Zendesk] de instantie is verder onderaan, in de [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Als markeerteken kunt u uw gebruikers een persoonlijke ervaring bieden op basis van kenmerken uit hun Adobe Experience Platform-profielen. U kunt segmenten maken van uw offlinegegevens en deze segmenten verzenden naar [!DNL Zendesk], om in de feeds van de gebruikers weer te geven zodra de segmenten en profielen in Adobe Experience Platform zijn bijgewerkt.

## Vereisten {#prerequisites}

### Voorwaarden voor Experience Platforms {#prerequisites-in-experience-platform}

Voordat u gegevens activeert naar de [!DNL Zendesk] doel, u moet een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) gemaakt in [!DNL Experience Platform].

Raadpleeg de documentatie bij het Experience Platform voor [Segment Membership Details schema groep](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op segmentstatussen nodig hebt.

### [!DNL Zendesk] voorwaarden {#prerequisites-destination}

Als u gegevens van Platform wilt exporteren naar uw [!DNL Zendesk] account die u nodig hebt [!DNL Zendesk] account.

#### Gather [!DNL Zendesk] geloofsbrieven {#gather-credentials}

Noteer de onderstaande items voordat u deze verifieert voor de [!DNL Zendesk] bestemming:

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `Bearer token` | Het toegangstoken u in uw hebt geproduceerd [!DNL Zendesk] account. <br> Volg de documentatie om [een [!DNL Zendesk] toegangstoken](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) als u er geen hebt. | `a0b1c2d3e4...v20w21x22y23z` |

## Guardrails {#guardrails}

De [Prijs- en snelheidsbeperkingen](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) pagina bevat de details van [!DNL Zendesk] API-limieten die aan uw account zijn gekoppeld. U moet ervoor zorgen dat uw gegevens en lading binnen deze beperkingen zijn.

## Ondersteunde identiteiten {#supported-identities}

[!DNL Zendesk] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Voorbeeld | Beschrijving | Verplicht |
|---|---|---|---|
| `email` | `test@test.com` | E-mailadres van de contactpersoon. | Ja |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een segment samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)*, op basis van uw veldtoewijzing.</li><li> Elke segmentstatus in [!DNL Zendesk] wordt bijgewerkt met de corresponderende segmentstatus van het Platform, gebaseerd op de **[!UICONTROL Mapping ID]** waarde die tijdens de [segment plannen](#schedule-segment-export-example) stap.</li></ul> |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Within **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** zoeken naar [!DNL Zendesk]. U kunt de locatie ook onder de **[!UICONTROL CRM]** categorie.

### Verifiëren voor bestemming {#authenticate}

Vul de vereiste velden hieronder in. Zie de [Gather [!DNL Zendesk] geloofsbrieven](#gather-credentials) voor eventuele richtsnoeren.
* **[!UICONTROL Bearer Token]**: Het toegangstoken dat u in uw [!DNL Zendesk] account.

Om voor authentiek te verklaren aan de bestemming, selecteer **[!UICONTROL Connect to destination]**.
![Het schermschot van het Platform UI die toont hoe te voor authentiek te verklaren.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

Als de verstrekte gegevens geldig zijn, geeft de interface een **[!UICONTROL Connected]** status met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![Het schermschot van het Platform UI die de bestemmingsdetails toont.](../../assets/catalog/crm/zendesk/destination-details.png)

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

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL Zendesk] doel, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming.

Kenmerken die zijn opgegeven in het dialoogvenster **[!UICONTROL Target field]** zou precies moeten worden genoemd zoals die in de lijst van attributenafbeeldingen wordt beschreven aangezien deze attributen de verzoeklichaam zullen vormen.

Kenmerken die zijn opgegeven in het dialoogvenster **[!UICONTROL Source field]** zich niet aan een dergelijke beperking houden. U kunt deze toewijzen op basis van uw behoefte, maar als de gegevensindeling niet correct is wanneer u naar [!DNL Zendesk] resulteert in een fout.

Uw XDM-velden op de juiste wijze toewijzen aan de [!DNL Zendesk] doelvelden, voer de volgende stappen uit:

1. In de **[!UICONTROL Mapping]** stap, selecteren **[!UICONTROL Add new mapping]**. Er verschijnt een nieuwe toewijzingsrij op het scherm.
1. In de **[!UICONTROL Select source field]** venster, kiest u de **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk of kies de **[!UICONTROL Select identity namespace]** en selecteer een identiteit.
1. In de **[!UICONTROL Select target field]** venster, kiest u de **[!UICONTROL Select identity namespace]** en selecteer een identiteit of kies **[!UICONTROL Select custom attributes]** en selecteer een kenmerk.
   * Herhaal deze stappen om de volgende toewijzingen tussen uw XDM-profielschema en uw [!DNL Zendesk] instantie: |Bronveld|Doelveld| Verplicht| |—|—|—| |`xdm: person.name.lastName`|`Attribute: last_name` <br>of `Attribute: name`| Ja | |`IdentityMap: Email`|`Identity: email`| Ja |

   * Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
      ![Voorbeeld van schermopname met gebruikersinterface van Platform met kenmerktoewijzingen.](../../assets/catalog/crm/zendesk/mappings.png)

      >[!IMPORTANT]
      >
      >Zowel zijn de afbeeldingen van het doelveld verplicht en vereist voor [!DNL Zendesk] om te werken.
      >
      >De toewijzing voor *Achternaam* of *Naam* anders is de [!DNL Zendesk] API reageert niet met een fout en doorgegeven kenmerkwaarden worden genegeerd.

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

### De segmentuitvoer van het programma en voorbeeld {#schedule-segment-export-example}

In de [[!UICONTROL Schedule segment export]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) stap van de activeringsworkflow, moet u de segmenten van het Platform handmatig toewijzen aan het aangepaste veldkenmerk in [!DNL Zendesk].

Om dit te doen, selecteer elk segment, dan ga het overeenkomstige attribuut van het douaneveld van in [!DNL Zendesk] in de **[!UICONTROL Mapping ID]** veld.

Hieronder ziet u een voorbeeld:
![Het het schermschot van het Platform UI die de segmentuitvoer van het Programma toont.](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteren **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en navigeer naar de lijst met bestemmingen.
1. Selecteer vervolgens de bestemming en schakel over naar de **[!UICONTROL Activation data]** selecteert u vervolgens een segmentnaam.
   ![Het het schermschot van het Platform UI die de Gegevens van de Activering van Doelen toont.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. Controleer de samenvatting van het segment en zorg ervoor dat de telling van profielen aan de telling binnen het segment beantwoordt.
   ![Platform UI-screenshot voorbeeld met segment.](../../assets/catalog/crm/zendesk/segment.png)

1. Aanmelden bij de [!DNL Zendesk] website, navigeer vervolgens naar de **[!UICONTROL Contacts]** pagina om te controleren of de profielen van het segment zijn toegevoegd. Deze lijst kan worden gevormd om kolommen voor de extra gebieden te tonen die met het segment worden gecreeerd **[!UICONTROL Mapping ID]** en segmentstatussen.
   ![Het schermschot van Zendesk UI die de pagina van Contacten met de extra gebieden toont die met de segmentnaam worden gecreeerd.](../../assets/catalog/crm/zendesk/contacts.png)

1. U kunt ook naar beneden boren in een individu **[!UICONTROL Person]** pagina en controleer de **[!UICONTROL Additional fields]** sectie waarin de segmentnaam en de segmentstatus worden weergegeven.
   ![Het schermschot van Zendesk UI die de Person pagina met de extra gebiedssectie toont die de segmentnaam en segmentstatus toont.](../../assets/catalog/crm/zendesk/contact.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Aanvullende bronnen {#additional-resources}

Aanvullende nuttige informatie uit de [!DNL Zendesk] de documentatie is hieronder:
* [Je eerste telefoontje maken](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [Aangepaste velden](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)