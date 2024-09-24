---
title: Query Pro-modus doorlopen
description: Leer hoe u van elke grafiek naar een nieuw dashboard kunt navigeren om uw gegevens te verkennen aan de hand van een boor door.
source-git-commit: d851f7b1ac9b2fda5297cf752013c2ffb775e33d
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Doorboor {#drill-through}

De booronderzoeken vergemakkelijken multi-layered gegevensanalyse door het eenvoudig te maken om van om het even welke grafiek aan een nieuw dashboard te navigeren. Deze eigenschap maakt het gemakkelijk om van overzichten op hoog niveau aan diepgaande rapporten over te schakelen wanneer het bestuderen van tendensen, klantengedrag, operationele indicatoren, en meer, ervoor zorgend dat u altijd de context hebt u wenst.

Het systeem zorgt ervoor dat de analyse u begint naadloos door de volledige boor door ervaring wordt voortgezet door globale filters en datumwaaierfilters van de brondashboards aan de doeldashboards automatisch over te gaan. Om de navigatie tussen verschillende lagen van de studie te vergemakkelijken, staat het systeem meervoudige boor door.

## Een boor maken door {#create-drill-through}

Als u een doorboor wilt maken, selecteert u eerst **[!UICONTROL Edit]** in de dashboardweergave.

![ A douanedashboard met Edit benadrukte.](../../images/query-pro-mode/drill-through.png)

Selecteer de ellips in het diagram dat u wilt doorlopen en selecteer vervolgens **[!UICONTROL Edit]** .

![ een grafiek die het elliptische menu met uitgezocht geeft tonen.](../../images/query-pro-mode/drill-through-chart-edit.png)

Gebruik in het deelvenster [!UICONTROL Properties] de schakeloptie om **[!UICONTROL Enable drill through]** in te schakelen en selecteer vervolgens de vervolgkeuzelijst **[!UICONTROL Target dashboard]** . Zorg ervoor dat de schakeloptie voor **[!UICONTROL Filter pass-through]** is ingeschakeld en selecteer vervolgens **[!UICONTROL Save and close]** .

![ de eigenschappen van de Grafiek paneel met toelaten boor door, benadrukt het dashboard van het Doel, en de aangewezen pas-door van de Filter.](../../images/query-pro-mode/drill-through-chart-properties.png)

>[!INFO]
>
>Herhaal bovenstaande stappen voor het doeldashboard om een boor met meerdere niveaus in te stellen.

## Boren weergeven {#view-drill-through}

Als u een boor wilt bekijken, selecteert u eerst de ovaal in het diagram in de dashboardweergave en vervolgens **[!UICONTROL Drill through]** .

![ een grafiek die van A het elliptische menu met Boor door benadrukt toont.](../../images/query-pro-mode/drill-through-chart-view.png)

De boor door doeldashboard wordt getoond. U kunt deze stap herhalen als u drillingcontroles op meerdere niveaus hebt.

![ het doeldasboard dat met de boor door benadrukt wordt getoond.](../../images/query-pro-mode/drill-through-target-dashboard.png)

>[!NOTE]
>
>Alle filters die worden toegepast op het brondashboard, worden doorgegeven aan het doeldashboard. Datumfilters en algemene filters worden echter uitgeschakeld op onderliggende dashboards.

## Een boor verwijderen {#remove-drill-through}

Als u een boor wilt verwijderen, selecteert u eerst **[!UICONTROL Edit]** in de dashboardweergave.

![ A douanedashboard met Edit benadrukte.](../../images/query-pro-mode/drill-through.png)

Selecteer de ellips in het diagram waardoor u een boor wilt verwijderen en selecteer vervolgens **[!UICONTROL Edit]** .

![ een grafiek die het elliptische menu met uitgezocht geeft tonen.](../../images/query-pro-mode/drill-through-chart-edit.png)

Selecteer in het deelvenster [!UICONTROL Properties] de schakeloptie die u wilt uitschakelen **[!UICONTROL Enable drill through]** en selecteer vervolgens **[!UICONTROL Save and close]** .

![ de eigenschappen van de Grafiek paneel met knevel voor [!UICONTROL Enable drill through] wordt onbruikbaar gemaakt benadrukt.](../../images/query-pro-mode/drill-through-disable.png)

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u een boor kunt maken voor het dashboard. U kunt ook leren hoe te om grafieken van bestaande gegevensmodellen in Adobe Experience Platform UI met de [ geleide gids van de ontwerpwijze ](../../user-defined-dashboards.md) te produceren.
