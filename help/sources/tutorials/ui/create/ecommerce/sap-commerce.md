---
title: Een SAP Commerce-bronverbinding maken in de gebruikersinterface
description: Leer hoe u een SAP Commerce-bronverbinding maakt met de Adobe Experience Platform-gebruikersinterface.
badge: Beta
source-git-commit: a848ea11e388678ade780fd81ef3ff6a3477b741
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---

# Een [!DNL SAP Commerce] bronverbinding in de gebruikersinterface

>[!NOTE]
>
>De [!DNL SAP Commerce] De bron is in bèta. Zie de [overzicht van bronnen](../../../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

De volgende zelfstudie begeleidt u door de stappen om een [!DNL SAP Commerce] bronverbinding die moet worden opgehaald [[!DNL SAP] Abonnementsfacturering](https://www.sap.com/products/financial-management/subscription-billing.html) contactpersonen en klantgegevens via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag {#getting-started}

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema-editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe u aangepaste schema&#39;s maakt met de gebruikersinterface van de Schema-editor.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u al een geldige [!DNL SAP Commerce] account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [configureren, gegevensstroom](../../dataflow/ecommerce.md).

### Vereiste referenties verzamelen {#gather-credentials}

Om verbinding te maken [!DNL SAP Commerce] als u een Experience Platform wilt maken, moet u waarden opgeven voor de volgende verbindingseigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| Client-id | De waarde van `clientId` uit de servicesleutel. |
| Clientgeheim | De waarde van `clientSecret` uit de servicesleutel. |
| Punt Token | De waarde van `url` van de de dienstsleutel, zal het gelijkaardig zijn aan `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Regio | De locatie van uw datacenter. De regio is aanwezig in de `url` en heeft een waarde vergelijkbaar met `eu10` of `us10`. Als de `url` is `https://eu10.revenue.cloud.sap/api` u hebt `eu10`. |

Voor meer informatie raadpleegt u de [[!DNL SAP Commerce] documentatie](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Een Platform-schema maken {#create-platform-schema}

Voordat u een [!DNL SAP Commerce] bronverbinding, moet u ook ervoor zorgen dat u eerst een schema van het Experience Platform aan gebruik voor uw bron creeert. Zie de zelfstudie aan [een Platform-schema maken](../../../../../xdm/schema/composition.md) voor uitvoerige stappen op hoe te om een schema tot stand te brengen.

Vouw de volgende sectie uit om een voorbeeldschema weer te geven.

+++ Voorbeeld van een schema weergeven

```
{
  "_extconndev": {
    "addresses": [
      {
        "addressUUID": "{ADDRESS_UUID}",
        "city": "Burnaby",
        "country": "Canada",
        "email": "chandni@acme.com",
        "houseNumber": "27",
        "isDefault": false,
        "phone": "123-456-7890",
        "postalCode": "V3J 1X9",
        "state": "British Columbia",
        "street": "Beresford"
      }
    ],
    "changedAt": "1687204041",
    "changedBy": "vero@acme.com",
    "contactNumber": "123-456-7980",
    "corporateInfo": {
      "company": "acme"
    },
    "createAt": "1687204041",
    "createdBy": "vero@acme.com",
    "customReferences": [
      {
        "id": "Sample value",
        "typeCode": "Sample value"
      }
    ],
    "customerNumber": "Sample value",
    "customerType": "Sample value",
    "defaultAddress": {
      "addressUUID": "Sample value",
      "city": "North Vancouver",
      "country": "Canada",
      "email": "chandni@acme.come",
      "houseNumber": "34",
      "isDefault": false,
      "phone": "123-456-7890",
      "postalCode": "V7H 2P1",
      "state": "British Columbia",
      "street": "Maple"
    },
    "externalObjectReferences": [
      {
        "externalId": "{EXTERNAL_ID}",
        "externalIdTypeCode": "{EXTERNAL_ID_TYPE_CODE}",
        "externalSystemId": "{EXTERNAL_SYSTEM_ID}"
      }
    ],
    "markets": [
      {
        "active": false,
        "country": "USA",
        "currency": "USD",
        "marketId": "Sample value",
        "priceinfo": {
          "incoterms": "{INCO_TERMS}",
          "incotermsLocation": "{INCO_TERMS_LOCATION}",
          "priceGroup": "{PRICE_GROUP}",
          "priceListType": "{PRICE_LIST_TYPE}"
        },
        "salesArea": {
          "distributionChannel": "{DISTRIBUTION_CHANNEL}",
          "division": "{DIVISION}",
          "salesOrganization": "{SALES_ORGANIZATION}"
        }
      }
    ],
    "personalInfo": {
      "firstName": "Chandni",
      "lastName": "Kaur"
    }
  },
  "_id": "/uri-reference",
  "_repo": {
    "createDate": "2004-10-23T12:00:00-06:00",
    "modifyDate": "2004-10-23T12:00:00-06:00"
  },
  "createdByBatchID": "/uri-reference",
  "modifiedByBatchID": "/uri-reference",
  "personID": "{PERSON_ID}",
  "repositoryCreatedBy": "kevin@acme.com",
  "repositoryLastModifiedBy": "kevin@acme.com"
}
```

+++

## Verbind uw [!DNL SAP Commerce] account {#connect-account}

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatiebalk voor toegang tot de [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de *eCommerce* categorie, selecteert u **[!UICONTROL SAP Commerce]** en selecteer vervolgens **[!UICONTROL Add data]**.

![Platform UI screenshot voor catalogus met SAP Commerce-kaart](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

De **[!UICONTROL Connect SAP Commerce account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account {#existing-account}

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL SAP Commerce] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![Platform UI screenshot om SAP Commerce-account te verbinden met een bestaande account](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### Nieuwe account {#new-account}

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam, een optionele beschrijving en uw referenties op. Selecteer **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![Platform UI screenshot om SAP Commerce-account te verbinden met een nieuwe account](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### Gegevens selecteren {#select-data}

Ten slotte moet u het objecttype selecteren dat u aan het Platform wilt toevoegen.

| Objecttype | Beschrijving |
| --- | --- |
| `Customers` | De entiteiten met abonnementen. |
| `Contacts` | De contactgegevens voor klanten. |

>[!BEGINTABS]

>[!TAB Klanten]

Als u klantgegevens wilt invoeren, selecteert u **[!UICONTROL Customers]** als het objecttype en selecteer vervolgens **[!UICONTROL Next]**.

![Het schermschot van UI van het Platform voor de Handel van SAP die configuratie met de geselecteerde optie van Klanten toont](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB Contactpersonen]

Als u contactgegevens wilt invoeren, selecteert u **[!UICONTROL Contacts]** als het objecttype en selecteer vervolgens **[!UICONTROL Next]**.

![Platform UI screenshot voor SAP Commerce die configuratie met geselecteerde optie van Contacten toont](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## Volgende stappen {#next-steps}

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL SAP Commerce] account. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom configureren om gegevens naar het Platform te brengen](../../dataflow/ecommerce.md).

## Aanvullende bronnen {#additional-resources}

In de volgende secties vindt u aanvullende bronnen die u kunt raadplegen wanneer u de [!DNL SAP Commerce] bron.

### Toewijzing {#mapping}

Platform biedt intelligente aanbevelingen voor automatisch toegewezen velden op basis van het doelschema of de gegevensset die u hebt geselecteerd. U kunt toewijzingsregels handmatig aanpassen aan uw gebruiksgevallen. Op basis van uw behoeften kunt u ervoor kiezen om velden rechtstreeks toe te wijzen of gegevens prep-functies te gebruiken om brongegevens om berekende of berekende waarden af te leiden. Voor uitvoerige stappen bij het gebruiken van de kaartperinterface en berekende gebieden, zie [UI-hulplijn voor gegevensvoorinstelling](../../../../../data-prep/ui/mapping.md).

De configuraties van de toewijzing voor uw gegevensstroom zullen afhankelijk van uw schema en het objecten type verschillen dat u selecteert om in te voeren.

>[!BEGINTABS]

>[!TAB Klanten]

Voor klantgegevens [!DNL SAP Commerce] gebruikt de [klanten](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) en de [klant-contacten verhoudingen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) eindpunten van de [!DNL SAP Business Partners] API om de gegevens op te halen

Hieronder ziet u een voorbeeld van het toewijzen van configuraties voor [!DNL SAP Commerce] dataflow voor klantgegevens:

| Doelveld | Beschrijving |
| --- | --- |
| `customerNumber` | Het klantnummer. |
| `corporateInfo` | Het klantnummer. |
| `customerType` | Het type klant. |
| `createdAt` | Een tijdstempel die aangeeft wanneer de klant is gemaakt. |
| `changedAt` | Een tijdstempel die aangeeft wanneer de klant voor het laatst is bijgewerkt. |
| `markets[*].country` | De klanten markten, die als serievoorwerp worden teruggewonnen. |
| `addresses[*].email` | E-mails die zijn gekoppeld aan de meerdere adressen van de klant, opgehaald als een arrayobject. |
| `addresses[*].city` | De steden verbonden aan de veelvoudige adressen van de klant, die als serievoorwerp worden teruggewonnen. |
| `addresses[*].addressUUID` | Id is gekoppeld aan de meerdere adressen van de klant, opgehaald als een matrixobject. |
| `externalObjectReferences[*].externalSystemId` | Aanvullende gegevens, opgehaald als een matrixobject. |
| `externalObjectReferences[*].externalId` | Aanvullende gegevens, opgehaald als een matrixobject. |
| `customReferences[*].id` | Aanvullende gegevens, opgehaald als een matrixobject. |
| `customReferences[*].typeCode` | Aanvullende gegevens, opgehaald als een matrixobject. |

![De toewijzingsstap van de workflow voor bronnen.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-customers.png)

>[!TAB Contactpersonen]

Voor contactgegevens [!DNL SAP Commerce] gebruikt de [contactpersonen](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) het eindpunt van de [!DNL SAP Business Partners] API om de gegevens op te halen.

Hieronder ziet u een voorbeeld van het toewijzen van configuraties voor [!DNL SAP Commerce] dataflow voor contactgegevens:

| Doelveld | Beschrijving |
| --- | --- |
| `contactNumber` | Het contactnummer. |
| `createdAt` | Een tijdstempel die aangeeft wanneer de contactpersoon is gemaakt. |
| `changedAt` | Een tijdstempel die aangeeft wanneer de contactpersoon voor het laatst is bijgewerkt. |
| `personalInfo.lastName` | De achternaam van de contactpersoon. |
| `personalInfo.firstName` | De voornaam van de contactpersoon. |
| `externalObjectReferences[*].externalSystemId` | Aanvullende gegevens, opgehaald als een matrixobject. |
| `externalObjectReferences[*].externalId` | Aanvullende gegevens, opgehaald als een matrixobject. |
| `externalObjectReferences[*].externalIdTypeCode` | Aanvullende gegevens, opgehaald als een matrixobject. |

![De toewijzingsstap van de workflow voor bronnen.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-contacts.png)

>[!ENDTABS]

