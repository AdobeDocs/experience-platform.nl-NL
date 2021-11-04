---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: API-handleiding voor beleidsservice
topic-legacy: developer guide
description: Met de Beleidsservice-API kunnen ontwikkelaars labels en beleidsregels voor gegevensgebruik in Experience Platform beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# [!DNL Policy Service] API-handleiding

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik worden nageleefd. Het speelt een sleutelrol binnen [!DNL Experience Platform] op verschillende niveaus, waaronder catalogisering, gegevenskoppeling, etikettering van het gegevensgebruik, beleid inzake gegevensgebruik en controle op het gebruik van gegevens voor marketingacties.

De [!DNL Policy Service] API biedt verschillende eindpunten waarmee u labels en beleidsregels voor gegevensgebruik programmatisch kunt beheren en marketingacties voor beleidsovertredingen kunt evalueren. Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de [[!DNL Policy Service] API-wagen](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Labels

Met labels voor gegevensgebruik kunt u gegevenssets en velden categoriseren op basis van het gebruiksbeleid dat op die gegevens van toepassing is. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het wordt opgenomen in [!DNL Experience Platform]of zodra gegevens beschikbaar zijn voor gebruik in [!DNL Platform]. U kunt labels maken, weergeven, bewerken en verwijderen met de opdracht `/labels` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, bezoek [eindhulplijn voor labels](./labels.md).

## Marketingacties

Handelingen voor het in de handel brengen (ook wel marketinggevallen genoemd) zijn in het kader van het gegevensbeheerkader acties die een [!DNL Experience Platform] gegevens kan de consument nemen, waarvoor uw organisatie gegevensgebruik wil beperken. Voor gedetailleerde informatie over het werken met marketingacties raadpleegt u de [eindgids voor marketingacties](./marketing-actions.md).

## Beleid

Het beleid van het gebruik van gegevens is regels die de soorten marketing acties beschrijven die u aan, of beperkt van, op gegevens binnen mag uitvoeren [!DNL Experience Platform]. Een beleid wordt gedefinieerd door het volgende:

1. Een specifieke marketingactie
1. De labels voor gegevensgebruik waarvoor de handeling niet kan worden uitgevoerd

Zie voor meer informatie over het beheren van beleid in de API [leidraad voor beleidseindpunten](./policies.md)

## Evaluatie

Nadat labels voor gegevensgebruik zijn toegepast op [!DNL Platform] De datasets, en het beleid van het gegevensgebruik zijn bepaald voor marketing acties tegen die etiketten, de mogelijkheden van het Beleid van Gegevens staan u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

De [!DNL Policy Service] API verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om te controleren als om het even welke beleidsschendingen voorkomen. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om op de juiste wijze de naleving van het gegevensgebruiksbeleid af te dwingen. Zie de [eindpuntgids voor evaluatie](./evaluation.md) voor meer informatie .

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Policy Service] API, lees de [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken. Als u met labels en beleidsregels wilt werken, gebruikt u de opdracht [!DNL Experience Platform] UI, gelieve te verwijzen naar [gebruikershandleiding voor labels](../labels/user-guide.md) en [beleidsgebruikershandleiding](../policies/user-guide.md), respectievelijk.
