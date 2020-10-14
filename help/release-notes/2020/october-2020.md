---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform oktober 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 43ceda3d95511c3972fd0588f472c6c412dd95bf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 2%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 14 oktober 2020**

- [Gegevensprep](#data-prep)
- [Klantprofiel in realtime](#profile)
- [Bronnen](#sources)

## Gegevensprep {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ------- | ----------- |
| `is_set` -functie | Met de `is_set` functie kunt u de aanwezigheid van een kenmerk in de brongegevens controleren. `is_set` kan worden gebruikt in combinatie met `is_empty` om zowel de aanwezigheid van het kenmerk als de aanwezigheid van de waarde binnen het kenmerk te controleren. |
| `get_values` -functie | Met de `get_values` functie kunt u de waarden van de invoerkaart voor een bepaalde toets ophalen. |

Lees voor meer informatie het overzicht [van de](../../data-prep/home.md)Data Prep.

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-time Customer Profile], kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| ------- | ----------- |
| API-uitbreidingen voor voorvertoning van profiel | De API (`/previewsamplestatus`) voor de voorvertoning van profielen bevat nu de mogelijkheid om een uitsplitsing te bekijken van de totale profielfragmenten in uw IMS-organisatie en om de distributie van profielfragmenten in verschillende naamruimten te bekijken. |
| Updates van de Unieschemaweergave | In het Experience Platform UI, kunnen de gebruikers informatie over alle schema&#39;s en datasets gemakkelijker vinden die tot het unieschema bijdragen, evenals oppervlakte zeer belangrijke attributen zoals identiteit en relatievelden. Deze updates verbeteren de capaciteit om problemen op te lossen en te bevestigen dat de profielen correct worden gevormd, worden de identiteiten correct vastgemaakt, en de gegevens zijn met succes opgenomen. |

Lees voor meer informatie over [!DNL Real-time Customer Profile], waaronder zelfstudies en aanbevolen procedures voor het werken met [!DNL Profile] gegevens, het overzicht [](../../profile/home.md)van het realtime-klantprofiel.

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