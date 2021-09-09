---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui guide;mapper;mapping;data prep;data voorbereiden;voorbereiden van gegevens;
solution: Experience Platform
title: Overzicht van Data Prep
topic-legacy: overview
description: Dit document introduceert Data Prep in Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---


# Berekende velden

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken.

Selecteer **[!UICONTROL Add calculated field]** om een berekend veld te maken.

![](./images/calculated-fields/add-calculated-field.png)

Het **[!UICONTROL Create calculated field]** paneel verschijnt. Het linkerdialoogvenster bevat de velden, functies en operatoren die in berekende velden worden ondersteund. Selecteer een van de tabbladen om functies, velden of operatoren toe te voegen aan de expressie-editor.

![](./images/calculated-fields/create-calculated-field.png)

| Tab | Beschrijving |
| --- | ----------- |
| -functie | Op het tabblad Functies staan de functies die beschikbaar zijn voor het transformeren van de gegevens. Voor meer informatie over de functies die u kunt gebruiken binnen berekende velden, leest u de handleiding op [met de functies Data Prep (Mapper)](./functions.md). |
| Veld | Het tabblad Veld bevat velden en kenmerken die beschikbaar zijn in het bronschema. |
| Operator | Het tabblad Operatoren bevat een lijst met operatoren die beschikbaar zijn om de gegevens te transformeren. |

U kunt handmatig velden, functies en operatoren toevoegen met de expressieeditor in het midden. Selecteer de editor om een expressie te maken.

![](./images/calculated-fields/write-calculated-field.png)

Selecteer **[!UICONTROL Save]** om door te gaan.

Het kaartscherm verschijnt weer met het nieuwe bronveld. Pas het desbetreffende doelveld toe en selecteer **[!UICONTROL Finish]** om de toewijzing te voltooien.

![](./images/calculated-fields/new-calculated-field.png)