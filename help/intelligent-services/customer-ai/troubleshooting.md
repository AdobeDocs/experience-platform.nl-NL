---
keywords: Experience Platform;aan de slag;klantenondersteuning;populaire onderwerpen;input van klantenondersteuning;klantenservice uitvoer;problemen oplossen;fouten in klantenondersteuning
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Probleemoplossing van AI-fouten van klant
topic-legacy: Getting started
description: Zoek antwoorden op algemene fouten in Customer AI.
type: Documentation
source-git-commit: ceb203899cda83aa79b994d45798d6147c3ff3b8
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---


# Probleemoplossing van AI-fouten van klant

De AI van de klant toont fouten wanneer de modelopleiding, het scoren, en de configuratie ontbreken. In de **[!UICONTROL Service instances]** sectie, toont een kolom voor **[!UICONTROL LAST RUN STATUS]** één van de volgende berichten: **[!UICONTROL Success]**, **[!UICONTROL Training issue]** en **[!UICONTROL Failed]**.

![status laatste uitvoering](./images/errors/last-run-status.png)

Als **[!UICONTROL Failed]** of **[!UICONTROL Training issue]** wordt weergegeven, kunt u de uitvoerstatus selecteren om een zijpaneel te openen. Het zijpaneel bevat uw **[!UICONTROL Last run status]** en **[!UICONTROL Last run details]**. **[!UICONTROL Last run details]** bevat informatie over waarom de uitvoering is mislukt. Als de AI van de Klant geen details over uw fout kan verstrekken, contacteer steun met de foutencode die verstrekt wordt.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Modelkwaliteit is slecht

Als u de fout &quot;[!UICONTROL Model Quality is poor. We recommend creating a new app with the modified configuration]&quot;ontvangt. Volg onderstaande aanbevolen stappen om problemen op te lossen.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Aanbevolen correctie

&quot;Modelkwaliteit is slecht&quot; betekent dat de nauwkeurigheid van het model niet binnen een aanvaardbaar bereik ligt. Klantenservice-AI kon na training geen betrouwbaar model en AUC (Area under the ROC curve) &lt; 0,65 maken. Om de fout te bevestigen, adviseert men dat u één van de configuratieparameters verandert en de opleiding opnieuw uitvoert.

Begin door de nauwkeurigheid van uw gegevens te controleren. Het is belangrijk dat uw gegevens de velden bevatten die nodig zijn voor uw voorspelbare resultaat.

- Controleer of uw dataset de recentste data heeft. De AI van de Klant veronderstelt altijd dat de gegevens bijgewerkt zijn wanneer het model wordt teweeggebracht.
- Controleer of er gegevens ontbreken in het gedefinieerde voorspellings- en geschiktheidsvenster. Uw gegevens moeten volledig zijn zonder tussenruimten. Zorg er ook voor dat uw gegevensset voldoet aan de [historische gegevensvereisten voor AI van de klant](./input-output.md#data-requirements).
- Controle voor ontbrekende gegevens in handel, toepassing, Web, en onderzoek, binnen uw eigenschappen van het schemagebied.

Als uw gegevens niet het probleem lijken te zijn, probeert u de toelatingsvoorwaarde van de populatie te veranderen om het model tot bepaalde profielen (bijvoorbeeld, `_experience.analytics.customDimensions.eVars.eVar142` bestaat in afgelopen 56 dagen) te beperken. Dit beperkt de populatie en de grootte van de gegevens die in het trainingsvenster worden gebruikt.

Als het beperken van de toelatingspopulatie niet werkte of niet mogelijk is, verander uw voorspellingsvenster.

- Probeer het voorspellingsvenster te wijzigen in 7 dagen en controleer of de fout zich blijft voordoen. Als de fout niet meer voorkomt, wijst dit erop dat u niet genoeg gegevens voor uw bepaalde voorspellingsvenster kunt hebben.

