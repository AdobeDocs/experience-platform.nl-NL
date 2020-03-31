---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Recept voor productaanbevelingen
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Recept voor productaanbevelingen

Het recept van de Aanbevelingen van het Product laat u toe om gepersonaliseerde productaanbevelingen te verstrekken die aan de behoeften en de belangen van uw klant worden aangepast. Met een accuraat voorspellingsmodel kan de aankoopgeschiedenis van een klant u inzicht verschaffen in welke producten zij geïnteresseerd kunnen zijn.

## Voor wie is dit recept gebouwd?

In de moderne tijd kan een detailhandelaar een veelheid van producten aanbieden, die hun klanten een heleboel keuzen geven die ook hun klanten kunnen hinderen zoeken. Vanwege tijd- en inspanningsbeperkingen kunnen klanten het gewenste product wellicht niet vinden, wat leidt tot aankopen met een hoog niveau van cognitieve dissonantie of helemaal geen aankoop.

## Wat doet dit recept?

Het recept van de Aanbevelingen van het Product gebruikt machine het leren om de interactie van een klant met producten in het verleden te analyseren, en een gepersonaliseerde lijst van productaanbevelingen snel en moeiteloos te produceren. Dit optimaliseert het productontdekkingsproces en elimineert lange, onproductieve, irrelevante onderzoeken naar uw klanten. Dientengevolge, kan het recept van de Aanbevelingen van het Product de algemene aankoopervaring van een klant verbeteren, die tot hogere betrokkenheid en grotere merkloyaliteit leidt.

## Hoe begin ik?

U kunt aan de slag door de zelfstudie van het Laboratorium van het Platform van de Ervaring van Adobe te volgen (zie de verbinding van het Laboratorium hieronder). Deze zelfstudie laat u zien hoe u het recept voor productaanbevelingen kunt maken in een Jupyter-laptop door de [laptop te volgen om de workflow voor recept](../jupyterlab/create-a-recipe.md) te volgen en het recept te implementeren in de Data Science Workspace van het Experience Platform.

* [Lab: De toekomst voorspellen met Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Lab-bronnen](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Gegevensschema

In dit recept worden aangepaste [XDM-schema](../../xdm/schema/field-dictionary.md) &#39;s gebruikt om de invoer- en uitvoergegevens te modelleren:

### Invoergegevensschema

| Veldnaam | Type |
--- | ---
| itemId | String |
| interactionType | String |
| tijdstempel | String |
| userId | String |

### Uitvoergegevensschema

| Veldnaam | Type |
--- | ---
| aanbevelingen | String |
| userId | Geheel |

## Algorithm

Het recept van de Aanbevelingen van het Product gebruikt samenwerkings het filtreren om een gepersonaliseerde lijst van productaanbevelingen voor uw klanten te produceren. Bij collectieve filtering is, in tegenstelling tot een op inhoud gebaseerde benadering, geen informatie over een specifiek product vereist, maar worden de historische voorkeuren van een klant voor een set producten gebruikt. Deze krachtige aanbeveling gebruikt twee eenvoudige veronderstellingen:
* Er zijn klanten met vergelijkbare belangen, en deze kunnen worden gegroepeerd door hun aankoop en het bladeren te vergelijken.
* Een klant is meer geïnteresseerd in een aanbeveling die is gebaseerd op soortgelijke klanten wat betreft hun aankoop- en browsergedrag.

Dit proces wordt opgesplitst in twee hoofdstappen. Eerst definieert u een subset van vergelijkbare klanten. Dan, binnen die reeks, identificeer gelijkaardige eigenschappen onder die klanten om een aanbeveling voor de doelklant terug te keren.