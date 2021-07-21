---
keywords: Experience Platform;home;populaire onderwerpen;randsegmentatie;Segmentatie;Segmenteringsservice;segmenteringsservice;ui-hulplijn;streamingrand;
solution: Experience Platform
title: gebruikersgids voor Edge Segmentation
topic-legacy: ui guide
description: De segmentatie van de rand is de capaciteit om segmenten in Platform op de rand onmiddellijk te evalueren, toelatend de zelfde pagina en volgende de gebruikscituaties van de paginagrootte.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 8375d5a35ef652335c60b4b8b4571bf42ec1924a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Edge segmentation UI-handleiding (bèta)

>[!NOTE]
>
>Edge-segmentatie bevindt zich momenteel in bèta. De documentatie en de functionaliteit kunnen worden gewijzigd.

De segmentatie van de rand is de capaciteit om segmenten in Adobe Experience Platform onmiddellijk op de rand te evalueren, toelatend de zelfde pagina en volgende het verpersoonlijkingsgebruiksgevallen van de paginagrootte.

## Type Edge-segmenteringsquery

Een vraag kan met randsegmentatie worden geëvalueerd als het aan om het even welke volgende criteria voldoet:

| Type query | Details | Voorbeeld |
| ---------- | ------- | ------- |
| Binnenkomende hit | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| Binnenkomende hit die verwijst naar een profiel | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, zonder tijdbeperking, en een of meer profielkenmerken. | ![](../images/ui/edge-segmentation/profile-hit.png) |
| Frequentiequery | Elke segmentdefinitie die verwijst naar een gebeurtenis die minstens een bepaald aantal keer plaatsvindt. |  |
| Frequentiequery die naar een profiel verwijst | Elke segmentdefinitie die verwijst naar een gebeurtenis die minstens een bepaald aantal keren plaatsvindt en die een of meer profielkenmerken heeft. |  |

Als de vraag om het even welke bovengenoemde vraagtypes aanpast, zal het automatisch worden geëvalueerd gebruikend randsegmentatie.

De volgende vraagtypes zijn **not** momenteel gesteund voor randsegmentatie:

| Type query | Details |
| ---------- | ------- |
| Het venster Relative-time | Als een vraag naar een tijdvenster verwijst, kan het niet worden geëvalueerd gebruikend randsegmentatie. |
| Negatie | Als een vraag een negatie, of een `not` gebeurtenis bevat, kan het niet worden geëvalueerd gebruikend randsegmentatie. |
| Meerdere gebeurtenissen | Als een query meer dan één gebeurtenis bevat, kan deze niet worden geëvalueerd met behulp van randsegmentatie. |

## Volgende stappen

In deze gebruikershandleiding wordt uitgelegd hoe u segmenten met randsegmentatie op Adobe Experience Platform kunt evalueren.

Lees voor meer informatie over het gebruik van de Adobe Experience Platform-gebruikersinterface de [gebruikershandleiding voor segmentatie](./overview.md). Als u wilt leren hoe u vergelijkbare acties kunt uitvoeren en met segmenten kunt werken via de Adobe Experience Platform-gebruikersinterface, gaat u naar de [handleiding voor segmentatie van randen in de API](../api/edge-segmentation.md).
