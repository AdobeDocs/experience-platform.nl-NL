---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform oktober 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: ab87cac94ae69acde3be75ae95b11cf003a274e9
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: Oktober 2020**

- [Gegevensprep](#data-prep)
- [Bronnen](#sources)

## Gegevensprep {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| `is_set` -functie | Met de `is_set` functie kunt u de aanwezigheid van een kenmerk in de brongegevens controleren. `is_set` kan worden gebruikt in combinatie met `is_empty` om zowel de aanwezigheid van het kenmerk als de aanwezigheid van de waarde binnen het kenmerk te controleren. |
| `get_values` -functie | Met de `get_values` functie kunt u de waarden van de invoerkaart voor een bepaalde toets ophalen. |

Lees voor meer informatie het overzicht [van de](../../data-prep/home.md)Data Prep.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Hiërarchische toewijzing | U kunt een hiërarchisch bronbestand, zoals JSON of Parquet, voorvertonen tijdens het invoeren van gegevens. |
| SSH-verificatieondersteuning voor SFTP | U kunt uw rekening SFTP met het [!DNL Platform] gebruiken van RSA/DSA Open SSH sleutels verbinden. Zie het [SFTP-overzicht](../../sources/connectors/cloud-storage/ftp-sftp.md) voor meer informatie. |
| UX-verbeteringen | U kunt uw dataset voor [!DNL Profile] tijdens het proces van gegevensinvoer toelaten. Raadpleeg de zelfstudie over de workflow [](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) voor gegevens over cloudopslag voor meer informatie. |

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.