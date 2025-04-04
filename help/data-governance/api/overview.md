---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: API-handleiding voor beleidsservice
description: Met de Beleidsservice-API kunnen ontwikkelaars labels en beleidsregels voor gegevensgebruik in Experience Platform beheren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 3%

---

# [!DNL Policy Service] API-handleiding

Met Adobe Experience Platform Data Governance kunt u klantgegevens beheren en ervoor zorgen dat de regels, beperkingen en beleidsregels die van toepassing zijn op het gebruik van gegevens worden nageleefd. De klasse speelt binnen [!DNL Experience Platform] op verschillende niveaus een sleutelrol, zoals catalogisering, gegevenskoppeling, labels voor gegevensgebruik, beleid voor gegevensgebruik en het beheren van het gebruik van gegevens voor marketingacties.

De API van [!DNL Policy Service] biedt verschillende eindpunten waarmee u labels en beleidsregels voor gegevensgebruik programmatisch kunt beheren en marketingacties voor beleidsovertredingen kunt evalueren. Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [ begonnen gids ](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Om alle beschikbare eindpunten en verrichtingen te bekijken CRUD, bezoek de [[!DNL Policy Service]  API schakelaar ](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Labels

Pas de etiketten van het gegevensgebruik op schema&#39;s toe om datasets en gebieden volgens gebruiksbeleid te categoriseren die op die gegevens van toepassing zijn. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. Op basis van de aanbevolen procedures worden labelgegevens aangemoedigd zodra deze worden opgenomen in [!DNL Experience Platform] of zodra gegevens beschikbaar komen voor gebruik in [!DNL Experience Platform] . U kunt labels maken, weergeven, bewerken en verwijderen met behulp van het `/labels` -eindpunt. Leren hoe te om dit eindpunt te gebruiken, bezoek de [ gids van het etiketteneindpunt ](./labels.md).

## Marketingacties

Marketing-acties (ook wel marketinggebruiksgevallen genoemd) zijn in het kader van het gegevensbeheerkader acties die een [!DNL Experience Platform] gegevensconsument kan uitvoeren en waarvoor uw organisatie het gegevensgebruik wil beperken. Voor gedetailleerde informatie bij het werken met marketing acties, zie de [ gids van het marketing actiepunten ](./marketing-actions.md).

## Beleid

Beleid voor gegevensbeheer is regels die het soort marketingacties beschrijven dat u mag uitvoeren op gegevens binnen [!DNL Experience Platform] of waarvan u een beperking hebt ingesteld.

>[!NOTE]
>
>Beleid voor gegevensbeheer mag niet worden verward met beleid voor toegangsbeheer, dat de specifieke gegevenskenmerken bepaalt die toegankelijk zijn voor bepaalde Experience Platform-gebruikers in uw organisatie. Zie de gids op [ op attributen-gebaseerde toegangscontrole ](../../access-control/abac/overview.md) voor meer informatie.

Een beleid inzake gegevensbeheer wordt als volgt gedefinieerd:

1. Een specifieke marketingactie
1. De labels voor gegevensgebruik waarvoor de handeling niet kan worden uitgevoerd

Leren hoe te om beleid in API te beheren, zie de [ gids van het beleidseindpunt ](./policies.md)

## Evaluatie

Zodra de etiketten van het gegevensgebruik op de schema&#39;s van Experience Platform zijn toegepast, en het beleid van het gegevensgebruik voor marketing acties tegen die etiketten is bepaald, staat de mogelijkheden van het Beleid van Gegevens u toe om dat beleid te handhaven en gegevensverrichtingen te verhinderen die beleidsschendingen vormen.

De API van [!DNL Policy Service] verstrekt eindpunten die u toestaan om marketing acties tegen datasets of willekeurige combinaties etiketten van het gegevensgebruik te testen om als om het even welke beleidsschendingen te controleren. Op basis van de API-reactie kunt u vervolgens protocollen in uw ervaringstoepassing instellen om op de juiste wijze de naleving van het gegevensgebruiksbeleid af te dwingen. Zie de [ gids van de evaluatie eindpunten ](./evaluation.md) voor meer informatie.

## Volgende stappen

Begin makend vraag gebruikend [!DNL Policy Service] API, lees [ begonnen gids ](./getting-started.md) toen selecteren één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken. Om met etiketten en beleid te werken gebruikend [!DNL Experience Platform] UI, gelieve te verwijzen naar de [ gids van de etiketgebruiker ](../labels/user-guide.md) en [ gids van de beleidsgebruiker ](../policies/user-guide.md), respectievelijk.
