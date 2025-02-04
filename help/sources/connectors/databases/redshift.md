---
title: Amazon Redshift Source Connector Overzicht
description: Leer hoe u Amazon Redshift kunt verbinden met Adobe Experience Platform met behulp van API's of de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: 77941e08df893fab6dfdaf987c56c4d5a3fd4757
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# [!DNL Amazon Redshift] bron

>[!IMPORTANT]
>
>- De [!DNL Amazon Redshift] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>- U kunt nu de [!DNL Amazon Redshift] -bron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform dat op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van het Experience Platform leren, zie het [ Experience Platform multi-cloud overzicht ](../../../landing/multi-cloud.md).


Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Het platform kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. Ondersteuning voor databaseproviders is onder andere [!DNL Amazon Redshift] .

## Uw [!DNL Amazon Redshift] source instellen voor Experience Platform op Azure {#azure}

Volg de onderstaande stappen om te leren hoe u uw [!DNL Amazon Redshift] -account kunt instellen voor Experience Platform in Azure.

### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## De [!DNL Amazon Redshift] -bron instellen voor Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform dat op Amazon Web Services (AWS) loopt. Experience Platform dat op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van het Experience Platform leren, zie het [ Experience Platform multi-cloud overzicht ](../../../landing/multi-cloud.md).

Voeg de volgende IP adressen aan uw lijst van gewenste personen toe, om uw [!DNL Amazon Redshift] rekening aan Experience Platform op Amazon Web Services (AWS) te verbinden:

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

## Verbinding maken [!DNL Amazon Redshift] met platform met behulp van API&#39;s

- [Connect Amazon Opnieuw overschakelen naar Experience Platform met behulp van de Flow Service API](../../tutorials/api/create/databases/redshift.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL Amazon Redshift] met platform via de gebruikersinterface

- [Een Amazon Redshift-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/redshift.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
