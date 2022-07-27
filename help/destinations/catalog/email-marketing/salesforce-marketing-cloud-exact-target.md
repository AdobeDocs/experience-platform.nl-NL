---
keywords: e-mail;E-mail;e-mail;e-mailbestemmingen;salesforce;api salesforce marketing cloudbestemming
title: (API) Verbinding met Salesforce-Marketing Cloud
description: Met de Salesforce-Marketing Cloud (voorheen ExactTarget genoemd) kunt u uw accountgegevens exporteren en activeren binnen de Salesforce-Marketing Cloud voor uw zakelijke behoeften.
source-git-commit: ce7b28ce31c652965a6eaad81348e330bd38e9ac
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 1%

---


# [!DNL (API) Salesforce Marketing Cloud] verbinding

## Overzicht {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (voorheen ExactTarget genoemd) is een digitale marketingsuite waarmee u reizen kunt maken en aanpassen voor bezoekers en klanten om hun ervaring aan te passen.

>[!IMPORTANT]
> 
> Let op het verschil tussen deze verbinding en de andere [Verbinding met Salesforce-Marketing Cloud](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/salesforce-marketing-cloud.html?lang=en) bestaat in de sectie E-mailmarketingcatalogus. Met de andere verbinding met de Salesforce-Marketing Cloud kunt u bestanden exporteren naar een opgegeven opslaglocatie, terwijl dit een op API gebaseerde streamingverbinding is.

Dit [!DNL Adobe Experience Platform] [doel](/help/destinations/home.md) gebruikt de [REST-API voor updates van Salesforce](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html), waardoor u contactpersonen kunt toevoegen/contactgegevens voor uw bedrijfsbehoeften kunt bijwerken nadat u deze hebt geactiveerd in een nieuw Salesforce-segment.

De Marketing Cloud van Salesforce gebruikt OAuth 2 met de Referenties van de Cliënt als authentificatiemechanisme om met Salesforce REST API te communiceren. Instructies voor verificatie voor uw Salesforce-exemplaar vindt u hieronder in het gedeelte [Verifiëren voor bestemming](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de bestemming van de Marketing Cloud van Salesforce zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform door deze bestemming kunnen oplossen.

### E-mails verzenden naar contactpersonen voor marketingcampagnes {#use-case-send-emails}

De verkoopafdeling van een platform van de huishuur wil een marketing e-mail aan een gericht klantenpubliek uitzenden. Het marketing team van het platform kan nieuwe contacten toevoegen/bestaande contacten bijwerken *(en hun e-mailadres)* door Adobe Experience Platform, bouwt segmenten van hun eigen off-line gegevens, en verzendt deze segmenten naar de Marketing Cloud van Salesforce, die dan kan worden gebruikt om de marketing campagne e-mail te verzenden.

## Vereisten {#prerequisites}

### Vereisten in Experience Platform {#prerequisites-in-experience-platform}

Voordat u gegevens kunt activeren naar de bestemming van de Salesforce-Marketing Cloud, moet u een [schema](/help/xdm/schema/composition.md), [gegevensset](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), en [segmenten](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) gemaakt in [!DNL Experience Platform].

### Vereisten in Salesforce CRM {#prerequisites-destination}

Neem nota van de volgende eerste vereisten in Salesforce, om gegevens van Platform naar uw rekening van de Marketing Cloud van Salesforce uit te voeren:

#### U moet een Salesforce-account hebben {#prerequisites-account}

Ga naar de Salesforce [proefversie](https://www.salesforce.com/in/form/signup/freetrial-sales/) pagina om een Salesforce-account te registreren en te maken, als u er nog geen hebt.

#### Aangepast veld maken in Salesforce {#prerequisites-custom-field}

Het aangepaste kenmerk van het type maken `Text Area Long` welk Experience Platform zal gebruiken om de segmentstatus binnen de Marketing Cloud van Salesforce bij te werken.

Raadpleeg de documentatie bij de Salesforce-Marketing Cloud op [aangepaste velden maken](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) als u aanvullende instructies nodig hebt.

>[!IMPORTANT]
>
> Zorg ervoor dat u het aangepaste kenmerk maakt onder het kenmerk &#39;Demographics E-mail&#39; in uw Salesforce-Marketing Cloud-account.

>[!NOTE]
>
> * Het aantal toegestane aangepaste kenmerken per object is afhankelijk van uw Salesforce Edition. Raadpleeg de documentatie bij Salesforce voor [aangepaste velden toegestaan per object](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) als u aanvullende instructies nodig hebt.
> * Als u deze grens binnen Salesforce hebt bereikt, zult u de douaneattributen uit Salesforce moeten verwijderen die werden gebruikt om de segmentstatus tegen oudere segmenten binnen Experience Platform op te slaan alvorens een nieuwe mappingId kan worden gebruikt.


Raadpleeg de documentatie bij Adobe Experience Platform voor [Segment Membership Details schema groep](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op segmentstatussen nodig hebt.

#### Referenties van Salesforce verzamelen {#gather-credentials}

Noteer de onderstaande items voordat u de Salesforce-bestemming verifieert.

| Credentials | Beschrijving | Voorbeeld |
| --- | --- | --- |
| <ul><li>Salesforce-voorvoegsel Marketing Cloud</li></ul> | Zie [Domeinvoorvoegsel van Salesforce-Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) voor aanvullende richtsnoeren. | <ul><li>Als uw domein is zoals hieronder, hebt u de benadrukte waarde nodig.<br> <i>`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com</i></li></ul> |
| <ul><li>Client-id</li><li>Clientgeheim</li></ul> | Zie de [Salesforce-documentatie](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) als u aanvullende instructies nodig hebt. | <ul><li>r23kxxxxxx0z05xxxxxx</li><li>ipxxxxxxxxT4xxxxxxxx</li></ul> |

## Ondersteunde identiteiten {#supported-identities}

De Salesforce-Marketing Cloud ondersteunt de activering van identiteiten die in de onderstaande tabel worden beschreven. Meer informatie over [identiteiten](/help/identity-service/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
|---|---|---|
| contactKey | Salesforce-contactsleutel. Zie de [Salesforce-documentatie](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) als u aanvullende instructies nodig hebt. | Verplicht |

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | U exporteert alle leden van een segment samen met de gewenste schemavelden (bijvoorbeeld: e-mailadres, telefoonnummer, achternaam), zoals gekozen in het scherm met de kenmerken van het geselecteerde profiel [doelactiveringsworkflow](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md). In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

![Catalogus](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/catalog.png)

### Verifiëren voor bestemming {#authenticate}

Als u zich wilt verifiëren bij de bestemming, vult u de vereiste velden in en selecteert u **[!UICONTROL Connect to destination]**.

![Voorbeeldscreenshot waarin wordt getoond hoe u op Salesforce-Marketing Cloud kunt verifiëren](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

* **[!UICONTROL Subdomain]**: Het domeinvoorvoegsel van uw Salesforce-Marketing Cloud. Als uw domein bijvoorbeeld *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com* hebt u de gemarkeerde waarde nodig.
* **[!UICONTROL Client ID]**: Uw Salesforce-client-id.
* **[!UICONTROL Client Secret]**: Uw Salesforce-clientgeheim.

Als de verstrekte gegevens geldig zijn, geeft de interface een **Verbonden** Als u een groene markering hebt, kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.

![Voorbeeldscreenshot waarin wordt getoond hoe u de details voor de Salesforce-Marketing Cloud invult](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u deze bestemming in de toekomst zult erkennen.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Customer name]**: Dit kan elke waarde zijn, maar een waarde is verplicht. Anders mislukt de doelactivering.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over waarschuwingen raadpleegt u de handleiding over [het abonneren aan bestemmingen alarm gebruikend UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Segmenten naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Profielen en segmenten activeren voor streaming segmentexportdoelen](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

### Afbeeldingsoverwegingen en voorbeeld {#mapping-considerations-example}

Om uw publieksgegevens van Adobe Experience Platform naar de bestemming van de Marketing Cloud van Salesforce correct te verzenden, moet u door de stap van de gebiedstoewijzing gaan. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Platform-account en de bijbehorende equivalenten van de doelbestemming. Voer de volgende stappen uit om uw XDM-velden correct toe te wijzen aan de Salesforce-doelvelden van de Marketing Cloud:

De lijst met kenmerktoewijzingen die kan worden ingesteld voor de [Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) wordt hieronder gegeven. Het doel gebruikt de [REST-API voor kenmerkgedefinieerde definities in Salesforce-zoekopdracht](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) om de kenmerken op te halen die in Salesforce zijn gedefinieerd voor uw contactpersonen en die specifiek zijn voor uw account.

>[!IMPORTANT]
> 
> Hoewel de namen van uw kenmerken overeenkomen met uw Salesforce-account, worden de toewijzingen voor `contactKey` en `personalEmail.address` zijn verplicht.

1. Klik in de stap Toewijzing op **[!UICONTROL Add new mapping]**, ziet u een nieuwe toewijzingsrij op het scherm.
   ![Nieuwe toewijzing toevoegen](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)

1. Kies in het venster Bronveld selecteren de optie **[!UICONTROL Select attributes]** en voeg de gewenste toewijzingen toe.
   ![Brontoewijzing](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/source-mapping.png)

1. Selecteer het doelveld in het venster Selecteer het doelveld en kies de optie **[!UICONTROL Select identity namespace]** en voeg de gewenste toewijzingen toe.
   ![Doeltoewijzing](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping.png)

1. Als u aangepaste kenmerken wilt toewijzen, selecteert u het venster Doelveld, selecteert u het doelveld en kiest u de optie **[!UICONTROL Select attributes]** > **E-maildemografie** categorie. Geef vervolgens de gewenste naam voor het doelkenmerk op en voeg de gewenste toewijzingen toe.
   ![Doeltoewijzing](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/target-mapping-custom.png)

1. U kunt bijvoorbeeld de volgende toewijzing toevoegen tussen uw XDM-profielschema en uw [!DNL Salesforce Marketing Cloud] instantie:

   |  | XDM-profielschema | [!DNL Salesforce Marketing Cloud] Instantie | Verplicht |
   |---|---|---|---|
   | Attributen | <ul><li>person.name.firstName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>Demografische gegevens per e-mail.voornaam</code></li><li>E-mailadressen.E-mailadres</code></li></ul> | <ul><li>-</li><li>Ja</code></li></ul> |
   | Identiteiten | <ul><li>contactKey</code></li></ul> | <ul><li>salesforceContactKey</code></li></ul> | Ja |

1. Hieronder ziet u een voorbeeld waarin deze toewijzingen worden gebruikt:
   ![Doeltoewijzing LastName](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

### De segmentuitvoer van het programma en voorbeeld {#schedule-segment-export-example}

Bij het uitvoeren van de [Segmentexport plannen](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) stap u moet de segmenten van het Platform aan het douanekenmerk in Salesforce manueel in kaart brengen.

Om dit te doen, selecteer elk segment, dan ga het overeenkomstige douanekenmerk van Salesforce in **[!UICONTROL Mapping ID]** veld.

>[!IMPORTANT]
>
> De waarde die voor de toewijzingsid wordt gebruikt, moet exact overeenkomen met de naam van het aangepaste kenmerk dat in Salesforce is gemaakt onder de kenmerkset &quot;Demografie e-mail&quot;.

Hieronder ziet u een voorbeeld:
![Segmentexport plannen](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

1. Selecteren **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** om naar de lijst met bestemmingen te navigeren.

   ![Door doelen bladeren](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Selecteer het doel en controleer of de status **[!UICONTROL enabled]**.

   ![Doelen DataFlow uitvoeren](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Naar de **[!DNL Activation data]** selecteert u vervolgens een segmentnaam.

   ![Gegevens doelactivering](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Controleer de samenvatting van het segment en zorg ervoor dat de telling van profielen aan de telling beantwoordt die binnen het segment wordt gecreeerd.

   ![Segment](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Meld u aan bij de website van Salesforce Marketing Cloud. Navigeer vervolgens naar de **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** en controleer of de profielen van het segment zijn toegevoegd.

   ![Salesforce-contactpersonen](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Als u wilt controleren of profielen zijn bijgewerkt, navigeert u naar de **[!DNL Email]** controleren of de kenmerkwaarden voor het profiel van het segment zijn bijgewerkt.

   ![Salesforce-contactpersonen](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [Overzicht van gegevensbeheer](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

### Onbekende fouten aangetroffen tijdens het verplaatsen van gebeurtenissen naar de Salesforce-Marketing Cloud {#unknown-errors}

Als u een gegevensstroomuitvoering controleert en het foutbericht hieronder ziet, controleert u of de toewijzingsid die u hebt opgegeven [!DNL Salesforce CRM] voor uw segment van het Platform is geldig en bestaat binnen [!DNL Salesforce CRM].
![Fout](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

## Aanvullende bronnen {#additional-resources}

* [Salesforce Developer Portal](https://developer.salesforce.com/)

### Limieten {#limits}

* Salesforce stelt bepaalde [tarieflimieten](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
* Zie de [tarieflimieten](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) pagina om eventuele fouten te controleren.
* Zie de [Prijsstelling Salesforce Marketing Cloud Engagement](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) pagina naar *Download de vergelijkingstabel van de Volledige Uitgave* als een pdf waarin de limieten worden uiteengezet die in uw plan worden opgelegd.
* De [API-overzicht](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) pagina details extra limieten.
* Er is een KB-item beschikbaar waarin deze details worden gesorteerd [hier](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits#:~:text=Day%2FHour%2FMinute%20Limit&amp;text=We%20recommend%20a%20limit%20of,per%20minute%20for%20SOAP%20calls.&amp;text=As%20has%20was%20added%20in,interactie%20with%20the%20REST%2DAPI).

