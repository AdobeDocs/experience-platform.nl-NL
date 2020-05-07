---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Real-time Machine Learning-overzicht
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Real-time Machine Learning-overzicht

>[!IMPORTANT]
>Het leren van de machine in real time is niet beschikbaar aan alle gebruikers nog. Deze functie bevindt zich in alfa en wordt nog steeds getest. Dit document kan worden gewijzigd.

Met het Real-Time Machine Learning-framework van het Adobe Experience Platform kunt u computerleren gebruiken om de juiste eindgebruikers op het juiste moment op het juiste moment de juiste ervaring te bieden, op het juiste kanaal en met een tweede tijdsperiode.

## Voordelen

Het leren van machines in real time kan de relevantie van uw digitale ervaringsinhoud voor uw eindgebruikers drastisch verbeteren. Dit wordt mogelijk gemaakt door real-time conferenties en voortdurend leren op de Experience Edge te gebruiken.

Een combinatie naadloze berekening op zowel de Hub als de Rand vermindert dramatisch de latentie die traditioneel betrokken bij het aandrijven van hyper-gepersonaliseerde ervaringen is die zowel relevant als ontvankelijk zijn. Vandaar, het Leren van de machine in real time verstrekt conclusies met ongelooflijk lage latentie voor synchrone besluitvorming. Voorbeelden zijn het renderen van gepersonaliseerde webpagina-inhoud of het surfen op een aanbieding of korting om de kans op fouten te verkleinen en conversies in een webwinkel te verhogen.

## Real-time Machine Learning-architectuur

Het volgende diagram verstrekt een overzicht voor de het Leren architectuur van de machine in real time.

![Vereenvoudigd overzicht](../images/rtml/simple-overview.png)

## Werkstroom voor het leren van machines in realtime (alfa)

In de volgende workflow worden de typische stappen en resultaten beschreven die zijn betrokken bij het maken en gebruiken van een Real-Time Machine Learning-model.

### Inname van gegevens en preparaten

Gegevens worden opgenomen en getransformeerd met het XDM (Experience Data Model) op het Adobe Experience Platform. Deze gegevens worden gebruikt voor modeltraining. Meer informatie over XDM vindt u in het [XDM-overzicht](../../xdm/home.md).

### Authoring

Maak een real-time model voor het leren van machines door deze helemaal zelf te ontwerpen of in te voeren als een vooraf geserialiseerd ONNX-model in Jupyter-laptops van het Adobe Experience Platform.

### Implementatie

Stel uw model aan de Rand van de Ervaring op om een Echte - tijdSysteem het Leren dienst in de Galerij van de Dienst tot stand te brengen gebruikend het Voorspelling API eindpunt.

### Opkomst

Met het voorspellingsREST API-eindpunt kunt u inzichten van machines in real-time genereren.

### Aflevering

Marketers kunnen vervolgens segmenten en regels definiëren die de leerscores voor machines in realtime toewijzen aan ervaringen met Adobe Target. Op deze manier kunnen bezoekers van de website van uw merk in real-time (minder dan 100 ms) dezelfde of hyperpersoonlijke ervaring van de volgende pagina zien.

## Ontwikkelingsplan

Het leren van de machine in real time is momenteel in de Alpha- fase. In de onderstaande tabel staan enkele functies en updates die naar verwachting in de toekomstige bètaherhaling beschikbaar zullen zijn.

<table>
    <th></th>
    <th>Alfa (mei)</th>
    <th>Beta</th>
    <tr>
        <td>
            <strong>Functies</strong>
        </td>
        <td>
            <li>De Werkruimte van de Wetenschap van gegevens brengt uw eigen Model en auteur via de integratie van de Ontvanger van het Notitieboekje.</li>
            <li>Starterset van ontwerperatoren.</li>
            <li>Distribueren naar hub</li>
            <li>Scikit Learn based Models.</li>
        </td>
        <td>
            <li>Integratie van de gebruikersinterface van de Data Science Workspace Service Gallery.</li>
            <li>Automatisch verrijken van Real-time Klantprofiel met resultaten van de gevolgtrekking.</li>
            <li>Diepe leermodellen.</li>
            <li>Uitgebreide set ontwerpers, inclusief aangepaste operatoren.</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Beschikbaarheid</strong>
        </td>
        <td>
            Noord-Amerika
        </td>
        <td>
            <li>Noord-Amerika</li>
            <li>Europa en het Midden-Oosten (EMEA)</li>
            <li>Azië-Stille Oceaan (APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Authoring</strong>
        </td>
        <td>
            <li>Python-ondersteuning</li>
            <li>Real-time Machine Learning SDK</li>
            <li>Python-ontwerpknooppunten: Pandas, ScikitLearn, ONNXNode, Split, ModelUpload, OneHotEncoder.</li>
        </td>
        <td>
            <li>Tensorflow-ondersteuning.</li>
            <li>Aanvullende Python-ontwerpknooppunten: Klantprofiellezer in realtime, realtime schrijver van klantprofiel, noomarrays, XDM2Frame, Frame2XDM. </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Runtime van scores</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## Volgende stappen

U kunt beginnen met het volgen van de gids Aan de [slag](./getting-started.md) . Deze gids begeleidt u door vestiging alle vereiste eerste vereisten voor het creëren van een In real time het Leren van de Machine model.

