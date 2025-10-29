---
keywords: Experience Platform;product aanbeveling recept;Data Science Workspace;populaire onderwerpen;recepten;pre-build recept
solution: Experience Platform
title: Recipe productaanbeveling
description: Het recept van de Aanbevelingen van het Product laat u toe om gepersonaliseerde productaanbevelingen te verstrekken die aan de behoeften en de belangen van uw klant worden aangepast. Met een accuraat voorspellingsmodel kan de aankoopgeschiedenis van een klant u insight voorzien van welke producten ze willen.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Recept voor productaanbevelingen

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Het recept van de Aanbevelingen van het Product laat u toe om gepersonaliseerde productaanbevelingen te verstrekken die aan de behoeften en de belangen van uw klant worden aangepast. Met een accuraat voorspellingsmodel kan de aankoopgeschiedenis van een klant u insight voorzien van welke producten ze willen.

## Voor wie is dit recept gebouwd?

In de moderne tijd kan een retailer een groot aantal producten aanbieden, waardoor hun klanten een hoop keuzes kunnen maken die ook het zoeken van hun klanten kunnen belemmeren. Vanwege tijd- en inspanningsbeperkingen kunnen klanten het gewenste product wellicht niet vinden, wat leidt tot aankopen met een hoog niveau van cognitieve dissonantie of helemaal geen aankoop.

## Wat doet dit recept?

Het recept van de Aanbevelingen van het Product gebruikt machine het leren om de interactie van een klant met producten in het verleden te analyseren, en een gepersonaliseerde lijst van productaanbevelingen snel en moeiteloos te produceren. Dit optimaliseert het productontdekkingsproces en elimineert lange, onproductieve, irrelevante onderzoeken naar uw klanten. Dientengevolge, kan het recept van de Aanbevelingen van het Product de algemene aankoopervaring van een klant verbeteren, die tot hogere betrokkenheid en grotere merkloyaliteit leidt.

## Hoe begin ik?

U kunt aan de slag door de zelfstudie van Adobe Experience Platform Lab te volgen (zie de verbinding van het Laboratorium hieronder). Deze zelfstudie zal u tonen hoe te om het recept van de Aanbevelingen van het Product in een Notitieboekje van Jupyter tot stand te brengen door [ notitieboekje te volgen aan recept ](../jupyterlab/create-a-model.md) werkschema, en het recept in [!DNL Experience Platform] uit te voeren [!DNL Data Science Workspace].

* [ Laboratorium: Verwacht de Toekomst met de Wetenschap van Gegevens Workspace ](https://expleague.azureedge.net/labs/L777/index.html)
* [ middelen van het Laboratorium ](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Gegevensschema

Dit recept gebruikt douane [ XDM schema&#39;s ](../../xdm/schema/field-dictionary.md) om de input en outputgegevens te modelleren:

### Invoergegevensschema

| Veldnaam | Type |
| --- | --- |
| itemId | String |
| interactionType | String |
| tijdstempel | String |
| userId | String |

### Uitvoergegevensschema

| Veldnaam | Type |
| --- | --- |
| aanbevelingen | String |
| userId | Geheel |

## Algorithm

Het recept van de Aanbevelingen van het Product gebruikt samenwerkings het filtreren om een gepersonaliseerde lijst van productaanbevelingen voor uw klanten te produceren. Bij collectieve filtering is, in tegenstelling tot een op inhoud gebaseerde benadering, geen informatie over een specifiek product vereist, maar worden de historische voorkeuren van een klant voor een set producten gebruikt. Deze krachtige aanbeveling gebruikt twee eenvoudige veronderstellingen:

* Er zijn klanten met vergelijkbare belangen, en deze kunnen worden gegroepeerd door hun aankoop en het bladeren te vergelijken.
* Een klant is meer geïnteresseerd in een aanbeveling die is gebaseerd op soortgelijke klanten wat betreft hun aankoop- en browsergedrag.

Dit proces wordt opgesplitst in twee hoofdstappen. Eerst definieert u een subset van vergelijkbare klanten. Dan, binnen die reeks, identificeer gelijkaardige eigenschappen onder die klanten om een aanbeveling voor de doelklant terug te keren.
