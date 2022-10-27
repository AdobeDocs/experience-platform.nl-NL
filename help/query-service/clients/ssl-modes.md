---
keywords: Experience Platform;thuis;populaire onderwerpen;de dienst van de vraag;de vraagdienst;verbind;verbindt met de vraagdienst;SSL;ssl;sslmode;
title: SSL-opties voor Query Service
description: Leer meer over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en hoe u verbinding maakt via de SSL-modus Volledig controleren.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] SSL-opties

Voor meer veiligheid, Adobe Experience Platform [!DNL Query Service] biedt native ondersteuning voor SSL-verbindingen om client-/servercommunicatie te coderen. In dit document worden de beschikbare SSL-opties besproken voor clientverbindingen van derden met [!DNL Query Service] en hoe u verbinding maakt met de `verify-full` SSL-parameterwaarde.

## Vereisten

In dit document wordt ervan uitgegaan dat u al een clienttoepassing van een andere fabrikant hebt gedownload voor gebruik met uw Platform-gegevens. Specifieke instructies over hoe te om SSL veiligheid op te nemen wanneer het verbinden met een derdecliënt worden gevonden in hun respectieve documentatie van de verbindingsgids. Voor een lijst van allen [!DNL Query Service] ondersteunde clients, raadpleegt u de [Overzicht van clientverbindingen](./overview.md).

## Beschikbare SSL-opties {#available-ssl-options}

Platform biedt ondersteuning voor verschillende SSL-opties die aansluiten bij uw behoeften op het gebied van gegevensbeveiliging en die een evenwicht bieden tussen de verwerkingsoverhead van codering en sleuteluitwisseling.

De verschillende `sslmode` parameterwaarden bieden verschillende beschermingsniveaus. Door uw gegevens in beweging met SSL certificaten te coderen, helpt het &quot;man-in-the-middle&quot; (MITM) aanvallen, afluisteren, en imitatie te voorkomen. De onderstaande tabel bevat een uitsplitsing van de verschillende beschikbare SSL-modi en het beschermingsniveau dat zij bieden.

>[!NOTE]
>
> De SSL-waarde `disable` wordt niet ondersteund door Adobe Experience Platform vanwege de vereiste naleving van de gegevensbescherming.

| sslmode | Afvalbeveiliging | MITM-beveiliging | Beschrijving |
|---|---|---|---|
| `allow` | Gedeeltelijk | Nee | Veiligheid is geen prioriteit, snelheid en een lage verwerkingsoverhead zijn belangrijker. Deze modus kiest alleen voor codering als de server erop staat. |
| `prefer` | Gedeeltelijk | Nee | Codering is niet vereist, maar de communicatie wordt gecodeerd als de server dit ondersteunt. |
| `require` | Ja | Nee | Codering is vereist voor alle communicatie. Het netwerk wordt vertrouwd om met de correcte server te verbinden. ServerSSL-certificaatvalidatie is niet vereist. |
| `verify-ca` | Ja | Afhankelijk van CA-beleid | Codering is vereist voor alle communicatie. Servervalidatie is vereist voordat gegevens worden gedeeld. Hiervoor moet u een basiscertificaat instellen in uw [!DNL PostgreSQL] thuismap. [Details worden hieronder gegeven](#instructions) |
| `verify-full` | Ja | Ja | Codering is vereist voor alle communicatie. Servervalidatie is vereist voordat gegevens worden gedeeld. Hiervoor moet u een basiscertificaat instellen in uw [!DNL PostgreSQL] thuismap. [Details worden hieronder gegeven](#instructions). |

>[!NOTE]
>
>Het verschil tussen `verify-ca` en `verify-full` is afhankelijk van het beleid van de basiscertificeringsinstantie (CA). Als u uw eigen lokale CA hebt gemaakt voor het uitgeven van persoonlijke certificaten voor uw toepassingen, gebruikt u `verify-ca` biedt vaak voldoende bescherming. Indien een openbare CA wordt gebruikt, `verify-ca` staat verbindingen met een server toe die iemand anders bij CA kan hebben geregistreerd. `verify-full` moet altijd worden gebruikt met een openbare wortel CA.

Wanneer het vestigen van een derdeverbinding aan een gegevensbestand van het Platform, wordt u geadviseerd te gebruiken `sslmode=require` minimaal voor een veilige verbinding voor uw gegevens in beweging. De `verify-full` SSL-modus wordt aanbevolen voor gebruik in de meeste omgevingen die gevoelig zijn voor beveiliging.

## Een basiscertificaat instellen voor serververificatie {#root-certificate}

Om een veilige verbinding te verzekeren, moet SSL gebruik op zowel de cliënt als de server worden gevormd alvorens de verbinding wordt gemaakt. Als SSL slechts op de server wordt gevormd, zou de cliënt gevoelige informatie zoals wachtwoorden kunnen verzenden alvorens het wordt gevestigd dat de server hoge veiligheid vereist.

Standaard, [!DNL PostgreSQL] voert geen verificatie van het servercertificaat uit. Om de identiteit van de server te verifiëren en een veilige verbinding te verzekeren alvorens om het even welke gevoelige gegevens worden verzonden (als deel van SSL `verify-full` (modus), moet u een basiscertificaat (zelfondertekend) op uw lokale computer plaatsen (`root.crt`) en een bladcertificaat dat is ondertekend door het basiscertificaat op de server.

Als de `sslmode` parameter is ingesteld op `verify-full`, zal libpq verifiëren dat de server betrouwbaar is door de certificaatketen tot het wortelcertificaat te controleren dat op de cliënt wordt opgeslagen. Vervolgens wordt gecontroleerd of de hostnaam overeenkomt met de naam die is opgeslagen in het servercertificaat.

Als u verificatie met servercertificaten wilt toestaan, moet u een of meer basiscertificaten plaatsen (`root.crt`) in de [!DNL PostgreSQL] in uw thuismap. Het bestandspad lijkt op `~/.postgresql/root.crt`.

## Verifiëren-volledige SSL-modus inschakelen voor gebruik met een derde [!DNL Query Service] verbinding {#instructions}

Als u strengere beveiligingscontrole nodig hebt dan `sslmode=require`kunt u de gemarkeerde stappen volgen om een client van een derde te verbinden met [!DNL Query Service] gebruiken `verify-full` SSL-modus.

>[!NOTE]
>
>Er zijn veel opties beschikbaar om een SSL-certificaat te verkrijgen. Vanwege de toenemende trend in schurkencertificaten wordt DigiCert in deze handleiding gebruikt omdat deze wereldwijd een vertrouwde leverancier zijn van hoogwaardige TLS/SSL-, PKI-, IoT- en ondertekeningsoplossingen.

1. Navigeren naar [de lijst met beschikbare DigiCert-basiscertificaten](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Zoeken naar &quot;[!DNL DigiCert Global Root CA]&quot; uit de lijst met beschikbare certificaten.
1. Selecteren [!DNL **PEM downloaden**] om het bestand naar uw lokale computer te downloaden.
   ![De lijst met beschikbare DigiCert-basiscertificaten met Download PEM gemarkeerd.](../images/clients/ssl-modes/digicert.png)
1. De naam van het beveiligingscertificaatbestand wijzigen in `root.crt`.
1. Kopieer het bestand naar de [!DNL PostgreSQL] map. Het vereiste bestandspad is afhankelijk van uw besturingssysteem. Als de map nog niet bestaat, maakt u de map.
   - Als u macOS gebruikt, is het pad `/Users/<username>/.postgresql`
   - Als u Windows gebruikt, is het pad `%appdata%\postgresql`

>[!TIP]
>
>Als u uw `%appdata%` bestandslocatie op een Windows-besturingssysteem, druk op ⊞ **Win + R** en invoer `%appdata%` in het zoekveld.

Na de [!DNL DigiCert Global Root CA] CRT-bestand is beschikbaar in uw [!DNL PostgreSQL] map, kunt u verbinding maken met [!DNL Query Service] met de `sslmode=verify-full` of `sslmode=verify-ca` optie.

## Volgende stappen

Door dit document te lezen, hebt u een beter inzicht in de beschikbare SSL-opties voor het verbinden van een client van derden met [!DNL Query Service], en hoe de `verify-full` SSL-optie om uw gegevens in beweging te coderen.

Indien u dit nog niet hebt gedaan, volgt u de aanwijzingen op [een client van een andere fabrikant verbinden met [!DNL Query Service]](./overview.md).
