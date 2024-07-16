---
title: ECID-toewijzing migreren van persoon naar activiteit met de bron van het Marketo Engage
description: Leer hoe te om uw ECID afbeelding van de persoondataset aan de activiteitendataset te migreren gebruikend de bron van het Marketo Engage.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# ECID-toewijzing migreren van [!DNL Person] dataset naar [!DNL Activity] dataset

U kunt uw ECID-toewijzing migreren van uw [!DNL Marketo Engage Person] -gegevensset naar uw [!DNL Activity] -gegevensset voor een stabieler gedrag bij gegevensinvoer en identiteitsbeheer. Bovendien, richt deze migratie het volgende:

| Probleem | Oplossing |
| --- | --- |
| Wanneer uw [!DNL Marketo Person] dataset verbindingen aan veelvoudige ECIDs heeft, ontbreekt de gegevensopname wanneer het [ totale aantal identiteiten in een verslag van de Gegevens van de Ervaring van het Model (XDM) 20 ](../../../../identity-service/guardrails.md) overschrijdt. | Door de ECID-veldtoewijzing te migreren naar [!DNL Activity], kunt u ervoor zorgen dat het aantal identiteiten van de [!DNL Marketo Person] -gegevensstroom binnen de limiet blijft en dat het opnemen van gegevens daardoor lukt. |
| Telkens wanneer de [!DNL Marketo Person] dataset met ECIDs wordt opgenomen, wordt timestamp op alle ECIDs van de [!DNL Marketo Person] dataset bijgewerkt met laatste bijgewerkte timestamp van het Person verslag. Dit kon in de [ onjuiste schrapping van recentere identiteiten van de identiteitsgrafiek ](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated) resulteren. | Door de ECID-veldtoewijzingen naar [!DNL Activity] te migreren, kan Identity Service de tijdstempel van ECID&#39;s correct weerspiegelen en het &quot;first-in, first-out&quot; mechanisme van Identity Service zal een stabieler gedrag opleveren. |
| Wanneer ECID&#39;s via [!DNL Marketo Person] dataflow worden opgenomen, worden nieuw toegevoegde ECID&#39;s niet in het Experience Platform opgenomen, tenzij de [!DNL Person] record in [!DNL Marketo] wordt bijgewerkt. | Wanneer een nieuwe ECID is gekoppeld aan de [!DNL Person] -record in [!DNL Marketo] , kunt u die ECID-gegevens invoeren via een [!DNL Marketo Activity] -gegevensstroom en direct een update van de identiteitsgrafiek op het Experience Platform vragen. |

In wezen moet u:

* Werk de [!DNL Marketo Activity] -gegevensstroom bij.
* Werk de [!DNL Marketo Person] -gegevensstroom bij.

## [!DNL Marketo Activity] -gegevensstroom bijwerken {#update-activity-dataflow}

Voer de onderstaande stappen uit om uw [!DNL Marketo Activity] -gegevensstroom bij te werken:

* In het Experience Platform UI, navigeer aan de *Bronnen* werkruimte en vind uw bestaande dataflow voor [!DNL Marketo Activity] gegevens.
* Aangezien de gegevensstroom wordt toegelaten, selecteer de ellipsen (`...`) naast de dataflow naam en selecteer dan **[!UICONTROL Update dataflow]**.
* Dan, selecteer **[!UICONTROL Next]** tot u de *Afbeelding* interface bereikt.
* In de *interface van de Toewijzing*, selecteer **[!UICONTROL New field]** en selecteer dan **[!UICONTROL Add calculated field]**. Van hier, moet u het volgende toevoegen:

| Source-gegevensset | XDM-doelveld |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Als uw update naar een bestaande [!DNL Marketo] -gegevensstroom alleen bestaat uit het toevoegen of verwijderen van het ECID-toewijzingsveld, slaat de gegevensstroom automatisch de historische back-uptaak over. Nieuwe gegevensinvoer vindt alleen plaats wanneer activiteitstypen zoals &quot;Bezoek webpagina&quot; en &quot;Klikken webpagina&quot; plaatsvinden.

## [!DNL Marketo Person] -gegevensstroom bijwerken {#update-person-dataflow}

Voer de onderstaande stappen uit om uw [!DNL Marketo Person] -gegevensstroom bij te werken:

* In het Experience Platform UI, navigeer aan de *Bronnen* werkruimte en vind uw bestaande dataflow voor [!DNL Marketo Person] gegevens.
* Aangezien de gegevensstroom wordt toegelaten, selecteer de ellipsen (`...`) naast de dataflow naam en selecteer dan **[!UICONTROL Update dataflow]**.
* Dan, selecteer **[!UICONTROL Next]** tot u de *Afbeelding* interface bereikt.
* In de *interface van de Toewijzing*, verwijder het berekende gebied dat aan `identityMap` toewijst en selecteer dan **[!UICONTROL Next]** en **[!UICONTROL Save & Ingest]**.

>[!NOTE]
>
>Als uw update naar een bestaande [!DNL Marketo] -gegevensstroom alleen bestaat uit het toevoegen of verwijderen van het ECID-toewijzingsveld, slaat de gegevensstroom automatisch de historische back-uptaak over. De tijdstempel van eerder opgenomen ECID&#39;s blijft ongewijzigd. Deze worden alleen bijgewerkt wanneer nieuwe gegevens worden ingevoerd die overeenkomen met de bestaande ECID&#39;s.

## Volgende stappen

Door dit document te lezen, weet u nu hoe u uw ECID-toewijzing vanuit uw [!DNL Marketo Person] -dataset naar [!DNL Marketo Activity] -dataset kunt migreren. Lees de volgende [!DNL Marketo] -documenten voor meer informatie:

* [ creeer een dataflow om  [!DNL Marketo]  gegevens aan Experience Platform ](../../../tutorials/ui/create/adobe-applications/marketo.md) in te voeren.
* [ de afbeeldingsgids van het Gebied ](../mapping/marketo.md).
