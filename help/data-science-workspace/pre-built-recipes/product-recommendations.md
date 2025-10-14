---
keywords: Experience Platform;product aanbeveling recept;Data Science Workspace;populaire onderwerpen;recepten;pre-build recipe
solution: Experience Platform
title: Recipe productaanbeveling
description: Met het product Recommendations-recept kun je gepersonaliseerde productaanbevelingen bieden die zijn afgestemd op de behoeften en interesses van je klant. Met een accuraat voorspellingsmodel kan de aankoopgeschiedenis van een klant u inzicht verschaffen in welke producten zij geïnteresseerd kunnen zijn.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
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

Met het product Recommendations-recept kunt u op maat gemaakte productaanbevelingen doen die zijn afgestemd op de behoeften en belangen van uw klant. Met een accuraat voorspellingsmodel kan de aankoopgeschiedenis van een klant u inzicht verschaffen in welke producten zij geïnteresseerd kunnen zijn.

## Voor wie is dit recept gebouwd?

In de moderne tijd kan een detailhandelaar een groot aantal producten aanbieden, waardoor zijn klanten een heleboel keuzemogelijkheden hebben die ook het zoeken van klanten kunnen belemmeren. Vanwege tijd- en inspanningsbeperkingen kunnen klanten het product dat ze willen niet vinden, wat leidt tot aankopen met een hoog cognitieve dissonantie of helemaal geen aankoop.

## Wat doet dit recept?

Het Product Recommendations-recept maakt gebruik van machine learning om de interacties van klanten met producten in het verleden te analyseren en snel en moeiteloos een gepersonaliseerde lijst met productaanbevelingen te genereren. Zo optimaliseert u het proces voor productontdekking en voorkomt u lange, onproductieve, irrelevante zoekopdrachten voor uw klanten. Als gevolg hiervan kan het Product Recommendations-recept de algehele aanschafervaring van een klant verbeteren, wat leidt tot meer betrokkenheid en een sterkere merkloyaliteit.

## Hoe begin ik?

U kunt aan de slag door de zelfstudie van Adobe Experience Platform Lab te volgen (zie de verbinding van het Laboratorium hieronder). Dit leerprogramma zal u tonen hoe te om het recept van Recommendations van het Product in een Notitieboekje van de Jupyter tot stand te brengen door [&#x200B; notitieboekje aan recept &#x200B;](../jupyterlab/create-a-model.md) werkschema te volgen, en het recept in [!DNL Experience Platform] uit te voeren [!DNL Data Science Workspace].

* [&#x200B; Laboratorium: Verwacht de Toekomst met de Wetenschap van Gegevens Workspace &#x200B;](https://expleague.azureedge.net/labs/L777/index.html)
* [&#x200B; middelen van het Laboratorium &#x200B;](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Gegevensschema

Dit recept gebruikt douane [&#x200B; XDM schema&#39;s &#x200B;](../../xdm/schema/field-dictionary.md) om de input en outputgegevens te modelleren:

### Invoergegevensschema

| Veldnaam | Type |
| --- | --- |
| itemId | Tekenreeks |
| interactionType | String |
| tijdstempel | String |
| userId | Tekenreeks |

### Uitvoergegevensschema

| Veldnaam | Type |
| --- | --- |
| aanbevelingen | Tekenreeks |
| userId | Geheel |

## Algorithm

Het product Recommendations-recept maakt gebruik van collectieve filtering om een gepersonaliseerde lijst met productaanbevelingen voor uw klanten te genereren. Bij collectieve filtering is, in tegenstelling tot een op inhoud gebaseerde benadering, geen informatie over een specifiek product vereist, maar worden de historische voorkeuren van een klant voor een set producten gebruikt. Deze krachtige aanbeveling gebruikt twee eenvoudige veronderstellingen:
* Er zijn klanten met vergelijkbare interesses, en deze kunnen worden gegroepeerd door hun aankoop- en browsergedrag te vergelijken.
* Een klant is eerder geïnteresseerd in een aanbeveling op basis van soortgelijke klanten in termen van aankoop- en browsergedrag.

Dit proces is onderverdeeld in twee hoofdstappen. Definieer eerst een subset van vergelijkbare klanten. Vervolgens identificeert u binnen die set vergelijkbare functies onder die klanten om een aanbeveling voor de doelklant te retourneren.
