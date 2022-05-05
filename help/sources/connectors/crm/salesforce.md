---
keywords: Experience Platform;home;populaire onderwerpen;crm-schema;crm;CRM;salesforce;Salesforce
solution: Experience Platform
title: Overzicht van de Salesforce Source Connector
topic-legacy: overview
description: Leer hoe u Salesforce met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: fa861e9740e05b4fcc4e8039bb288301d42b8357
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# [!DNL Salesforce] connector

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de services van het Platform. U kunt gegevens van diverse bronnen, zoals Adobe-toepassingen, cloudopslag, databases en vele andere, invoeren.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-systeem van derden. Ondersteuning voor CRM-providers omvat [!DNL Salesforce].

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Veldtoewijzing van [!DNL Salesforce] naar XDM

Een bronverbinding tot stand brengen tussen [!DNL Salesforce] en Platform [!DNL Salesforce] brongegevensvelden moeten worden toegewezen aan de juiste XDM-doelvelden voordat ze in het Platform worden opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels voor het in kaart brengen van velden tussen [!DNL Salesforce] gegevenssets en Platform:

- [Contactpersonen](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Accounts](../adobe-applications/mapping/salesforce.md#account)
- [Kansen](../adobe-applications/mapping/salesforce.md#opportunity)
- [Contactrollen opportunity](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagnes](../adobe-applications/mapping/salesforce.md#campaign)
- [Campagneleden](../adobe-applications/mapping/salesforce.md#campaign-member)

## Stel de [!DNL Salesforce] naamruimte en schema automatisch genereren

Als u de opdracht [!DNL Salesforce] bron als onderdeel van [!DNL B2B-CDP]moet u eerst een [!DNL Postman] hulpprogramma om uw [!DNL Salesforce] naamruimten en schema&#39;s. In de volgende documentatie vindt u aanvullende informatie over het instellen van de [!DNL Postman] nut:

- U kunt de inzameling en het milieu van het nut van de naamruimte en van het schema auto-generatie van dit downloaden [GitHub-opslagplaats](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- Voor informatie over het gebruik van Platform APIs met inbegrip van details over hoe te om waarden voor vereiste kopballen te verzamelen en steekproefAPI vraag te lezen, zie de gids op [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).
- Raadpleeg de zelfstudie voor informatie over het genereren van referenties voor Platform-API&#39;s [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md).
- Voor informatie over het instellen [!DNL Postman] voor Platform-API&#39;s raadpleegt u de zelfstudie [ontwikkelaarsconsole instellen en [!DNL Postman]](../../../landing/postman.md).

Met een Platform ontwikkelaarsconsole en [!DNL Postman] nu kunt u de juiste omgevingswaarden op uw [!DNL Postman] milieu.

De volgende tabel bevat voorbeeldwaarden en aanvullende informatie over het vullen van de tabel [!DNL Postman] milieu:

| Variabele | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `CLIENT_SECRET` | Een unieke id die wordt gebruikt om uw `{ACCESS_TOKEN}`. Zie de zelfstudie aan [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md) voor informatie over hoe u uw `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) is een verificatiereferentie die wordt gebruikt om uw {ACCESS_TOKEN} te genereren. Zie de zelfstudie aan [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md) voor informatie over hoe u uw `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Een unieke id die wordt gebruikt om aanroepen van Experience Platform-API&#39;s te verifiëren. Zie de zelfstudie aan [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md) voor informatie over hoe u uw `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Het toestemmingstoken dat wordt vereist om vraag aan Experience Platform APIs te voltooien. Zie de zelfstudie aan [Experience Platform-API&#39;s verifiëren en openen](../../../landing/api-authentication.md) voor informatie over hoe u uw `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Met betrekking tot [!DNL Marketo]Deze waarde is vast en wordt altijd ingesteld op: `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | De `global` de container houdt alle standaardAdobe en de partner van het Experience Platform verstrekte klassen, de groepen van het schemagebied, gegevenstypes, en schema&#39;s. Met betrekking tot [!DNL Marketo], is deze waarde vast en wordt altijd ingesteld op `global`. | `global` |
| `PRIVATE_KEY` | Een referentie die wordt gebruikt voor het verifiëren van uw [!DNL Postman] -instantie naar Experience Platform-API&#39;s. Zie de zelfstudie over het instellen van de ontwikkelaarsconsole en [ontwikkelaarsconsole instellen en [!DNL Postman]](../../../landing/postman.md) voor instructies over het ophalen van uw {PRIVATE_KEY}. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Een referentie die wordt gebruikt om te integreren in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Het Identity Management System (IMS) biedt het framework voor verificatie van Adobe-services. Met betrekking tot [!DNL Marketo]Deze waarde is vast en wordt altijd ingesteld op: `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Een onderneming die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden. Zie de zelfstudie aan [ontwikkelaarsconsole instellen en [!DNL Postman]](../../../landing/postman.md) voor instructies over hoe u uw `{IMS_ORG}` informatie. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | De naam van de virtuele sandboxpartitie die u gebruikt. | `prod` |
| `TENANT_ID` | Een id die wordt gebruikt om ervoor te zorgen dat de bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw IMS-organisatie bevinden. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Het URL-eindpunt waarnaar u API-aanroepen maakt. Deze waarde is vast en wordt altijd ingesteld op: `http://platform.adobe.io/`. | `http://platform.adobe.io/` |
| `munchkinId` | De unieke id voor uw [!DNL Marketo] account. Zie de zelfstudie aan [uw [!DNL Marketo] instance](../adobe-applications/marketo/marketo-auth.md) voor informatie over hoe u uw `munchkinId`. | `123-ABC-456` |
| `sfdc_org_id` | De organisatie-id voor uw [!DNL Salesforce] account. Zie het volgende [[!DNL Salesforce] hulplijn](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) voor meer informatie over het aanschaffen van uw [!DNL Salesforce] organisatie-id. | `00D4W000000FgYJUA0` |
| `has_abm` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Account-Based Marketing]. | `false` |
| `has_msi` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Sales Insight]. | `false` |

{style=&quot;table-layout:auto&quot;}

### Scripts uitvoeren

Met uw [!DNL Postman] verzameling en omgeving instellen, kunt u het script nu uitvoeren via de [!DNL Postman] interface.

In de [!DNL Postman] interface, selecteer de wortelomslag van het auto-generatornut en selecteer dan **[!DNL Run]** in de bovenste koptekst.

![hoofdmap](../../images/tutorials/create/salesforce/root-folder.png)

De [!DNL Runner] wordt weergegeven. Controleer vanaf hier of alle selectievakjes zijn ingeschakeld en selecteer **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![loopgenerator](../../images/tutorials/create/salesforce/run-generator.png)

Een succesvol verzoek leidt tot B2B namespaces en schema&#39;s volgens bètaspecificaties.

## Verbinden [!DNL Salesforce] naar Platform met API&#39;s

In de onderstaande documentatie vindt u informatie over het maken van een verbinding [!DNL Salesforce] Platforms met behulp van API&#39;s of de gebruikersinterface:

- [Een Salesforce-basisverbinding maken met de Flow Service API](../../tutorials/api/create/crm/salesforce.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Creeer een dataflow voor een bron van CRM gebruikend de Dienst API van de Stroom](../../tutorials/api/collect/crm.md)

## Verbinden [!DNL Salesforce] naar Platform met behulp van de gebruikersinterface

- [Een Salesforce-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/crm/salesforce.md)
- [Een gegevensstroom maken voor een CRM-verbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
