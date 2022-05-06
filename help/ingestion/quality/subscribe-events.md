---
keywords: Experience Platform;home;populaire onderwerpen;meldingen over het opnemen van gegevens;meldingen;subscribe gebeurtenissen;statusgebeurtenissen voor het invoeren van gegevens;statusgebeurtenissen;subscribe;statusmeldingen;
solution: Experience Platform
title: Gegevensinscriptie
topic-legacy: overview
description: Om bij het controleren van het innameproces te helpen, maakt Adobe Experience Platform het mogelijk om aan een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u op de hoogte brengen van de status van de opgenomen gegevens en om het even welke mogelijke mislukkingen.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 1%

---

# Meldingen voor gegevensinvoer

Het proces om gegevens in Adobe Experience Platform in te voeren bestaat uit meerdere stappen. Zodra u gegevensbestanden identificeert waarin moeten worden opgenomen [!DNL Platform], begint het innameproces en elke stap komt achtereenvolgens voor tot de gegevens met succes worden opgenomen of ontbreken. Het innameproces kan worden gestart met behulp van de [Adobe Experience Platform-API voor gegevensverwerking](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) of door [!DNL Experience Platform] gebruikersinterface.

Gegevens geladen in [!DNL Platform] moet door veelvoudige stappen gaan om zijn bestemming te bereiken, [!DNL Data Lake] of de [!DNL Real-time Customer Profile] gegevensopslag. Elke stap omvat het verwerken van de gegevens, het valideren van de gegevens en het opslaan van de gegevens voordat u deze doorgeeft aan de volgende stap. Afhankelijk van de hoeveelheid gegevens die wordt opgenomen, kan dit een tijdrovend proces worden en er is altijd een kans dat het proces mislukt door validatie-, semantiek- of verwerkingsfouten. In geval van een fout moeten de gegevensproblemen worden opgelost en moet het volledige innameproces opnieuw worden gestart met de gecorrigeerde gegevensbestanden.

Bijstaan bij het toezicht op het inslikken [!DNL Experience Platform] maakt het mogelijk om op een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u op de hoogte brengen van de status van de opgenomen gegevens en om het even welke mogelijke mislukkingen.

## Webhaak registreren voor meldingen over gegevensinvoer

Als u meldingen over gegevensinvoer wilt ontvangen, moet u [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) om een webhaak voor uw Experience Platform te registreren.

Volg de zelfstudie op [abonneren op [!DNL Adobe I/O Event] meldingen](../../observability/alerts/subscribe.md) voor gedetailleerde stappen over hoe te om dit te verwezenlijken.

>[!IMPORTANT]
>
>Zorg ervoor dat u tijdens het abonnementsproces **[!UICONTROL Platform notifications]** als de gebeurtenisprovider en selecteer de **[!UICONTROL Data ingestion notification]** abonnement op gebeurtenis wanneer hierom wordt gevraagd.

## Meldingen over gegevensinvoer ontvangen

Nadat u de webhaak hebt geregistreerd en nieuwe gegevens zijn ingevoerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden weergegeven met de webhaak zelf of door de **[!UICONTROL Debug Tracing]** in het overzicht van de gebeurtenisregistratie van uw project in Adobe Developer Console.

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
| `event.xdm:eventCode` | Een statuscode die het type gebeurtenis aangeeft dat voor de gegevensset is geactiveerd. Zie de [aanhangsel](#event-codes) voor specifieke waarden en hun definities. |

Als u het volledige schema voor gebeurtenismeldingen wilt weergeven, raadpleegt u de [public GitHub-opslagplaats](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Volgende stappen

Zodra je bent ingeschreven [!DNL Platform] meldingen aan uw project, kunt u ontvangen gebeurtenissen van de [!UICONTROL Project overview]. Raadpleeg de handleiding op [Adobe I/O-gebeurtenissen overtrekken](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) voor gedetailleerde instructies over hoe te om uw gebeurtenissen te volgen.

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het interpreteren van gegevensinvoer-berichtladingen.

### Beschikbare statusmeldingsgebeurtenissen {#event-codes}

In de volgende tabel staan de statusmeldingen voor gegevensinvoer waarop u zich kunt abonneren.

| Gebeurteniscode | Platform Service | Status | Beschrijving van een gebeurtenis |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | Een partij werd succesvol opgenomen in een dataset binnen [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fout | Een partij kon niet in een dataset binnen worden opgenomen [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | succes | Een batch is opgenomen in de [!DNL Profile] gegevensopslag. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | fout | Er kan geen batch in de [!DNL Profile] gegevensopslag. |
| `ig_load_success` | [!DNL Identity Service] | succes | Gegevens zijn geladen in de identiteitsgrafiek. |
| `ig_load_failure` | [!DNL Identity Service] | fout | Gegevens kunnen niet in de identiteitsgrafiek worden geladen. |

>[!NOTE]
>
>Er is slechts één gebeurtenisonderwerp dat voor alle gegevens wordt verstrekt die berichten invoeren. Om onderscheid te maken tussen verschillende statussen, kan de gebeurteniscode worden gebruikt.
