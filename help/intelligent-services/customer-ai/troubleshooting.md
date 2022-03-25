---
keywords: Experience Platform;aan de slag;klantenondersteuning;populaire onderwerpen;input van klantenondersteuning;klantenservice uitvoer;problemen oplossen;fouten in klantenondersteuning
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Probleemoplossing van AI-fouten van klant
topic-legacy: Getting started
description: Zoek antwoorden op algemene fouten in Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# Probleemoplossing van AI-fouten van klant

De AI van de klant toont fouten wanneer de modelopleiding, het scoren, en de configuratie ontbreken. In de **[!UICONTROL Service instances]** sectie, een kolom voor **[!UICONTROL LAST RUN STATUS]** geeft een van de volgende berichten weer: **[!UICONTROL Success]**, **[!UICONTROL Training issue]**, en **[!UICONTROL Failed]**.

![status laatste uitvoering](./images/errors/last-run-status.png)

In het geval dat **[!UICONTROL Failed]** of **[!UICONTROL Training issue]** wordt weergegeven, kunt u de uitvoerstatus selecteren om een zijpaneel te openen. Het zijpaneel bevat uw **[!UICONTROL Last run status]** en **[!UICONTROL Last run details]**. **[!UICONTROL Last run details]** bevat informatie over waarom de uitvoering is mislukt. Als de AI van de Klant geen details over uw fout kan verstrekken, contacteer steun met de foutencode die verstrekt wordt.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Geen toegang tot AI van klant in Chrome-incognito

Er treden laadfouten op in de incognitomodus van Google Chrome vanwege updates in de beveiligingsinstellingen van de incognitomodus van Google Chrome. Het probleem wordt actief besproken met Chrome en maakt van experience.adobe.com een vertrouwd domein.

<img src="./images/errors/error.PNG" width="500" /><br />

### Aanbevolen correctie

Als u dit probleem wilt oplossen, moet u Experience.adobe.com toevoegen als een site die cookies altijd kan gebruiken. Begin door naar **chrome://settings/cookies**. Blader vervolgens omlaag naar de **Aangepast gedrag** gevolgd door het selecteren van de **Toevoegen** knop naast &quot;sites die altijd cookies kunnen gebruiken&quot;. Kopieer en plak de pop-up die wordt weergegeven `[*.]experience.adobe.com` Selecteer vervolgens de **Cookies van derden opnemen** op deze site. Selecteer **Toevoegen** en de AI van de Klant in incognito opnieuw laden.

![aanbevolen correctie](./images/errors/cookies2.gif)

## Modelkwaliteit is slecht

Als de fout &quot;[!UICONTROL Model Quality is poor. We recommend creating a new app with the modified configuration]&quot;. Volg onderstaande aanbevolen stappen om problemen op te lossen.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Aanbevolen correctie

&quot;Modelkwaliteit is slecht&quot; betekent dat de nauwkeurigheid van het model niet binnen een aanvaardbaar bereik ligt. Klantenservice-AI kon na training geen betrouwbaar model en AUC (Area under the ROC curve) &lt; 0,65 maken. Om de fout te bevestigen, adviseert men dat u één van de configuratieparameters verandert en de opleiding opnieuw uitvoert.

Begin door de nauwkeurigheid van uw gegevens te controleren. Het is belangrijk dat uw gegevens de velden bevatten die nodig zijn voor uw voorspelbare resultaat.

- Controleer of uw dataset de recentste data heeft. De AI van de Klant veronderstelt altijd dat de gegevens bijgewerkt zijn wanneer het model wordt teweeggebracht.
- Controleer of er gegevens ontbreken in het gedefinieerde voorspellings- en geschiktheidsvenster. Uw gegevens moeten volledig zijn zonder tussenruimten. Zorg er ook voor dat uw gegevensset voldoet aan de [Vereisten voor historische gegevens van AI-klanten](./input-output.md#data-requirements).
- Controle voor ontbrekende gegevens in handel, toepassing, Web, en onderzoek, binnen uw eigenschappen van het schemagebied.

Als uw gegevens niet het probleem lijken te zijn, probeer veranderend de toelatingsvoorwaarde van de bevolking om het model tot bepaalde profielen (bijvoorbeeld) te beperken `_experience.analytics.customDimensions.eVars.eVar142` bestaat in de afgelopen 56 dagen). Dit beperkt de populatie en de grootte van de gegevens die in het trainingsvenster worden gebruikt.

Als het beperken van de toelatingspopulatie niet werkte of niet mogelijk is, verander uw voorspellingsvenster.

- Probeer het voorspellingsvenster te wijzigen in 7 dagen en controleer of de fout zich blijft voordoen. Als de fout niet meer voorkomt, wijst dit erop dat u niet genoeg gegevens voor uw bepaalde voorspellingsvenster kunt hebben.
