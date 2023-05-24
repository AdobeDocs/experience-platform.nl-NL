---
title: Extension Upgrades
description: Leer hoe extensieupgrades worden verpakt en weergegeven in de extensiecatalogus.
exl-id: 4a7e0c5c-4bd1-4fb8-8509-f88a0aa42ac4
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
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

Wanneer een extensieontwikkelaar een nieuwe versie van de extensie heeft opgegeven, wordt die nieuwe versie beschikbaar in de extensiecatalogus. In de catalogus wordt alleen de meest recente versie van een extensie weergegeven. U kunt geen andere extensieversie installeren dan `latest`.

Wanneer u een extensie aan uw eigenschap installeert, wordt de momenteel beschikbare versie geïnstalleerd en blijft uw eigenschap met die specifieke versie vanaf dat punt actief, zelfs als er nieuwere versies aan de catalogus worden toegevoegd.

## Upgrademeldingen

Als u een extensie voor uw eigenschap hebt geïnstalleerd en er een nieuwere versie beschikbaar is in de catalogus, wordt een [!UICONTROL Upgrade] op de extensiekaart wanneer u de pagina Geïnstalleerde extensies weergeeft.

U zult ook een bericht zien wanneer het uitgeven van middelen die door die uitbreiding worden verstrekt.

## Upgrades zijn permanent

Als u wilt bijwerken naar een nieuwere versie die beschikbaar is in de catalogus, moet u die upgrade zelf installeren. Een upgrade is een &#39;wijziging&#39; die moet worden toegevoegd aan een bibliotheek, getest en gepubliceerd voordat deze van invloed is op uw geïmplementeerde tags.

De verbetering zou niet lichtjes moeten worden genomen. U zou niet moeten bevorderen tenzij u bereid bent om de nieuwe uitbreiding te testen en bereid bent om het op te stellen. Nadat de upgrade aan de eigenschap is toegevoegd, moet deze in alle bibliotheken worden opgenomen. Elke bibliotheek die de bijgewerkte extensie niet bevat, mislukt tijdens het samenstellen.

Er is momenteel geen mogelijkheid om de extensie te verlagen naar een vorige versie. Zodra u hebt bevorderd (of u publiceert of niet), is de nieuwe uitbreidingsversie op uw bezit om te blijven.

## Upgradeproces

Het installeren van een upgrade is vrijwel hetzelfde als het voor het eerst installeren van de extensie.

1. Selecteren **[!UICONTROL Upgrade]** om naar de [!UICONTROL Extension Configuration] scherm.
1. Breng om het even welke configuratieveranderingen aan u zou willen aanbrengen.
1. Selecteer **[!UICONTROL Save]**.

De upgrade wordt pas uitgevoerd als u op **[!UICONTROL Save]**. U kunt [!UICONTROL Cancel] en blijft bij de momenteel geïnstalleerde versie. Selecteren **[!UICONTROL Save]** is het punt van geen terugkeer.

Extension Upgrades zijn niet toegestaan als u een bibliotheek hebt in het dialoogvenster `Approved` of `Submitted` status.  Dit komt doordat de volgende build de nieuwe extensieversie moet bevatten.  Voor een bibliotheek die `Approved` of `Submitted`De volgende bouwsteen is de productiefase.  Die build zou mislukken omdat deze niet de meest recente versie bevat. De workflow bestaat dus uit het publiceren of afwijzen van bibliotheken in de `Approved` of `Submitted` state _voor_ de extensie upgraden.

## Een upgrade publiceren

Nadat de promotieuitbreiding op uw bezit wordt geïnstalleerd, moet u het in alle Bibliotheken van dat punt door:sturen omvatten. Er wordt een foutbericht over de build weergegeven voor alle bibliotheken die dit bericht niet bevatten.

Bovendien is het toevoegen van de bijgewerkte extensie aan uw bibliotheek hetzelfde als [andere wijzigingen toevoegen](../../publishing/libraries.md) naar een bibliotheek.

Van de [!UICONTROL Edit Library] scherm kunt u de &quot;[!UICONTROL Add All Changed Resources]&quot; of u kunt de &quot;[!UICONTROL Add a Resource]&quot; en selecteer de bijgewerkte extensie als zodanig.

>[!TIP]
>
>Het is mogelijk voor uitbreidingsontwikkelaars om nieuwe configuratiepunten aan hun uitbreidingsmeningen toe te voegen om nieuwe functionaliteit toe te laten.  Als u bouwstijlmislukkingen na bevordering aan een nieuwe uitbreidingsversie ziet - en u hebt geïsoleerd om mislukkingen aan die uitbreiding te bouwen - dan het eerste te doen ding is naar de Configure pagina van de uitbreiding gaan en zeker zijn om te sparen (zelfs als u niets) veranderde.  Voeg vervolgens de nieuwe wijziging toe aan uw bibliotheek en probeer opnieuw samen te stellen.

Nadat u de extensie-upgrade aan uw bibliotheek hebt toegevoegd, kunt u de stappen volgen die worden beschreven in [publicatiestroom](../../publishing/publishing-flow.md) om uw bibliotheek te publiceren tot en met Production.
