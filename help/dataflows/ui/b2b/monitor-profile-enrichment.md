---
description: Gebruik de [!UICONTROL Profile Enrichment] dashboard om te begrijpen of de banen van de profielverrijking met succes liepen en voltooiden, en de basismetriek te bekijken om de doeltreffendheid van de verrijking te meten.
solution: Experience Platform
title: Verbeteringstaken voor profielen controleren
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Verbeteringstaken voor profielen controleren in de gebruikersinterface {#monitor-profile-enrichment}

Gebruik de [!UICONTROL Profile Enrichment] dashboard om te begrijpen of de banen van de profielverrijking met succes liepen en voltooiden, en de basismetriek te bekijken om de doeltreffendheid van de verrijking te meten.

In de [UI Platform](https://platform.adobe.com), selecteert u **[!UICONTROL Monitoring]** van de linkernavigatie om tot [!UICONTROL Monitoring] dashboard. Selecteer in de weergavekiezer de optie **B2B-stroom** om de specifieke dashboardelementen voor [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  De [!UICONTROL Monitoring] dashboard bevat de basismeetgegevens van de meest recente succesvolle uitvoering en de dagelijkse taakstatus tot 90 dagen in het verleden.

## Verrijking van het accountprofiel {#related-accounts}

De [!UICONTROL Related accounts] het dashboard toont basismeetgegevens en de status van de dagelijkse baan specifiek voor [Gerelateerde accounts](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) profielverrijking.

![Visuele aanwijzing van hoe te om aan het scherm van de Taakcontrole van de Verrijking van het Profiel in de UI van het Experience Platform te krijgen.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

De gegevens in de **[!UICONTROL Metrics]** De kaart bevat de basisgegevens van de meest recente geslaagde uitvoering van de taak Verwante accounts.

De volgende cijfers zijn beschikbaar voor verrijkingstaken van het accountprofiel:

| Metrisch | Beschrijving |
| --------- | ---------- |
| **[!UICONTROL Total account profiles]** | Hiermee geeft u het totale aantal accountprofielen aan waartoe uw organisatie toegang heeft. |
| **[!UICONTROL Account groups]** | Geeft het aantal accountgroepen aan dat wordt gegroepeerd door de verwante rekeningenmachine die de taak leert. |
| **[!UICONTROL Single-account groups]** | Geeft het aantal rekeningen aan die niet samen met andere rekeningen zijn gegroepeerd. |
| **[!UICONTROL Largest group size]** | Hiermee wordt de grootte van de grootste groep verwante accounts aangegeven. De maximaal toegestane groepsgrootte is 30. |
| **[!UICONTROL Median group size]** | Hiermee geeft u de mediane grootte van gerelateerde accountgroepen in uw organisatie aan. |
| **[!UICONTROL Last successful run]** | Geeft de datum en het tijdstip aan van de laatste geslaagde uitvoering van de verwante accounttaak. |
| **[!UICONTROL Status]** | Geeft de status (geslaagd, mislukt of verwerkt) van de verwante accounttaak aan. |
| **[!UICONTROL Message]** | Geeft een fout- of waarschuwingsbericht voor een bepaalde taak aan. |

## Verrijking van overeenkomende profielen voor accounts leiden {#lead-to-account-matching}

De [!UICONTROL Lead to account matching] op het dashboard worden de basismaatstaven en de dagelijkse taakrun-status weergegeven die specifiek zijn voor het [Overeenkomende lead-account](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) profielverrijking.

![Verrijking van overeenkomende profielen voor accounts leiden](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

De volgende metriek is beschikbaar voor lood aan de banen van de de profielverrijking van de rekening passende:

| Metrisch | Beschrijving |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Hiermee wordt het totale aantal personen aangegeven dat aan een account is gekoppeld. |
| **[!UICONTROL Total accounts]** | Geeft het totale aantal accounts aan. |
| **[!UICONTROL Existing persons with accounts]** | Hiermee wordt het aantal personen aangegeven dat al is gekoppeld aan een account uit de gegevensbronnen. |
| **[!UICONTROL Persons matched]** | Hiermee geeft u het aantal personen aan dat aan een account is gekoppeld. |
| **[!UICONTROL Persons unmatched]** | Hiermee geeft u het aantal personen aan dat niet aan een account is gekoppeld. |
| **[!UICONTROL Last successful run]** | Geeft de datum en tijd aan van de laatste geslaagde poging om een overeenkomstige taak uit te voeren. |
| **[!UICONTROL Status]** | Geeft de status (geslaagd, mislukt of verwerkt) aan van de lead in de overeenkomende taak van de account. |

## Verrijking van het profiel voor lood en accountscoring {#predictive-lead-to-account-scoring}

De [!UICONTROL Predictive lead and account scoring] op het dashboard worden de basismaatstaven en de dagelijkse taakrun-status weergegeven die specifiek zijn voor het [Voorspelend lood en account scoring](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) profielverrijking.

![Verrijking van het profiel voor lood en accountscoring](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

De volgende metriek is beschikbaar voor voorspellende lood en de banen van de de profielverrijking van de rekening:

| Metrisch | Beschrijving |
| --------- | ---------- |
| **[!UICONTROL Job start]** | Geeft de begindatum en -tijd aan van de voorspellende lead- en accountscoringstaak die wordt uitgevoerd. |
| **[!UICONTROL Processing time]** | De totale tijd die nodig is om de taak te voltooien. |
| **[!UICONTROL Score name]** | De scorenaam van de taak. |
| **[!UICONTROL Profile type]** | Het type van de score: <ul><li>Persoon</li><li>Account</li></ul>. |
| **[!UICONTROL Job type]** | Het type taak:<ul><li>Scores</li><li>Training</li>. |
| **[!UICONTROL Status]** | Geeft de status (geslaagd, mislukt of verwerkt) van de voorspellende lead- en accountscoringtaak aan. |

## UI-besturingselementen {#ui-controls}

In deze sectie worden diverse gebruikersinterface-opties (UI) in de monitoringinterface beschreven waarmee u de metriek kunt filteren die op de pagina wordt weergegeven.

Het pijlpictogram gebruiken (![pijlpictogram](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) om de kaart boven aan het scherm uit te vouwen of te sluiten, waarin in één oogopslag informatie over de taken voor profielverrijking wordt weergegeven.

![De opname van het scherm die de controle UI van het pijlpictogram toont.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Gebruik de **[!UICONTROL Metrics and graphs]** Schakel deze optie in om de weergave met de meest recente meetgegevens te sluiten.

![Schermopname die de schakeloptie Metriek en Grafieken toont.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Gebruik de **[!UICONTROL Show failures only]** schakelen om alleen de mislukte verrijkingstaken voor profielen weer te geven.

![De opname van het scherm die toont tonen slechts mislukkingen knevel.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, kunt u metriek voor profielverrijkingsbanen met succes controleren en begrijpen. Raadpleeg de volgende documenten voor meer informatie:

* [Verwante rekeningen in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Het tabblad Verwante accounts in de gebruikersinterface voor het accountprofiel](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lood-aan-rekening matching in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Voorspelende lead- en accountscoring in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
