---
title: On-demand-insluiting voor gegevensstromen van bronnen in UI
description: Leer hoe u op aanvraag gegevensstromen voor uw bronverbindingen kunt maken via de Experience Platform-gebruikersinterface.
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: fabacf273fb5774ddcee42d0cdcf12281eb0216b
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Op bestelling opnemen voor brongegevens in de gebruikersinterface

Met de werkruimte Bronnen in de Adobe Experience Platform-gebruikersinterface kunt u op aanvraag insluiten gebruiken om een lusrun-iteratie van een bestaande gegevensstroom te activeren.

Dit document biedt u stappen over hoe te om dataflows op bestelling voor bronnen tot stand te brengen, evenals hoe te om stroomlooppas opnieuw te proberen die zijn verwerkt of ontbroken.

>[!BEGINSHADEBOX]

**wat is een stroom in werking gesteld?**

De looppas van de stroom vertegenwoordigt een geval van dataflow uitvoering. Bijvoorbeeld, als een dataflow om bij 9 :00 AM, 10 :00 AM, en 11 :00 AM gepland is te lopen, dan zou u drie instanties van een stroomlooppas hebben. De looppas van de stroom is specifiek voor uw bepaalde organisatie.

>[!ENDSHADEBOX]

## Aan de slag

>[!NOTE]
>
>Als u een flowuitvoering wilt maken, moet u eerst over de flow-id van een gegevensstroom beschikken die voor eenmalige invoer is gepland.

Voor dit document is een goed begrip van de volgende Experience Platform-componenten vereist:

* [&#x200B; Bronnen &#x200B;](../../home.md): Experience Platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van Experience Platform.
* [&#x200B; Dataflows &#x200B;](../../../dataflows/home.md): Een dataflow is een vertegenwoordiging van gegevensbanen die gegevens over Experience Platform bewegen. Dataflows worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets, aan de Dienst van de Identiteit en het Profiel van de Klant in real time, en aan Doelen helpen verplaatsen.
* [&#x200B; Sandboxes &#x200B;](../../../sandboxes/home.md): Experience Platform verstrekt virtuele zandbakken die één enkele instantie van Experience Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

## Een gegevensstroom op aanvraag maken {#create-a-dataflow-on-demand}

Navigeer naar het tabblad *[!UICONTROL Dataflows]* van de werkruimte Bronnen. Van hier, vind dataflow die u op bestelling wilt in werking stellen, en selecteer dan de ellipsen (**`...`**) naast uw dataflow naam.

![&#x200B; een lijst van gegevens in de bronwerkruimte.](../../images/tutorials/on-demand/select-dataflow.png)

Selecteer vervolgens **[!UICONTROL Run on-demand]** in het vervolgkeuzemenu dat wordt weergegeven.

![&#x200B; dropdown menu van A met de Looppas op bestelling geselecteerde optie.](../../images/tutorials/on-demand/run-on-demand.png)

Vorm het programma van uw opname op bestelling. Selecteer **[!UICONTROL Ingestion start time]**, **[!UICONTROL Date range start time]**, en **[!UICONTROL Date range end time]**.

| Configuratie plannen | Beschrijving |
| --- | --- |
| [!UICONTROL Ingestion start time] | De geplande tijd van wanneer de de stroomlooppas op bestelling zal beginnen. |
| [!UICONTROL Date range start time] | De vroegste datum en tijd waarop de gegevens worden opgehaald. |
| [!UICONTROL Date range end time] | De datum en tijd waarop de gegevens worden opgehaald tot. |

Selecteer **[!UICONTROL Schedule]** en wacht even tot uw gegevensstroom op aanvraag wordt geactiveerd.

![&#x200B; het plannen configuratievenster voor op bestelling opnemen.](../../images/tutorials/on-demand/configure-schedule.png)

Selecteer de naam van uw gegevensstroom om uw gegevensstroomactiviteit te bekijken. Hier ziet u een lijst van uw dataflow looppas die zijn verwerkt. U kunt individuele herhalingen van uw dataflow looppas opnieuw in werking stellen ongeacht of zij of succesvol zijn ontbroken. Voor mislukte herhalingen kunt u met **[!UICONTROL Retry]** de uitvoering opnieuw starten nadat u eventuele fouten tijdens het maken hebt gediagnosticeerd en verholpen.

>[!TIP]
>
>Als u een flowuitvoering opnieuw uitvoert, worden alleen bestanden met tijdstempels verwerkt die binnen het bereik van de oorspronkelijke uitvoering vallen.

![&#x200B; een lijst van verwerkte stroomlooppas voor een geselecteerde dataflow.](../../images/tutorials/on-demand/processed.png)

Selecteer **[!UICONTROL Scheduled]** om een lijst van dataflow looppas te zien die voor toekomstige opname gepland is.

![&#x200B; een lijst van geplande stroomlooppas voor geselecteerde dataflow.](../../images/tutorials/on-demand/scheduled.png)

## Volgende stappen

Door dit document te lezen, hebt u geleerd hoe te om stroomlooppas op bestelling voor bestaande brondataflows tot stand te brengen. Voor meer informatie over bronnen, lees het [&#x200B; overzicht van bronnen &#x200B;](../../home.md)
