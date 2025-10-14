---
keywords: Experience Platform;home;populaire onderwerpen;meldingen voor gegevensinvoer;meldingen;subscribe gebeurtenissen;statusgebeurtenissen voor gegevensinvoer;statusgebeurtenissen;subscribe;statusmeldingen; statusmeldingen;
solution: Experience Platform
title: Gegevensinscriptie
description: Om bij het controleren van het innameproces te helpen, maakt Adobe Experience Platform het mogelijk om aan een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u op de hoogte brengen van de status van de opgenomen gegevens en om het even welke mogelijke mislukkingen.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 0%

---

# Meldingen voor gegevensinvoer

Het proces om gegevens in Adobe Experience Platform in te voeren bestaat uit meerdere stappen. Zodra u gegevensbestanden hebt geïdentificeerd die in [!DNL Experience Platform] moeten worden opgenomen, begint het innameproces en elke stap komt opeenvolgend voor tot de gegevens met succes worden opgenomen of ontbreken. Het insluitingsproces kan worden in werking gesteld gebruikend [&#x200B; de Ingestie API van de Partij van Adobe Experience Platform &#x200B;](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) of het gebruiken van het [!DNL Experience Platform] gebruikersinterface.

Gegevens die in [!DNL Experience Platform] worden geladen, moeten meerdere stappen doorlopen om het doel, de [!DNL Data Lake] of de [!DNL Real-Time Customer Profile] gegevensopslag, te bereiken. Elke stap omvat het verwerken van de gegevens, het valideren van de gegevens en het opslaan van de gegevens voordat u deze doorgeeft aan de volgende stap. Afhankelijk van de hoeveelheid gegevens die wordt opgenomen, kan dit een tijdrovend proces worden en er is altijd een kans dat het proces mislukt door validatie-, semantiek- of verwerkingsfouten. In geval van een fout moeten de gegevensproblemen worden opgelost en moet het volledige innameproces opnieuw worden gestart met de gecorrigeerde gegevensbestanden.

Als hulp bij het controleren van het innameproces, maakt [!DNL Experience Platform] het mogelijk om op een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u op de hoogte brengen van de status van de opgenomen gegevens en om het even welke mogelijke mislukkingen.

## Webhaak registreren voor meldingen over gegevensinvoer

Om gegevensopname berichten te ontvangen, moet u [&#x200B; Adobe Developer Console &#x200B;](https://www.adobe.com/go/devs_console_ui) gebruiken om een webhaak aan uw integratie van Experience Platform te registreren.

Volg het leerprogramma op [&#x200B; intekenend aan  [!DNL Adobe I/O Event]  berichten &#x200B;](../../observability/alerts/subscribe.md) voor gedetailleerde stappen op hoe te om dit te verwezenlijken.

>[!IMPORTANT]
>
>Zorg er tijdens het abonnementsproces voor dat u **[!UICONTROL Platform notifications]** als gebeurtenisprovider selecteert en selecteer het **[!UICONTROL Data ingestion notification]** -gebeurtenisabonnement wanneer u daarom wordt gevraagd.

## Meldingen over gegevensinvoer ontvangen

Nadat u de webhaak hebt geregistreerd en nieuwe gegevens zijn ingevoerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden weergegeven met de webhaak zelf of door het tabblad **[!UICONTROL Debug Tracing]** te selecteren in het overzicht met gebeurtenisregistratie in Adobe Developer Console van uw project.

De volgende JSON is een voorbeeld van een berichtlading die naar uw webhaak in het geval van een ontbroken partijingestitie gebeurtenis zou worden verzonden:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `event_id` | Een unieke, door het systeem gegenereerde id voor het bericht. |
| `event` | Een object dat de details bevat van de gebeurtenis die de melding heeft geactiveerd. |
| `event.xdm:datasetId` | De id van de gegevensset waarop de insluitingsgebeurtenis van toepassing is. |
| `event.xdm:eventCode` | Een statuscode die het type gebeurtenis aangeeft dat voor de gegevensset is geactiveerd. Zie [&#x200B; bijlage &#x200B;](#event-codes) voor specifieke waarden en hun definities. |

Om het volledige schema voor gebeurtenisberichten te bekijken, verwijs naar de [&#x200B; openbare bewaarplaats GitHub &#x200B;](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Volgende stappen

Nadat u [!DNL Experience Platform] -berichten hebt geregistreerd voor uw project, kunt u ontvangen gebeurtenissen van [!UICONTROL Project overview] weergeven. Verwijs naar de gids op [&#x200B; het vinden Adobe I/O Events &#x200B;](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) voor gedetailleerde instructies op hoe te om uw gebeurtenissen te vinden.

## Bijlage

De volgende sectie bevat aanvullende informatie over het interpreteren van gegevensinvoer-berichtladingen.

### Beschikbare statusmeldingsgebeurtenissen {#event-codes}

In de volgende tabel staan de statusmeldingen voor gegevensinvoer waarop u zich kunt abonneren.

| Gebeurteniscode | Experience Platform Service | Status | Beschrijving van een gebeurtenis |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | succes | Een batch is opgenomen in een dataset in de [!DNL Data Lake] . |
| `ing_load_failure` | [!DNL Data Ingestion] | fout | Een batch kan niet worden opgenomen in een dataset binnen de [!DNL Data Lake] . |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | succes | Een batch is opgenomen in de gegevensopslag van [!DNL Profile] . |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | fout | Een batch kan niet in de gegevensopslag van [!DNL Profile] worden opgenomen. |
| `ig_load_success` | [!DNL Identity Service] | succes | Gegevens zijn geladen in de identiteitsgrafiek. |
| `ig_load_failure` | [!DNL Identity Service] | fout | Gegevens kunnen niet in de identiteitsgrafiek worden geladen. |

>[!NOTE]
>
>Er is slechts één gebeurtenisonderwerp dat voor alle gegevens wordt verstrekt die berichten invoeren. Om onderscheid te maken tussen verschillende statussen, kan de gebeurteniscode worden gebruikt.
