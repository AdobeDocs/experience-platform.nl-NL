---
keywords: Experience Platform;product aanbeveling recept;Data Science Workspace;populaire onderwerpen;recepten;pre-build recept
solution: Experience Platform
title: Recipe productaanbeveling
topic-legacy: overview
description: Met het product Recommendations-recept kunt u op maat gemaakte productaanbevelingen doen die zijn afgestemd op de behoeften en belangen van uw klant. Met een accuraat voorspellingsmodel kan de aankoopgeschiedenis van een klant u inzicht verschaffen in welke producten zij geïnteresseerd kunnen zijn.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 38c493e6306e493f4ef5caf90509bda6f4d80023
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# Recept voor productaanbevelingen

Met het product Recommendations-recept kunt u op maat gemaakte productaanbevelingen doen die zijn afgestemd op de behoeften en belangen van uw klant. Met een accuraat voorspellingsmodel kan de aankoopgeschiedenis van een klant u inzicht verschaffen in welke producten zij geïnteresseerd kunnen zijn.

## Voor wie is dit recept gebouwd?

In de moderne tijd kan een detailhandelaar een veelheid van producten aanbieden, die hun klanten een heleboel keuzen geven die ook hun klanten kunnen hinderen zoeken. Vanwege tijd- en inspanningsbeperkingen kunnen klanten het gewenste product wellicht niet vinden, wat leidt tot aankopen met een hoog niveau van cognitieve dissonantie of helemaal geen aankoop.

## Wat doet dit recept?

Het product-Recommendations-recept gebruikt automatisch leren om de interactie van een klant met producten in het verleden te analyseren en snel en moeiteloos een persoonlijke lijst met productaanbevelingen te genereren. Dit optimaliseert het productontdekkingsproces en elimineert lange, onproductieve, irrelevante onderzoeken naar uw klanten. Als gevolg hiervan kan het Product Recommendations-recept de algehele aankoopervaring van een klant verbeteren, wat leidt tot meer betrokkenheid en een sterkere merkloyaliteit.

## Hoe begin ik?

U kunt aan de slag door de zelfstudie van Adobe Experience Platform Lab te volgen (zie de verbinding van het Laboratorium hieronder). Deze zelfstudie laat u zien hoe u het product Recommendations-recept kunt maken in een Jupyter-laptop door het volgende te doen: [notebook naar recept](../jupyterlab/create-a-model.md) werkschema en de toepassing van het recept in [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Lab: De toekomst voorspellen met Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Lab-bronnen](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Gegevensschema

In dit recept wordt aangepaste [XDM-schema&#39;s](../../xdm/schema/field-dictionary.md) om de invoer- en uitvoergegevens te modelleren:

### Invoergegevensschema

| Veldnaam | Type |
| --- | --- |
| itemId | Tekenreeks |
| interactionType | Tekenreeks |
| timestamp | Tekenreeks |
| userId | Tekenreeks |

### Uitvoergegevensschema

| Veldnaam | Type |
| --- | --- |
| aanbevelingen | Tekenreeks |
| userId | Geheel |

## Algorithm

Het product Recommendations-recept maakt gebruik van collectieve filtering om een gepersonaliseerde lijst met productaanbevelingen voor uw klanten te genereren. Bij collectieve filtering is, in tegenstelling tot een op inhoud gebaseerde benadering, geen informatie over een specifiek product vereist, maar worden de historische voorkeuren van een klant voor een set producten gebruikt. Deze krachtige aanbeveling gebruikt twee eenvoudige veronderstellingen:
* Er zijn klanten met vergelijkbare belangen, en deze kunnen worden gegroepeerd door hun aankoop en het bladeren te vergelijken.
* Een klant is meer geïnteresseerd in een aanbeveling die is gebaseerd op soortgelijke klanten wat betreft hun aankoop- en browsergedrag.

Dit proces wordt opgesplitst in twee hoofdstappen. Eerst definieert u een subset van vergelijkbare klanten. Dan, binnen die reeks, identificeer gelijkaardige eigenschappen onder die klanten om een aanbeveling voor de doelklant terug te keren.
