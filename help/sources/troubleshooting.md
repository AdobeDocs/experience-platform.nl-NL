---
keywords: Experience Platform;huis;populaire onderwerpen;bronnen;opname;het oplossen van problemen;bronnen het oplossen van problemen;bronnen faq;faq;bron schakelaars;bron schakelaar;bron schakelaars komt voor;bron schakelaars het oplossen van problemen; bron schakelaars;
solution: Experience Platform
title: Bronoplossing
topic-legacy: troubleshooting
description: Dit document bevat antwoorden op veelgestelde vragen over bronnen op Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# (Bèta) de gids van het oplossen van problemenproblemen van Bronnen

Dit document bevat antwoorden op veelgestelde vragen over bronnen op Adobe Experience Platform. Raadpleeg de [handleiding voor het oplossen van Experience Platforms](../landing/troubleshooting.md) voor vragen en problemen met betrekking tot andere [!DNL Platform]-services, inclusief de services die worden aangetroffen in alle [!DNL Platform]-API&#39;s.

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over bronnen.

### Moet ik wijzigingen aanbrengen in onze instellingen voor netwerkbeveiliging om bronnen in te schakelen?

U kunt bepaalde IP adressen moeten lijsten van gewenste personen om bronnen toe te laten. Lees voor meer informatie de documentatie op de specifieke bronaansluiting.

### Welke authentificatietypen door bronnen worden gesteund?

De bronnen kunnen door verbindingskoorden, gebruikersnamen en wachtwoorden, of toegangstokens en sleutels voor authentiek worden verklaard. Specifieke details over gesteunde authentificatietypen kunnen in de documentatie van de gespecificeerde bronschakelaar worden gevonden.

### Waarom schiet al mijn recente stroom tekort?

Als u opmerkt dat al uw recente stroomlooppas ontbreekt, kunnen uw geloofsbrieven of veranderd of verlopen zijn. U kunt dit probleem verhelpen door de verbinding met de meest recente gegevens bij te werken.

### Welke bestandstypen worden ondersteund?

Momenteel zijn de ondersteunde bestandstypen gescheiden bestanden, JSON en Parquet.

### Wat zijn de beperkingen op bestandsnamen en -grootten?

Hieronder volgt een lijst met beperkingen die u voor bestanden in bronnen moet opgeven.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 besturen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).
- Het maximumaantal bestanden per batch is 1500, met een maximale batch-grootte van 100 GB.
- Het maximumaantal eigenschappen of velden per rij is 10.000.
- Het maximumaantal batches dat per gebruiker kan worden verzonden, per minuut is 138.

### Welke gegevenstypen worden ondersteund?

Tot de ondersteunde gegevenstypen behoren gehele getallen, tekenreeksen, booleans, datetime-objecten, arrays en objecten.

### Welke datum- en tijdnotaties worden ondersteund?

De bronnen steunen een grote verscheidenheid van datetime formaten terwijl het opnemen van gegevens. Meer informatie over ondersteunde datetime-indelingen vindt u in de datumsectie van de [handleiding voor de verwerking van gegevensindelingen](../data-prep/data-handling.md#dates) in de Prep-documentatie voor gegevens.

### Hoe kan ik arrays opmaken in CSV-, JSON- en Parquet-bestanden?

JSON- en Parquet-bestanden bieden native ondersteuning voor arrays. Voor vlakke structuren, zoals CSV&#39;s, worden arrays niet ondersteund. Tekenreeksen met meerdere waarden kunnen echter worden opgedeeld in een array, waarbij gebruik wordt gemaakt van prep-functies, zoals exploderen en samenvoegen. Meer informatie over deze functies van het gegevensvoorvoegsel vindt u in de [handleiding voor functies van het gegevensvoorvoegsel](../data-prep/functions.md#string)

### Welke bronnen ondersteunen gedeeltelijke inname?

Alle bronnen van inname in de batch ondersteunen gedeeltelijke inname. Bij streamingbronnen wordt gedeeltelijke inname echter niet ondersteund.

### Wanneer moet ik gedeeltelijke inname gebruiken?

Gedeeltelijke inname moet worden gebruikt als u **geen** beperkingen heeft, zoals het hebben van het volledige dossier dat in Platform wordt opgenomen. U kunt ook gedeeltelijke inname gebruiken als u er geen moeite mee hebt gegevens in te voeren die fouten erin kunnen bevatten.

### Wat is de typische drempel voor gedeeltelijke inname?

Er is geen &quot;typische foutendrempel&quot;voor gedeeltelijke inname. In plaats daarvan kan deze waarde variëren van het gebruik van hoofdletters en kleine letters. Standaard is de foutdrempel ingesteld op 5%.
