---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Abonneren op Privacy Service Events
description: Leer hoe te om aan de gebeurtenissen van de Privacy Service in te schrijven gebruikend een vooraf gevormde webhaak.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 1%

---

# Abonneren op [!DNL Privacy Service Events]

[!DNL Privacy Service Events] zijn berichten die worden geleverd door Adobe Experience Platform [!DNL Privacy Service] . Deze berichten maken gebruik van Adobe I/O Events die naar een geconfigureerde webhaak worden verzonden om een efficiënte automatisering van taakaanvragen te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de [!DNL Privacy Service] API te raadplegen om te controleren of een taak voltooid is of dat een bepaalde mijlpaal in een workflow is bereikt.

Er zijn momenteel vier typen meldingen die betrekking hebben op de levenscyclus van de privacytaakaanvraag:

| Type | Beschrijving |
| --- | --- |
| Taak voltooid | Alle [!DNL Experience Cloud] -toepassingen hebben een melding ontvangen en de algemene of algemene status van de taak is als voltooid gemarkeerd. |
| Taakfout | Een of meer toepassingen hebben een fout gemeld tijdens het verwerken van de aanvraag. |
| Product voltooid | Een van de toepassingen voor deze taak heeft zijn werk voltooid. |
| Productfout | Een van de toepassingen heeft een fout gemeld tijdens het verwerken van de aanvraag. |

Dit document bevat stappen voor het instellen van een gebeurtenisregistratie voor [!DNL Privacy Service] -meldingen en voor het interpreteren van berichtladingen.

## Aan de slag

Raadpleeg de volgende documentatie bij de Privacy Service voordat u deze zelfstudie start:

* [Overzicht van Privacy Service](./home.md)
* [Handleiding Privacy Service-API](./api/overview.md)

## Webhaak registreren voor [!DNL Privacy Service Events]

Als u [!DNL Privacy Service Events] wilt ontvangen, moet u Adobe Developer Console gebruiken om een webhaak te registreren voor uw [!DNL Privacy Service] -integratie.

Volg het leerprogramma op [ het intekenen aan [!DNL I/O Gebeurtenis] berichten ](../observability/alerts/subscribe.md) voor gedetailleerde stappen op hoe te om dit te verwezenlijken. Zorg ervoor dat u **[!UICONTROL Privacy Service Events]** als uw gebeurtenisprovider kiest om toegang te krijgen tot de hierboven vermelde gebeurtenissen.

## [!DNL Privacy Service Event] meldingen ontvangen

Nadat u de webhaak en privacytaken hebt geregistreerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden weergegeven met de webhaak zelf of door het tabblad **[!UICONTROL Debug Tracing]** te selecteren in het overzicht met gebeurtenisregistratie in Adobe Developer Console van uw project.

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
| `type` | Het type melding dat wordt verzonden, met een context voor de informatie die onder `data` wordt verstrekt. Mogelijke waarden zijn: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Een tijdstempel van wanneer de gebeurtenis heeft plaatsgevonden. |
| `data.value` | Bevat aanvullende informatie over de aanleiding voor de kennisgeving: <ul><li>`jobId`: De id van de privacytaak die de melding heeft geactiveerd.</li><li>`message`: Een bericht over de specifieke status van de taak. Voor `productcomplete` - of `producterror` -berichten geeft dit veld de desbetreffende toepassing van het Experience Cloud aan.</li></ul> |

## Volgende stappen

In dit document wordt beschreven hoe u Privacy Service-gebeurtenissen kunt registreren voor een geconfigureerde webhaak en hoe u berichtladingen kunt interpreteren. Leren hoe te om privacybanen te volgen gebruikend het gebruikersinterface, zie de [ gebruikersgids van de Privacy Service ](./ui/user-guide.md).
