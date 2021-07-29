---
title: Notities
description: Leer hoe u tekstuele annotaties kunt toevoegen aan bepaalde tagbronnen in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Notities

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Opmerkingen zijn tekstuele annotaties die u kunt toevoegen aan bepaalde codebronnen in Adobe Experience Platform. De nota&#39;s kunnen aan de volgende middelen worden vastgemaakt:

* Extensies
* Gegevenselementen
* Regels
* Regelcomponenten
* Bibliotheken
* Properties

Notities kunnen maximaal 512 Unicode-tekens bevatten.

Opmerkingen zijn opmerkingen die geen invloed hebben op het gedrag van de bronnen waaraan ze zijn gekoppeld. Ze zijn niet opgenomen in ingebouwde bibliotheken.  U kunt notities gebruiken voor:

* Achtergrondinformatie over een bron opgeven
* Functie als een lijst van taken voor toekomstige verbeteringen
* Doorgeven van advies over hulpbronnengebruik aan andere gebruikers
* Instructies geven aan andere teamleden
* Historische context opnemen
* Herinner me wat een middel doet, waarom het wordt gebouwd zoals het is, of waar het wordt gebruikt

## Een notitie maken

Bij notebookbronnen wordt een smalle rail aan de rechterkant van het scherm weergegeven.  De rail bevat een pictogram voor notities.  Dit pictogram geeft het huidige aantal notities weer dat aan de bron is gekoppeld.

Selecteer **[!UICONTROL Notes]** om de rechterrail uit te breiden en de nota&#39;s, met de meest recente nota&#39;s bij de bovenkant te tonen.  Als u een nieuwe notitie wilt toevoegen, typt u de notitietekst in het vak bovenaan en selecteert u **[!UICONTROL Add Note]**.

## Overige

* Opmerkingen over labelbronnen komen overeen met het gedrag van notities in DTM, omdat ze onveranderlijk zijn en niet kunnen worden bewerkt of verwijderd.
* Wanneer het bekijken van oudere revisies van een middel, slechts worden de nota&#39;s die vóór de datum `created_at` van die revisie werden gecreeerd getoond.
* Wanneer u een bron verwijdert, worden alle notities die aan de bron zijn gekoppeld, ook verwijderd.
