---
title: Beste praktijken voor het Geavanceerde Beheer van de Levenscyclus van Gegevens
description: Leer hoe u verzoeken voor gegevenshygiëne efficiënt kunt beheren in Adobe Experience Platform met de API voor geavanceerd gegevenslevenscyclusbeheer en gegevenshygiëne. Deze gids behandelt beste praktijken zoals het maximaliseren van identiteiten per verzoek, het specificeren van individuele datasets, en het bewust zijn van API het vertragen om vertragingen te verhinderen. Het document bevat richtlijnen voor het instellen van automatische gegevensset-opschoonbewerkingen, het controleren van de werkorderstatus en gedetailleerde methoden voor het ophalen van reacties. Volg deze procedures om de verwerking van uw verzoek te stroomlijnen en de reactietijden te optimaliseren.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Aanbevolen procedures voor geavanceerd levenscyclusbeheer van gegevens

Gebruik de Advanced Data Lifecycle Management UI en de Data Hygiene API om opschoonverzoeken efficiënt te beheren en gegevens uit Adobe Experience Platform-services te verwijderen. Volg de onderstaande aanbevolen procedures om de verwerking van uw verzoek te stroomlijnen en de responstijden voor voltooiing te optimaliseren.

## Vereisten {#prerequisites}

Deze gids vereist een werkend begrip van de werkruimte van de Levenscyclus van Gegevens en [ Hygiene API van Gegevens ](./api/overview.md). Alvorens dit document voort te zetten, vertrouwt u met de gidsen op [ het Geavanceerde Beheer van de Levenscyclus van Gegevens ](./home.md) en [ creërend verslagen schrapt verzoeken ](./ui/record-delete.md) of [ datasettermijnen in UI ](./ui/dataset-expiration.md), of door API.

## Richtlijnen voor het maken van werkorders {#work-order-creation-guidelines}

U kunt het `/workorder` eindpunt in de API van de Hygiëne van Gegevens gebruiken om verslagen te beheren schrapt verzoeken in Experience Platform. Met dit eindpunt, kunt u een schrappingsverzoek tot stand brengen, zijn status controleren, of een bestaand verzoek bijwerken. Zie het [ document van het de ordeeindpunt van het Werk ](./api/workorder.md) leren hoe te om deze acties uit te voeren gebruikend API.

>[!TIP]
>
>Een werkorder is een gestructureerd verzoek dat specifieke gegevensbeheerbewerkingen uitvoert, zoals het opschonen of transformeren van gegevens, om een efficiënte en systematische verwerking te garanderen.

Volg de onderstaande richtlijnen om uw opmerkingen voor opschoonverzoeken te optimaliseren:

1. **maximaliseer identiteiten per verzoek:** omvat tot 100.000 identiteiten per schoonmaakbeurtverzoek om efficiency te verbeteren. Door meerdere identiteiten in één aanvraag op te nemen, vermindert u de frequentie van API-aanroepen en minimaliseert u het risico op prestatieproblemen als gevolg van buitensporige Single-identity-aanvragen. Verzend aanvragen met maximale aantallen identiteitsgegevens voor een snellere verwerking, aangezien werkorders batchgewijs worden verwerkt.
2. **specificeer individuele datasets:** voor maximumefficiency, specificeer de individuele dataset die moet worden verwerkt.
3. **API throttling overwegingen:** ben bedacht van API throttling om langzame-verduisteringen te verhinderen. Kleinere aanvragen (&lt; 100 IDs) bij hogere frequenties kunnen resulteren in 429 reacties en moeten opnieuw worden ingediend met aanvaardbare snelheden.

### 429 fouten beheren {#manage-429-errors}

Als u een fout van 429 ontvangt, wijst het erop dat u het toegestane aantal verzoeken binnen een bepaalde tijdspanne hebt overschreden. Volg deze best practices om 429 fouten effectief te beheren:

- **las &quot;opnieuw-na&quot;kopbal**: Wanneer een 429 fout is teruggekeerd, controleer de &quot;opnieuw-na&quot;antwoordkopbal. Deze kopbal specificeert de tijd te wachten alvorens het verzoek opnieuw te proberen.
- **voert logica opnieuw uit**: Gebruik de &quot;opnieuw proberen-na&quot;waarde om opnieuw te proberen logica in uw toepassing uit te voeren, die ervoor zorgt dat de pogingen na de gespecificeerde tijd worden geprobeerd om verdere 429 fouten te vermijden.
- **Batch uw verzoeken**: Vermijd het voorleggen van talrijke kleine verzoeken snel achtereenvolgens. In plaats daarvan plaatst u meerdere identiteiten in één aanvraag om de frequentie van oproepen te verminderen en het risico van het bereiken van tarieflimieten tot een minimum te beperken.

## Vervaldatum gegevensset {#dataset-expiration}

Stel automatische gegevensset opschonen in voor gegevens van korte duur. Gebruik het `/ttl` eindpunt op de API van de Hygiëne van Gegevens om vervaldata voor datasets voor schoonmaakbeurt te plannen die op een gespecificeerde tijd of een datum wordt gebaseerd. Zie de het eindpuntgids van de Vervaldatum van de Dataset leren hoe te [ een datasetvervaldatum ](./api/dataset-expiration.md) en [ toegelaten vraagparameters ](./api/dataset-expiration.md#query-params) creëren.

## Bewaking van werkorder en vervalstatus van gegevensset {#monitor}

U kunt de vooruitgang van uw beheer van de gegevenslevenscyclus efficiënt controleren door het gebruik van **I/O Gebeurtenissen**. Een I/O-gebeurtenis is een mechanisme voor het ontvangen van realtime meldingen over wijzigingen of updates in verschillende services in Experience Platform.

I/O-gebeurteniswaarschuwingen kunnen naar een geconfigureerde webhaak worden verzonden om de automatisering van activiteitencontrole mogelijk te maken. Als u waarschuwingen wilt ontvangen via webhaak, moet u uw webhaak registreren voor Experience Platform-waarschuwingen in de Adobe Developer Console. Zie de gids op [ het intekenen aan de berichten van de Gebeurtenis van Adobe I/O ](../observability/alerts/subscribe.md) voor de gedetailleerde instructies.

Gebruik de volgende methoden en richtlijnen voor de levenscyclus van gegevens om taakstatussen effectief op te halen en te controleren:

### I/O-gebeurtenissen {#io-events}

U kunt de voortgang van uw taken tijdens de levenscyclus van gegevens op efficiënte wijze controleren door I/O-gebeurtenissen in te stellen en te gebruiken door de volgende stappen uit te voeren:

- Websites instellen om pushmeldingen voor statuswijzigingen te ontvangen.
- Gebruik meldingen om de voortgang te volgen en updates te ontvangen wanneer deze zijn voltooid.
- Implementeer geen opiniepeilingsmechanismen om het API-verkeer te minimaliseren.

### Gedetailleerde antwoorden ophalen voor één werkorder {#retrieve-detailed-work-order-response}

Voor diepgaande informatie over individuele werkorders, gebruik de volgende benadering:

- Voer een GET-aanvraag in bij het `/workorder/{work_order_id}` -eindpunt voor gedetailleerde reactiegegevens.
- Haal productspecifieke reacties en succesberichten op.
- Vermijd het gebruik van deze methode voor regelmatige opiniepeilingsactiviteiten.

Door deze beste praktijken na te leven, kunt u schoonmaakverzoeken effectief beheren en reactietijden optimaliseren binnen het Geavanceerde Beheer van de Levenscyclus van Gegevens.
