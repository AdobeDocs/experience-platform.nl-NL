---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Handleiding voor ontwikkelaars van API voor beleidsservice
topic: developer guide
description: Leer hoe u de API voor beleidsservice gebruikt om labels en beleidsregels voor gegevensgebruik in Experience Platform te beheren.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# [!DNL Policy Service] Handleiding voor API-ontwikkelaars

Met Adobe Experience Platform [!DNL Data Governance] kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een belangrijke rol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, en het controleren van het gebruik van gegevens voor marketing acties.

De [!DNL Policy Service] API verstrekt verscheidene eindpunten die u toestaan om de etiketten en het beleid van het gegevensgebruik programmatically te beheren, evenals marketing acties voor beleidsschendingen te evalueren. Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [begonnen gids](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de API-wagen](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).[[!DNL Policy Service] 

## Labels

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken moedigen etiketteringsgegevens aan zodra het in [!DNL Experience Platform] wordt opgenomen, of zodra de gegevens voor gebruik in [!DNL Platform] beschikbaar worden. U kunt etiketten tot stand brengen, bekijken, uitgeven en schrappen gebruikend het `/labels` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, bezoek [etiketeindpuntgids](./labels.md).

## Marketingacties

Marketing-acties (ook wel marketinggebruiksgevallen genoemd) zijn in de context van het [!DNL Data Governance]-framework acties die een [!DNL Experience Platform]-gegevensconsument kan uitvoeren en waarvoor uw organisatie het gegevensgebruik wil beperken. Voor gedetailleerde informatie bij het werken met marketing acties, zie [marketing acties eindgids](./marketing-actions.md).

## Beleid

Beleid voor gegevensgebruik is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen [!DNL Experience Platform]. Een beleid wordt gedefinieerd door het volgende:

1. Een specifieke marketingactie
1. De labels voor gegevensgebruik waarvoor de handeling niet kan worden uitgevoerd

Om te leren hoe te om beleid in API te beheren, zie [beleidseindpuntgids](./policies.md)

## Evaluatie

Zodra de etiketten van het gegevensgebruik op [!DNL Platform] datasets zijn toegepast, en het beleid van het gegevensgebruik is bepaald voor marketing acties tegen die etiketten, staan de mogelijkheden van de Governance van Gegevens u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

De [!DNL Policy Service] API verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om te controleren als om het even welke beleidsschendingen voorkomen. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om op de juiste wijze de naleving van het gegevensgebruiksbeleid af te dwingen. Zie [de gids van de evaluatie eindpunten](./evaluation.md) voor meer informatie.

## Volgende stappen

Wanneer u begint met het maken van aanroepen met de [!DNL Policy Service]-API, leest u de [gids Aan de slag](./getting-started.md) en selecteert u vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken. Als u met labels en beleidsregels wilt werken met de interface [!DNL Experience Platform], raadpleegt u de [handleiding voor labelgebruikers](../labels/user-guide.md) en [Gebruiksgids voor beleidsregels](../policies/user-guide.md).