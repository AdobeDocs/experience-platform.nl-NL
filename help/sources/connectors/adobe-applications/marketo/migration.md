---
title: ECID-toewijzing migreren van persoon naar activiteit met de bron van het Marketo Engage
description: Leer hoe te om uw ECID afbeelding van de persoondataset aan de activiteitendataset te migreren gebruikend de bron van het Marketo Engage.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# ECID-toewijzing migreren vanuit [!DNL Person] gegevensset naar [!DNL Activity] gegevensset

U kunt uw ECID-toewijzing migreren vanuit uw [!DNL Marketo Engage Person] gegevensset naar uw [!DNL Activity] dataset om een stabieler gedrag van gegevensopname en identiteitsbeheer te verstrekken. Bovendien, richt deze migratie het volgende:

| Probleem | Oplossing |
| --- | --- |
| Wanneer uw [!DNL Marketo Person] dataset heeft verbindingen aan veelvoudige ECIDs, ontbreekt de gegevensopname wanneer [totaal aantal identiteiten in een XDM-record (Experience Data Model) groter is dan 20](../../../../identity-service/guardrails.md). | Door de ECID-veldtoewijzing te migreren naar [!DNL Activity], kunt u ervoor zorgen dat het aantal identiteiten van [!DNL Marketo Person] dataflow blijft binnen de limiet en maakt het dus mogelijk gegevens in te voeren. |
| Telkens als [!DNL Marketo Person] dataset wordt opgenomen met ECIDs, timestamp op alle ECIDs van [!DNL Marketo Person] dataset wordt bijgewerkt met laatste bijgewerkte timestamp van het Person verslag. Dit kan leiden tot [onjuiste verwijdering van recentere identiteiten uit de identiteitsgrafiek](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | De ECID-veldtoewijzingen migreren naar [!DNL Activity]Identiteitsdienst kan de tijdstempel van ECID&#39;s correct weergeven en het &quot;first-in, first-out&quot; mechanisme van Identity Service zal een stabieler gedrag opleveren. |
| Wanneer ECID&#39;s via [!DNL Marketo Person] dataflow, nieuw toegevoegde ECIDs niet in Experience Platform worden opgenomen tenzij er updates aan zijn [!DNL Person] opnemen in [!DNL Marketo]. | Wanneer een nieuwe ECID is gekoppeld aan de [!DNL Person] opnemen in [!DNL Marketo], kunt u die ECID-gegevens via een [!DNL Marketo Activity] en onmiddellijk een update van de identiteitsgrafiek op Experience Platform vragen. |

In wezen moet u:

* Werk uw [!DNL Marketo Activity] dataflow.
* Werk uw [!DNL Marketo Person] dataflow.

## Bijwerken [!DNL Marketo Activity] dataflow {#update-activity-dataflow}

Voer de onderstaande stappen uit om uw [!DNL Marketo Activity] dataflow:

* In Experience Platform UI, navigeer aan *Bronnen* werkruimte en zoek naar uw bestaande gegevensstroom voor [!DNL Marketo Activity] gegevens.
* Als de gegevensstroom is ingeschakeld, selecteert u de ovalen (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Update dataflow]**.
* Selecteer vervolgens **[!UICONTROL Next]** totdat u de *Toewijzing* interface.
* In de *Toewijzing* interface, selecteren **[!UICONTROL New field]** en selecteer vervolgens **[!UICONTROL Add calculated field]**. Van hier, moet u het volgende toevoegen:

| Brongegevensset | XDM-doelveld |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Als u een bestaande update uitvoert [!DNL Marketo] dataflow bestaat alleen uit het toevoegen of verwijderen van het ECID-toewijzingsveld, waarna de dataflow de historische back-fill-taak automatisch overslaat. Nieuwe gegevensinvoer vindt alleen plaats wanneer activiteitstypen zoals &quot;Bezoek webpagina&quot; en &quot;Klikken webpagina&quot; plaatsvinden.

## Bijwerken [!DNL Marketo Person] dataflow {#update-person-dataflow}

Voer de onderstaande stappen uit om uw [!DNL Marketo Person] dataflow:

* In Experience Platform UI, navigeer aan *Bronnen* werkruimte en zoek naar uw bestaande gegevensstroom voor [!DNL Marketo Person] gegevens.
* Als de gegevensstroom is ingeschakeld, selecteert u de ovalen (`...`) naast de naam van de gegevensstroom en selecteer vervolgens **[!UICONTROL Update dataflow]**.
* Selecteer vervolgens **[!UICONTROL Next]** totdat u de *Toewijzing* interface.
* In de *Toewijzing* interface, verwijder het berekende gebied dat aan in kaart brengt `identityMap` en selecteer vervolgens **[!UICONTROL Next]** en **[!UICONTROL Save & Ingest]**.

>[!NOTE]
>
>Als u een bestaande update uitvoert [!DNL Marketo] dataflow bestaat alleen uit het toevoegen of verwijderen van het ECID-toewijzingsveld, waarna de dataflow de historische back-fill-taak automatisch overslaat. De tijdstempel van eerder opgenomen ECID&#39;s blijft ongewijzigd. Deze worden alleen bijgewerkt wanneer nieuwe gegevens worden ingevoerd die overeenkomen met de bestaande ECID&#39;s.

## Volgende stappen

Door dit document te lezen, weet u nu hoe u uw ECID-toewijzing uit uw [!DNL Marketo Person] gegevensset naar [!DNL Marketo Activity] dataset. Lees voor meer informatie het volgende: [!DNL Marketo] documenten:

* [Een gegevensstroom maken om in te voeren [!DNL Marketo] gegevens naar Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Veldtoewijzingshulplijn](../mapping/marketo.md).