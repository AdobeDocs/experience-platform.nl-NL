---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Abonneren op Privacy Service Events
topic: privacy events
description: Leer hoe te om aan de gebeurtenissen van de Privacy Service in te schrijven gebruikend een vooraf gevormde webhaak.
translation-type: tm+mt
source-git-commit: 2b919a3b6cbbd59521874cfd2d11e20de3077740
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# Abonneren op [!DNL Privacy Service Events]

[!DNL Privacy Service Events] Dit zijn berichten van Adobe Experience Platform  [!DNL Privacy Service], die Adobe I/O Events gebruiken die naar een geconfigureerde webhaak worden verzonden om efficiënte automatisering van taakaanvragen te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de [!DNL Privacy Service] API te raadplegen om te controleren of een taak voltooid is of of een bepaalde mijlpaal binnen een workflow is bereikt.

Er zijn momenteel vier typen meldingen die betrekking hebben op de levenscyclus van de privacytaakaanvraag:

| Type | Beschrijving |
| --- | --- |
| Taak voltooid | Alle [!DNL Experience Cloud] toepassingen hebben gemeld en de algemene of globale status van de baan is duidelijk volledig. |
| Taakfout | Een of meer toepassingen hebben een fout gemeld tijdens het verwerken van de aanvraag. |
| Product voltooid | Een van de toepassingen voor deze taak heeft zijn werk voltooid. |
| Productfout | Een van de toepassingen heeft een fout gemeld tijdens het verwerken van de aanvraag. |

Dit document bevat stappen voor het instellen van een gebeurtenisregistratie voor [!DNL Privacy Service]-berichten en voor het interpreteren van berichtladingen.

## Aan de slag

Raadpleeg de volgende documentatie bij de Privacy Service voordat u deze zelfstudie start:

* [Overzicht van Privacy Service](./home.md)
* [Handleiding voor ontwikkelaars van Privacy Service-API](./api/getting-started.md)

## Webhaak registreren voor [!DNL Privacy Service Events]

Als u [!DNL Privacy Service Events] wilt ontvangen, moet u de Adobe Developer Console gebruiken om een webhaak te registreren voor uw [!DNL Privacy Service]-integratie.

Volg de zelfstudie op [Abonneren op [!DNL I/O Event] notifications](../observability/notifications/subscribe.md) voor gedetailleerde stappen op hoe te om dit te verwezenlijken. Zorg ervoor dat u **[!UICONTROL Gebeurtenissen van de Privacy Service]** als uw gebeurtenisleverancier kiest om tot de hierboven vermelde gebeurtenissen toegang te hebben.

## [!DNL Privacy Service Event] meldingen ontvangen

Nadat u de webhaak en privacytaken hebt geregistreerd, kunt u gebeurtenismeldingen ontvangen. Deze gebeurtenissen kunnen worden bekeken gebruikend de webhaak zelf, of door **[!UICONTROL Debug het Vinden]** lusje in het de gebeurtenisregistratieoverzicht van uw project in de Console van de Ontwikkelaar van Adobe te selecteren.

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
| `type` | Het type kennisgeving dat wordt verzonden, met context voor de informatie die wordt verstrekt onder `data`. Mogelijke waarden zijn: <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | Een tijdstempel van wanneer de gebeurtenis heeft plaatsgevonden. |
| `data.value` | Bevat aanvullende informatie over de aanleiding voor de kennisgeving: <ul><li>`jobId`: De id van de privacytaak die de melding heeft geactiveerd.</li><li>`message`: Een bericht over de specifieke status van de baan. Voor `productcomplete`- of `producterror`-berichten geeft dit veld de Experience Cloud-toepassing in kwestie aan.</li></ul> |

## Volgende stappen

In dit document wordt beschreven hoe u Privacy Service-gebeurtenissen kunt registreren voor een geconfigureerde webhaak en hoe u berichtladingen kunt interpreteren. Zie [Gebruikershandleiding voor Privacys Service](./ui/user-guide.md) voor meer informatie over het bijhouden van privacytaken via de gebruikersinterface.