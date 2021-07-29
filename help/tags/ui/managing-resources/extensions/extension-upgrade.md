---
title: Extension Upgrades
description: Leer hoe extensieupgrades worden verpakt en weergegeven in de extensiecatalogus.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# Uitbreidingen upgraden

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Extensieontwikkelaars voegen voortdurend nieuwe functies toe aan hun extensies en corrigeren vaak bugs. Deze updates worden verpakt in nieuwe versies van een extensie en beschikbaar gesteld in de extensiecatalogus als upgrades.

## Extensiecatalogus

Wanneer een extensieontwikkelaar een nieuwe versie van de extensie heeft opgegeven, wordt die nieuwe versie beschikbaar in de extensiecatalogus. In de catalogus wordt alleen de meest recente versie van een extensie weergegeven. U kunt geen extensieversie installeren anders dan `latest`.

Wanneer u een extensie aan uw eigenschap installeert, wordt de momenteel beschikbare versie geïnstalleerd en blijft uw eigenschap met die specifieke versie vanaf dat punt actief, zelfs als er nieuwere versies aan de catalogus worden toegevoegd.

## Upgrademeldingen

Wanneer u een extensie voor uw eigenschap hebt geïnstalleerd en er een nieuwere versie beschikbaar is in de catalogus, ziet u een [!UICONTROL Upgrade] knop op de extensiekaart wanneer u de pagina Geïnstalleerde extensies weergeeft.

U zult ook een bericht zien wanneer het uitgeven van middelen die door die uitbreiding worden verstrekt.

## Upgrades zijn permanent

Als u wilt bijwerken naar een nieuwere versie die beschikbaar is in de catalogus, moet u die upgrade zelf installeren. Een upgrade is een &#39;wijziging&#39; die moet worden toegevoegd aan een bibliotheek, getest en gepubliceerd voordat deze van invloed is op uw geïmplementeerde tags.

De verbetering zou niet lichtjes moeten worden genomen. U zou niet moeten bevorderen tenzij u bereid bent om de nieuwe uitbreiding te testen en bereid bent om het op te stellen. Nadat de upgrade aan de eigenschap is toegevoegd, moet deze in alle bibliotheken worden opgenomen. Elke bibliotheek die de bijgewerkte extensie niet bevat, mislukt tijdens het samenstellen.

Er is momenteel geen mogelijkheid om de extensie te verlagen naar een vorige versie. Zodra u hebt bevorderd (of u publiceert of niet), is de nieuwe uitbreidingsversie op uw bezit om te blijven.

## Upgradeproces

Het installeren van een upgrade is vrijwel hetzelfde als het voor het eerst installeren van de extensie.

1. Selecteer **[!UICONTROL Upgrade]** om naar het [!UICONTROL Extension Configuration] scherm te gaan.
1. Breng om het even welke configuratieveranderingen aan u zou willen aanbrengen.
1. Selecteer **[!UICONTROL Save]**.

De upgrade wordt pas daadwerkelijk uitgevoerd wanneer u **[!UICONTROL Save]** hebt bereikt. U kunt [!UICONTROL Cancel] op elk gewenst moment selecteren en bij de momenteel geïnstalleerde versie blijven. Het selecteren van **[!UICONTROL Save]** is het punt van geen terugkeer.

Extensieupgrades zijn niet toegestaan als u een bibliotheek hebt met de status `Approved` of `Submitted`.  Dit komt doordat de volgende build de nieuwe extensieversie moet bevatten.  Voor een bibliotheek die `Approved` of `Submitted` is, is volgende bouwstijl de productie bouwstijl.  Die build zou mislukken omdat deze niet de nieuwste versie bevat. De workflow bestaat dus uit het publiceren of afwijzen van bibliotheken in de `Approved`- of `Submitted`-status _before_ om de extensie te upgraden.

## Een upgrade publiceren

Nadat de promotieuitbreiding op uw bezit wordt geïnstalleerd, moet u het in alle Bibliotheken van dat punt door:sturen omvatten. Er wordt een foutbericht over de build weergegeven voor alle bibliotheken die dit bericht niet bevatten.

Buiten dat, is het toevoegen van de promotieuitbreiding aan uw bibliotheek het zelfde als [toevoegend een andere verandering](../../publishing/libraries.md) aan een bibliotheek.

Van het [!UICONTROL Edit Library] scherm, kunt u &quot;[!UICONTROL Add All Changed Resources]&quot;knoop gebruiken of u kunt &quot;[!UICONTROL Add a Resource]&quot;knoop gebruiken en de promotieuitbreiding op zich selecteren.

>[!TIP]
>
>Het is mogelijk voor uitbreidingsontwikkelaars om nieuwe configuratiepunten aan hun uitbreidingsmeningen toe te voegen om nieuwe functionaliteit toe te laten.  Als u bouwstijlmislukkingen na bevordering aan een nieuwe uitbreidingsversie ziet - en u hebt geïsoleerd om mislukkingen aan die uitbreiding te bouwen - dan het eerste te doen ding is naar de Configure pagina van de uitbreiding gaan en zeker zijn om te sparen (zelfs als u niets) veranderde.  Voeg vervolgens de nieuwe wijziging toe aan uw bibliotheek en probeer opnieuw samen te stellen.

Nadat u de extensie-upgrade aan uw bibliotheek hebt toegevoegd, kunt u de stappen volgen die worden beschreven in [publicatiestroom](../../publishing/publishing-flow.md) om uw bibliotheek te publiceren naar Production.
