---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: Abonneren op gebeurtenissen voor gegevensinvoer
topic: overview
description: Om bij het controleren van het innameproces te helpen, maakt Adobe Experience Platform het mogelijk om aan een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u op de hoogte brengen van de status van de opgenomen gegevens en om het even welke mogelijke mislukkingen.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---


# Meldingen voor gegevensinvoer

Het proces om gegevens in Adobe Experience Platform in te voeren bestaat uit meerdere stappen. Zodra u gegevensdossiers identificeert die in moeten worden opgenomen [!DNL Platform], begint het innameproces en elke stap komt achtereenvolgens tot de gegevens of met succes worden opgenomen of ontbreken. Het insluitingsproces kan worden gestart met de [Adobe Experience Platform-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) voor gegevensinsluiting of met de [!DNL Experience Platform] gebruikersinterface.

De gegevens die in worden geladen [!DNL Platform] moeten door veelvoudige stappen gaan om zijn bestemming, [!DNL Data Lake] of de [!DNL Real-time Customer Profile] gegevensopslag te bereiken. Elke stap omvat het verwerken van de gegevens, het valideren van de gegevens en het opslaan van de gegevens voordat u deze doorgeeft aan de volgende stap. Afhankelijk van de hoeveelheid gegevens die wordt opgenomen, kan dit een tijdrovend proces worden en er is altijd een kans dat het proces mislukt door validatie-, semantiek- of verwerkingsfouten. In geval van een fout moeten de gegevensproblemen worden opgelost en moet het volledige innameproces opnieuw worden gestart met de gecorrigeerde gegevensbestanden.

Als u wilt helpen bij het controleren van het innameproces, [!DNL Experience Platform] kunt u zich abonneren op een set gebeurtenissen die door elke stap van het proces worden gepubliceerd, waarbij u op de hoogte wordt gebracht van de status van de ingesloten gegevens en van mogelijke fouten.

## Webhaak registreren voor meldingen over gegevensinvoer

Als u meldingen over gegevensinvoer wilt ontvangen, moet u de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) gebruiken om een webhaak te registreren voor de integratie van uw Experience Platform.

Volg de zelfstudie over het [abonneren van [!DNL Adobe I/O Event] toonmeldingen](../../observability/notifications/subscribe.md) voor gedetailleerde stappen over hoe u dit kunt doen.

>[!IMPORTANT]
>
>Zorg er tijdens het abonnementsproces voor dat u **[!UICONTROL Platform-berichten]** selecteert als gebeurtenisprovider en selecteer het **[!UICONTROL gegevensinvoer-berichtgebeurtenisabonnement]** wanneer hierom wordt gevraagd.

## Meldingen over gegevensinvoer ontvangen

Nadat u de webhaak hebt geregistreerd en nieuwe gegevens zijn ingevoerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden bekeken gebruikend webhaak zelf, of door het **** Debug vinden lusje in het overzicht van de gebeurtenisregistratie van uw project in de Console van de Ontwikkelaar van de Adobe te selecteren.

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
| `event.xdm:eventCode` | Een statuscode die het type gebeurtenis aangeeft dat voor de gegevensset is geactiveerd. Zie de [bijlage](#event-codes) voor specifieke waarden en de bijbehorende definities. |

Om het volledige schema voor gebeurtenisberichten te bekijken, verwijs naar de [openbare bewaarplaats](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)van GitHub.

## Volgende stappen

Zodra u [!DNL Platform] berichten aan uw project hebt geregistreerd, kunt u ontvangen gebeurtenissen van het overzicht [!UICONTROL van het]Project bekijken. Raadpleeg de handleiding voor het [overtrekken van Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) voor gedetailleerde instructies over het overtrekken van gebeurtenissen.

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het interpreteren van gegevensinvoer-berichtladingen.

### Beschikbare statusmeldingsgebeurtenissen {#event-codes}

In de volgende tabel staan de statusmeldingen voor gegevensinvoer waarop u zich kunt abonneren.

| Gebeurteniscode | Platform Service | Status | Beschrijving van gebeurtenis |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | succes | Een partij werd succesvol opgenomen in een dataset binnen [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | fout | Een partij kon niet in een dataset binnen [!DNL Data Lake]worden opgenomen. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | succes | Een batch is opgenomen in de [!DNL Profile] gegevensopslag. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | fout | Een batch kan niet in de [!DNL Profile] gegevensopslag worden opgenomen. |
| `ig_load_success` | [!DNL Identity Service] | succes | Gegevens zijn geladen in de identiteitsgrafiek. |
| `ig_load_failure` | [!DNL Identity Service] | fout | Gegevens kunnen niet in de identiteitsgrafiek worden geladen. |

>[!NOTE]
>
>Er is slechts één gebeurtenisonderwerp dat voor alle gegevens wordt verstrekt die berichten invoeren. Om onderscheid te maken tussen verschillende statussen, kan de gebeurteniscode worden gebruikt.