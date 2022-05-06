---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Abonneren op Privacy Service Events
topic-legacy: privacy events
description: Leer hoe te om aan de gebeurtenissen van de Privacy Service in te schrijven gebruikend een vooraf gevormde webhaak.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 1%

---

# Abonneren op [!DNL Privacy Service Events]

[!DNL Privacy Service Events] zijn berichten van Adobe Experience Platform [!DNL Privacy Service], die gebruikmaakt van Adobe I/O-gebeurtenissen die naar een geconfigureerde webhaak worden verzonden om efficiënte automatisering van taakaanvragen te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de [!DNL Privacy Service] API om te controleren of een baan volledig is of een bepaalde mijlpaal binnen een werkschema is bereikt.

Er zijn momenteel vier typen meldingen die betrekking hebben op de levenscyclus van de privacytaakaanvraag:

| Type | Beschrijving |
| --- | --- |
| Taak voltooid | Alles [!DNL Experience Cloud] de aanvragen zijn teruggestuurd en de algemene of algemene status van de baan is als volledig gemarkeerd. |
| Taakfout | Een of meer toepassingen hebben een fout gemeld tijdens het verwerken van de aanvraag. |
| Product voltooid | Een van de toepassingen voor deze taak heeft zijn werk voltooid. |
| Productfout | Een van de toepassingen heeft een fout gemeld tijdens het verwerken van de aanvraag. |

Dit document bevat stappen voor het instellen van een gebeurtenisregistratie voor [!DNL Privacy Service] meldingen en hoe u berichtlading kunt interpreteren.

## Aan de slag

Raadpleeg de volgende documentatie bij de Privacy Service voordat u deze zelfstudie start:

* [Overzicht van Privacy Service](./home.md)
* [Handleiding Privacy Service-API](./api/overview.md)

## Webhaak registreren voor [!DNL Privacy Service Events]

Om [!DNL Privacy Service Events], moet u Adobe Developer Console gebruiken om een webhaak te registreren bij uw [!DNL Privacy Service] integratie.

Volg de zelfstudie op [abonneren op [!DNL I/O Event]-meldingen](../observability/alerts/subscribe.md) voor gedetailleerde stappen over hoe te om dit te verwezenlijken. Zorg ervoor dat u **[!UICONTROL Privacy Service Events]** als uw gebeurtenisprovider om toegang te krijgen tot de hierboven vermelde gebeurtenissen.

## Ontvangen [!DNL Privacy Service Event] meldingen

Nadat u de webhaak en privacytaken hebt geregistreerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden weergegeven met de webhaak zelf of door de **[!UICONTROL Debug Tracing]** in het overzicht van de gebeurtenisregistratie van uw project in Adobe Developer Console.

![](images/privacy-events/debug-tracing.png)

De volgende JSON is een voorbeeld van een [!DNL Privacy Service Event] berichtlading die naar uw website zou worden verzonden wanneer één van de toepassingen verbonden aan een privacybaan zijn werk heeft voltooid:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
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
| `type` | Het soort kennisgeving dat wordt verzonden, met vermelding van de context van de krachtens `data`. Mogelijke waarden zijn: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Een tijdstempel van wanneer de gebeurtenis heeft plaatsgevonden. |
| `data.value` | Bevat aanvullende informatie over de aanleiding voor de kennisgeving: <ul><li>`jobId`: De id van de privacytaak die de melding heeft geactiveerd.</li><li>`message`: Een bericht over de specifieke status van de baan. Voor `productcomplete` of `producterror` in dit veld wordt de desbetreffende Experience Cloud-toepassing aangegeven.</li></ul> |

## Volgende stappen

In dit document wordt beschreven hoe u Privacy Service-gebeurtenissen kunt registreren voor een geconfigureerde webhaak en hoe u berichtladingen kunt interpreteren. Als u wilt leren hoe u privacytaken kunt bijhouden via de gebruikersinterface, raadpleegt u de [Gebruikershandleiding voor Privacy Service](./ui/user-guide.md).
