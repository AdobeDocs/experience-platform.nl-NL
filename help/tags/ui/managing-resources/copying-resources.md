---
title: Bronnen kopiëren
description: Leer hoe u een nieuwe tagbron maakt met behulp van de instellingen van een bestaande tagbron in Adobe Experience Platform.
exl-id: 7e52ceae-97df-4c64-aba3-4f5ba6018a47
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Bronnen kopiëren

Soms is het handig om een nieuwe bron te maken met behulp van de instellingen van een bestaande bron. In deze gevallen kunt u een kopie maken.

Eigenschappen, Extensies, Regels en Gegevenselementen kunnen allemaal worden gekopieerd.

Het kopiëren van een middel leidt tot een duplicaat van dat middel in de gespecificeerde bestemming. Dit is een discrete, eenmalige actie en er is geen permanente relatie tussen de oorspronkelijke bron en eventuele kopieën die zijn gemaakt.

## Een kopie starten

U kunt een kopie van een extensie starten door de geïnstalleerde extensies te bekijken, de vervolgkeuzepijl op de knop **[!UICONTROL Configure]** te selecteren en **[!UICONTROL Copy]** te selecteren.

![&#x200B; het Kopiëren van de uitbreiding van Analytics &#x200B;](../../images/copy-initiate-extension.png)

Voor eigenschappen, regels, en gegevenselementen, selecteer eenvoudig de bron u wilt kopiëren en dan **[!UICONTROL Copy]** in het actiemenu selecteren.

![&#x200B; Kopend mijn regel van Analytics &#x200B;](../../images/copy-initiate-rule.png)

Als u een regel of een gegevenselement kopieert, kunt u in het dialoogvenster Kopiëren het vervolgkeuzemenu gebruiken om een eigenschap Doel te selecteren waarnaar u wilt kopiëren (standaardinstelling is de huidige eigenschap). Extensies kunnen niet naar dezelfde eigenschap worden gekopieerd, zodat deze optie niet beschikbaar is.

>[!NOTE]
>
>Het is niet mogelijk om middelen aan een ander bezit te kopiëren als één bezit voor uitbreidingsontwikkeling wordt gevormd en het andere bezit niet is.

Selecteer **[!UICONTROL Copy]** nadat u het gewenste gedrag hebt geconfigureerd.

## Eigenschappen kopiëren

Wanneer u een kopie van een volledige eigenschap maakt, zijn er een paar dingen die u over het proces moet begrijpen.

>[!IMPORTANT]
>
>De middelen die het veranderlijke type gebruiken van de gegevenselement bijwerken zullen extra stappen na het kopiëren vereisen. Bewerk elke actie voor een updatevariabele, wijzig een waarde in het gegevens- of XDM-object en sla de wijzigingen op. De gepubliceerde bibliotheek zou dan zoals verwacht moeten werken. Neem contact op met Technische ondersteuning als u vragen hebt over dit proces.

* De eigenschapinstellingen worden op exact dezelfde wijze gekopieerd (domeinen, geavanceerde instellingen, enz.)
* Regels, gegevenselementen en extensies vanuit de oorspronkelijke eigenschap worden naar de nieuwe doeleigenschap gekopieerd.  Adapters, omgevingen en bibliotheken worden niet gekopieerd.
* Vereiste extensies (extensies die worden vereist door bestaande gegevenselementen of regelcomponenten) worden naar de eigenschap target gekopieerd, zelfs als ze zijn verwijderd uit de eigenschap origin.
* Het kopiëren van een eigenschap kan enige tijd duren.  Dit gebeurt op de achtergrond.  U kunt de voortgang van de kopie controleren of u kunt andere taken uitvoeren terwijl deze plaatsvindt.
* Als u een individuele bron wijzigt nadat deze al naar de eigenschap target is gekopieerd (maar voordat de kopie is voltooid), worden de nieuwe wijzigingen niet meer gekopieerd.

## Extensies kopiëren

Wanneer u een extensie naar een andere eigenschap kopieert, zijn er een paar dingen die u moet begrijpen.

* Als de doeleigenschap de extensie niet heeft geïnstalleerd, wordt deze geïnstalleerd met dezelfde instellingen als de oorspronkelijke eigenschap.
* Als de extensie al is geïnstalleerd in de doeleigenschap, worden alleen de instellingen gekopieerd.
* Als het bestemmingsbezit een lagere geïnstalleerde versie van de uitbreiding heeft, zult u een bericht ontvangen dat u de uitbreiding op het bestemmingsbezit moet bevorderen alvorens u het exemplaar kunt uitvoeren.  Extensieontwikkelaars kunnen in de loop der tijd instellingen toevoegen aan hun extensies, zodat instellingen van een nieuwere extensie niet betrouwbaar kunnen worden toegepast op oudere versies.
* Als de bestemmingseigenschap een hogere versie van de geïnstalleerde extensie heeft, worden de instellingen overgekopieerd, maar wordt er geen downgrade uitgevoerd.  Het bestemmingsbezit behoudt nog zijn huidig versieaantal.

## Regels en gegevenselementen kopiëren

Alle regels en gegevenselementen worden verstrekt door een uitbreiding, zodat wanneer u over eigenschappen kopieert, Experience Platform deze onderliggende uitbreidingen moet rekenschap geven.

![&#x200B; het kopiëren van een Regel aan mijn Bezit van de Demo &#x200B;](../../images/copy-rules-dialog1.png)

Het dialoogvenster Kopiëren bevat een uitleg van wat er precies zal gebeuren voordat u begint met kopiëren. Het bovenstaande dialoogvenster is bedoeld voor een regel, maar hetzelfde geldt voor gegevenselementen.

1. **Extensies die door deze regels worden vereist worden gekopieerd.** Dit laat u weten dat de vereiste uitbreidingen met de regel zullen gaan.  Deze kopieën volgen dezelfde regels als een kopie van een reguliere extensie die hierboven wordt beschreven.
1. **de montages van de Uitbreiding zullen NIET worden gekopieerd als de uitbreiding reeds geïnstalleerd is.** Dit betekent dat als de vereiste extensies al bestaan op de eigenschap destination, de extensie ongewijzigd blijft.  Als u wenst om de uitbreidingsmontages eveneens te kopiëren, kunt u **gebruiken vervangt uitbreidingsmontages op bestemmingsBezit** knevel en de verklaring wordt dienovereenkomstig bijgewerkt.
1. **Elementen van Gegevens die door deze Regels worden vereist zullen NIET worden gekopieerd.** Deze uitleg is alleen van toepassing op regels.  Regels vertrouwen vaak op gegevenselementen om correct te functioneren.  Als u een regel naar een nieuwe eigenschap kopieert, moet u ook alle vereiste gegevenselementen als een afzonderlijke actie kopiëren.
