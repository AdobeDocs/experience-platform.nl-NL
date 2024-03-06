---
title: Importeren van Acrobat-perspectiefgegevens
description: Leer hoe u via de gebruikersinterface verbinding maakt met Acrobat Prospecting Data naar Adobe Experience Platform en Adobe Real-time Customer Data Platform.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>De [!DNL Acxiom Prospecting Data Import] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor gegevenspartners. De steun van gegevens en identiteitspartners omvat [!DNL Acxiom Prospecting Data Import].

[!DNL Acxiom]De &#39;Prospecting Data Import for Adobe Real-time Customer Data Platform&#39; is een proces om het meest productieve mogelijke publiek te bieden. [!DNL Acxiom] neemt de gegevens van de eerste partij van Real-Time CDP via een veilige uitvoer en voert die gegevens door een bekroond systeem van hygiëne en identiteitsresolutie uit. Een gegevensbestand dat als onderdrukkingslijst kan worden gebruikt wordt geproduceerd. Dit gegevensbestand komt dan overeen met [!DNL Acxiom Global] gegevensbestand, dat toelaat dat de perspectieflijsten voor de invoer worden aangepast.

U kunt de [!DNL Acxiom] bron om reacties van de [!DNL Acxiom] de dienst van het vooruitzicht gebruikend [!DNL Amazon S3] als een neerzetpunt.

## Vereisten

Om tot uw emmer op Experience Platform toegang te hebben, moet u geldige waarden voor de volgende geloofsbrieven verstrekken:

| Credentials | Beschrijving |
| --- | --- |
| [!DNL Acxiom] verificatiesleutel | De verificatiesleutel. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| [!DNL Amazon S3] toegangstoets | De toegangs belangrijkste identiteitskaart voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| [!DNL Amazon S3] geheime sleutel | De geheime sleutel-id voor uw emmer. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |
| Naam van emmertje | Dit is uw emmertje waar de dossiers zullen worden gedeeld. U kunt deze waarde ophalen uit het dialoogvenster [!DNL Acxiom] team. |

### Machtigingen

U moet beide hebben **[!UICONTROL View Sources]** en **[!UICONTROL Manage Sources]** machtigingen die zijn ingeschakeld voor uw account om verbinding te maken met uw [!DNL Acxiom Prospecting Data Import] aan Experience Platform. Neem contact op met de productbeheerder om de benodigde machtigingen te verkrijgen. Lees voor meer informatie de [gebruikershandleiding voor toegangsbeheer](../../../access-control/abac/ui/permissions.md).

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Met de onderstaande beperkingen moet rekening worden gehouden bij de naamgeving van uw cloudopslagbestand of -map:

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens zijn niet toegestaan. Codepunten zoals `\uE000`zijn, hoewel geldig in NTFS-bestandsnamen, geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [RFC 2616, afdeling 2.2: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Volgende stappen

Door dit document te lezen, hebt u de vereiste setup voltooid die nodig is om gegevens van uw [!DNL Acxiom] aan Experience Platform. U kunt nu doorgaan naar de handleiding op [verbinden [!DNL Acxiom Prospecting Data Import] naar Experience Platform via de gebruikersinterface](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).