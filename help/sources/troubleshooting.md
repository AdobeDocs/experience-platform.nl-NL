---
keywords: Experience Platform;huis;populaire onderwerpen;bronnen;opname;het oplossen van problemen;bronnen het oplossen van problemen;bronnen faq;faq;bron schakelaars;bron schakelaar;bron schakelaars komt voor;bron schakelaars het oplossen van problemen; bron schakelaars;
solution: Experience Platform
title: Bronoplossing
topic-legacy: troubleshooting
description: Dit document bevat antwoorden op veelgestelde vragen over bronnen op Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: b55097b6e7cd49166f68d0c86b788cd36ebdebab
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Bronhulp voor probleemoplossing

Dit document bevat antwoorden op veelgestelde vragen over bronnen op Adobe Experience Platform. Voor vragen en problemen met betrekking tot andere problemen [!DNL Platform] services, inclusief services die overal worden aangetroffen [!DNL Platform] API&#39;s, raadpleeg de [Handleiding voor het oplossen van problemen met Experience Platforms](../landing/troubleshooting.md).

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
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000`zijn, hoewel geldig in NTFS-bestandsnamen, geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [RFC 2616, punt 2.2: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).
- Het maximumaantal bestanden per batch is 1500, met een maximale batch-grootte van 100 GB.
- Het maximumaantal eigenschappen of velden per rij is 10.000.
- Het maximumaantal batches dat per gebruiker kan worden verzonden, per minuut is 138.

### Welke gegevenstypen worden ondersteund?

Tot de ondersteunde gegevenstypen behoren gehele getallen, tekenreeksen, booleans, datetime-objecten, arrays en objecten.

### Welke datum- en tijdnotaties worden ondersteund?

De bronnen steunen een grote verscheidenheid van datetime formaten terwijl het opnemen van gegevens. Meer informatie over ondersteunde datumnotaties vindt u in het gedeelte met datums van het dialoogvenster [handleiding voor gegevensverwerking](../data-prep/data-handling.md#dates) in de documentatie van de Prep van Gegevens.

### Hoe kan ik arrays opmaken in CSV-, JSON- en Parquet-bestanden?

JSON- en Parquet-bestanden bieden native ondersteuning voor arrays. Voor vlakke structuren, zoals CSV&#39;s, worden arrays niet ondersteund. Tekenreeksen met meerdere waarden kunnen echter worden opgedeeld in een array, waarbij gebruik wordt gemaakt van prep-functies, zoals exploderen en samenvoegen. Meer informatie over deze functies van het gegevensvoorvoegsel vindt u in de [handleiding voor functies voor gegevenprep](../data-prep/functions.md#string)

### Welke bronnen ondersteunen gedeeltelijke inname?

Alle bronnen van inname in de batch ondersteunen gedeeltelijke inname. Bij streamingbronnen wordt gedeeltelijke inname echter niet ondersteund.

### Wanneer moet ik gedeeltelijke inname gebruiken?

Gedeeltelijke inname dient te worden gebruikt als u **niet** U hebt beperkingen, zoals het opnemen van het gehele bestand in het Platform. U kunt ook gedeeltelijke inname gebruiken als u er geen moeite mee hebt gegevens in te voeren die fouten erin kunnen bevatten.

### Wat is de typische drempel voor gedeeltelijke inname?

Er is geen &quot;typische foutendrempel&quot;voor gedeeltelijke inname. In plaats daarvan kan deze waarde variëren van het gebruik van hoofdletters en kleine letters. Standaard is de foutdrempel ingesteld op 5%.

### Hoe lang duurt het voordat een status van een flowuitvoering wordt bijgewerkt nadat een nieuwe gegevensstroom is gemaakt?

Er worden geen stroomuitvoeringen onmiddellijk gegenereerd en het kan ongeveer twee tot drie minuten duren voordat de gegevens zijn bijgewerkt. `startTime`. Als u de status van een flow-run controleert, wordt direct na het maken van een nieuwe dataflow geen informatie over de flow-run geretourneerd `lastRunDetails` aangezien dit nog niet is gebeurd . Het wordt aanbevolen de gegevensstroom een paar minuten te laten genereren voordat de status van de flow wordt gecontroleerd.