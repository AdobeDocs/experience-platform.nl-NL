---
title: Overzicht van de Salesforce Source Connector
description: Leer hoe u Salesforce met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# [!DNL Salesforce]

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-systeem van derden. Tot de ondersteuning voor CRM-providers behoren [!DNL Salesforce] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Veldtoewijzing van [!DNL Salesforce] naar XDM

Om een bronverbinding tussen [!DNL Salesforce] en Platform tot stand te brengen, moeten de [!DNL Salesforce] brongegevensgebieden aan hun aangewezen doelXDM gebieden worden in kaart gebracht alvorens in Platform wordt opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels voor het in kaart brengen van velden tussen [!DNL Salesforce] datasets en Platform:

- [Contactpersonen](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Accounts](../adobe-applications/mapping/salesforce.md#account)
- [Kansen](../adobe-applications/mapping/salesforce.md#opportunity)
- [Contactrollen opportunity](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagnes](../adobe-applications/mapping/salesforce.md#campaign)
- [Campagneleden](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Contactpersoon account](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Het hulpprogramma voor automatisch genereren van naamruimten en schema [!DNL Salesforce] instellen

Als u de [!DNL Salesforce] bron wilt gebruiken als onderdeel van [!DNL B2B-CDP] , moet u eerst een hulpprogramma [!DNL Postman] instellen om automatisch uw [!DNL Salesforce] naamruimten en schema&#39;s te genereren. In de volgende documentatie vindt u aanvullende informatie over het instellen van het hulpprogramma [!DNL Postman] :

- U kunt namespace en schema auto-generatie nutsinzameling en milieu van deze [ bewaarplaats GitHub ](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) downloaden.
- Voor informatie bij het gebruiken van Platform APIs met inbegrip van details over hoe te om waarden voor vereiste kopballen te verzamelen en steekproefAPI vraag te lezen, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).
- Voor informatie over hoe te om uw geloofsbrieven voor Platform APIs te produceren, zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md).
- Voor informatie over hoe te opstelling [!DNL Postman] voor Platform APIs, zie het leerprogramma op [ vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../landing/postman.md).

Met een platformontwikkelaarsconsole en [!DNL Postman] -configuratie kunt u nu de juiste omgevingswaarden toepassen op uw [!DNL Postman] -omgeving.

De volgende tabel bevat voorbeeldwaarden en aanvullende informatie over het vullen van de [!DNL Postman] -omgeving:

| Variabele | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `CLIENT_SECRET` | Een unieke id die wordt gebruikt om de `{ACCESS_TOKEN}` te genereren. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{CLIENT_SECRET}` terug te winnen. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) is een verificatiereferentie die wordt gebruikt om uw {ACCESS_TOKEN} te genereren. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{JWT_TOKEN}` te produceren. | `{JWT_TOKEN}` |
| `API_KEY` | Een unieke id die wordt gebruikt om aanroepen van Experience Platform-API&#39;s te verifiëren. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{API_KEY}` terug te winnen. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Het toestemmingstoken dat wordt vereist om vraag aan Experience Platform APIs te voltooien. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{ACCESS_TOKEN}` terug te winnen. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ent_dataservices_sdk` . | `ent_dataservices_sdk` |
| `CONTAINER_ID` | De `global` container houdt alle standaard Adobe en partner van het Experience Platform verstrekte klassen, de groepen van het schemagebied, gegevenstypes, en schema&#39;s. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op `global` . | `global` |
| `PRIVATE_KEY` | Een referentie die wordt gebruikt om de [!DNL Postman] -instantie te verifiëren voor Experience Platform-API&#39;s. Zie het leerprogramma bij de console van de opstellingsontwikkelaar en [ vestiging de console van de opsteller en  [!DNL Postman]](../../../landing/postman.md) voor instructies op hoe te om uw {PRIVATE_KEY} terug te winnen. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Een referentie die wordt gebruikt om te integreren in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Het Identity Management System (IMS) biedt het framework voor verificatie van Adobe-services. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ims-na1.adobelogin.com` . | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Een onderneming die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden. Zie het leerprogramma op [ vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../landing/postman.md) voor instructies op hoe te om uw `{ORG_ID}` informatie terug te winnen. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | De naam van de virtuele sandboxpartitie die u gebruikt. | `prod` |
| `TENANT_ID` | Een id die wordt gebruikt om ervoor te zorgen dat de bronnen die u maakt, correct worden genoemd en zich binnen uw organisatie bevinden. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Het URL-eindpunt waarnaar u API-aanroepen maakt. Deze waarde is vast en wordt altijd ingesteld op: `http://platform.adobe.io/` . | `http://platform.adobe.io/` |
| `munchkinId` | De unieke id voor uw [!DNL Marketo] -account. Zie het leerprogramma op [ voor authentiek verklaren uw  [!DNL Marketo]  instantie ](../adobe-applications/marketo/marketo-auth.md) voor informatie over hoe te om uw `munchkinId` terug te winnen. | `123-ABC-456` |
| `sfdc_org_id` | De organisatie-id voor uw [!DNL Salesforce] -account. Zie de volgende [[!DNL Salesforce]  gids ](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) voor meer informatie bij het verwerven van uw [!DNL Salesforce] organisatie identiteitskaart | `00D4W000000FgYJUA0` |
| `has_abm` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Account-Based Marketing] . | `false` |
| `has_msi` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Sales Insight] . | `false` |

{style="table-layout:auto"}

### Scripts uitvoeren

Als de verzameling van [!DNL Postman] is ingesteld en de omgeving is ingesteld, kunt u het script nu uitvoeren via de interface van [!DNL Postman] .

Selecteer in de interface [!DNL Postman] de hoofdmap van het hulpprogramma voor automatische generator en selecteer vervolgens **[!DNL Run]** in de bovenste koptekst.

![ wortel-omslag ](../../images/tutorials/create/salesforce/root-folder.png)

De interface [!DNL Runner] wordt weergegeven. Controleer van hieruit of alle selectievakjes zijn ingeschakeld en selecteer vervolgens **[!DNL Run Namespaces and Schemas Autogeneration Utility]** .

![ looppas-generator ](../../images/tutorials/create/salesforce/run-generator.png)

Een succesvol verzoek leidt tot B2B namespaces en schema&#39;s volgens bètaspecificaties.

## Verbinding maken [!DNL Salesforce] met platform met behulp van API&#39;s

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Salesforce] en Platform via API&#39;s of de gebruikersinterface:

- [Een Salesforce-basisverbinding maken met de Flow Service API](../../tutorials/api/create/crm/salesforce.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een CRM-bron met behulp van de Flow Service API](../../tutorials/api/collect/crm.md)

## Verbinding maken [!DNL Salesforce] met platform via de gebruikersinterface

- [Een Salesforce-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/crm/salesforce.md)
- [Een gegevensstroom maken voor een CRM-verbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
