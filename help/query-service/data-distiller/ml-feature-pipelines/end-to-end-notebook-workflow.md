---
title: Workflow van begin tot einde voor toevoeging van AI/ML-gegevenspipet
description: Gebruik cloudgebaseerde laptops voor computerleren om een training te maken en een populiteitsmodel te scoren dat abonnementconversies van Adobe Experience Platform-gegevens voorspelt.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# Verrijking van end-to-end workflow voor de AI/ML-gegevenspijpleiding

Met Data Distiller kunt u uw computers verrijken met leerleidingen met hoogwaardige gegevens voor klanten die zijn verzameld en verwerkt in Adobe Experience Platform.

Dit document bevat een reeks cloudgebaseerde laptops voor de computerleeromgeving die een complete workflow demonstreren. In de workflow worden aangepaste gegevensmodellen gemaakt die uw gebruiksscenario&#39;s voor marketingdoeleinden ondersteunen met behulp van Experience Platforms.

Voor deze workflow is het gebruik van [!DNL Python] -laptops in uw computerleeromgevingen. Instructies om met deze [!DNL Python] -laptops worden in hun respectievelijke Lees mij-bestanden opgenomen.

Volg de stappen in het dialoogvenster [Overzicht AI/ML-functiepijpleidingen](./overview.md) om het gebruik mogelijk te maken van het monster Python-laptops die in deze AI/ML-functiepijpleiding worden gebruikt.

## Laptops voor de leeromgeving van cloudmachines {#cmle-notebooks}

De end-to-end workflow kan in drie brede fasen worden verdeeld op basis van de services die worden gebruikt om de workflow te implementeren.

- De eerste exploratie en voorbereiding van de gegevens van het Platform zijn afhankelijk van de diensten van het Platform.
- Modeltraining en -scoring maken gebruik van gereedschappen in uw op de cloud gebaseerde XML-omgeving. De gemeenschappelijke keuzen voor de platforms van ML omvatten: Databricks ML, AWS Sagemaker, DataRobot, etc.
- Het aanzetten van scores terug in Platform en om het even welke code-gebaseerde publieksverwezenlijking en activering die op die scores wordt gebaseerd zouden opnieuw op de diensten van het Platform vertrouwen.

Al deze fasen kunnen echter worden uitgevoerd in een of meer laptops uit uw XML-omgeving zonder dat de gebruiker de context moet schakelen tussen Platform en de bijbehorende op de cloud gebaseerde ML-tools.

De typische stappen van deze end-to-end-flow zijn verdeeld in een reeks modulaire laptops die, samen genomen, de stappen aantonen die betrokken zijn bij een typisch machinaal leerproject met behulp van platformgegevens. Hierdoor wordt het gemakkelijker om de laptops te gebruiken als referentie voor het uitvoeren van specifieke activiteiten, en om code van de relevante notebooks te selecteren en aan te passen om een praktijkgeval te implementeren. In de praktijk kan een gegevenswetenschapper één enkel notitieboekje opstellen dat de pijpleiding van begin tot eind voor hun project van XML uitvoert. Alternatief, kan een gegevenswetenschapper eenvoudig de steekproefcode voor het vragen van de gegevens van het Platform en het ter beschikking stellen van het in hun milieu van ML alvorens het project op UI-Gebaseerde eigenschappen in hun platform van ML verder te gaan aanpassen.

De voorbeeldlaptops in de gekoppelde opslagplaats worden hieronder kort beschreven. Gedetailleerde documentatie voor elke laptop is afgestemd op de code in de laptops zelf.

<!-- Below is the meat - the how to (but without links or details) -->

### synthetische gegevens genereren {#generate-synthetic-data}

Deze laptop bevat code voor het genereren van gegevenssets met synthetische profielen en Experience Events in uw platform die worden gebruikt om de CMLE-workflow te illustreren.

### EDA en kenmerking met de Dienst van de Vraag {#eda-and-featurization-with-query-service}

Deze laptop bevat voorbeelden van verkennende analyse van gegevenssets van het platform met behulp van interactieve query&#39;s via de Platform Query Service. Deze worden gevolgd met voorbeelden van featuriseringsvragen om een opleidingsdataset voor het model van de voorbeeldaandrijving tot stand te brengen.

### Trainingsgegevens exporteren {#export-training-data}

Dit notitieboekje illustreert het uitvoeren van de trainingsdataset naar wolkenopslag die door uw hulpmiddelen van XML kan worden gelezen.

### Trein met een voortstuwingsmodel {#train-a-propensity-model}

Deze laptop illustreert het trainen van een model van eigenaardigheid. Het veronderstelt Databricks ML als uw milieu van XML, maar algemeen geschreven (namelijk zonder zwaar gebruik van gegevensbestand-specifieke eigenschappen/APIs) zodat het aan andere platforms kan worden aangepast.

### Score het aandrijvingsmodel

Deze laptop illustreert het scoren van het getrainde neigheidsmodel om een dataset van nevenscores voor elk profiel van de Klant van het Platform te produceren.

### Muziek opnemen in AEP

Dit korte notitieboekje illustreert het opnemen van de dataset van eigenschapscores om de klantenprofielen in AEP te verrijken.

### Soorten publiek maken en activeren op basis van code

In deze laptop wordt geïllustreerd hoe de gebruiker een publiek kan maken op basis van de scores en dat publiek kan activeren via Platform-apps op basis van de notebookcode.
