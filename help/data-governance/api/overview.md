---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van API voor beleidsservice
topic: developer guide
translation-type: tm+mt
source-git-commit: cb3a17aa08c67c66101cbf3842bf306ebcca0305
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# [!DNL Policy Service] Handleiding voor API-ontwikkelaars

Met Adobe Experience Platform [!DNL Data Governance] kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen [!DNL Experience Platform] op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van het gegevensgebruik, en het controleren van het gebruik van gegevens voor marketing acties.

De [!DNL Policy Service] API biedt verschillende eindpunten waarmee u labels en beleidsregels voor gegevensgebruik programmatisch kunt beheren en marketingacties voor beleidsovertredingen kunt evalueren. Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar de [begonnen gids](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de API- [beleidsservice](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Labels

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in wordt opgenomen [!DNL Experience Platform], of zodra de gegevens voor gebruik in [!DNL Platform]. U kunt etiketten creëren, bekijken, uitgeven en schrappen gebruikend het `/labels` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, bezoek de gids [van het](./labels.md)etiketeindpunt.

## Marketingacties

Marketing-acties (ook wel marketinggebruiksgevallen genoemd) zijn in de context van het [!DNL Data Governance] kader acties die een [!DNL Experience Platform] gegevensconsument kan ondernemen en waarvoor uw organisatie het gebruik van gegevens wil beperken. Voor gedetailleerde informatie bij het werken met marketing acties, zie de gids [van het](./marketing-actions.md)marketing actiepunten.

## Beleid

Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, het uitvoeren op gegevens binnen wordt toegestaan [!DNL Experience Platform]. Een beleid wordt gedefinieerd door het volgende:

1. Een specifieke marketingactie
1. De labels voor gegevensgebruik waarvoor de handeling niet kan worden uitgevoerd

Leren hoe te om beleid in API te beheren, zie de gids van het [beleidseindpunt](./policies.md)

## Evaluatie

Zodra de etiketten van het gegevensgebruik op [!DNL Platform] datasets zijn toegepast, en het beleid van het gegevensgebruik voor marketing acties tegen die etiketten is bepaald, staat de mogelijkheden van het Beleid van Gegevens u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

De [!DNL Policy Service] API verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om te controleren of om het even welke beleidsschendingen voorkomen. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om op de juiste wijze de naleving van het gegevensgebruiksbeleid af te dwingen. Zie de gids [van de](./evaluation.md) evaluatieeindpunten voor meer informatie.

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Policy Service] API, lees de [begonnen gids](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken. Als u met labels en beleidsregels wilt werken met de [!DNL Experience Platform] gebruikersinterface, raadpleegt u respectievelijk de gebruikershandleiding [voor](../labels/user-guide.md) labels en de gebruikershandleiding voor [beleidsregels](../policies/user-guide.md).