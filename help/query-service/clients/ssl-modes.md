---
keywords: Experience Platform;home;populaire onderwerpen;Query-service;queryservice;connect;connect met queryservice;SSL;ssl;sslmode;
title: SSL-opties voor Query Service
description: Leer meer over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en hoe u verbinding maakt via de SSL-modus Volledig controleren.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 0%

---

# [!DNL Query Service] SSL-opties

Voor meer beveiliging biedt Adobe Experience Platform [!DNL Query Service] native ondersteuning voor SSL-verbindingen om client-/servercommunicatie te coderen. In dit document wordt beschreven welke SSL-opties beschikbaar zijn voor clientverbindingen van derden met [!DNL Query Service] en hoe verbinding kan worden gemaakt met behulp van de waarde van de parameter `verify-full` SSL.

## Vereisten

In dit document wordt ervan uitgegaan dat u al een clienttoepassing van een andere fabrikant hebt gedownload voor gebruik met uw Experience Platform-gegevens. Specifieke instructies over hoe te om SSL veiligheid op te nemen wanneer het verbinden met een derdecliënt worden gevonden in hun respectieve documentatie van de verbindingsgids. Voor een lijst van alle [!DNL Query Service] gesteunde cliënten, zie het [ overzicht van cliëntverbindingen ](./overview.md).

## Beschikbare SSL-opties {#available-ssl-options}

Experience Platform biedt ondersteuning voor verschillende SSL-opties die zijn afgestemd op uw behoeften op het gebied van gegevensbeveiliging en die de verwerkingsoverhead van codering en sleuteluitwisseling op elkaar afstemmen.

De verschillende `sslmode` -parameterwaarden bieden verschillende beveiligingsniveaus. Door uw gegevens in beweging met SSL certificaten te coderen, helpt het &quot;man-in-the-middle&quot; (MITM) aanvallen, afluisteren, en imitatie te voorkomen. De onderstaande tabel bevat een uitsplitsing van de verschillende beschikbare SSL-modi en het beschermingsniveau dat zij bieden.

>[!NOTE]
>
> De SSL-waarde `disable` wordt niet ondersteund door Adobe Experience Platform vanwege de vereiste compatibiliteit met gegevensbeveiliging.

| sslmode | Afvalbeveiliging | MITM-beveiliging | Beschrijving |
|---|---|---|---|
| `allow` | Ja | Nee | Codering is vereist voor alle communicatie. Het netwerk wordt vertrouwd om met de correcte server te verbinden. |
| `prefer` | Ja | Nee | Codering is vereist voor alle communicatie. Het netwerk wordt vertrouwd om met de correcte server te verbinden. |
| `require` | Ja | Nee | Codering is vereist voor alle communicatie. Het netwerk wordt vertrouwd om met de correcte server te verbinden. ServerSSL-certificaatvalidatie is niet vereist. |
| `verify-ca` | Ja | Afhankelijk van CA-beleid | Codering is vereist voor alle communicatie. Servervalidatie is vereist voordat gegevens worden gedeeld. Hiervoor moet u een basiscertificaat instellen in de [!DNL PostgreSQL] -thuismap. [ de Details worden verstrekt hieronder ](#instructions) |
| `verify-full` | Ja | Ja | Codering is vereist voor alle communicatie. Servervalidatie is vereist voordat gegevens worden gedeeld. Hiervoor moet u een basiscertificaat instellen in de [!DNL PostgreSQL] -thuismap. [ Details worden verstrekt hieronder ](#instructions). |

>[!NOTE]
>
>Het verschil tussen `verify-ca` en `verify-full` is afhankelijk van het beleid van de basiscertificeringsinstantie (CA). Als u uw eigen lokale CA hebt gemaakt om persoonlijke certificaten voor uw toepassingen uit te geven, biedt het gebruik van `verify-ca` vaak voldoende beveiliging. Als u een openbare CA gebruikt, staat `verify-ca` verbindingen toe met een server die iemand anders mogelijk bij de CA heeft geregistreerd. `verify-full` moet altijd worden gebruikt met een openbare basis-CA.

Wanneer u een verbinding van derden tot stand brengt met een Experience Platform-database, wordt u aangeraden `sslmode=require` minimaal te gebruiken om een veilige verbinding tot stand te brengen voor uw gegevens in beweging. De SSL-modus van `verify-full` wordt aanbevolen voor gebruik in de meeste beveiligingsgevoelige omgevingen.

## Een basiscertificaat instellen voor serververificatie {#root-certificate}

>[!IMPORTANT]
>
>De TLS/SSL-certificaten op productieomgevingen voor de API voor interactieve posters van Query Service zijn op woensdag 24 januari 2024 vernieuwd.<br> Hoewel dit een jaarlijks vereiste is, is het wortelcertificaat in de ketting ook veranderd aangezien de Adobe TLS/SSL certificaatleverancier hun certificaathiërarchie heeft bijgewerkt. Dit kan gevolgen hebben voor bepaalde klanten van Postgres als hun lijst van de Autoriteiten van het Certificaat de wortelcert mist. Een PSQL CLI-client moet bijvoorbeeld de basiscertificaten toevoegen aan een expliciet bestand `~/postgresql/root.crt` , anders kan dit resulteren in een fout. Bijvoorbeeld `psql: error: SSL error: certificate verify failed` . Zie de [ officiële documentatie PostgreSQL ](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) voor meer informatie over deze kwestie.<br> het wortelcertificaat om toe te voegen kan van [ https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem ](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem) worden gedownload.

Om een veilige verbinding te verzekeren, moet SSL gebruik op zowel de cliënt als de server worden gevormd alvorens de verbinding wordt gemaakt. Als SSL slechts op de server wordt gevormd, zou de cliënt gevoelige informatie zoals wachtwoorden kunnen verzenden alvorens het wordt gevestigd dat de server hoge veiligheid vereist.

Standaard voert [!DNL PostgreSQL] geen verificatie van het servercertificaat uit. Als u de identiteit van de server wilt verifiëren en een beveiligde verbinding wilt garanderen voordat vertrouwelijke gegevens worden verzonden (als onderdeel van de SSL `verify-full` -modus), moet u een basiscertificaat (zelfondertekend) op uw lokale computer (`root.crt` ) en een bladcertificaat dat is ondertekend door het basiscertificaat op de server plaatsen.

Als de parameter `sslmode` is ingesteld op `verify-full` , controleert libpq of de server betrouwbaar is door de certificaatketen tot aan het basiscertificaat te controleren dat op de client is opgeslagen. Vervolgens wordt gecontroleerd of de hostnaam overeenkomt met de naam die is opgeslagen in het servercertificaat.

Als u verificatie met servercertificaten wilt toestaan, moet u een of meer basiscertificaten (`root.crt`) in het [!DNL PostgreSQL] -bestand in de thuismap plaatsen. Het bestandspad lijkt op `~/.postgresql/root.crt` .

## Verifiëren-volledige SSL-modus inschakelen voor gebruik met een [!DNL Query Service] -verbinding van derden {#instructions}

Als u een strikter beveiligingsbeheer nodig hebt dan `sslmode=require` , kunt u de gemarkeerde stappen volgen om een client van een derde te verbinden met [!DNL Query Service] via de SSL-modus `verify-full` .

>[!NOTE]
>
>Er zijn veel opties beschikbaar om een SSL-certificaat te verkrijgen. Vanwege de toenemende trend in schurkencertificaten wordt DigiCert in deze handleiding gebruikt omdat deze wereldwijd een vertrouwde leverancier zijn van hoogwaardige TLS/SSL-, PKI-, IoT- en ondertekeningsoplossingen.

1. Ga aan [ de lijst van beschikbare DigiCert wortelcertificaten ](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Zoek naar &quot;[!DNL DigiCert Global Root G2]&quot;van de lijst van beschikbare certificaten.
1. Selecteer [!DNL **PEM van de Download**] om het dossier aan uw lokale machine te downloaden.
   ![ de lijst van beschikbare DigiCert wortelcertificaten met benadrukte Download PEM.](../images/clients/ssl-modes/digicert.png)
1. Wijzig de naam van het beveiligingscertificaatbestand in `root.crt` .
1. Kopieer het bestand naar de map [!DNL PostgreSQL] . Het vereiste bestandspad is afhankelijk van uw besturingssysteem. Als de map nog niet bestaat, maakt u de map.
   - Als u macOS gebruikt, is het pad `/Users/<username>/.postgresql`
   - Als u Windows gebruikt, is het pad `%appdata%\postgresql`

>[!TIP]
>
>Om uw `%appdata%` dossierplaats op een werkend systeem van Vensters te vinden, druk ⊞ **Win + R** en input `%appdata%` in het onderzoeksgebied.

Nadat het [!DNL DigiCert Global Root G2] CRT-bestand beschikbaar is in de [!DNL PostgreSQL] -map, kunt u verbinding maken met [!DNL Query Service] via de optie `sslmode=verify-full` of `sslmode=verify-ca` .

## Volgende stappen

Door dit document te lezen, hebt u een beter inzicht in de beschikbare SSL-opties voor het aansluiten van een client van derden op [!DNL Query Service] en ook in de manier waarop u de optie `verify-full` SSL kunt inschakelen om uw gegevens in beweging te coderen.

Als u dit niet reeds hebt gedaan, volg de begeleiding bij [ verbindend een derdecliënt aan  [!DNL Query Service]](./overview.md).
