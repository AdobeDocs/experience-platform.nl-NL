---
title: API-handleiding voor queryservice
description: Leer hoe te om de Vergunning API van de Dienst van de Vraag te gebruiken om op netwerk-gebaseerde IP beperkingen voor veilige verbindingen door SQL af te dwingen. Gebruik deze API om het beheer van gegevenstoegang voor uw Adobe Experience Platform-gegevens te verbeteren.
role: Developer
exl-id: bcc5ea0e-cb6d-4c7b-bf9f-a0336f76c4c8
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---

# API-handleiding voor queryservice

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die de Data Distiller-add hebben aangeschaft. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger.

Gebruik de Vergunning API van de Dienst van de Vraag om op IP-Gebaseerde beperkingen af te dwingen. Door deze maatregelen toe te passen, krijgen alleen erkende netwerken en clientcomputers toegang tot gegevens via SQL in Adobe Experience Platform. Deze controles helpen u aan strenge veiligheidsnormen voldoen terwijl het verstrekken van toegang in real time controle en alarmering.

Met deze API kunt u IP-beperkingen configureren, afdwingen en controleren voor toegang tot gegevens via de SQL-interface. Dit document biedt een overzicht op hoog niveau van de kernfuncties van de API, eindpuntfuncties en toekomstige mogelijkheden.

## Belangrijkste kenmerken

De volgende eigenschappen laten u toe om op IP-Gebaseerde toegangsbeperkingen te bepalen, toegangspogingen te controleren, en de montages van de netwerkveiligheid voor de Dienst van de Vraag aan te passen:

- **bepaalt op netwerk-gebaseerde controles van de gegevenstoegang**: Specificeer toegestane IP waaiers voor de toegang van de Dienst van de Vraag. Deze beperking is specifiek op SQL gegevensbestandverbindingen, met inbegrip van die gemaakt door Business Intelligence (BI) hulpmiddelen, gegevensbestandcliënten, of programmeringsinterfaces zoals JDBC.
- **laat uitvoerige controle en alarm** toe: Alle toegangspogingen, met inbegrip van ontkende verbindingen, worden geregistreerd en verzonden naar de [ Logboeken van de Controle van Adobe Experience Platform ](../../landing/governance-privacy-security/audit-logs/overview.md) voor het volgen in real time. Gebruik dit vermogen om toegangspatronen te controleren en potentiële veiligheidsbreuken te ontdekken.
- **vorm flexibele IP beperkingen**: Specificeer toegestane IPs in zowel individuele IP als het blokformaten CIDR. Deze instellingen gelden per sandbox, zodat u de netwerkbeperkingen kunt aanpassen aan uw specifieke beveiligingsbehoeften.

## Functies voor controle en toezicht

Om veilige praktijken van de gegevenstoegang te steunen, registreert de Dienst van de Vraag alle cliënt IPs die toegang hebben of proberen om tot AEP toegang te hebben. De gebeurtenissen van de controle, met inbegrip van ontkende verbindingen, worden verzonden naar de Logboeken van de Controle van het Platform. Hierdoor wordt het volgende ingeschakeld:

- **Realtime Controle**: De op IP-Gebaseerde toegangspatronen van het spoor om naleving te verzekeren.
- **het Alarm op Onbevoegde Toegang**: Identificeer en antwoordt aan toegangspogingen van onbevoegde IPs.

Voor meer details op controleregistreren, verwijs naar de [ documentatie van de Dienst van de Controle ](https://experienceleague.adobe.com/docs/experience-platform/audit/audit-overview.html).

## Volgende stappen

Krijg begonnen met de Vergunning API van de Dienst van de Vraag door de [ Begonnen gids ](./getting-started.md) voor essentiële opstellingsstappen, met inbegrip van vereiste kopballen en API vraagovereenkomsten te herzien. Dan, onderzoek de eindpunt-specifieke gidsen op [ IP Toegang ](./ip-access.md) en [ IP Bevestiging ](./validate.md) voor het vormen en het beheren van veilige gegevenstoegang.
