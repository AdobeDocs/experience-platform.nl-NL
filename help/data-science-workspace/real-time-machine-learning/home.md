---
keywords: Experience Platform;ontwikkelaarshandleiding;Data Science Workspace;populaire onderwerpen;In real time machinaal leren;
solution: Experience Platform
title: Real-time Machine Learning-overzicht
description: Het leren van machines in real time kan de relevantie van uw digitale ervaringsinhoud voor uw eindgebruikers drastisch verbeteren. Dit wordt mogelijk gemaakt door real-time conferenties en voortdurend leren op de Edge Network van het Experience Platform te benutten.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Real-time Machine Learning-overzicht (Alpha)

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Het leren van machines in real time kan de relevantie van uw digitale ervaringsinhoud voor uw eindgebruikers drastisch verbeteren. Dit wordt mogelijk gemaakt door real-time conferenties en voortdurend leren over de [!DNL Experience Platform Edge Network] te benutten.

Een combinatie van naadloze berekeningen op zowel de Hub als de [!DNL Edge] vermindert dramatisch de latentie die traditioneel betrokken is bij het aansturen van hypergepersonaliseerde ervaringen die zowel relevant als responsief zijn. Daarom biedt Real-time Machine Learning ongekend lage latentie voor synchrone besluitvorming. Voorbeelden zijn het renderen van gepersonaliseerde webpagina-inhoud of het onthullen van een aanbieding of korting om het aantal fouten te verminderen en het aantal conversies in een webwinkel te verhogen.

## Real-time Machine Learning-architectuur {#architecture}

De volgende diagrammen verstrekken een overzicht voor de het Leren architectuur van de machine in real time. Alfa heeft momenteel een vereenvoudigde versie.

![ alpha- boog ](../images/rtml/alpha-arch.png)

![ Vereenvoudigd overzicht ](../images/rtml/end-to-end-arch.png)

## Workflow in real-time leren

In de volgende workflow worden de typische stappen en resultaten beschreven die zijn vereist voor het maken en gebruiken van een Real-Time Machine Learning-model.

### Inname van gegevens en preparaten

Gegevens worden opgenomen en getransformeerd met de [!DNL Experience Data Model] (XDM) op Adobe Experience Platform. Deze gegevens worden gebruikt voor modeltraining. Meer over XDM leren, bezoek het [ overzicht XDM ](../../xdm/home.md).

### Authoring

Maak een real-time model voor het leren van machines door deze volledig te ontwerpen of in te voeren als een vooraf geserialiseerd ONNX-model in Adobe Experience Platform Jupyter-laptops.

### Implementatie

Implementeer uw model naar de [!DNL Edge Network] om een real-time machine learning-service in het [!UICONTROL Service Gallery] te maken met behulp van het voorspellings-API-eindpunt.

### gevolgtrekking

Met het voorspellingsREST API-eindpunt kunt u in real-time inzichten van machines genereren.

### Levering

Marketers kunnen vervolgens segmenten en regels definiëren die de leerscores voor machines in real time toewijzen aan ervaringen met Adobe Target. Op deze manier kunnen bezoekers van de website van uw merk in real-time dezelfde of hyperpersonaliseerde ervaring van de volgende pagina zien.

## Huidige functionaliteit

Het leren van machines in real time is momenteel in alpha. De hieronder beschreven functionaliteit kan worden gewijzigd wanneer meer functies en knooppunten beschikbaar worden gemaakt.

>[!NOTE]
>
> Beperkingen van de Alpha:
> - Momenteel worden alleen ONNX-modellen ondersteund.
> - De functies die in knopen worden gebruikt kunnen niet in series worden vervaardigd. Bijvoorbeeld, een lambdafunctie die in een knoop van Pandas wordt gebruikt.
> - Er is 20 seconden slaap nadat [!DNL Edge] de plaatsing manueel wordt gedaan.
> - Voor diep leren moeten uw gegevens zodanig worden verzonden dat wanneer `df.values` wordt genoemd, een array wordt geretourneerd die door uw DL-model wordt geaccepteerd. De reden hiervoor is dat het ONNX model scoring knooppunt `df.values` gebruikt en de uitvoer naar de score stuurt voor het model.


### Functies:

| | Alpha (mei) |
| --- | --- |
| **Eigenschappen** | - Gebruik de RTML-laptopsjabloon, ontwerp, test en implementeer een aangepast machine-learningmodel. <br> - Ondersteuning voor het importeren van vooraf getrainde modellen voor machine learning. <br> - Real-time Machine Learning SDK. <br> - Startset van ontwerpknooppunten. <br> - Gedistribueerd naar Adobe Experience Platform Hub. |
| **Beschikbaarheid** | North America |
| **Authoring Nodes** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Splitsen <br> - ModelUpload <br> - OneHotEncoder |
| **het Scoren runtime** | ONNX |

## Volgende stappen

U kunt beginnen door [ te volgen begonnen wordt ](./getting-started.md) gids. Deze gids begeleidt u door vestiging alle vereiste eerste vereisten voor het creëren van een In real time het Leren van de Machine model.
