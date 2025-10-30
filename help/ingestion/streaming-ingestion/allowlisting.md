---
title: IP-adres dat Voegt op lijst van gewenste personen voor Streaming Ingestie-API
description: Leer hoe u de toegang tot de API voor streaming insluiting beveiligt door alleen opgegeven IP-adressen toe te staan via voegende op lijst van gewenste personen . Deze gids verklaart hoe te opstelling, laat toe en beheert IP-adres-gebaseerde beperkingen voor API veiligheid toe.
hide: true
hidefromtoc: true
badge: bèta
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# IP adres voegende op lijst van gewenste personen  voor Streaming Ingestie API

>[!AVAILABILITY]
>
>Ondersteuning voor IP-adresvoegende op lijst van gewenste personen voor Streaming Ingestie-API is in bèta en uw organisatie heeft er wellicht nog geen toegang tot. De functionaliteit en documentatie kunnen worden gewijzigd.

U kunt nu IP-adressen van lijsten van gewenste personen voor de Streaming Ingestie-API. Gebruik deze functie om uw ingesloten eindpunten te beveiligen door toegang tot slechts de IP adressen te beperken die u specificeert.

## Hoe IP adres voegend op lijst van gewenste personen de werking van de 

De IP voegende op lijst van gewenste personen eigenschap werkt als volgt:

1. **legt IP adressen voor:** u verstrekt een lijst van vertrouwde op IP adressen, die aan uw zandbakken in kaart worden gebracht.
2. **Configuratie:** Adobe vormt de lijst van gewenste personen op de organisatie en zandbakniveau voor uw organisatie.
3. **Handhaving:** De inkomende verzoeken worden geëvalueerd tegen uw verstrekte lijst van gewenste personen:
   * Als het IP adres uw lijst van gewenste personen aanpast, wordt het verzoek verwerkt normaal.
   * Als het IP adres niet op de lijst van gewenste personen is, wordt het verzoek geblokkeerd en een fout van HTTP 403 zal zonder enige reactielichaam worden ontvangen.

## Belangrijkste overwegingen

* De IP adres voegende op lijst van gewenste personen eigenschap is slechts op [ van toepassing Streaming Ingestie API ](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) (`dcs.adobedc.net`) en **** is niet van toepassing `server.adobedc.net` of `edge.adobedc.net`.
* Nieuwe sandboxen zijn standaard geopend totdat voegend op lijst van gewenste personen maken is ingeschakeld.
* Als u een sandbox uit de lijst van gewenste personen verwijdert, wordt deze weer op internet geopend.
* U moet de volledige lijst van zandbak-aan-IP-adresafbeeldingen op uw kant handhaven en altijd de volledige lijst in het IP adres voorleggen voegend op lijst van gewenste personen vorm. Incrementele updates worden niet ondersteund.

## IP-adres voegend op lijst van gewenste personen maken

Volg de stappen hieronder om IP adres toe te laten voegend op lijst van gewenste personen voor uw organisatie:

1. De download en voltooit het [ IP adres voegend op lijst van gewenste personen vorm ](../images/assets/ip_allowlisting_aep.xlsx.zip).
2. Open een steunkaartje en dossier het onderwerp als **AEP DCS &amp; Streaming Ingestie - IP Voegend op lijst van gewenste personen verzoek**. Voeg het ingevulde formulier bij dit ticket.
3. Na het verzenden van uw ticket stuurt de klantenservice van Adobe uw aanvraag door naar de technicus.
4. De ingenieurs laten voegend op lijst van gewenste personen toe en bevestigen opstelling.
5. Vervolgens valideert u de toegang en bevestigt u het gebruik van het ondersteuningsticket.

| Organisatie | Naam van sandbox | Toegestane IP adressen |
| --- | --- | --- |
| ACME | Prod | 203.0.113.42, 198.51.100.25, 192.0.2.10 |
| ACME | Dev | 203.0.113.43, 198.51.100.26, 192.0.2.11 |
| LUMA | Prod | 203.0.113.46, 198.51.100.29, 192.0.2.14 |

## Veelgestelde vragen

Lees het volgende voor antwoorden op vaak gestelde vragen betreffende IP adres voegend op lijst van gewenste personen voor de Streaming Ingestie API.

### Welke API&#39;s worden behandeld?

Alleen de `dcs.adobedc.net` Streaming Ingestie API-eindpunten.

## Wat gebeurt als mijn verzoek uit een niet vermeld IP adres komt?

Het wordt geblokkeerd met een HTTP 403 fout.

### Worden nieuwe sandboxen automatisch beveiligd?

Nee. Zij zijn open tot u IP adresafbeeldingen via de voegende op lijst van gewenste personen vorm verstrekt.

### Kan ik slechts bijgewerkte IP adressen verzenden wanneer mijn lijst van gewenste personen verandert?

Nee. U moet altijd de volledige lijst met sandbox- en IP-adrestoewijzingen verzenden. Gedeeltelijke (incrementele) updates worden niet geaccepteerd.