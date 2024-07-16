---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui guide;mapper;mapping;data prep;data voorbereiden;voorbereiden van gegevens;
solution: Experience Platform
title: Overzicht van Data Prep
description: Dit document introduceert Data Prep in Adobe Experience Platform.
exl-id: 9bef5c3b-368d-4492-bdef-64e67fc25bfd
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# Berekende velden

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken.

Selecteer **[!UICONTROL Add calculated field]** om een berekend veld te maken.

![](./images/calculated-fields/add-calculated-field.png)

Het deelvenster **[!UICONTROL Create calculated field]** wordt weergegeven. Het linkerdialoogvenster bevat de velden, functies en operatoren die in berekende velden worden ondersteund. Selecteer een van de tabbladen om functies, velden of operatoren toe te voegen aan de expressie-editor.

![](./images/calculated-fields/create-calculated-field.png)

| Tabtoets | Beschrijving |
| --- | ----------- |
| Functie | Op het tabblad Functies staan de functies die beschikbaar zijn voor het transformeren van de gegevens. Om meer over de functies te leren u binnen berekende gebieden kunt gebruiken, te lezen gelieve de gids op [ gebruikend de functies van de Prep van Gegevens (Mapper) ](./functions.md). |
| Veld | Het tabblad Veld bevat velden en kenmerken die beschikbaar zijn in het bronschema. |
| Operator | Het tabblad Operatoren bevat een lijst met operatoren die beschikbaar zijn om de gegevens te transformeren. |

U kunt handmatig velden, functies en operatoren toevoegen met de expressieeditor in het midden. Selecteer de editor om een expressie te maken.

![](./images/calculated-fields/write-calculated-field.png)

Selecteer **[!UICONTROL Save]** om door te gaan.

Het kaartscherm verschijnt weer met het nieuwe bronveld. Pas het desbetreffende doelveld toe en selecteer **[!UICONTROL Finish]** om de toewijzing te voltooien.

![](./images/calculated-fields/new-calculated-field.png)
