---
description: Deze pagina illustreert de API vraag die wordt gebruikt om een credentiële configuratie Adobe Experience Platform Destination SDK te schrappen.
title: Een referentieconfiguratie verwijderen
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Een referentieconfiguratie verwijderen

>[!IMPORTANT]
>
>**API eindpunt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Deze pagina illustreert de API-aanvraag en -lading die u kunt gebruiken om een referentieconfiguratie te verwijderen met behulp van het API-eindpunt `/authoring/credentials` .

## Wanneer gebruikt u het API-eindpunt `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In de meeste gevallen, te hoeven u ***niet*** om het `/credentials` API eindpunt te gebruiken. In plaats daarvan kunt u de verificatiegegevens voor uw doel configureren via de `customerAuthenticationConfigurations` -parameters van het `/destinations` -eindpunt.
> 
>Lees [ de authentificatieconfiguratie van de Klant ](../functionality/destination-configuration/customer-authentication.md) voor gedetailleerde informatie over de gesteunde authentificatietypen.

Gebruik dit API-eindpunt om alleen een referentie-configuratie te maken als er een algemeen verificatiesysteem is tussen Adobe en uw doelplatform. De [!DNL Experience Platform] -klant hoeft geen verificatiegegevens op te geven om verbinding te maken met uw bestemming. In dit geval moet u een referentieconfiguratie maken met het API-eindpunt van `/credentials` .

Wanneer het gebruiken van een globaal authentificatiesysteem, moet u `"authenticationRule":"PLATFORM_AUTHENTICATION"` in de [ 2&rbrace; configuratie van de bestemmingslevering plaatsen, wanneer ](../functionality/destination-configuration/destination-delivery.md) creërend een nieuwe bestemmingsconfiguratie [. ](../authoring-api/destination-configuration/create-destination-configuration.md) Dan, moet u de configuratie van de a [ geloofsbrieven ](../credentials-api/create-credential-configuration.md) tot stand brengen en identiteitskaart van de referentie objecten in de `authenticationId` parameter in de [ configuratie van de bestemmingslevering ](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication) overgaan.

>[!IMPORTANT]
>
>Alle parameternamen en waarden die door Destination SDK worden gesteund zijn **gevoelig geval**. Om fouten in hoofdlettergevoeligheid te voorkomen, gebruikt u de namen en waarden van parameters exact zoals in de documentatie wordt getoond.

## Aan de slag met API-bewerkingen voor gebruikersgegevens {#get-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Een referentieconfiguratie verwijderen {#delete}

U kunt een [ bestaande ](create-credential-configuration.md) credentiële configuratie schrappen door a `DELETE` verzoek aan het `/authoring/credentials` eindpunt met `{INSTANCE_ID}` van de referentie configuratie te maken die u wilt schrappen.

Om een bestaande bestemmingsconfiguratie en zijn overeenkomstige `{INSTANCE_ID}` te verkrijgen, zie het artikel over [ het terugwinnen van een credentiële configuratie ](retrieve-credential-configuration.md).

**API formaat**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{INSTANCE_ID}` | De `ID` van de referentieconfiguratie die u wilt verwijderen. |

Met de volgende aanvraag wordt een referentieconfiguratie verwijderd die door de parameter `{INSTANCE_ID}` wordt gedefinieerd.

+++Verzoek

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwoord

Een geslaagde reactie retourneert HTTP-status 200 samen met een lege HTTP-respons.

+++

## API-foutafhandeling {#error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu hoe u een referentieconfiguratie kunt verwijderen met behulp van het API-eindpunt van `/authoring/credentials` . Lees [ hoe te om Destination SDK te gebruiken om uw bestemming ](../guides/configure-destination-instructions.md) te vormen om te begrijpen waar deze stap in het proces past om uw bestemming te vormen.
