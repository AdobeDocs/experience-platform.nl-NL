---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Invoer en uitvoer van AI van de klant
topic: Getting started
translation-type: tm+mt
source-git-commit: 5cab341138e809bae79623bb65e499ac6b955f27
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---


# Invoer en uitvoer van AI van de klant

In het volgende document worden de verschillende invoer- en uitvoerbestanden beschreven die in de AI van de Klant worden gebruikt.

## Invoergegevens van AI van de klant

AI van de Klant gebruikt de gegevens van de Gebeurtenis van de Ervaring van de Consumenten om volheidsscores te berekenen. Voor meer informatie over de gebeurtenis Consumer Experience raadpleegt u de [Voorbereidende gegevens voor gebruik in de documentatie](../data-preparation.md)Intelligent Services.

### Historische gegevens

Klanten-AI hebben historische gegevens nodig voor modeltraining, maar de hoeveelheid vereiste gegevens is gebaseerd op twee sleutelelementen: resultaatvenster en in aanmerking komende populatie.

Standaard zoekt de AI van de Klant naar een gebruiker die activiteit heeft gehad in de laatste 120 dagen als er tijdens de toepassingsconfiguratie geen definitie van de in aanmerking komende populatie is opgegeven. Naast de vereiste minimale hoeveelheid gegevens van de Consumer Experience Event, heeft de AI van de Klant ook een minimale hoeveelheid succesgebeurtenissen nodig op basis van een voorspelde doeldefinitie. Momenteel heeft de AI van de Klant minimaal 500 succesgebeurtenissen nodig.

In de volgende voorbeelden wordt een eenvoudige formule gebruikt om u te helpen de minimale vereiste hoeveelheid gegevens te bepalen. Als u meer dan de minimumvereiste hebt, zal uw model waarschijnlijk nauwkeurigere resultaten verstrekken. Als u minder dan het vereiste minimumbedrag hebt, zal het model ontbreken aangezien er geen voldoende hoeveelheid gegevens voor modelopleiding is.

**Formule**:

Minimumlengte van de vereiste gegevens = subsidiabele populatie + resultaatvenster

>[!NOTE]
> 30 is het minimumaantal dagen dat vereist is voor de in aanmerking komende bevolking. Als dit niet wordt verstrekt is het gebrek 120 dagen.

Voorbeelden :

- U wilt voorspellen of een klant waarschijnlijk een horloge in de komende 30 dagen zal kopen. U wilt ook gebruikers scoren die de afgelopen 60 dagen enige internetactiviteit hebben gehad. In dat geval is de minimumlengte van de vereiste gegevens 60 dagen + 30 dagen. De in aanmerking komende populatie is 60 dagen en het resultaatvenster is 30 dagen in totaal 90 dagen.

- U wilt voorspellen of de gebruiker waarschijnlijk de komende 7 dagen een horloge zal kopen. In dat geval is de minimumlengte van de vereiste gegevens 120 dagen + 7 dagen. De in aanmerking komende populatie staat standaard op 120 dagen en het resultaatvenster is 7 dagen in totaal 127 dagen.

- U wilt voorspellen of de klant waarschijnlijk de komende 7 dagen een horloge zal kopen. U wilt ook gebruikers scoren die de afgelopen 7 dagen enige internetactiviteit hebben gehad. In dat geval is de minimumlengte van de vereiste gegevens 30 dagen + 7 dagen. De in aanmerking komende populatie duurt minimaal 30 dagen en de resultaatperiode bedraagt 7 dagen in totaal 37 dagen.

Naast de minimaal vereiste gegevens, werkt de AI van de Klant ook het best met recente gegevens. In dit geval doet de AI van de Klant een prognose voor de toekomst op basis van recente gedragsgegevens van een gebruiker. Met andere woorden, recentere gegevens zullen waarschijnlijk een nauwkeurigere voorspelling opleveren.

## AI-uitvoergegevens van klant

De AI van de Klant produceert verscheidene attributen voor individuele profielen die als verkiesbaar worden beschouwd. Er zijn twee manieren om de score te verbruiken op basis van wat u hebt voorzien. Als u het Profiel van de Klant in real time voor uw dataset wordt toegelaten, kunt u het via het Profiel van de Klant in real time verbruiken. Als u geen Real-Time Klantprofiel hebt, kunt u de de outputdataset downloaden van de Klant AI beschikbaar op het gegevenspop.

>[!NOTE]
>De waarden van de output worden verbruikt door het Profiel van de Klant in real time dat kan worden gebruikt om segmenten tot stand te brengen en te bepalen.

In de onderstaande tabel worden de verschillende kenmerken beschreven die in de uitvoer van AI van de Klant zijn aangetroffen:

| Kenmerk | Beschrijving |
| ----- | ----------- |
| Score | De relatieve waarschijnlijkheid voor een klant om het voorspelde doel binnen het bepaalde tijdkader te bereiken. Deze waarde moet niet worden beschouwd als een waarschijnlijkheidspercentage, maar veeleer als de waarschijnlijkheid dat een individu vergeleken wordt met de totale populatie. Deze score varieert van 0 tot 100. |
| Waarschijnlijkheid | Deze eigenschap is de ware waarschijnlijkheid van een profiel voor het bereiken van het voorspelde doel binnen het bepaalde tijdkader. Bij het vergelijken van outputs over verschillende doelstellingen, wordt geadviseerd dat u waarschijnlijkheid over percentiel of score overweegt. Bij het bepalen van de gemiddelde waarschijnlijkheid in de in aanmerking komende populatie moet altijd rekening worden gehouden met de waarschijnlijkheid, aangezien de waarschijnlijkheid aan de onderkant ligt voor gebeurtenissen die niet vaak voorkomen. Waarden voor de waarschijnlijkheid liggen tussen 0 en 1. |
| Percentage | Deze waarde biedt informatie over de prestaties van een profiel ten opzichte van andere profielen met een vergelijkbare score. Een profiel met een percentielrang van 99 voor churn geeft bijvoorbeeld aan dat het risico op churning groter is dan 99% van alle andere profielen die zijn gescaureerd. De percentages variëren van 1 tot 100. |
| Type volheid | Het geselecteerde type buigzaamheid. |
| Score-datum | De datum waarop de scoring heeft plaatsgevonden. |
| Influentiële factoren | Voorspelde redenen waarom een profiel waarschijnlijk wordt omgezet of afgekapt. Factoren bestaan uit de volgende kenmerken:<ul><li>Code: Het profiel of gedragskenmerk dat de voorspelde score van een profiel positief beïnvloedt. </li><li>Waarde: De waarde van het profiel of gedragskenmerk.</li><li>Belangrijk: Hiermee wordt het gewicht van het profiel of gedragskenmerk op de voorspelde score aangegeven (laag, gemiddeld, hoog)</li></ul> |

## Volgende stappen {#next-steps}

Zodra u uw gegevens hebt voorbereid en al uw geloofsbrieven en schema&#39;s op zijn plaats hebt, begin door de [Configure een gids van de Instantie](./user-guide/configure.md) van de Klant te volgen. Deze gids begeleidt u door het creëren van een geval voor Klant AI.