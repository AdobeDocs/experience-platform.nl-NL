---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbinding maken met PSQL
topic: connect
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Verbinding maken met PSQL

PSQL is een opdrachtregelinterface die wordt weergegeven wanneer u Postgres op uw computer installeert. U kunt het installeren door deze instructies te volgen.

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

## Postcodes installeren op een pc

Download en installeer Postgres vanaf deze [locatie](https://www.postgresql.org/download/windows/).

De padvariabele bewerken:

![Afbeelding](../images/clients/psql/path.png)

Voeg de twee getoonde lijnen toe die &quot;Postgres.&quot;omvatten

Sla de updates op en open vervolgens een opdrachtprompt en typ:

```shell
psql -V
```

Je zou iets als dit moeten zien:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL en Query Service

Ga terug naar de interface Platform op de pagina &quot;Connect BI Tools&quot;.

Klik op **kopie** voor &quot;PSQL-opdracht&quot;.

![Afbeelding](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]: Als u op PC bent, gebruik een tekstredacteur om de lijnonderbrekingen in het bevelkoord te verwijderen, dan kopieer het koord.

Plak de opdrachttekenreeks in een terminal- of opdrachtvenster en druk op Enter.

U zou een resultaat als dit moeten zien:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Als u versie 10.5 of hoger niet ziet, moet u die versie of nieuwer downloaden.