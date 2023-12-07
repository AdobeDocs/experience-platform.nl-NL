---
title: Overzicht van de Merkury Enterprise Identity Resolution Source
description: Leer hoe u Merkury Enterprise Identity Resolution via de gebruikersinterface kunt verbinden met Adobe Experience Platform.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: bf6a3422d9af6eaa4f3f4a8a573dc587b3cfdbd5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>De [!DNL Merkury Enterprise Identity Resolution] De bron is in bèta. Lees de [overzicht van bronnen](../../home.md#terms-and-conditions) voor meer informatie over het gebruik van bronnen met een bètalabel.

Adobe Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor gegevenspartners. De steun van gegevenspartners omvat [!DNL Merkury Enterprise Identity Resolution].

U kunt [!DNL Merkury] door [!DNL Merkle] om meer digitale bezoekers te herkennen - zelfs zonder het gebruik van cookies - en de relevante en gepersonaliseerde ervaringen te leveren die de klant nodig heeft.

U kunt de **persoon-id** als onderdeel van de [!DNL Merkury] bron om alles wat uw organisatie weet over een individu te combineren in één volledig profiel. Deze details kunnen zijn:

- digitaal gedrag
- aankoopvoorkeuren
- identificeert informatie zoals een naam, e-mailadres, fysiek adres of apparaat-id.

U kunt ingesloten gegevens opmaken als JSON, XDM Parquet of gescheiden Experience Data Model (XDM). Elke stap van het proces is geïntegreerd in het werk van bronnen

![Een voorbeeld van de gegevensverwerkingsworkflow voor de Merkury-bron.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP adres lijst van gewenste personen](../../ip-address-allow-list.md) voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000`zijn, hoewel geldig in NTFS-bestandsnamen, geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [RFC 2616, afdeling 2.2: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Vereisten

U moet aan de volgende voorwaarden voldoen voordat u kunt gaan werken met de [!DNL Merkury] bron:

- U moet uw [!DNL Merkury] instellen met uw [!DNL Merkury] team.
- U moet uw geloofsbrieven (toegangstoets, geheime sleutel, en emmernaam) van uw terugwinnen [!DNL Merkury] team. 

>[!NOTE]
>
>Bestandspad als `myBucket/folder/subfolder/subsubfolder/abc.csv` kan ertoe leiden dat u slechts toegang hebt `subsubfolder/abc.csv`. Als u toegang wilt krijgen tot de submap, kunt u de parameter bucket opgeven als myBucket en de folderPath als map/submap om ervoor te zorgen dat de bestandsexploratie start in submap in plaats van `subsubfolder/abc.csv`.

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid die nodig zijn om gegevens van uw [!DNL Merkury] aan Experience Platform. U kunt nu doorgaan naar de handleiding op [verbinden [!DNL Merkury] naar Experience Platform via de gebruikersinterface](../../tutorials/ui/create/data-partners/merkury.md).
