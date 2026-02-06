---
description: Gebruik het dashboard van [!UICONTROL Profile Enrichment] om te begrijpen of de banen van de profielverrijking met succes liepen en voltooiden, en om de basismetriek te bekijken om de doeltreffendheid van de verrijking te meten.
solution: Experience Platform
title: Verbeteringstaken voor profielen controleren
type: Tutorial
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 0e993f7d0791f5f6f9dce63eb3848609d892e788
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Verbeteringstaken voor profielen controleren in de gebruikersinterface {#monitor-profile-enrichment}

Gebruik het dashboard van [!UICONTROL Profile Enrichment] om te begrijpen of de banen van de profielverrijking met succes liepen en voltooiden, en om de basismetriek te bekijken om de doeltreffendheid van de verrijking te meten.

In [&#x200B; Experience Platform UI &#x200B;](https://platform.adobe.com), selecteer **[!UICONTROL Monitoring]** van de linkernavigatie om tot het [!UICONTROL Monitoring] dashboard toegang te hebben. In de meningsselecteur, uitgezochte **B2B Stroom** om de dashboardelementen te zien specifiek voor [&#x200B; Real-Time CDP B2B &#x200B;](/help/rtcdp/b2b-overview.md).  Het dashboard van [!UICONTROL Monitoring] bevat de basismetriek van de laatste succesvolle looppas, en dagelijkse baanstatus tot 90 dagen in het verleden.

## Verrijking van het accountprofiel {#related-accounts}

Het [!UICONTROL Related accounts] dashboard toont basismetriek en het statuut van de dagelijkse baan specifiek voor de [&#x200B; Verwante 2&rbrace; profielverrijking van Rekeningen &lbrace;.](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)

![&#x200B; Visuele aanwijzing van hoe te om aan de de verrijking van het Profiel te krijgen banen controlerend het scherm in Experience Platform UI.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

De gegevens op de **[!UICONTROL Metrics]** -kaart bevatten de basisgegevens van de meest recente succesvolle uitvoering van de taak Verwante accounts.

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

Het [!UICONTROL Lead to account matching] dashboard toont de basismetriek en de dagelijkse baan-in werking gestelde status specifiek voor [&#x200B; Lood aan rekening passende &#x200B;](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) profielverrijking.

![&#x200B; Lood aan rekening passende profielverrijking &#x200B;](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

De volgende metriek is beschikbaar voor lood aan de banen van de de profielverrijking van de rekening passende:

| Metrisch | Beschrijving |
| --------- | ---------- |
| **[!UICONTROL Total persons with accounts]** | Hiermee wordt het totale aantal personen aangegeven dat aan een account is gekoppeld. |
| **[!UICONTROL Total accounts]** | Geeft het totale aantal accounts aan. |
| **[!UICONTROL Existing persons with accounts]** | Hiermee wordt het aantal personen aangegeven dat al is gekoppeld aan een account uit de gegevensbronnen. |
| **[!UICONTROL Persons matched]** | Hiermee geeft u het aantal personen aan dat aan een account is gekoppeld. |
| **[!UICONTROL Persons unmatched]** | Hiermee geeft u het aantal personen aan dat niet aan een account is gekoppeld. |
| **[!UICONTROL Last successful run]** | Geeft de datum en tijd aan van de laatste geslaagde poging om een overeenkomende taak uit te voeren. |
| **[!UICONTROL Status]** | Geeft de status (geslaagd, mislukt of verwerkt) aan van de lead in de overeenkomende taak van de account. |

## Verrijking van het profiel voor lood en accountscoring {#predictive-lead-to-account-scoring}

Het [!UICONTROL Predictive lead and account scoring] dashboard toont de basismetriek en de dagelijkse baan-in werking gestelde status specifiek voor de [&#x200B; Predictieve lood en rekening die &#x200B;](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) profielverrijking scoren.

![&#x200B; Predictive lood en de verbetering van het rekeningsprofiel van de rekening &#x200B;](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

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

Gebruik het pijlpictogram (![&#x200B; pijlpictogram &#x200B;](/help/images/icons/chevron-up.png)) om de kaart bij de bovenkant van het scherm uit te breiden of te sluiten, dat informatie van de bij-a-blik over de banen van de profielverrijking toont.

![&#x200B; opname van het Scherm die de controle van het pijlpictogram UI toont.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Met de schakeloptie **[!UICONTROL Metrics and graphs]** kunt u de weergave met de meest recente meetgegevens negeren.

![&#x200B; opname van het Scherm die de metriek en grafieken knevel toont.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Gebruik de schakeloptie **[!UICONTROL Show failures only]** om alleen de mislukte taken voor profielverrijking weer te geven.

![&#x200B; opname van het Scherm die toont tonen mislukkingen slechts knevel.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Volgende stappen {#next-steps}

Door deze zelfstudie te volgen, kunt u metriek voor profielverrijkingsbanen met succes controleren en begrijpen. Raadpleeg de volgende documenten voor meer informatie:

* [Verwante rekeningen in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Het tabblad Verwante accounts in de gebruikersinterface voor het accountprofiel](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Lood-aan-rekening matching in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Voorspelende lead- en accountscoring in Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
