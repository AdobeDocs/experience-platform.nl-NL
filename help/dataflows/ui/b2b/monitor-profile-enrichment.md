---
description: Gebruik de [!UICONTROL Profile Enrichment] dashboard om te begrijpen of de banen van de profielverrijking met succes liepen en voltooiden, en de basismetriek te bekijken om de doeltreffendheid van de verrijking te meten.
solution: Experience Platform
title: Verbeteringstaken voor profielen controleren
type: Tutorial
source-git-commit: f3389ef2c2bd9ff52ecde2a4f5fd55e5b86783fc
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Verbeteringstaken voor profielen controleren in de gebruikersinterface

Gebruik de [!UICONTROL Profile Enrichment] dashboard om te begrijpen of de banen van de profielverrijking met succes liepen en voltooiden, en de basismetriek te bekijken om de doeltreffendheid van de verrijking te meten.

In de [UI Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Monitoring]** van de linkernavigatie om tot [!UICONTROL Monitoring] dashboard. Selecteer in de weergavekiezer de optie **B2B-stroom** om de specifieke dashboardelementen voor [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  De [!UICONTROL Monitoring] dashboard bevat de basismeetgegevens van de meest recente succesvolle uitvoering en de dagelijkse taakstatus tot 90 dagen in het verleden. De [!UICONTROL Related accounts] het dashboard toont de basismaatstaven en de dagelijkse taakstatus die specifiek zijn voor de [Gerelateerde accounts](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) profielverrijking.

![Visuele aanwijzing van hoe te om aan het scherm van de Taakcontrole van de Verrijking van het Profiel in de UI van het Experience Platform te krijgen.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

De gegevens in de **[!UICONTROL Metrics]** De kaart bevat de basisgegevens van de meest recente geslaagde uitvoering van de taak Verwante accounts.

De volgende cijfers zijn beschikbaar voor verrijkingstaken van het accountprofiel:

| Metrisch | Beschrijving |
---------|----------|
| **[!UICONTROL Total account profiles]** | Hiermee geeft u het totale aantal accountprofielen aan waartoe uw organisatie toegang heeft. |
| **[!UICONTROL Account groups]** | Hiermee wordt het aantal accountgroepen aangegeven dat wordt gegroepeerd door de leertaak Verwante accounts. |
| **[!UICONTROL Single-account groups]** | Geeft het aantal rekeningen aan die niet samen met andere rekeningen zijn gegroepeerd. |
| **[!UICONTROL Largest group size]** | Hiermee wordt de grootte van de grootste groep verwante accounts aangegeven. De maximaal toegestane groepsgrootte is 30. |
| **[!UICONTROL Median group size]** | Hiermee geeft u de mediane grootte van gerelateerde accountgroepen in uw organisatie aan. |
| **[!UICONTROL Last successful run]** | Geeft de datum en tijd aan van de laatste geslaagde uitvoering van de taak Verwante accounts. |
| **[!UICONTROL Status]** | Geeft de status (geslaagd, mislukt of verwerkt) van de taak Verwante accounts aan. |
| **[!UICONTROL Message]** | Geeft een fout- of waarschuwingsbericht voor een bepaalde taak aan. |

## UI-besturingselementen {#ui-controls}

In deze sectie worden diverse gebruikersinterface-opties (UI) in de monitoringinterface beschreven waarmee u de metriek kunt filteren die op de pagina wordt weergegeven.

Het pijlpictogram gebruiken (![pijlpictogram](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) om de kaart boven aan het scherm uit te vouwen of te sluiten, waarin in één oogopslag informatie over de taken voor profielverrijking wordt weergegeven.

![De opname van het scherm die de controle UI van het pijlpictogram toont.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Gebruik de **[!UICONTROL Metrics and graphs]** Schakel deze optie in om de weergave met de meest recente meetgegevens te sluiten.

![Schermopname die de schakeloptie Metriek en Grafieken toont.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Gebruik de **[!UICONTROL Show failures only]** schakelen om alleen de mislukte verrijkingstaken voor profielen weer te geven.

![De opname van het scherm die toont tonen slechts mislukkingen knevel.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, kunt u metriek voor verwante rekeningen nu met succes controleren en begrijpen verrijkingsbanen van het profiel van verrijking. Raadpleeg de volgende documenten voor meer informatie:

* [Verwante rekeningen in real time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Het tabblad Verwante accounts in de gebruikersinterface voor het accountprofiel](/help/rtcdp/accounts/account-profile-ui-guide.md)