---
keywords: Experience Platform;home;populaire onderwerpen;datumbereik
title: Overzicht van waarschuwingen
description: Meer informatie over waarschuwingen in Adobe Experience Platform, inclusief de structuur van hoe waarschuwingsregels worden gedefinieerd.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: 829d7da1dc53486eba1cdceddb7888b578e1c137
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Overzicht van waarschuwingen

>[!NOTE]
>
>Aangezien waarschuwingen worden ondersteund in zowel productie- als ontwikkelingssandboxen, kunt u zich hierop in elke sandbox abonneren. Wanneer een sandbox opnieuw wordt ingesteld, worden ook alle abonnementswaarschuwingen opnieuw ingesteld. Wanneer een sandbox wordt verwijderd, worden alle abonnementswaarschuwingen verwijderd.

Met Adobe Experience Platform kunt u zich abonneren op waarschuwingen voor gebeurtenissen met betrekking tot Adobe Experience Platform-activiteiten. Het alarm vermindert of elimineert de behoefte om [[!DNL Observability Insights]  API ](../api/overview.md) te peilen om te controleren als een baan heeft voltooid, als een bepaalde mijlpaal binnen een werkschema is bereikt, of als om het even welke fouten zijn voorgekomen.

Wanneer een bepaalde reeks voorwaarden in uw verrichtingen van het Platform wordt bereikt (zoals een potentieel probleem wanneer het systeem een drempel) schendt, kan het Platform waakzame berichten aan om het even welke gebruikers in uw organisatie leveren die aan hen hebben ingetekend. Deze berichten kunnen over een vooraf bepaald tijdinterval herhalen tot het alarm is opgelost.

Dit document biedt een overzicht van waarschuwingen in Adobe Experience Platform, inclusief de structuur van de wijze waarop waarschuwingsregels worden gedefinieerd.

## Eenmalige waarschuwingen versus herhaalde waarschuwingen

Platformwaarschuwingen kunnen één keer worden verzonden of worden herhaald gedurende een vooraf gedefinieerd interval totdat ze zijn opgelost. De gebruiksgevallen van elk van deze opties zijn bedoeld om op de volgende manieren te verschillen:

| Eenmalige waarschuwing | Herhalingswaarschuwing |
| --- | --- |
| Geeft niet noodzakelijkerwijs een probleem aan. | Geeft een mogelijk ongewenste status aan. |
| Wordt niet herhaald. | Kan herhalen als de afwijkende situatie aanhoudt. |
| Voorbeelden zijn:<ul><li>Gegevens zijn ingevoerd.</li><li>De uitvoering van een query is voltooid.</li><li>Gegevens zijn verwijderd.</li></ul> | Voorbeelden zijn:<ul><li>De duur van de inname overschrijdt de service-level overeenkomst (SLA).</li><li>Dagelijkse inname vond niet plaats in de afgelopen 24 uur.</li><li>De foutensnelheid van de stroombewerker is boven de gevormde drempel.</li><li>Het totale aantal profielen overschrijdt de machtiging.</li></ul> |

{style="table-layout:auto"}

## Anatomie van een waarschuwing

Een alarm kan in de volgende componenten worden verdeeld:

| Component | Beschrijving |
| --- | --- |
| **Metrisch** | Een metrische van de Waarneming [ ](../api/metrics.md#available-metrics) de waarvan waarde het alarm, zoals het aantal ontbroken partijingestitiegebeurtenissen teweegbrengt (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condition** | Een voorwaarde met betrekking tot metrisch die het alarm teweegbrengt als het aan waar, zoals telmetrisch die een bepaald aantal overschrijdt. Deze voorwaarde kan aan een vooraf bepaald tijdvenster worden geassocieerd. |
| **Venster** | (Optioneel) De voorwaarde voor een waarschuwing kan worden beperkt tot een vooraf gedefinieerd tijdvenster. Een waarschuwing kan bijvoorbeeld worden geactiveerd afhankelijk van het aantal mislukte batches in de afgelopen vijf minuten. |
| **Actie** | Wanneer een alarm wordt teweeggebracht, wordt een actie uitgevoerd. Specifiek, worden de berichten verzonden naar toepasselijke ontvangers door een leveringskanaal, zoals een pre-gevormde webhaak of Experience Platform UI. |
| **Frequentie** | (Optioneel) Een waarschuwing kan worden geconfigureerd om de handeling met een bepaald interval te herhalen als de voorwaarde waar blijft of op een andere manier niet wordt opgelost. |

{style="table-layout:auto"}

## Ontvangen en beheren van waarschuwingen

U kunt waarschuwingen ontvangen en beheren via twee kanalen:

* [Adobe I/O Events](#events)
* [Platforminterface](#ui)

### I/O-gebeurtenissen {#events}

U kunt waarschuwingen verzenden naar een geconfigureerde webhaak om een efficiënte automatisering van de bewaking van activiteiten te vergemakkelijken. Als u waarschuwingen wilt ontvangen via webhaak, moet u uw webhaak registreren voor Platformwaarschuwingen in Adobe Developer Console. Zie de gids op [ het intekenen aan de berichten van de Gebeurtenis van Adobe I/O ](./subscribe.md) voor specifieke stappen.

### Platforminterface {#ui}

De interface van het Platform staat u toe om ontvangen alarm te bekijken en waakzame regels te beheren. De volgende video biedt een inleiding tot deze mogelijkheden.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Als u met waarschuwingen wilt werken in de interface van het platform, moet u de volgende toegangsbeheermachtigingen hebben ingeschakeld via Adobe Admin Console:

| Machtiging | Beschrijving |
| --- | --- |
| Waarschuwingen weergeven | Hiermee kunt u ontvangen waarschuwingsberichten weergeven. |
| Geschiedenis van waarschuwingen weergeven* | Hiermee kunt u een geschiedenis van ontvangen waarschuwingen weergeven via het tabblad [!UICONTROL Alerts] . |
| Waarschuwingen beheren* | Hiermee kunt u waarschuwingsregels in- en uitschakelen via de tab [!UICONTROL Alerts] . |
| Waarschuwingen oplossen* | Hiermee kunt u getriggerde waarschuwingen oplossen via het tabblad [!UICONTROL Alerts] . |

{style="table-layout:auto"}

**om tot het [!UICONTROL Alerts] lusje toegang te hebben, moet u ook de toestemming van het Alarm van de Mening in combinatie met één van de andere toestemmingen worden verleend.*

>[!NOTE]
>
>Voor meer informatie over hoe te om toestemmingen in Platform te beheren, verwijs naar de [ documentatie van de toegangscontrole ](../../access-control/ui/overview.md).

Met de toestemming van het Alarm van de Mening, kan ontvangen alarm bekijken door het klokpictogram (![ Pictogram van de Telling ](/help/images/icons/bell.png)) in de hoger-juiste hoek te selecteren.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Selecteer een waarschuwing om naar een verwant dashboard te navigeren voor meer gedetailleerde informatie over waarom de alarm is teweeggebracht.

Bovendien staat het [!UICONTROL Alerts] lusje in UI individuele gebruikers toe om aan specifieke waakzame types in te tekenen, en staat beheerders toe om waakzame regels geheel toe te laten of onbruikbaar te maken. Zie de [ gids UI ](./ui.md) voor meer informatie bij het beheren van alarm.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in Platformwaarschuwingen en hun rol in het ecosysteem van het Platform. Raadpleeg de procesdocumentatie waarnaar in dit overzicht wordt verwezen voor meer informatie over het ontvangen en beheren van waarschuwingen.
