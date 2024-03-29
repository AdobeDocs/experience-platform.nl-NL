---
keywords: Experience Platform;ontwikkelaarsgids;de Werkruimte van de Wetenschap van Gegevens;populaire onderwerpen;In real time machine het leren;
solution: Experience Platform
title: Real-time Machine Learning-overzicht
description: Het leren van machines in real time kan de relevantie van uw digitale ervaringsinhoud voor uw eindgebruikers drastisch verbeteren. Dit wordt mogelijk gemaakt door real-time conferenties en voortdurend leren op het Edge Network van het Experience Platform te benutten.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# Real-time Machine Learning-overzicht (Alpha)

>[!IMPORTANT]
>
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Het leren van machines in real time kan de relevantie van uw digitale ervaringsinhoud voor uw eindgebruikers drastisch verbeteren. Dit wordt mogelijk gemaakt door real-time conferenties en voortdurend leren over de [!DNL Experience Platform Edge Network].

Een combinatie naadloze berekening op zowel de Hub als de [!DNL Edge] vermindert dramatisch de latentie die traditioneel betrokken is bij het aandrijven van hyper-gepersonaliseerde ervaringen die zowel relevant als ontvankelijk zijn. Vandaar, het Leren van de machine in real time verstrekt conclusies met ongelooflijk lage latentie voor synchrone besluitvorming. Voorbeelden zijn het renderen van gepersonaliseerde webpagina-inhoud of het surfen op een aanbieding of korting om de kans op fouten te verkleinen en conversies in een webwinkel te verhogen.

## Real-time Machine Learning-architectuur {#architecture}

De volgende diagrammen verstrekken een overzicht voor de het Leren architectuur van de machine in real time. Alfa heeft momenteel een vereenvoudigde versie.

![alfakanaal](../images/rtml/alpha-arch.png)

![Vereenvoudigd overzicht](../images/rtml/end-to-end-arch.png)

## Workflow voor het leren van machines in realtime

In de volgende workflow worden de typische stappen en resultaten beschreven die zijn betrokken bij het maken en gebruiken van een Real-Time Machine Learning-model.

### Inname van gegevens en preparaten

Gegevens worden opgenomen en getransformeerd met de [!DNL Experience Data Model] (XDM) op Adobe Experience Platform. Deze gegevens worden gebruikt voor modeltraining. Ga voor meer informatie over XDM naar de [XDM-overzicht](../../xdm/home.md).

### Authoring

Maak een real-time model voor het leren van machines door deze volledig te ontwerpen of in te voeren als een vooraf geserialiseerd ONNX-model in Adobe Experience Platform Jupyter-laptops.

### Implementatie

Stel uw model aan het [!DNL Edge Network] om een Echte - tijdMachine het Leren dienst in te leiden [!UICONTROL Service Gallery] het API-eindpunt van de voorspelling gebruiken.

### Opkomst

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
> - Na 20 seconden slaap [!DNL Edge] de implementatie wordt handmatig uitgevoerd.
> - Voor diep leren moeten uw gegevens zodanig worden verzonden dat wanneer `df.values` wordt genoemd keert het een serie terug die door uw model DL aanvaardbaar is. Dit komt omdat de ONNX model scoring node gebruikt `df.values` en verzendt de uitvoer naar de score ten opzichte van het model.


### Functies:

| | Alpha (mei) |
| --- | --- |
| **Functies** | - Het gebruiken van het de notitieboekjecalplaatje van RTML, auteur, test, en stelt een model van het douanemachine leren op. <br> - Ondersteuning voor het importeren van vooraf opgeleide modellen voor machinaal leren. <br> - Real-time Machine Learning SDK. <br> - Starterset van ontwerpknooppunten. <br> - Gedistribueerd naar Adobe Experience Platform Hub. |
| **Beschikbaarheid** | Noord-Amerika |
| **Ontwerpknooppunten** | - Pandas <br> - ScikitLearn <br> - ONNXNode <br> - Splitsen <br> - ModelUpload <br> - OneHotEncoder |
| **Runtime van scores** | ONNX |

## Volgende stappen

U kunt beginnen door [aan de slag](./getting-started.md) hulplijn. Deze gids begeleidt u door vestiging alle vereiste eerste vereisten voor het creëren van een In real time het Leren van de Machine model.
