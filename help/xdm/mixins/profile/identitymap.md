---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: IdentityMap-mixin
topic: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


#  IdentityMapmixin

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../name-updates.md) voor meer informatie.

 IdentityMapis een standaardmix voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De mix biedt één kaartveld dat een set gebruikersidentiteiten bevat die door naamruimte worden vastgehouden.

>[!WARNING]
>
>Het veld `IdentityMap` wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. Als u dit veld correct wilt gebruiken voor [Real-time klantprofiel](../../../profile/home.md), moet u niet handmatig de inhoud van het veld bijwerken in uw gegevensbewerkingen.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Zie de sectie over identiteitskaarten in de [grondbeginselen van schemacompositie](../../schema/composition.md#identityMap) voor meer informatie over hun gebruiksgeval.