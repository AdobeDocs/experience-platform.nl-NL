---
title: Source-overzicht van Merkury Enterprise Identity
description: Leer hoe u Merkury Enterprise Identity Resolution via de gebruikersinterface kunt verbinden met Adobe Experience Platform.
last-substantial-update: 2023-12-12T00:00:00Z
badge: Beta
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>De bron [!DNL Merkury Enterprise Identity Resolution] is in bèta. Gelieve te lezen het [ overzicht van bronnen ](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde bronnen.

Adobe Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor gegevenspartners. Ondersteuning voor gegevenspartners is [!DNL Merkury Enterprise Identity Resolution] .

U kunt [!DNL Merkury] door [!DNL Merkle] gebruiken om meer digitale bezoekers te herkennen - zelfs zonder het gebruik van cookies - en de relevante en gepersonaliseerde ervaringen te leveren die de klant nodig heeft.

U kunt **persoonsidentiteitskaart** als deel van de [!DNL Merkury] bron gebruiken om alles te combineren dat uw organisatie over een individu in één enkel uitvoerig profiel kent. Deze details kunnen zijn:

- digitaal gedrag
- aankoopvoorkeuren
- identificeert informatie zoals een naam, e-mailadres, fysiek adres of apparaat-id.

U kunt ingesloten gegevens opmaken als JSON, XDM Parquet of gescheiden Experience Data Model (XDM). Elke stap van het proces is geïntegreerd in het werk van bronnen

![ een illustratie van het werkschema van de gegevensverwerking voor de bron van de Merkury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [&#128279;](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0&rbrace; IP adres &lbrace;voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Vereisten

U moet aan de volgende voorwaarden voldoen voordat u de [!DNL Merkury] -bron kunt gebruiken:

- U moet de installatie van [!DNL Merkury] voltooien met uw [!DNL Merkury] -team.
- U moet uw geloofsbrieven (toegangssleutel, geheime sleutel, en emmer naam) van uw [!DNL Merkury] team terugwinnen. 

>[!NOTE]
>
>Een bestandspad als `myBucket/folder/subfolder/subsubfolder/abc.csv` kan ertoe leiden dat u alleen toegang krijgt tot `subsubfolder/abc.csv` . Als u toegang wilt krijgen tot de submap, kunt u de parameter bucket opgeven als myBucket en de folderPath als map/submap om ervoor te zorgen dat de bestandsexploratie start in submap in tegenstelling tot `subsubfolder/abc.csv` .

## Volgende stappen

Door dit document te lezen, hebt u de vereiste instellingen voltooid om gegevens van uw [!DNL Merkury] -account naar het Experience Platform te kunnen verzenden. U kunt aan de gids nu te werk gaan op [ verbindend  [!DNL Merkury]  met Experience Platform gebruikend het gebruikersinterface ](../../tutorials/ui/create/data-partners/merkury.md).
