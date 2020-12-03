---
keywords: Experience Platform;home;popular topics;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Verbinding maken met PSQL
topic: connect
description: 'PSQL is een opdrachtregelinterface die wordt weergegeven wanneer u Postgres op uw computer installeert. U kunt het installeren door deze instructies te volgen. '
translation-type: tm+mt
source-git-commit: 8ffe7c68c87cacb6b54d9634a5204fa24a9986ac
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Verbinding maken met PSQL

PSQL is een opdrachtregelinterface die wordt geleverd wanneer u [!DNL Postgres] op uw computer installeert. U kunt het installeren door deze instructies te volgen.

## Postcodes installeren op een Mac

Open een eindvenster en geef deze drie bevelen uit:

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Na het uitgeven van deze bevelen, zou u het volgende moeten zien:

```shell
/usr/local/bin/psql
```

## Installeren [!DNL Postgres] op een pc

Download en installeer [!DNL Postgres] vanaf deze [locatie](https://www.postgresql.org/download/windows/).

De padvariabele bewerken:

![Image](../images/clients/psql/path.png)

Voeg de twee getoonde lijnen toe die &quot;[!DNL Postgres].&quot;omvatten

Sla de updates op en open vervolgens een opdrachtprompt en typ:

```shell
psql -V
```

Je zou iets als dit moeten zien:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL en [!DNL Query Service]

Ga terug naar de [!DNL Platform] gebruikersinterface op de pagina Tools **[!UICONTROL voor]** Connect BI.

Klik **[!UICONTROL exemplaar]** voor **[!UICONTROL Bevel]** PSQL.

![Image](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]
>
>Als u op PC bent, gebruik een tekstredacteur om de lijnonderbrekingen in het bevelkoord te verwijderen, dan kopieer het koord. Als u versie 12.0 of hoger gebruikt, moet u bovendien een verbindingstekenreeks toevoegen `PGGSSENCMODE=disable` aan de verbindingstekenreeks.

Plak de opdrachttekenreeks in een terminal- of opdrachtvenster en druk op Enter.

U zou een resultaat als dit moeten zien:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Als u versie 10.5 of hoger niet ziet, moet u die versie of nieuwer downloaden.