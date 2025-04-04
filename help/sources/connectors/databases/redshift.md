---
title: Amazon Redshift Source Connector Overzicht
description: Leer hoe u Amazon Redshift kunt verbinden met Adobe Experience Platform met behulp van API's of de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 75e577dd-a0b0-4f82-a371-5ec9255544f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# [!DNL Amazon Redshift] bron

>[!IMPORTANT]
>
>- De [!DNL Amazon Redshift] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>- U kunt nu de [!DNL Amazon Redshift] -bron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../landing/multi-cloud.md).


Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een database van derden. Experience Platform kan verbinding maken met verschillende typen databases, zoals relationele databases, NoSQL-databases of gegevensopslagruimten. Ondersteuning voor databaseproviders is onder andere [!DNL Amazon Redshift] .

## Stel uw [!DNL Amazon Redshift] source in voor Experience Platform on Azure {#azure}

Volg de onderstaande stappen om te leren hoe u uw [!DNL Amazon Redshift] -account voor Experience Platform on Azure kunt instellen.

### IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## De [!DNL Amazon Redshift] source voor Experience Platform instellen op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../landing/multi-cloud.md).

### IP adres lijst van gewenste personen voor verbinding op AWS

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform op AWS aan te sluiten. Voor meer informatie, lees de gids op [ voegend op lijst van gewenste personen IP adressen om met Experience Platform op AWS ](../../ip-address-allow-list.md) voor meer informatie te verbinden.

## Verbinding maken [!DNL Amazon Redshift] met Experience Platform via API&#39;s

- [Connect Amazon Opnieuw overschakelen naar Experience Platform met behulp van de Flow Service API](../../tutorials/api/create/databases/redshift.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL Amazon Redshift] met Experience Platform via de gebruikersinterface

- [Een Amazon Redshift-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/redshift.md)
- [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
