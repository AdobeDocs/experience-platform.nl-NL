---
keywords: Experience Platform;home;populaire onderwerpen;randsegmentatie;Segmentatie;Segmenteringsservice;segmenteringsservice;ui-hulplijn;streamingrand;
solution: Experience Platform
title: gebruikersgids voor Edge Segmentation
topic-legacy: ui guide
description: De segmentatie van de rand is de capaciteit om segmenten in Platform op de rand onmiddellijk te evalueren, toelatend de zelfde pagina en volgende de gebruikscituaties van de paginagrootte.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c89971668839555347e9b84c7c0a4ff54a394c1a
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Edge segmentation UI-handleiding (bèta)

>[!IMPORTANT]
>
>Edge-segmentatie bevindt zich momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

Randsegmentatie is de mogelijkheid om segmenten in Adobe Experience Platform ogenblikkelijk te evalueren [op de rand](../../edge/home.md)en de volgende pagina aanpassen.

## Type Edge-segmenteringsquery

Momenteel kunnen alleen bepaalde querytypen worden geëvalueerd met randsegmentatie. De volgende secties verstrekken een lijst van vraagtypes die met randsegmentatie en die kunnen worden geëvalueerd die momenteel niet worden gesteund.

### Ondersteunde querytypen

Een vraag kan met randsegmentatie worden geëvalueerd als het aan om het even welke criteria voldoet die in de volgende lijst worden geschetst.

>[!NOTE]
>
>Als de vraag om het even welke vraagtypes in de volgende lijst aanpast, zal het automatisch worden geëvalueerd gebruikend randsegmentatie. Het systeem bepaalt deze mogelijkheid automatisch gebaseerd op de vraaguitdrukking.

| Type query | Details | Voorbeeld |
| ---------- | ------- | ------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die een artikel aan hun winkelwagentje hebben toegevoegd. |
| Eén gebeurtenis die naar een profiel verwijst | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die in de VS wonen en die de homepage hebben bezocht. |
| Een enkele gebeurtenis met een profielkenmerk negeren | Elke segmentdefinitie die verwijst naar een negatiefunctie van één binnenkomende gebeurtenis en een of meer profielkenmerken | Mensen die in de VS wonen en **niet** heeft de homepage bezocht. |
| Eén gebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen 24 uur. | Mensen die de laatste 24 uur de homepage hebben bezocht. |
| Een enkele gebeurtenis met een profielkenmerk in een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde enkele binnenkomende gebeurtenis binnen 24 uur. | Mensen die in de VS wonen en de laatste 24 uur de homepage hebben bezocht. |
| Eén gebeurtenis die binnen een tijdvenster van 24 uur is genegeerd met een profielkenmerk | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde enkele binnenkomende gebeurtenis binnen 24 uur. | Mensen die in de VS wonen en **niet** heeft de laatste 24 uur de homepage bezocht. |
| Frequentiegebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een gebeurtenis die een bepaald aantal keren binnen een tijdvenster van 24 uur plaatsvindt. | Personen die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. |
| Frequentiegebeurtenis met een profielkenmerk binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen uit de VS die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. |
| Gebeurtenis met een verwaarloosde frequentie met een profiel binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen die de homepage niet hebben bezocht **meer** meer dan vijf keer in de laatste 24 uur. |
| Meerdere inkomende treffers binnen een tijdprofiel van 24 uur | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen die de homepage hebben bezocht **of** heeft de laatste 24 uur de afhandelingspagina bezocht. |
| Meerdere gebeurtenissen met een profiel binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen uit de VS die de homepage hebben bezocht **en** heeft de laatste 24 uur de afhandelingspagina bezocht. |

## Volgende stappen

In deze handleiding wordt uitgelegd hoe u segmenten met randsegmentatie op Adobe Experience Platform kunt evalueren. Voor meer informatie over het gebruik van de gebruikersinterface van het Experience Platform leest u de [Gebruikershandleiding voor segmentatie](./overview.md). Ga voor meer informatie over het uitvoeren van vergelijkbare acties en het werken met segmenten met Experience Platform-API&#39;s naar de [hulplijn voor Edge-segmentatie-API](../api/edge-segmentation.md).
