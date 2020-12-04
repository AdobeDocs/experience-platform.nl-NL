---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abonneren op Privacy Service Events
topic: privacy events
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 1%

---


# Abonneren op [!DNL Privacy Service Events]

[!DNL Privacy Service Events] Dit zijn berichten van Adobe Experience Platform [!DNL Privacy Service], die Adobe I/O Events gebruiken die naar een geconfigureerde webhaak worden verzonden om efficiënte automatisering van taakaanvragen te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de [!DNL Privacy Service] API te raadplegen om te controleren of een taak voltooid is of dat een bepaalde mijlpaal in een werkstroom is bereikt.

Er zijn momenteel vier typen meldingen die betrekking hebben op de levenscyclus van de privacytaakaanvraag:

| Type | Beschrijving |
| --- | --- |
| Taak voltooid | Alle [!DNL Experience Cloud] toepassingen zijn gemeld en de algemene of algemene status van de taak is als voltooid gemarkeerd. |
| Taakfout | Een of meer toepassingen hebben een fout gemeld tijdens het verwerken van de aanvraag. |
| Product voltooid | Een van de toepassingen voor deze taak heeft zijn werk voltooid. |
| Productfout | Een van de toepassingen heeft een fout gemeld tijdens het verwerken van de aanvraag. |

Dit document bevat stappen voor het instellen van een gebeurtenisregistratie voor [!DNL Privacy Service] meldingen en voor het interpreteren van berichtladingen.

## Aan de slag

Raadpleeg de volgende documentatie bij de Privacy Service voordat u deze zelfstudie start:

* [Overzicht van Privacy Service](./home.md)
* [Handleiding voor ontwikkelaars van Privacy Service-API](./api/getting-started.md)

## Webhaak registreren voor [!DNL Privacy Service Events]

Om te worden ontvangen [!DNL Privacy Service Events], moet u de Console van de Ontwikkelaar van Adobe gebruiken om een webhaak aan uw [!DNL Privacy Service] integratie te registreren.

Volg de zelfstudie over het [abonneren van [!DNL I/O Event] toonmeldingen](../observability/notifications/subscribe.md) voor gedetailleerde stappen over hoe u dit kunt doen. Zorg ervoor dat u Gebeurtenissen **[!UICONTROL van de]** Privacy Service als uw gebeurtenisleverancier kiest om tot de hierboven vermelde gebeurtenissen toegang te hebben.

## Meldingen ontvangen [!DNL Privacy Service Event]

Nadat u de webhaak en privacytaken hebt geregistreerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden bekeken gebruikend webhaak zelf, of door het **** Debug vinden lusje in het overzicht van de gebeurtenisregistratie van uw project in de Console van de Ontwikkelaar van de Adobe te selecteren.

![](images/privacy-events/debug-tracing.png)

De volgende JSON is een voorbeeld van een [!DNL Privacy Service Event] berichtlading die naar uw webhaak zou worden verzonden wanneer één van de toepassingen verbonden aan een privacybaan zijn werk heeft voltooid:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | Een unieke, door het systeem gegenereerde id voor het bericht. |
| `type` | Het soort kennisgeving dat wordt verzonden, met vermelding van de context van de krachtens `data`deze verordening verstrekte informatie. Mogelijke waarden zijn: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Een tijdstempel van wanneer de gebeurtenis heeft plaatsgevonden. |
| `data.value` | Bevat aanvullende informatie over de aanleiding voor de kennisgeving: <ul><li>`jobId`: De id van de privacytaak die de melding heeft geactiveerd.</li><li>`message`: Een bericht over de specifieke status van de baan. Voor `productcomplete` of `producterror` meldingen geeft dit veld de desbetreffende Experience Cloud-toepassing aan.</li></ul> |

## Volgende stappen

In dit document wordt beschreven hoe u Privacy Service-gebeurtenissen kunt registreren voor een geconfigureerde webhaak en hoe u berichtladingen kunt interpreteren. Raadpleeg de gebruikershandleiding bij de [Privacy Service voor informatie over het bijhouden van privacytaken via de gebruikersinterface](./ui/user-guide.md).