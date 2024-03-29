---
title: Bibliotheken
description: Leer meer over het concept tagbibliotheken en hoe ze in Adobe Experience Platform werken.
exl-id: 4d6f86e6-5684-4635-aaf1-87ba10cd7d94
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# Bibliotheken

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een bibliotheek is een reeks instructies voor hoe de uitbreidingen, gegevenselementen, en de regels met elkaar in wisselwerking staan nadat zij worden opgesteld. Wanneer u een bibliotheek maakt, geeft u de wijzigingen op die u in de bibliotheek wilt aanbrengen. Tijdens het maken worden deze wijzigingen gecombineerd met alles wat in vorige bibliotheken is verzonden, goedgekeurd of gepubliceerd.

Bibliotheken bevatten de toevoeging of verwijdering van:

* Regels
* Elementen
* Extensieconfiguratie

Bibliotheken moeten aan een omgeving worden toegewezen voordat ze in een build kunnen worden gecompileerd. Bibliotheken worden als geheel goedgekeurd of verworpen. U kunt afzonderlijke items in een bibliotheek niet goedkeuren of afwijzen. Een bibliotheek beweegt zich tussen verscheidene milieu&#39;s aangezien het zijn weg door het publiceren werkschema maakt.

## Een bibliotheek maken {#create-a-library}

Voer de volgende stappen uit om een bibliotheek te maken.

1. Open de [!UICONTROL Publishing] tab.

   De [!UICONTROL Publishing] De pagina bevat een lijst met de Dev-bibliotheken en biedt de middelen om deze ter goedkeuring in te dienen, naar de testfase te verplaatsen of naar de productie te publiceren.

1. Selecteer **[!UICONTROL Add New Library]**.

   ![](../../images/library-create.jpg)

1. Geef de bibliotheek een naam.
1. Wijs de bibliotheek toe aan een Dev-omgeving.
1. Voeg een wijziging toe aan de bibliotheek.
Als u een item wilt toevoegen, selecteert u **[!UICONTROL Add a Change]** kiest u vervolgens de items die u wilt toevoegen. Elk item dat is bewerkt of verwijderd, kan worden toegevoegd aan de gekozen bibliotheek.

   ![](../../images/library-add-change.jpg)

   U kunt het volgende toevoegen aan uw bibliotheek:

   * Regels
   * Gegevenselementen
   * Extensieconfiguraties

1. Als u bronnen wilt toevoegen die zijn gewijzigd, selecteert u **[!UICONTROL Add All Changed Resources]**.
1. Selecteren **[!UICONTROL Save]** of **[!UICONTROL Save and Build for Development]**.

   Het opstellen compileert een bouwstijl en stelt het aan het toegewezen milieu op.

Nadat u een bibliotheek hebt gemaakt, selecteert u een van de volgende opties in het keuzemenu voor die bibliotheek:

* **Bewerken**: Met deze optie kunt u de bibliotheekconfiguratie wijzigen.

* **Opbouwen voor ontwikkeling**: Deze optie compileert een bouwstijl en stelt het aan het toegewezen milieu op.

* **Ter goedkeuring verzenden**: Met deze optie stelt u de bibliotheek beschikbaar voor een fiatteur om deze naar de volgende stap in het publicatieproces te verplaatsen.

* **Verwijderen**: Met deze optie verwijdert u de momenteel geselecteerde bibliotheek uit het publicatieproces.

![](../../images/library-menu.png)

## Toevoegen aan een bibliotheek {#add-to-a-library}

Voer de volgende stappen uit om een bibliotheek toe te voegen.

1. Installeer de [extensions](../managing-resources/extensions/overview.md) wilt toevoegen.
1. Maak de [gegevenselementen](../managing-resources/data-elements.md) en regels die u wilt toevoegen.
1. Open de **[!UICONTROL Publishing]** tab.
1. Selecteer [bibliotheek](libraries.md) u wilt wijzigen, selecteert u vervolgens **[!UICONTROL Edit]**.
1. Gebruik de knoppen voor regels, gegevenselementen en extensies om de items te selecteren die u wilt toevoegen aan de bibliotheek.
1. Sla de wijzigingen op.

Wijzigingen in de bibliotheek worden weergegeven in het wijzigingslogboek Bibliotheek Inhoud.

>[!NOTE]
>
>Gegevenselementen kunnen afhankelijk zijn van extensies. De regels kunnen van zowel gegevenselementen als uitbreidingen afhangen. Als u niet alle noodzakelijke componenten in uw bibliotheek omvat, zal de bouwstijl bij bouwstijltijd ontbreken en u zult de noodzakelijke componenten moeten toevoegen alvorens u een succesvolle bouwstijl voltooit. Een toekomstige versie controleert afhankelijkheden wanneer u wijzigingen aanbrengt in een bibliotheek.

## Verwijderen uit een bibliotheek

Als u iets uit een bibliotheek wilt verwijderen, moet u het deactiveren en vervolgens de gedeactiveerde status publiceren.

1. Schakel de extensies die u wilt verwijderen uit, samen met de gegevenselementen en -regels die van deze extensies afhankelijk zijn.
1. Schakel de gegevenselementen en -regels uit die u wilt verwijderen.
1. Open de **[!UICONTROL Publishing]** tab.
1. Selecteer de bibliotheek die u wilt wijzigen.
1. Gebruik de knoppen voor regels, gegevenselementen en extensies om de uitgeschakelde items te selecteren die u uit de bibliotheek wilt verwijderen.
1. Sla de wijzigingen op.

## Bibliotheekwijzigingen beheren

Voer de volgende stappen uit om de bibliotheekopties te bewerken.

1. Kies een bibliotheek en selecteer **[!UICONTROL Edit]** om bibliotheekwijzigingen weer te geven. Alle wijzigingen worden weergegeven in het dialoogvenster [!UICONTROL Library Contents] lijst.

   ![](../../images/library-contents.jpg)

1. Selecteer een wijziging die u wilt weergeven en selecteer een revisie.

   ![](../../images/library-contents-revision.jpg)

1. Selecteren of deze moet worden weergegeven **Alles** objecten of **Gewijzigd** objecten.
1. Selecteer de revisie en selecteer vervolgens **[!UICONTROL Select Revision]**.
1. Selecteer **[!UICONTROL Add a Change]** of **[!UICONTROL Add All Changed Resources]**.

## Actieve bibliotheek {#active-library}

De bibliotheken kapselen een reeks veranderingen in u aan uw opgestelde code wilt aanbrengen. De actieve Bibliotheek maakt dit gemakkelijker, toestaand u om door veranderingen snel te herhalen en de invloed te zien.

Extensies, regels en gegevenselementen kunnen nu rechtstreeks worden opgeslagen in de bibliotheek waaraan u werkt. Indien nodig kan ook een nieuwe build worden gemaakt of zelfs een nieuwe bibliotheek worden gemaakt vanuit de [!UICONTROL Active Library] vervolgkeuzelijst.

De volgende lijst bevat meer informatie over het beheer van een actieve bibliotheek.

1. [Een nieuwe bibliotheek maken](libraries.md#create-a-library).
1. Ga naar [Regels](../managing-resources/rules.md), [Gegevenselementen](../managing-resources/data-elements.md), of [Extensies](../managing-resources/extensions/overview.md).
1. Selecteer uw actieve bibliotheek.
1. Breng de wijzigingen aan en sla de bibliotheek op en maak deze samen.
1. Test de wijzigingen en herhaal deze stappen zo nodig.
