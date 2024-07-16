---
title: Notities
description: Leer hoe u tekstuele annotaties kunt toevoegen aan bepaalde tagbronnen in Adobe Experience Platform.
exl-id: 14d6b6a1-3bd0-4181-8181-e6b35c197a44
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Notities

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

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

Selecteer **[!UICONTROL Notes]** om de rechtertrack uit te breiden en de notities weer te geven, met de meest recente notities bovenaan.  Als u een nieuwe notitie wilt toevoegen, typt u de notitietekst in het vak bovenaan en selecteert u **[!UICONTROL Add Note]** .

## Overige

* Opmerkingen over labelbronnen komen overeen met het gedrag van notities in DTM, omdat ze onveranderlijk zijn en niet kunnen worden bewerkt of verwijderd.
* Wanneer u oudere revisies van een bron weergeeft, worden alleen de notities weergegeven die zijn gemaakt vóór de datum `created_at` van die revisie.
* Wanneer u een bron verwijdert, worden alle notities die aan de bron zijn gekoppeld, ook verwijderd.
