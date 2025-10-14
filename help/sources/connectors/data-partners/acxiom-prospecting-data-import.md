---
title: Importeren van Acrobat-perspectiefgegevens
description: Leer hoe u via de gebruikersinterface verbinding maakt met Acrobat Prospecting Data naar Adobe Experience Platform en Adobe Real-Time Customer Data Platform.
exl-id: 6df674d9-c14b-42ea-a287-5377484e567d
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# [!DNL Acxiom Prospecting Data Import]

Adobe Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor gegevenspartners. Ondersteuning voor gegevens- en identiteitspartners is inclusief [!DNL Acxiom Prospecting Data Import] .

De [!DNL Acxiom] -programma voor het doorvoeren van gegevens voor Adobe Real-Time Customer Data Platform is een proces voor het bieden van het meest productieve mogelijke publiek. [!DNL Acxiom] gebruikt Real-Time CDP-gegevens van de eerste partij via een beveiligde exportbewerking en voert deze gegevens uit via een bekroond systeem voor het oplossen van hygiëne en identiteit. Een gegevensbestand dat als onderdrukkingslijst kan worden gebruikt wordt geproduceerd. Dit gegevensbestand wordt dan aangepast aan het [!DNL Acxiom Global] gegevensbestand, dat toelaat dat de perspectieflijsten worden aangepast voor de invoer.

U kunt de [!DNL Acxiom] -bron gebruiken om reacties van de [!DNL Acxiom] perspectiefservice op te halen en toe te wijzen met [!DNL Amazon S3] als een neerzetpunt.

![&#x200B; acxiom-prospecting-workflow &#x200B;](../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/acxiom-prospecting.png)

Lees het onderstaande document voor informatie over hoe u uw [!DNL Acxiom Prospecting Data Import] bronaccount kunt instellen.

## Vereisten

Als u toegang wilt tot uw emmertje op Experience Platform, moet u geldige waarden opgeven voor de volgende referenties:

| Credentials | Beschrijving |
| --- | --- |
| [!DNL Acxiom] verificatiesleutel | De verificatiesleutel. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| [!DNL Amazon S3] toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| [!DNL Amazon S3] geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen van het team van [!DNL Acxiom] . |

## IP adres lijst van gewenste personen

Alvorens u bronschakelaars kunt gebruiken, moet u de vereiste IP adressen voor uw gebied aan uw lijst van gewenste personen toevoegen. Als u deze IP adressen niet toevoegt, kunnen de bronschakelaars niet correct werken of fouten veroorzaken. Voor gedetailleerde instructies en de lijst van IP adressen om toe te staan, lees de [&#x200B; IP pagina van de adreslijst van gewenste personen &#x200B;](../../ip-address-allow-list.md).

### Machtigingen configureren voor Experience Platform

U moet zowel **[!UICONTROL View Sources]** - als **[!UICONTROL Manage Sources]** -machtigingen hebben ingeschakeld voor uw account om uw [!DNL Acxiom Prospecting Data Import] -account te kunnen verbinden met Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Voor meer informatie, lees de [&#x200B; gids UI van de toegangscontrole &#x200B;](../../../access-control/abac/ui/permissions.md).

## Naamgevingsbeperkingen voor bestanden en mappen

Met de onderstaande beperkingen moet rekening worden gehouden bij de naamgeving van uw cloudopslagbestand of -map:

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens zijn niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [&#x200B; RFC 2616, Sectie 2.2: BasisRegels &#x200B;](https://www.ietf.org/rfc/rfc2616.txt) en [&#x200B; RFC 3987 &#x200B;](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid die nodig zijn om gegevens van uw [!DNL Acxiom] -account naar Experience Platform te kunnen verzenden. U kunt aan de gids nu te werk gaan op [&#x200B; verbindend  [!DNL Acxiom Prospecting Data Import]  met Experience Platform gebruikend het gebruikersinterface &#x200B;](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).
