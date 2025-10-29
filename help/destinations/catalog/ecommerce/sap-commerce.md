---
title: SAP Commerce-verbinding
description: Gebruik de SAP Commerce-doelconnector om de klantgegevens in uw SAP-account bij te werken.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 3bd1a2a7-fb56-472d-b9bd-603b94a8937e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2175'
ht-degree: 0%

---

# [!DNL SAP Commerce]-verbinding

[!DNL SAP Commerce], vroeger gekend als [[!DNL Hybris] &#x200B;](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), is een op wolk-gebaseerde e-commerceoplossing voor B2B en B2C ondernemingen en beschikbaar als deel van de portefeuille van de Ervaring van de Klant van SAP. [[!DNL SAP]  het Factureren van het Abonnement 1&rbrace; is een product onder de portefeuille en laat volledig beheer van de abonnementslevenscyclus met vereenvoudigde het verkopen en betaling ervaringen door gestandaardiseerde integratie toe.](https://www.sap.com/products/financial-management/subscription-billing.html)

Dit [!DNL Adobe Experience Platform] [&#x200B; bestemming &#x200B;](/help/destinations/home.md) gebruikt [[!DNL SAP Subscription Billing]  klantenbeheer API &#x200B;](https://api.sap.com/api/BusinessPartner_APIs/path/PUT_customers-customerNumber), om uw klantendetails binnen [!DNL SAP Commerce] van een bestaand publiek van Experience Platform na activering bij te werken.

De instructies om aan uw [!DNL SAP Commerce] instantie voor authentiek te verklaren zijn verder hieronder, in [&#x200B; voor authentiek verklaren aan bestemmings &#x200B;](#authenticate) sectie.

## Gebruiksscenario’s {#use-cases}

Om u beter te helpen begrijpen hoe en wanneer u de [!DNL SAP Commerce] bestemming zou moeten gebruiken, is hier een geval van het steekproefgebruik dat de klanten van Adobe Experience Platform kunnen oplossen door deze bestemming te gebruiken.

[!DNL SAP Commerce] -klanten slaan informatie op over personen of organisaties die met uw bedrijf communiceren. Uw team gebruikt de klanten in [!DNL SAP Commerce] om het Experience Platform-publiek op te bouwen. Na het verzenden van deze soorten publiek naar [!DNL SAP Commerce] wordt hun informatie bijgewerkt en wordt aan elke klant een eigenschap toegewezen met de waarde ervan als de publieksnaam die aangeeft tot welk publiek de klant behoort.

## Vereisten {#prerequisites}

Raadpleeg de onderstaande secties voor alle voorwaarden die u in Experience Platform en [!DNL SAP Commerce] moet instellen en voor informatie die u moet verzamelen voordat u met het [!DNL SAP Commerce] -doel kunt werken.

### Experience Platform-voorwaarden {#prerequisites-in-experience-platform}

Alvorens gegevens aan de [!DNL SAP Commerce] bestemming te activeren, moet u a [&#x200B; schema &#x200B;](/help/xdm/schema/composition.md), a [&#x200B; dataset &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) hebben, en [&#x200B; publiek &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) dat in [!DNL Experience Platform] wordt gecreeerd.

Verwijs naar de documentatie van Experience Platform voor [&#x200B; het schemagroep van de Details van het Lidmaatschap van de Publiek &#x200B;](/help/xdm/field-groups/profile/segmentation.md) als u begeleiding op publieksstatus nodig hebt.

### Vereisten voor het doel [!DNL SAP Commerce] {#prerequisites-destination}

Houd rekening met de volgende voorwaarden om gegevens van Experience Platform naar uw [!DNL SAP Commerce] -account te exporteren:

#### U moet een [!DNL SAP Subscription Billing] -account hebben {#prerequisites-account}

Als u gegevens van Experience Platform naar uw [!DNL SAP Commerce] -account wilt exporteren, hebt u een [!DNL SAP Subscription Billing] -account nodig. Neem contact op met uw accountmanager van [!DNL SAP] als u geen geldige factureringsaccount hebt. Verwijs naar het [[!DNL SAP]  document van de Configuratie van het Platform &#x200B;](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) voor extra details.

#### Een servicesleutel genereren {#prerequisites-service-key}

* Met de servicetoets [!DNL SAP Commerce] hebt u via Experience Platform toegang tot de API van [!DNL SAP Subscription Billing] . Verwijs naar [!DNL SAP Commerce] [&#x200B; creeer een Sleutel van de Dienst met identiteitskaart van de Cliënt en Geheime Cliënt &#x200B;](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/87c11a0f5dc3494eaf3baa355925c030.html#create-a-service-key-with-client-id-and-client-secret) om een de dienstsleutel tot stand te brengen. [!DNL SAP Commerce] vereist het volgende:
   * Client-id
   * Clientgeheim
   * URL. Het URL-patroon is als volgt: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Deze waarde wordt later gebruikt om waarden voor `Region` en `Endpoint` op te halen.

+++Selecteer deze optie om een voorbeeld van de servicetoets weer te geven

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

#### Aangepaste verwijzingen maken in [!DNL SAP Subscription Billing] {#prerequisites-custom-reference}

Als u de Experience Platform-publieksstatus in [!DNL SAP Subscription Billing] wilt bijwerken, hebt u een aangepast referentieveld nodig voor elk publiek dat in Experience Platform is geselecteerd.

Om de douaneverwijzingen tot stand te brengen, login aan uw [!DNL SAP Subscription Billing] rekening en aan de **[Hoofdgegevens en Configuratie]** te navigeren > **[de pagina van de Verwijzingen van de Douane]**. Selecteer vervolgens **[!UICONTROL Create]** om een nieuwe referentie toe te voegen voor elk publiek dat in Experience Platform is geselecteerd. U zult deze namen van verwijzingsgebieden in de verdere [&#x200B; uitvoer van het publiek van het Programma en voorbeeld &#x200B;](#schedule-segment-export-example) stap vereisen.

Hieronder ziet u een voorbeeld van het maken van een aangepaste **[!UICONTROL Reference Type]** in [!DNL SAP Subscription Billing] :
![&#x200B; Beeld dat waar toont om een douaneverwijzing in het Factureren van het Abonnement van SAP tot stand te brengen.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Voor extra begeleiding, verwijs naar de [!DNL SAP Subscription Billing] [&#x200B; documentatie van douaneverwijzingen &#x200B;](https://help.sap.com/docs/CLOUD_TO_CASH_OD/80d121f216af43648e79664efe5595f7/85696a63c8d8453a934e86c9413a25cf.html?version=2023-11-27).

### Vereiste referenties verzamelen {#gather-credentials}

Als u [!DNL SAP Commerce] wilt verbinden met Experience Platform, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| Client-id | De waarde van `clientId` in de servicetoets. |
| Clientgeheim | De waarde van `clientSecret` in de servicetoets. |
| Endpoint | De waarde van `url` in de servicesleutel komt overeen met `https://subscriptionbilling.authentication.eu10.hana.ondemand.com` . |
| Regio | De locatie van uw datacenter. Het gebied is aanwezig in de `url` en heeft een waarde vergelijkbaar met `eu10` of `us10` . Als de waarde `url` bijvoorbeeld `https://eu10.revenue.cloud.sap/api` is, hebt u `eu10` nodig. |

## Guardrails {#guardrails}

API verzoeken aan [!DNL SAP Cloud Management service] zijn onderworpen aan [&#x200B; Grenswaarden van het Tarief &#x200B;](https://help.sap.com/docs/btp/sap-business-technology-platform/account-administration-rate-limiting). Wanneer de snelheidslimiet wordt overschreden, krijgt u een `HTTP 429 Too Many Requests` antwoordstatuscode.

## Ondersteunde identiteiten {#supported-identities}

[!DNL SAP Commerce] ondersteunt het bijwerken van de identiteiten die in de onderstaande tabel worden beschreven. Leer meer over [&#x200B; identiteiten &#x200B;](/help/identity-service/features/namespaces.md).

| Doelidentiteit | Beschrijving | Overwegingen |
| --- | --- | --- |
| `customerNumberSAP` | Een klant-id van de individuele of zakelijke klant die al in uw [!DNL SAP Commerce] -account aanwezig is. | Verplicht |

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie worden alle soorten publiek beschreven die u naar deze bestemming kunt exporteren.

Deze bestemming steunt de activering van alle die publiek door de Dienst van de Segmentatie van Experience Platform [&#x200B; wordt geproduceerd &#x200B;](../../../segmentation/home.md).

Deze bestemming ondersteunt ook de activering van het publiek dat in de onderstaande tabel wordt beschreven.

| Type publiek | Ondersteund | Beschrijving |
| ------------- | --------- | ----------- |
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Profile-based]** | <ul><li>U exporteert alle leden van een publiek samen met de gewenste schemavelden *(bijvoorbeeld: e-mailadres, telefoonnummer, achternaam)* volgens uw veldtoewijzing.</li><li> Voor elk geselecteerd publiek in Experience Platform wordt het bijbehorende [!DNL SAP Commerce] extra kenmerk bijgewerkt met de publieksstatus van Experience Platform.</li></ul> |
| Exportfrequentie | **[!UICONTROL Streaming]** | <ul><li>Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Wanneer een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!IMPORTANT]
>
>Om met de bestemming te verbinden, hebt u de **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Om met deze bestemming te verbinden, volg de stappen die in het [&#x200B; leerprogramma van de bestemmingsconfiguratie &#x200B;](../../ui/connect-destination.md) worden beschreven. In vormen bestemmingswerkschema, vul de gebieden in die in de twee hieronder secties worden vermeld.

Zoek in **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** naar [!DNL SAP Commerce] . U kunt de locatie ook in de categorie **[!UICONTROL eCommerce]** vinden.

### Verifiëren voor bestemming {#authenticate}

Vul de vereiste velden hieronder in. Verwijs naar [&#x200B; een de dienstsleutel &#x200B;](#prerequisites-service-key) sectie voor om het even welke begeleiding produceren.

| Veld | Beschrijving |
| --- | --- |
| **[!UICONTROL Client ID]** | De waarde van `clientId` in de servicetoets. |
| **[!UICONTROL Client secret]** | De waarde van `clientSecret` in de servicetoets. |
| **[!UICONTROL Endpoint]** | De waarde van `url` in de servicesleutel komt overeen met `https://subscriptionbilling.authentication.eu10.hana.ondemand.com` . |
| **[!UICONTROL Region]** | De locatie van uw datacenter. Het gebied is aanwezig in de `url` en heeft een waarde vergelijkbaar met `eu10` of `us10` . Als de waarde `url` bijvoorbeeld `https://eu10.revenue.cloud.sap/api` is, hebt u `eu10` nodig. |

Selecteer **[!UICONTROL Connect to destination]** als u wilt verifiëren bij het doel.
![&#x200B; Beeld van Experience Platform UI die tonen hoe te aan de bestemming voor authentiek te verklaren.](../../assets/catalog/ecommerce/sap-commerce/authenticate-destination.png)

Als de opgegeven gegevens geldig zijn, geeft de gebruikersinterface de status **[!UICONTROL Connected]** weer met een groen vinkje. Vervolgens kunt u verdergaan met de volgende stap.

### Doelgegevens invullen {#destination-details}

Als u details voor de bestemming wilt configureren, vult u de vereiste en optionele velden hieronder in. Een sterretje naast een veld in de gebruikersinterface geeft aan dat het veld verplicht is.
![&#x200B; Beeld van Experience Platform UI die de bestemmingsdetails tonen die na authentificatie moeten worden gevuld.](../../assets/catalog/ecommerce/sap-commerce/destination-details.png)

* **[!UICONTROL Name]**: Een naam waarmee u dit doel in de toekomst herkent.
* **[!UICONTROL Description]**: Een beschrijving die u zal helpen deze bestemming in de toekomst identificeren.
* **[!UICONTROL Type of Customer]**: Selecteer of ***Individueel*** of ***Collectief*** afhankelijk van de entiteiten binnen uw publiek. Het [!DNL SAP Subscription Billing] [&#x200B; schema &#x200B;](https://api.sap.com/api/BusinessPartner_APIs/schema) schakelt de verplichte gebieden afhankelijk van deze selectie die aan het `customerType` attribuut in kaart wordt gebracht. Als de selectie ***Collectief*** is, dan zullen de verplichte die afbeeldingen als `firstName` en `lastName` voor een individuele klant worden vereist worden genegeerd en `company` verplicht en vice versa.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Voor meer informatie over alarm, zie de gids bij [&#x200B; het intekenen aan bestemmingsalarm gebruikend UI &#x200B;](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.
>* Om *identiteiten* uit te voeren, hebt u de **[!UICONTROL View Identity Graph]** [&#x200B; toegangsbeheertoestemming &#x200B;](/help/access-control/home.md#permissions) nodig. <br> ![&#x200B; Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren.](/help/destinations/assets/overview/export-identities-to-destination.png " Uitgezochte identiteit namespace die in het werkschema wordt benadrukt om publiek aan bestemmingen te activeren."){width="100" zoomable="yes"}

Lees [&#x200B; activeer profielen en publiek aan het stromen publiek uitvoerbestemmingen &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md) voor instructies bij het activeren van publiek aan deze bestemming.

### Kenmerken en identiteiten toewijzen {#map}

Als u uw publieksgegevens correct vanuit Adobe Experience Platform naar de [!DNL SAP Commerce] -bestemming wilt verzenden, moet u de stap voor veldtoewijzing doorlopen. Toewijzing bestaat uit het maken van een koppeling tussen de schemavelden van uw Experience Data Model (XDM) in uw Experience Platform-account en de overeenkomstige equivalenten van de doelbestemming. Voer de onderstaande stappen uit om uw XDM-velden correct toe te wijzen aan de [!DNL SAP Commerce] -doelvelden:

#### Wijs de `customerNumberSAP` identiteit toe

De identiteit van `customerNumberSAP` is een verplichte toewijzing voor dit doel. Voer de onderstaande stappen uit om deze toe te wijzen:

1. Selecteer **[!UICONTROL Mapping]** in de stap **[!UICONTROL Add new mapping]** . U ziet nu een nieuwe toewijzingsrij op het scherm.
   {het schermschot van 0} Experience Platform UI met toegevoegde nieuwe benadrukte toewijzingsknoop.![](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Kies in het **[!UICONTROL Select source field]** -venster de **[!UICONTROL Select identity namespace]** en selecteer `customerNumberSAP` .
   {het schermschot van 0} Experience Platform UI die e-mail als bronattribuut selecteert om als identiteit in kaart te brengen.![](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-identity.png)
1. Kies in het **[!UICONTROL Select target field]** -venster de **[!UICONTROL Select identity namespace]** en selecteer de `customerNumber` -identiteit.
   {het schermschot van 0} Experience Platform UI die e-mail als doelattribuut selecteert om als identiteit in kaart te brengen.![](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-identity.png)

| Source-veld | Doelveld | Verplicht |
| --- | --- | --- |
| `IdentityMap: customerNumberSAP` | `Identity: customerNumber` | Ja |

Hieronder ziet u een voorbeeld met de identiteitstoewijzing:
![&#x200B; Beeld van Experience Platform UI die een voorbeeld van de identiteitstoewijzing van customerNumber toont.](../../assets/catalog/ecommerce/sap-commerce/mapping-identities.png)

#### Toewijzingskenmerken

Herhaal de onderstaande stappen om andere kenmerken toe te voegen die u tussen het XDM-profielschema en uw [!DNL SAP Subscription Billing] -account wilt bijwerken:

1. Selecteer **[!UICONTROL Mapping]** in de stap **[!UICONTROL Add new mapping]** . U ziet nu een nieuwe toewijzingsrij op het scherm.
   {het schermschot van 0} Experience Platform UI met toegevoegde nieuwe benadrukte toewijzingsknoop.![](../../assets/catalog/ecommerce/sap-commerce/mapping-add-new-mapping.png)
1. Kies in het venster **[!UICONTROL Select source field]** de categorie **[!UICONTROL Select attributes]** en selecteer het XDM-kenmerk.
   ![&#x200B; het schermschot van Experience Platform UI die Achternaam als bronattribuut selecteren.](../../assets/catalog/ecommerce/sap-commerce/mapping-select-source-attribute.png)
1. In het **[!UICONTROL Select target field]** venster, kies **[!UICONTROL Select custom attributes]** categorie en typ de naam van het [!DNL SAP Subscription Billing] attribuut van de lijst van klant [&#x200B; schema &#x200B;](https://api.sap.com/api/BusinessPartner_APIs/schema) attributen.
   {het schermschot van 0} Experience Platform UI waar lastName als doelattribuut wordt bepaald.![](../../assets/catalog/ecommerce/sap-commerce/mapping-select-target-attribute.png)

>[!IMPORTANT]
>
> Doelveldnamen zijn hoofdlettergevoelig en moeten overeenkomen met namen van [!DNL SAP Subscription Billing] -kenmerken. De enige uitzondering hiervoor is `country` waar u `countryCode` moet gebruiken. [!DNL SAP Subscription Billing] ondersteunt alpha-2 (ISO 3166)-landcodes. De waarde is hoofdlettergevoelig en moet tussen 0 en 3 tekens lang zijn. Zorg er dus voor dat u de gedefinieerde waarden exact opgeeft, anders treden er fouten op: `The country code {} does not exist` of `size must be between 0 and 3` .

#### Kenmerken toewijzen `mandatory` voor het geselecteerde klanttype

De verplichte kenmerktoewijzingen zijn afhankelijk van de **[!UICONTROL Type of Customer]** die u hebt geselecteerd. Selecteer een van de volgende opties om de verplichte kenmerken toe te wijzen:

>[!BEGINTABS]

>[!TAB  Individuele klant ]

| Source-veld | Doelveld | Verplicht |
| --- | --- | --- |
| `xdm: person.lastName` | `Attribute: lastName` | Ja |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Ja |

>[!TAB  Collectieve klant ]

| Source-veld | Doelveld | Verplicht |
| --- | --- | --- |
| `xdm: b2b.companyName` | `Attribute: company` | Ja |
| `xdm: workAddress.countryCode` | `Attribute: countryCode` | Ja |

>[!ENDTABS]

#### Extra kenmerken toewijzen

U kunt om het even welke extra afbeeldingen tussen uw XDM profielschema en [!DNL SAP Subscription Billing] [&#x200B; schema &#x200B;](https://api.sap.com/api/BusinessPartner_APIs/schema) attributen voor een klant zoals hieronder getoond dan toevoegen:

>[!BEGINTABS]

>[!TAB  Individuele klant ]

| Source-veld | Doelveld | Verplicht |
| --- | --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstName` | Nee |
| `xdm: workAddress.street1` | `Attribute: street` | Nee |
| `xdm: workAddress.city` | `Attribute: city` | Nee |

Een voorbeeld met zowel verplichte als optionele kenmerktoewijzingen waarbij de klant een individu is, wordt hieronder weergegeven:
![&#x200B; Beeld van Experience Platform UI die een voorbeeld met zowel verplichte als facultatieve attributenafbeeldingen toont waar de klant een individu is.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-individual.png)

>[!TAB  Collectieve klant ]

| Source-veld | Doelveld | Verplicht |
| --- | --- | --- |
| `xdm: workAddress.street1` | `Attribute: street` | Nee |
| `xdm: workAddress.city` | `Attribute: city` | Nee |

Een voorbeeld met zowel verplichte als optionele kenmerktoewijzingen waarbij de klant een onderneming is, wordt hieronder weergegeven:
![&#x200B; Beeld van Experience Platform UI die een voorbeeld met zowel verplichte als facultatieve attributenafbeeldingen toont waar de klant een collectief is.](../../assets/catalog/ecommerce/sap-commerce/mapping-attributes-corporate.png)

>[!ENDTABS]

Wanneer u klaar bent met het opgeven van de toewijzingen voor uw doelverbinding, selecteert u **[!UICONTROL Next]** .

### Het publiek van het programma uitvoeren en voorbeeld {#schedule-segment-export-example}

Wanneer het uitvoeren van de [&#x200B; stap van de de publieksuitvoer van het Programma &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling), moet u het publiek van Experience Platform aan de [&#x200B; attributen &#x200B;](#prerequisites-attribute) in kaart brengen [!DNL SAP Subscription Billing].

Hieronder ziet u een voorbeeld van de stap die het publiek van het venster Planning uitvoert en de locatie van de [!DNL SAP Commerce] **[!UICONTROL Mapping ID]** gemarkeerd is:
![&#x200B; Beeld van Experience Platform die de uitvoer van het planningspubliek met Bebevolkt Mapping IDs tonen.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export.png)

Hiervoor selecteert u elk segment en voert u vervolgens de naam in van de aangepaste verwijzing uit [!DNL SAP Subscription Billing] in het veld voor de [!DNL SAP Commerce] doelconnector **[!UICONTROL Mapping ID]** . Voor begeleiding bij het creëren van douaneverwijzingen, verwijs naar [&#x200B; creeer douaneverwijzingen in  [!DNL SAP Subscription Billing]](#prerequisites-custom-reference) sectie.

>[!IMPORTANT]
>
> Gebruik het aangepaste referentielabel niet als waarde.
> &#x200B;>![Het beeld erop wijst dat u niet de waarde van het douanelabel van de verwijzing voor afbeelding zou moeten gebruiken.](../../assets/catalog/ecommerce/sap-commerce/custom-reference-dont-use-label-for-mapping.png)

Als uw geselecteerde Experience Platform-publiek bijvoorbeeld `sap_audience1` is en u wilt dat de status wordt bijgewerkt naar de [!DNL SAP Subscription Billing] aangepaste referentie `SAP_1` , geeft u deze waarde op in het veld [!DNL SAP_Commerce] **[!UICONTROL Mapping ID]** .

Hieronder ziet u een voorbeeld **[!UICONTROL Reference Type]** van [!DNL SAP Subscription Billing] :
![&#x200B; Beeld dat waar toont om een douaneverwijzing in het Factureren van het Abonnement van SAP tot stand te brengen.](../../assets/catalog/ecommerce/sap-commerce/create-custom-reference.png)

Hieronder ziet u een voorbeeld van de stap die het publiek van het venster Planning uitvoert, met een geselecteerd publiek en de bijbehorende [!DNL SAP Commerce] **[!UICONTROL Mapping ID]** gemarkeerd:
![&#x200B; Beeld van Experience Platform die de uitvoer van het planningspubliek met Bebevolkt Mapping IDs tonen.](../../assets/catalog/ecommerce/sap-commerce/schedule-segment-export-example.png)

Zoals u ziet, moet de waarde in het veld **[!UICONTROL Mapping ID]** exact overeenkomen met de waarde [!DNL SAP Subscription Billing] **[!UICONTROL Reference Type]** .

Herhaal deze sectie voor elk geactiveerd Experience Platform-publiek.

Op basis van de bovenstaande afbeelding waarin u twee soorten publiek hebt geselecteerd, wordt de afbeelding als volgt toegewezen:

| [!DNL SAP Commerce] publieksnaam | [!DNL SAP Subscription Billing] **[!UICONTROL Reference Type]** | [!DNL SAP Commerce] **[!UICONTROL Mapping ID]** value |
| --- | --- | --- |
| sap_publiek1 | `SAP_1` | `SAP_1` |
| SAP-publiek2 | `SAP_2` | `SAP_2` |

## Gegevens exporteren valideren {#exported-data}

Volg onderstaande stappen om te controleren of u de bestemming correct hebt ingesteld:

Meld u aan bij de [!DNL SAP Subscription Billing] -account en navigeer naar de **[!UICONTROL Contacts]** -pagina om de status van het publiek te controleren. De lijst kan worden gevormd om kolommen voor de douaneverwijzingen te tonen en de overeenkomstige publieksstatus te tonen.
![&#x200B; Beeld van het Factureren van het Abonnement van SAP die de pagina van het klantenoverzicht met kolomkopballen tonen die de publieksnaam en de statistieken van het celpubliek tonen &#x200B;](../../assets/catalog/ecommerce/sap-commerce/customer-overview.png)

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; overzicht van het Beleid van Gegevens &#x200B;](/help/data-governance/home.md).

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Verwijs naar de [[!DNL SAP Subscription Billing]  de documentatiepagina van de Types van Fout &#x200B;](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/1a6a0dd6129c48e8b235190a1b5409fa.html) voor een lijst van mogelijke foutentypes en hun antwoordcodes.

## Aanvullende bronnen {#additional-resources}

Hieronder vindt u aanvullende nuttige informatie uit de documentatie van [!DNL SAP] :

* [&#x200B; Billing van het Abonnement van SAP aan boord &#x200B;](https://help.sap.com/docs/CLOUD_TO_CASH_OD/1216e7b79c984675b0a6f0005e351c74/e4b8badf7d124026991e4ab6b57d2a33.html)

### Changelog

Deze sectie vangt de functionaliteit en de significante documentatieupdates aan deze bestemmingsschakelaar worden aangebracht die.

+++ Wijzigingen weergeven

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| Januari 2024 | Eerste release | Oorspronkelijke doelversie en documentatie publiceren. |

{style="table-layout:auto"}

+++
