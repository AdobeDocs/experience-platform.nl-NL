---
title: On-demand-insluiting voor gegevensstromen van bronnen in UI
description: Leer hoe te om gegevensstromen op bestelling voor uw bronverbindingen tot stand te brengen gebruikend het gebruikersinterface van het Experience Platform.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: 38da1c1d5e563ea3f66cc25a69ad726f709784d0
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Op bestelling opnemen voor brongegevens in de gebruikersinterface

Met de werkruimte Bronnen in de Adobe Experience Platform-gebruikersinterface kunt u op aanvraag insluiten gebruiken om een lusrun-iteratie van een bestaande gegevensstroom te activeren.

Dit document biedt u stappen over hoe te om dataflows op bestelling voor bronnen tot stand te brengen, evenals hoe te om stroomlooppas opnieuw te proberen die zijn verwerkt of ontbroken.

>[!BEGINSHADEBOX]

**wat is een stroom in werking gesteld?**

De looppas van de stroom vertegenwoordigt een geval van dataflow uitvoering. Bijvoorbeeld, als een dataflow om 09:00 AM, 10:00 AM, en 11:00 AM gepland is te lopen, dan zou u drie instanties van een stroomlooppas hebben. De looppas van de stroom is specifiek voor uw bepaalde organisatie.

>[!ENDSHADEBOX]

## Aan de slag

>[!NOTE]
>
>Als u een flowuitvoering wilt maken, moet u eerst over de flow-id van een gegevensstroom beschikken die voor eenmalige invoer is gepland.

Voor dit document is een goed begrip van de volgende onderdelen van het Experience Platform vereist:

* [ Bronnen ](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Dataflows ](../../../dataflows/home.md): Een dataflow is een vertegenwoordiging van gegevensbanen die gegevens over Platform bewegen. Dataflows worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets, aan de Dienst van de Identiteit en het Profiel van de Klant in real time, en aan Doelen helpen verplaatsen.
* [ Sandboxes ](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Een gegevensstroom op aanvraag maken {#create-a-dataflow-on-demand}

Navigeer naar het tabblad *[!UICONTROL Dataflows]* van de werkruimte Bronnen. Van hier, vind dataflow die u op bestelling wilt in werking stellen, en selecteer dan de ellipsen (**`...`**) naast uw dataflow naam.

![ een lijst van gegevens in de bronwerkruimte.](../../images/tutorials/on-demand/select-dataflow.png)

Selecteer vervolgens **[!UICONTROL Run on-demand]** in het vervolgkeuzemenu dat wordt weergegeven.

![ dropdown menu van A met de Looppas op bestelling geselecteerde optie.](../../images/tutorials/on-demand/run-on-demand.png)

Vorm het programma van uw opname op bestelling. Selecteer **[!UICONTROL Ingestion start time]**, **[!UICONTROL Date range start time]**, en **[!UICONTROL Date range end time]**.

| Configuratie plannen | Beschrijving |
| --- | --- |
| [!UICONTROL Ingestion start time] | De geplande tijd van wanneer de de stroomlooppas op bestelling zal beginnen. |
| [!UICONTROL Date range start time] | De vroegste datum en tijd waarop de gegevens worden opgehaald. |
| [!UICONTROL Date range end time] | De datum en tijd waarop de gegevens worden opgehaald tot. |

Selecteer **[!UICONTROL Schedule]** en wacht even tot uw gegevensstroom op aanvraag wordt geactiveerd.

![ het plannen configuratievenster voor op bestelling opnemen.](../../images/tutorials/on-demand/configure-schedule.png)

Selecteer de naam van uw gegevensstroom om uw gegevensstroomactiviteit te bekijken. Hier ziet u een lijst van uw dataflow looppas die zijn verwerkt. Selecteer een dataflow-run en selecteer vervolgens **[!UICONTROL Retry]** in de rechterrail om opname opnieuw te proberen voor een geselecteerde dataflow-run-iteratie.

![ een lijst van verwerkte stroomlooppas voor een geselecteerde dataflow.](../../images/tutorials/on-demand/processed.png)

Selecteer **[!UICONTROL Scheduled]** om een lijst van dataflow looppas te zien die voor toekomstige opname gepland is.

![ een lijst van geplande stroomlooppas voor geselecteerde dataflow.](../../images/tutorials/on-demand/scheduled.png)

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe te om stroomlooppas op bestelling voor bestaande brondataflows tot stand te brengen. Voor meer informatie over bronnen, lees het [ overzicht van bronnen ](../../home.md)
