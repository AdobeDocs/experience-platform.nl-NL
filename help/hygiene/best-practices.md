---
title: Beste praktijken voor het Geavanceerde Beheer van de Levenscyclus van Gegevens
description: Leer hoe u verzoeken voor gegevenshygiëne efficiënt kunt beheren in Adobe Experience Platform met de API voor geavanceerd gegevenslevenscyclusbeheer en gegevenshygiëne. Deze gids behandelt beste praktijken zoals het maximaliseren van identiteiten per verzoek, het specificeren van individuele datasets, en het bewust zijn van API het vertragen om vertragingen te verhinderen. Het document bevat richtlijnen voor het instellen van automatische gegevensset-opschoonbewerkingen, het controleren van de werkorderstatus en gedetailleerde methoden voor het ophalen van reacties. Volg deze procedures om de verwerking van uw verzoek te stroomlijnen en de reactietijden te optimaliseren.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: 5174529d606ac0186ff3193790ada70a46c7e274
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Aanbevolen procedures voor geavanceerd levenscyclusbeheer van gegevens

Gebruik de Advanced Data Lifecycle Management UI en de Data Hygiene API om opschoonverzoeken efficiënt te beheren en gegevens uit Adobe Experience Platform-services te verwijderen. Volg de onderstaande aanbevolen procedures om de verwerking van uw verzoek te stroomlijnen en de responstijden voor voltooiing te optimaliseren.

## Vereisten {#prerequisites}

Deze handleiding vereist een goed begrip van de werkruimte van de levenscyclus van gegevens en de [API voor gegevenshygiëne](./api/overview.md). Voordat u doorgaat met dit document, moet u bekend zijn met de hulplijnen op [Geavanceerd levenscyclusbeheer van gegevens](./home.md) en [maken, aanvragen voor het verwijderen van records](./ui/record-delete.md) of [gegevenssetvervaltijden in UI](./ui/dataset-expiration.md)of via de API.

## Richtlijnen voor het maken van werkorders {#work-order-creation-guidelines}

U kunt de `/workorder` eindpunt in de Hygiene API van Gegevens om verslagen te beheren schrapt verzoeken in Experience Platform. Met dit eindpunt, kunt u een schrappingsverzoek tot stand brengen, zijn status controleren, of een bestaand verzoek bijwerken. Zie de [Document met het eindpunt van de werkorder](./api/workorder.md) om te leren hoe u deze handelingen uitvoert met de API.

>[!TIP]
>
>Een werkorder is een gestructureerd verzoek dat specifieke gegevensbeheerbewerkingen uitvoert, zoals het opschonen of transformeren van gegevens, om een efficiënte en systematische verwerking te garanderen.

Volg de onderstaande richtlijnen om uw opmerkingen voor opschoonverzoeken te optimaliseren:

1. **Identiteiten maximaliseren per aanvraag:** Omvat tot 100.000 identiteiten per schoonmaakbeurtverzoek om efficiency te verbeteren. Door meerdere identiteiten in één aanvraag op te nemen, vermindert u de frequentie van API-aanroepen en minimaliseert u het risico op prestatieproblemen als gevolg van buitensporige Single-identity-aanvragen. Verzend aanvragen met maximale aantallen identiteitsgegevens voor een snellere verwerking, aangezien werkorders batchgewijs worden verwerkt.
2. **Afzonderlijke gegevenssets opgeven:** Geef voor maximale efficiëntie de afzonderlijke gegevensset op die moet worden verwerkt.
3. **Overwegingen bij het vertragen van API&#39;s:** Houd rekening met de snelheid van de API om te voorkomen dat de toepassing langzaam afneemt. Kleinere aanvragen (&lt; 100 IDs) bij hogere frequenties kunnen resulteren in 429 reacties en moeten opnieuw worden ingediend met aanvaardbare snelheden.

### 429 fouten beheren {#manage-429-errors}

Als u een fout van 429 ontvangt, wijst het erop dat u het toegestane aantal verzoeken binnen een bepaalde tijdspanne hebt overschreden. Volg deze best practices om 429 fouten effectief te beheren:

- **De koptekst &#39;Opnieuw proberen-Na&#39; lezen**: Wanneer een fout van 429 wordt geretourneerd, controleert u de antwoordheader &#39;Opnieuw-Na&#39;. Deze kopbal specificeert de tijd te wachten alvorens het verzoek opnieuw te proberen.
- **Opnieuw proberen-logica implementeren**: Gebruik de waarde &#39;Opnieuw proberen-na&#39; om logica voor opnieuw proberen in uw toepassing te implementeren, zodat opnieuw wordt geprobeerd na de opgegeven tijd om volgende 429 fouten te voorkomen.
- **Batch uw verzoeken**: Vermijd het snel achter elkaar indienen van talrijke kleine verzoeken. In plaats daarvan plaatst u meerdere identiteiten in één aanvraag om de frequentie van oproepen te verminderen en het risico van het bereiken van tarieflimieten tot een minimum te beperken.

## Vervaldatum gegevensset {#dataset-expiration}

Stel automatische gegevensset opschonen in voor gegevens van korte duur. Gebruik de `/ttl` eindpunt op de API van de Hygiëne van Gegevens om vervaldata voor datasets voor schoonmaak te plannen die op een gespecificeerde tijd of een datum wordt gebaseerd. Zie de het eindpuntgids van de Vervaldatum van de Dataset leren hoe te [een gegevensset maken die vervalt](./api/dataset-expiration.md) en de [geaccepteerde queryparameters](./api/dataset-expiration.md#query-params).

## Bewaking van werkorder en vervalstatus van gegevensset {#monitor}

U kunt de voortgang van uw gegevenslevenscyclusbeheer efficiënt controleren door **I/O-gebeurtenissen**. Een I/O-gebeurtenis is een mechanisme voor het ontvangen van realtime meldingen over wijzigingen of updates in verschillende services binnen het platform.

I/O-gebeurteniswaarschuwingen kunnen naar een geconfigureerde webhaak worden verzonden om de automatisering van activiteitencontrole mogelijk te maken. Als u waarschuwingen wilt ontvangen via een webhaak, moet u uw webhaak registreren voor Platformwaarschuwingen in de Adobe Developer Console. Zie de handleiding op [abonneren op Adobe I/O Event-berichten](../observability/alerts/subscribe.md) voor de gedetailleerde instructies.

Gebruik de volgende methoden en richtlijnen voor de levenscyclus van gegevens om taakstatussen effectief op te halen en te controleren:

### I/O-gebeurtenissen {#io-events}

U kunt de voortgang van uw taken tijdens de levenscyclus van gegevens op efficiënte wijze controleren door I/O-gebeurtenissen in te stellen en te gebruiken door de volgende stappen uit te voeren:

- Websites instellen om pushmeldingen voor statuswijzigingen te ontvangen.
- Gebruik meldingen om de voortgang te volgen en updates te ontvangen wanneer deze zijn voltooid.
- Implementeer geen opiniepeilingsmechanismen om het API-verkeer te minimaliseren.

### Gedetailleerde antwoorden ophalen voor één werkorder {#retrieve-detailed-work-order-response}

Voor diepgaande informatie over individuele werkorders, gebruik de volgende benadering:

- Breng een verzoek van een GET aan de `/workorder/{work_order_id}` eindpunt voor gedetailleerde reactiegegevens.
- Haal productspecifieke reacties en succesberichten op.
- Vermijd het gebruik van deze methode voor regelmatige opiniepeilingsactiviteiten.

Door deze beste praktijken na te leven, kunt u schoonmaakverzoeken effectief beheren en reactietijden optimaliseren binnen het Geavanceerde Beheer van de Levenscyclus van Gegevens.
