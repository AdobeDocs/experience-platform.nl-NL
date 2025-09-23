---
title: Source-overzicht van Merkury Enterprise Identity
description: Leer hoe u Merkury Enterprise Identity Resolution via de gebruikersinterface kunt verbinden met Adobe Experience Platform.
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

Adobe Experience Platform biedt ondersteuning voor het opnemen van gegevens van een toepassing voor gegevenspartners. Ondersteuning voor gegevenspartners is [!DNL Merkury Enterprise Identity Resolution] .

U kunt [!DNL Merkury] door [!DNL Merkle] gebruiken om meer digitale bezoekers te herkennen - zelfs zonder het gebruik van cookies - en de relevante en gepersonaliseerde ervaringen te leveren die de klant nodig heeft.

U kunt **persoonsidentiteitskaart** als deel van de [!DNL Merkury] bron gebruiken om alles te combineren dat uw organisatie over een individu in één enkel uitvoerig profiel kent. Deze details kunnen zijn:

- Digitaal gedrag
- Kopervoorkeuren
- Gegevens identificeren zoals een naam, e-mailadres, fysiek adres of apparaat-id.

U kunt ingesloten gegevens opmaken als JSON, XDM Parquet of gescheiden Experience Data Model (XDM). Elke stap van het proces is geïntegreerd in het werk van bronnen

![ een illustratie van het werkschema van de gegevensverwerking voor de bron van de Merkury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## IP adres lijst van gewenste personen

Alvorens u bronschakelaars kunt gebruiken, moet u de vereiste IP adressen voor uw gebied aan uw lijst van gewenste personen toevoegen. Als u deze IP adressen niet toevoegt, kunnen de bronschakelaars niet correct werken of fouten veroorzaken. Voor gedetailleerde instructies en de lijst van IP adressen om toe te staan, lees de [ IP pagina van de adreslijst van gewenste personen ](../../ip-address-allow-list.md).

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

Door dit document te lezen, hebt u de vereiste instellingen voltooid om gegevens van uw [!DNL Merkury] -account naar Experience Platform te kunnen verzenden. U kunt aan de gids nu te werk gaan op [ verbindend  [!DNL Merkury]  met Experience Platform gebruikend het gebruikersinterface ](../../tutorials/ui/create/data-partners/merkury.md).
