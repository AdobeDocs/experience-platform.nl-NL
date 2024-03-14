---
title: Acxiale gegevensinname
description: Leer hoe u kunt innemen [!DNL Acxiom] gegevens naar Real-time Customer Data Platform, verrijken profielen van eerste partijen, verbeteren het publiek en activeren via marketingkanalen.
badge: Beta
source-git-commit: 9419da451616ca7f087ecea7aa66a6c10a474fb3
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>De [!DNL Acxiom Prospecting Data Import] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Gebruik de [!DNL Acxiom Data Ingestion] bron voor invoer [!DNL Acxiom] gegevens naar Real-time Customer Data Platform en verrijken profielen van eerste partijen. Vervolgens kunt u uw [!DNL Acxiom]- verrijkte first-party profielen om publiek te verbeteren en over marketing kanalen te activeren.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Lees het onderstaande document voor meer informatie over het instellen van uw [!DNL Acxiom Data Ingestion] bronaccount.

## Vereisten {#prerequisites}

Als u verbinding wilt maken met uw [!DNL Acxiom Data Ingestion] account aan Experience Platform, moet u waarden opgeven voor de volgende verificatiereferenties:

| Credentials | Beschrijving |
| --- | --- |
| [!DNL Acxiom] verificatiesleutel | De verificatiesleutel. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| [!DNL Amazon S3] toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| [!DNL Amazon S3] geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

### Machtigingen configureren voor Experience Platform

U moet beide hebben **[!UICONTROL View Sources]** en **[!UICONTROL Manage Sources]** machtigingen die zijn ingeschakeld voor uw account om verbinding te maken met uw [!DNL Acxiom Data Ingestion] aan Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Lees voor meer informatie de [gebruikershandleiding voor toegangsbeheer](../../../access-control/ui/overview.md).

### Naamgevingsbeperkingen voor bestanden en mappen

Met de onderstaande beperkingen moet rekening worden gehouden bij de naamgeving van uw cloudopslagbestand of -map:

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens zijn niet toegestaan. Codepunten zoals `\uE000`zijn, hoewel geldig in NTFS-bestandsnamen, geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [RFC 2616, afdeling 2.2: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Volgende stappen

Door dit document te lezen, hebt u de vereiste setup voltooid die nodig is om gegevens van uw [!DNL Acxiom] aan Experience Platform. U kunt nu doorgaan naar de handleiding op [verbinden [!DNL Acxiom Data Ingestion] naar Experience Platform via de gebruikersinterface](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
