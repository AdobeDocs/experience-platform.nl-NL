---
title: Overzicht Snowflake Source Connector
description: Leer hoe u Snowflake met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 8b0f6eca87deedd8090830e3375d5099bfb0dfc0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Snowflake] bron

>[!IMPORTANT]
>
>* De [!DNL Snowflake] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.
>* Standaard wordt [!DNL Snowflake] source `null` geïnterpreteerd als een lege tekenreeks. Neem contact op met uw Adobe om ervoor te zorgen dat de `null` -waarden correct worden geschreven zoals `null` in Adobe Experience Platform.
>* Voor Experience Platform om gegevens in te voeren, moeten de tijdzones voor alle op lijst-gebaseerde partijbronnen aan UTC worden gevormd. Het enige tijdstempel dat wordt ondersteund voor de [!DNL Snowflake] -bron is TIMESTAMP_NTZ met UTC-tijd.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform verleent steun voor het opnemen van gegevens van een derdegegevensbestand. Het platform kan met verschillende types van gegevensbestanden zoals relationeel, NoSQL, of gegevenspakhuizen verbinden. Ondersteuning voor databaseproviders is onder andere [!DNL Snowflake] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Snowflake] en Platform via API&#39;s of de gebruikersinterface:

## Verbinding maken [!DNL Snowflake] met platform met behulp van API&#39;s

* [Een basisverbinding voor Snowflaken maken met de Flow Service API](../../tutorials/api/create/databases/snowflake.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL Snowflake] met platform via de gebruikersinterface

* [Een Snowflake-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/snowflake.md)
* [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
