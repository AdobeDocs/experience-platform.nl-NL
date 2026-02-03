---
title: Salesforce Marketing Cloud Source - Overzicht
description: Leer hoe u Salesforce Marketing Cloud met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 7481a4c85f14847c13d20372dc7bd26c92a5c3d4
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>De [!DNL Oracle Salesforce Marketing Cloud] -bron is nu afgekeurd en is niet meer beschikbaar. Gebruik de nieuwe [[!DNL Salesforce Marketing Cloud]  (V2) bron &#x200B;](sfmc.md) als nieuwe schakelaar voor uw [!DNL Salesforce Marketing Cloud] gegevens.

[!DNL Salesforce Marketing Cloud] biedt u de mogelijkheid om de betrokkenheid van klanten te beheren en te automatiseren voor e-mail, mobiele apparaten, sociale media en advertenties, allemaal vanaf één platform. Met hulpmiddelen zoals E-mail Studio, de Bouwer van de Reis, en de Bouwer van het Publiek, kunt u gepersonaliseerde campagnes en klantenreizen tot stand brengen die aan uw publiek worden aangepast.

U kunt de bron van [!DNL Salesforce Marketing Cloud] gebruiken om uw account te verbinden en uw gegevens naar Adobe Experience Platform te brengen.

## Vereisten

Alvorens u uw [!DNL Salesforce Marketing Cloud] bron aan Experience Platform kunt verbinden, moet u ervoor zorgen dat het volgende **toestemmingswerkingsgebied** provisioned aan uw [!DNL Salesforce Marketing Cloud] cliënt identiteitskaart en cliënt geheime combinatie zijn:

* `campaign_read`
* `list_and_subscribers_read`

U kunt het bereik aanvragen door de `v2/userinfo` -bron van de [!DNL Salesforce Marketing Cloud] API aan te roepen. Zie het [[!DNL Salesforce Marketing Cloud]  document van de Scopes van de Toestemming van de Integratie API &#x200B;](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) voor begeleiding op hoe te om werkingsgebied te verzoeken en te vergelijken.

Voor meer informatie over werkingsgebied met inbegrip van een lijst van hun verwante toestemmingen en gedrag, zie dit [[!DNL Salesforce Marketing Cloud]  REST API document &#x200B;](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de bronintegratie van [!DNL Salesforce Marketing Cloud] .

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Voor meer informatie, lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

>[!WARNING]
>
>Als u niet de noodzakelijke IP adressen aan uw lijst van gewenste personen toevoegt, zal uw [!DNL Salesforce Marketing Cloud] rekening niet met Experience Platform verbinden.

### Verifiëren voor Experience Platform in Azure {#azure}

U moet waarden opgeven voor de volgende referenties om [!DNL Salesforce Marketing Cloud] op [!DNL Azure] met Experience Platform te verbinden.

| Credentials | Beschrijving |
| --- | --- |
| Host | De hostserver van uw toepassing. Dit is vaak uw subdomein. **Nota:** wanneer het ingaan van uw `host` waarde, moet u `{subdomain}.rest.marketingcloudapis.com` specificeren. Als de host-URL bijvoorbeeld `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` is, moet u `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` als waarde voor de host invoeren. |
| Client-id | De client-id die aan uw [!DNL Salesforce Marketing Cloud] -toepassing is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan de toepassing [!DNL Salesforce Marketing Cloud] is gekoppeld. |
| Verbinding, specificatie-id | **verbindingsspecificatie** verstrekt de schakelaareigenschappen van een gegevensbron. Dit omvat details zoals authentificatiespecificaties en vereisten voor het creëren van zowel **basis** als **bron** verbindingen. Voor [!DNL Salesforce Marketing Cloud] is de specificatie-id van de verbinding: `ea1c2a08-b722-11eb-8529-0242ac130003` . **Nota:** Deze referentie is slechts noodzakelijk wanneer het verbinden via APIs. |

### Verifiëren voor Experience Platform op Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](../../../landing/multi-cloud.md).

U moet waarden opgeven voor de volgende referenties om [!DNL Salesforce Marketing Cloud] te verbinden met Experience Platform op AWS.

| Credentials | Beschrijving |
| --- | --- |
| Subdomein | Het unieke gedeelte van de URL van de instantie [!DNL Salesforce Marketing Cloud] dat wordt gebruikt voor het samenstellen van API-eindpunten. |
| Client-id | Een openbare id voor uw toepassing die wordt gegenereerd wanneer u een geïnstalleerd pakket maakt in [!DNL Salesforce Marketing Cloud] |
| Clientgeheim | Een vertrouwelijke sleutel verbonden aan uw identiteitskaart van de Cliënt, die ook in het geïnstalleerde pakket wordt geproduceerd. |
| Verbinding, specificatie-id | **verbindingsspecificatie** verstrekt de schakelaareigenschappen van een gegevensbron. Dit omvat details zoals authentificatiespecificaties en vereisten voor het creëren van zowel **basis** als **bron** verbindingen. Voor [!DNL Salesforce Marketing Cloud] is de specificatie-id van de verbinding: `ea1c2a08-b722-11eb-8529-0242ac130003` . **Nota:** Deze referentie is slechts noodzakelijk wanneer het verbinden via APIs. |

Voor meer informatie, lees de [[!DNL Salesforce]  documentatie over toegangstoken voor server-aan-server integraties &#x200B;](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html).

## Verbinding maken [!DNL Salesforce Marketing Cloud] met Experience Platform via API&#39;s

In de onderstaande documentatie vindt u informatie over het maken van een verbinding tussen [!DNL Salesforce Marketing Cloud] en Experience Platform met behulp van API&#39;s:

* [Verbind  [!DNL Salesforce Marketing Cloud]  met Experience Platform gebruikend de Dienst API van de Stroom](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een marketingautomatiseringsbron met behulp van de Flow Service API](../../tutorials/api/collect/marketing-automation.md)

## Verbinding maken [!DNL Salesforce Marketing Cloud] met Experience Platform via de gebruikersinterface

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Salesforce Marketing Cloud] en Experience Platform via de gebruikersinterface:

* [Verbind  [!DNL Salesforce Marketing Cloud]  met Experience Platform in UI](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Een gegevensstroom maken voor een bronverbinding voor marketingautomatisering in de gebruikersinterface](../../tutorials/ui/dataflow/marketing-automation.md)
