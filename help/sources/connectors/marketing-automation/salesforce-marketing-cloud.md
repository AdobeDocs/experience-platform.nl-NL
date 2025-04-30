---
solution: Experience Platform
title: Salesforce Marketing Cloud Source - Overzicht
description: Leer hoe u Salesforce Marketing Cloud met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>De [!DNL Salesforce Marketing Cloud] -bron wordt afgekeurd in januari 2026. Later dit jaar zal een nieuwe bron worden vrijgegeven als alternatief. Zodra de nieuwe bron wordt vrijgegeven, moet u van plan zijn om aan de nieuwe bron te migreren door nieuwe rekeningsverbindingen en dataflows vóór eind Januari 2026 te creëren.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van externe systemen voor marketingautomatisering. Tot de ondersteuning voor marketingautomatiseringsproviders behoren [!DNL Salesforce Marketing Cloud] .

## Vereisten

Alvorens u uw [!DNL Salesforce Marketing Cloud] bron aan Experience Platform kunt verbinden, moet u ervoor zorgen dat het volgende **toestemmingswerkingsgebied** provisioned aan uw [!DNL Salesforce Marketing Cloud] cliënt identiteitskaart en cliënt geheime combinatie zijn:

* `campaign_read`
* `list_and_subscribers_read`

U kunt het bereik aanvragen door de `v2/userinfo` -bron van de [!DNL Salesforce Marketing Cloud] API aan te roepen. Zie het [[!DNL Salesforce Marketing Cloud]  document van de Scopes van de Toestemming van de Integratie API ](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) voor begeleiding op hoe te om werkingsgebied te verzoeken en te vergelijken.

Voor meer informatie over werkingsgebied met inbegrip van een lijst van hun verwante toestemmingen en gedrag, zie dit [[!DNL Salesforce Marketing Cloud]  REST API document ](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de bronintegratie van [!DNL Salesforce Marketing Cloud] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Verbinding maken [!DNL Salesforce Marketing Cloud] met Experience Platform via API&#39;s

In de onderstaande documentatie vindt u informatie over het maken van een verbinding tussen [!DNL Salesforce Marketing Cloud] en Experience Platform met behulp van API&#39;s:

* [Een Salesforce Marketing Cloud-basisverbinding maken met de Flow Service API](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een marketingautomatiseringsbron met behulp van de Flow Service API](../../tutorials/api/collect/marketing-automation.md)

## Verbinding maken [!DNL Salesforce Marketing Cloud] met Experience Platform via de gebruikersinterface

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Salesforce Marketing Cloud] en Experience Platform via de gebruikersinterface:

* [Een Salesforce Marketing Cloud-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Een gegevensstroom maken voor een bronverbinding voor marketingautomatisering in de gebruikersinterface](../../tutorials/ui/dataflow/marketing-automation.md)
