---
keywords: Experience Platform;home;populaire onderwerpen;meldingen over het invoeren van gegevens;meldingen;subscribe gebeurtenissen;statusgebeurtenissen voor het invoeren van gegevens;statusgebeurtenissen;subscribe;statusmeldingen;
solution: Experience Platform
title: Gegevensinscriptie
topic: overview
description: Om bij het controleren van het innameproces te helpen, maakt Adobe Experience Platform het mogelijk om aan een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u op de hoogte brengen van de status van de opgenomen gegevens en om het even welke mogelijke mislukkingen.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '681'
ht-degree: 0%

---


# Meldingen voor gegevensinvoer

Het proces om gegevens in Adobe Experience Platform in te voeren bestaat uit meerdere stappen. Zodra u gegevensdossiers identificeert die in [!DNL Platform] moeten worden opgenomen, begint het innameproces en elke stap komt achtereenvolgens tot de gegevens of met succes worden opgenomen of ontbreken. Het insluitingsproces kan worden gestart met de [Adobe Experience Platform-API voor gegevensinsluiting](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) of met de [!DNL Experience Platform]-gebruikersinterface.

Gegevens die in [!DNL Platform] worden geladen, moeten meerdere stappen doorlopen om het doel, de [!DNL Data Lake] of de [!DNL Real-time Customer Profile] gegevensopslag te bereiken. Elke stap omvat het verwerken van de gegevens, het valideren van de gegevens en het opslaan van de gegevens voordat u deze doorgeeft aan de volgende stap. Afhankelijk van de hoeveelheid gegevens die wordt opgenomen, kan dit een tijdrovend proces worden en er is altijd een kans dat het proces mislukt door validatie-, semantiek- of verwerkingsfouten. In geval van een fout moeten de gegevensproblemen worden opgelost en moet het volledige innameproces opnieuw worden gestart met de gecorrigeerde gegevensbestanden.

Als hulp bij het controleren van het innameproces, [!DNL Experience Platform] maakt het mogelijk om aan een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u aan de status van de ingeopgenomen gegevens en om het even welke mogelijke mislukkingen op de hoogte brengen.

## Webhaak registreren voor meldingen over gegevensinvoer

Als u meldingen over gegevensinvoer wilt ontvangen, moet u [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) gebruiken om een webhaak te registreren voor de integratie van uw Experience Platform.

Volg de zelfstudie op [Abonneren op [!DNL Adobe I/O Event] notifications](../../observability/notifications/subscribe.md) voor gedetailleerde stappen op hoe te om dit te verwezenlijken.

>[!IMPORTANT]
>
>Tijdens het abonnementsproces, zorg ervoor dat u **[!UICONTROL Platform berichten]** als gebeurtenisleverancier selecteert, en **[!UICONTROL de kennisgeving van de opname van Gegevens]** gebeurtenisabonnement selecteert wanneer ertoe aangezet.

## Meldingen over gegevensinvoer ontvangen

Nadat u de webhaak hebt geregistreerd en nieuwe gegevens zijn ingevoerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden bekeken gebruikend de webhaak zelf, of door **[!UICONTROL Debug het Vinden]** lusje in het de gebeurtenisregistratieoverzicht van uw project in de Console van de Ontwikkelaar van Adobe te selecteren.

De volgende JSON is een voorbeeld van een berichtlading die naar uw webhaak in het geval van een ontbroken partijingestitie gebeurtenis zou worden verzonden:

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
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
| `event.xdm:eventCode` | Een statuscode die het type gebeurtenis aangeeft dat voor de gegevensset is geactiveerd. Zie [appendix](#event-codes) voor specifieke waarden en hun definities. |

Om het volledige schema voor gebeurtenisberichten te bekijken, verwijs naar [openbare bewaarplaats GitHub](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## Volgende stappen

Zodra u [!DNL Platform] berichten aan uw project hebt geregistreerd, kunt u ontvangen gebeurtenissen van [!UICONTROL Overzicht van het Project] bekijken. Raadpleeg de handleiding bij [Het overtrekken van Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) voor gedetailleerde instructies over hoe u gebeurtenissen kunt overtrekken.

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het interpreteren van gegevensinvoer-berichtladingen.

### Beschikbare statusmeldingsgebeurtenissen {#event-codes}

In de volgende tabel staan de statusmeldingen voor gegevensinvoer waarop u zich kunt abonneren.

| Gebeurteniscode | Platform Service | Status | Beschrijving van gebeurtenis |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | succes | Een partij werd succesvol opgenomen in een dataset binnen [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fout | Een partij kon niet in een dataset binnen [!DNL Data Lake] worden opgenomen. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | succes | Een batch is opgenomen in de gegevensopslag [!DNL Profile]. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | fout | Een batch kan niet worden ingevoerd in de [!DNL Profile] gegevensopslag. |
| `ig_load_success` | [!DNL Identity Service] | succes | Gegevens zijn geladen in de identiteitsgrafiek. |
| `ig_load_failure` | [!DNL Identity Service] | fout | Gegevens kunnen niet in de identiteitsgrafiek worden geladen. |

>[!NOTE]
>
>Er is slechts één gebeurtenisonderwerp dat voor alle gegevens wordt verstrekt die berichten invoeren. Om onderscheid te maken tussen verschillende statussen, kan de gebeurteniscode worden gebruikt.