---
title: Overzicht Snowflake Source Connector
description: Leer hoe u Snowflake met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: df066463-1ae6-4ecd-ae0e-fb291cec4bd5
source-git-commit: 573691db9f71fcbe8b5edd4ea647d718ab3784e4
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 0%

---

# [!DNL Snowflake] bron

>[!IMPORTANT]
>
>* De [!DNL Snowflake] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.
>* Standaard wordt [!DNL Snowflake] source `null` geïnterpreteerd als een lege tekenreeks. Neem contact op met uw Adobe-vertegenwoordiger om ervoor te zorgen dat de `null` -waarden correct worden geschreven zoals `null` in Adobe Experience Platform.
>* Experience Platform kan alleen gegevens invoeren als tijdzones voor alle batchbronnen op basis van tabellen zijn geconfigureerd voor UTC. Het enige tijdstempel dat wordt ondersteund voor de [!DNL Snowflake] -bron is TIMESTAMP_NTZ met UTC-tijd.

>[!WARNING]
>
>De basisauthentificatie (of de authentificatie van de rekeningssleutel) voor [!DNL Snowflake] bron zal op November 2025 worden afgekeurd. U moet naar op sleutel-paar gebaseerde authentificatie bewegen om de bron te blijven gebruiken en gegevens van uw gegevensbestand in te voeren aan Experience Platform. Voor meer informatie over de veroudering, lees de [[!DNL Snowflake]  beste praktijkgids bij het verlichten van de risico&#39;s van credentieel compromis ](https://www.snowflake.com/en/resources/white-paper/best-practices-to-mitigate-the-risk-of-credential-compromise/).

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens uit een database van derden. Experience Platform kan verbinding maken met verschillende typen databases, zoals relationele databases, NoSQL-databases of gegevensopslagruimten. Ondersteuning voor databaseproviders is onder andere [!DNL Snowflake] .

## Vereisten {#prerequisites}

In deze sectie worden de instellingstaken beschreven die u moet uitvoeren voordat u de [!DNL Snowflake] -bron kunt verbinden met Experience Platform.

### Uw account-id ophalen {#retrieve-your-account-identifier}

U moet uw account-id ophalen van het [!DNL Snowflake] UI-dashboard omdat u de account-id gebruikt om uw [!DNL Snowflake] -instantie op Experience Platform te verifiëren.

Uw account-id ophalen:

* Navigeer aan uw rekening op het [[!DNL Snowflake]  toepassingsUI dashboard ](https://app.snowflake.com/).
* Selecteer in de linkernavigatie **[!DNL Accounts]** , gevolgd door **[!DNL Active Accounts]** in de koptekst.
* Selecteer vervolgens het informatiepictogram en selecteer en kopieer de domeinnaam van de huidige URL.

![ het dashboard van Snowflake UI met de geselecteerde domeinnaam.](../../images/tutorials/create/snowflake/snowflake-dashboard.png)

### Persoonlijke sleutel ophalen {#retrieve-your-private-key}

Als u sleutelparverificatie gebruikt voor uw [!DNL Snowflake] -verbinding, moet u ook uw persoonlijke sleutel genereren voordat u verbinding maakt met Experience Platform.

>[!BEGINTABS]

>[!TAB  creeer een gecodeerde privé sleutel ]

Voer de volgende opdracht op uw terminal uit om de gecodeerde [!DNL Snowflake] persoonlijke sleutel te genereren:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -v2 des3 -inform PEM -out rsa_key.p8
```

Als dit lukt, ontvangt u de persoonlijke sleutel in de PEM-indeling.

```shell
-----BEGIN ENCRYPTED PRIVATE KEY-----
MIIE6T...
-----END ENCRYPTED PRIVATE KEY-----
```

>[!TAB  creeer een niet gecodeerde privé sleutel ]

Als u de niet-gecodeerde [!DNL Snowflake] persoonlijke sleutel wilt genereren, voert u de volgende opdracht uit op uw terminal:

```shell
openssl genrsa 2048 | openssl pkcs8 -topk8 -inform PEM -out rsa_key.p8 -nocrypt
```

Als dit lukt, ontvangt u de persoonlijke sleutel in de PEM-indeling.

```shell
-----BEGIN PRIVATE KEY-----
MIIE6T...
-----END PRIVATE KEY-----
```

>[!ENDTABS]

Neem vervolgens uw persoonlijke sleutel en codeer deze in [!DNL Base64] . Zorg ervoor dat u geen transformaties of opmaakconversies uitvoert op de persoonlijke sleutel van [!DNL Snowflake] . Bovendien moet u ervoor zorgen dat er geen navolgende nieuwe-regeltekens aan het einde van de persoonlijke sleutel staan voordat u deze codeert in [!DNL Base64] .

### Configuraties verifiëren

Voordat u een bronverbinding voor uw [!DNL Snowflake] gegevens kunt maken, moet u ook controleren of aan de volgende configuraties is voldaan:

* Het standaardpakhuis dat aan een bepaalde gebruiker wordt toegewezen moet het zelfde zijn als het pakhuis dat u wanneer het voor authentiek verklaren aan Experience Platform invoert.
* De standaardrol die aan een bepaalde gebruiker wordt toegewezen moet toegang tot het zelfde gegevensbestand hebben dat u wanneer het voor authentiek verklaren aan Experience Platform invoert.

Om uw rol en pakhuis te verifiëren:

* Selecteer **[!DNL Admin]** in de linkernavigatie en selecteer vervolgens **[!DNL Users & Roles]** .
* Selecteer de juiste gebruiker en selecteer vervolgens de ellipsen (`...`) in de rechterbovenhoek.
* Navigeer in het [!DNL Edit user] -venster dat wordt weergegeven naar [!DNL Default Role] om de rol weer te geven die aan de opgegeven gebruiker is gekoppeld.
* Navigeer in hetzelfde venster naar [!DNL Default Warehouse] om het pakhuis weer te geven dat aan de opgegeven gebruiker is gekoppeld.

![ Snowflake UI waar u uw rol en pakhuis kunt verifiëren.](../../images/tutorials/create/snowflake/snowflake-configs.png)

Nadat de codering is voltooid, kunt u die [!DNL Base64] gecodeerde persoonlijke sleutel op Experience Platform gebruiken om uw [!DNL Snowflake] -account te verifiëren.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Snowflake] en Experience Platform via API&#39;s of de gebruikersinterface:

## Verbinding maken [!DNL Snowflake] met Experience Platform via API&#39;s

* [Een Snowflake-basisverbinding maken met de Flow Service API](../../tutorials/api/create/databases/snowflake.md)
* [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
* [Een gegevensstroom maken voor een databasebron met behulp van de Flow Service API](../../tutorials/api/collect/database-nosql.md)

## Verbinding maken [!DNL Snowflake] met Experience Platform via de gebruikersinterface

* [Een Snowflake-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/databases/snowflake.md)
* [Een gegevensstroom maken voor een databasebronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/databases.md)
