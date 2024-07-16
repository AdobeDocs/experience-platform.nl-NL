---
solution: Experience Platform
title: Bekende beperkingen en problemen met afspeelboeken oplossen
description: Meer informatie over de bekende problemen en algemene problemen met afspeelboeken en hoe u deze problemen kunt oplossen
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Problemen oplossen {#troubleshooting}

Suggesties voor het oplossen van problemen weergeven voor algemene fouten wanneer u werkt met Hoofdletters gebruiken

## Adobe Journey Optimizer-oppervlakken niet geconfigureerd {#surfaces-not-configured}

Wanneer u een instantie van een afspeelboek maakt, wordt mogelijk het onderstaande bericht weergegeven.

![Problemen oplossen](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Dit komt omdat Journey Optimizer-afspeelboeken berichten maken voor e-mail-, push- en SMS-kanalen. Lees [ begonnen wordt ](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) gids om de verschillende oppervlakten te vormen.

## Status *ontbroken* wanneer het creëren van een nieuwe instantie {#status-failed}

Als u een ontbroken bericht ziet wanneer u probeert om een geval tot stand te brengen, zou dit kunnen zijn omdat uw beheerder u niet de vereiste gebruikerstoestemmingen heeft verleend. Een afspeelboek bevat veel verschillende elementen en uw gebruiker heeft machtigingen nodig om deze elementen te maken, zodat de instantie van het afspeelboek correct kan worden gemaakt. Zie de [ toestemmingen ](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) sectie van deze gids op hoe te opstellingstoestemmingen.

## Importeren mislukt {#import-failure}

Klanten werken binnen verschillende testomgevingen en soms, terwijl het importeren van een instantie van hun omgeving naar de sandbox Adobe kan mislukken. Als u de status van deze importbewerkingen wilt weergeven, selecteert u Sandbox in de linkernavigatie en vervolgens Taken. Hier kunt u alle details van de geïmporteerde bestanden bekijken. Selecteer een bestand met een mislukte status en selecteer vervolgens Taakgegevens weergeven. Er wordt een modaal weergegeven. Selecteer JSON-bestand weergeven en blader omlaag en kopieer het foutbericht dat onder &quot;berichten&quot; wordt weergegeven. Het is heel mogelijk dat er meerdere foutberichten worden weergegeven, dus kopieer alle foutberichten. Verzend deze naar het team van de Adobe terwijl het proberen om een insectenkaartje te registreren. Dit versnelt het resolutieproces en geeft uw team meer context over wat er gebeurt.
