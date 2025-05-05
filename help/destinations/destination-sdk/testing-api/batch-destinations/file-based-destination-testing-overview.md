---
description: Leer hoe te om op dossier-gebaseerde bestemming te gebruiken testend API om de configuratie van uw op dossier-gebaseerde bestemmingen te bevestigen die door de Destination SDK worden gebouwd.
title: API voor doeltesten op basis van bestanden
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# API-overzicht voor testen op basis van bestand

De op een bestand gebaseerde API voor het testen van doelen is een reeks eindpunten die u kunt gebruiken om de configuratie van uw op een bestand gebaseerde doelen te valideren die via de Destination SDK zijn gemaakt.

Wij adviseren gebruikend deze hulpmiddelen om uw configuratie te bevestigen alvorens [&#128279;](../../guides/submit-destination.md) uw bestemming voor overzicht aan Adobe voor te leggen.

Voor de beste testresultaten raden we u aan deze API te gebruiken op basis van het onderstaande stroomdiagram.

![ Diagram die de geadviseerde stroom van het bestemmingstesten tonen ](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

Zie de secties hieronder voor een kort overzicht van wat elk eindpunt kan doen.

## Voorbeeldprofielen genereren {#generate-sample-profiles}

Gebruik het API-eindpunt van `/sample-profiles` om voorbeeldprofielen te genereren op basis van uw bestaande bronschema.

Voorbeeldprofielen kunnen u helpen de JSON-structuur van een profiel te begrijpen. Bovendien geven ze u een standaardinstelling die u kunt aanpassen met uw eigen profielgegevens voor verdere doeltests.

Zie de [ specifieke documentatie ](file-based-sample-profile-generation-api.md) leren hoe te om steekproefprofielen te produceren.

## Doelconfiguratie testen {#test-destination-configuration}

Gebruik het `/testing/destinationInstance` API eindpunt om te testen als uw op dossier-gebaseerde bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren.

U kunt verzoeken aan het het testen eindpunt met of zonder [ steekproefprofielen ](file-based-sample-profile-generation-api.md) aan de vraag toe te voegen. Als u geen profielen verzendt op de aanvraag, genereert de API automatisch een voorbeeldprofiel en voegt deze toe aan de aanvraag.

Zie de [ specifieke documentatie ](file-based-destination-testing-api.md) leren hoe te om uw bestemmingsconfiguratie met steekproefprofielen te testen.

## Gedetailleerde activeringsresultaten weergeven {#view-detailed-activation-results}

U kunt het API-eindpunt van `/testing/destinationInstance` gebruiken om de volledige details van de testresultaten voor bestandsgebaseerde doelen weer te geven.

Dit API eindpunt keert het zelfde resultaat terug zoals u wanneer het gebruiken van de [ Dienst API van de Stroom ](../../../api/update-destination-dataflows.md) zou verkrijgen om dataflows te controleren.

Zie de [ specifieke documentatie ](file-based-destination-results-api.md) leren hoe te om gedetailleerde activeringsresultaten te bekijken.

## Gegevensvelden van klanten renderen {#render-customer-data-fields}

Gebruik het `/authoring/testing/template/render` API eindpunt om te visualiseren hoe de templatized [ gebieden van klantengegevens ](../../functionality/destination-configuration/customer-data-fields.md) die in uw bestemmingsconfiguratie worden bepaald als zou kijken.

Het API eindpunt produceert willekeurige waarden voor uw gebieden van klantengegevens, en keert hen in de reactie terug. Hierdoor kunt u de semantische structuur van gegevensvelden van klanten, zoals emmernamen of mappaden, valideren.

Zie de [ specifieke documentatie ](file-based-render-template-api.md) leren hoe te om waarden voor uw gebieden van klantengegevens te produceren en te visualiseren.
