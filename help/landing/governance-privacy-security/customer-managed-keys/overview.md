---
title: Door de klant beheerde toetsen in Adobe Experience Platform
description: Leer hoe u uw eigen coderingssleutels instelt voor gegevens die in Adobe Experience Platform zijn opgeslagen.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Door de klant beheerde sleutels in Adobe Experience Platform

Gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die bovenop Platform wordt gebouwd, kunt u verkiezen om uw eigen encryptiesleutels in plaats daarvan te gebruiken, die u grotere controle over uw gegevensveiligheid geven.

>[!NOTE]
>
>Klantprofielgegevens die zijn opgeslagen in het profielarchief van Platform [!DNL Azure Data Lake] en [!DNL Azure Cosmos DB] , worden uitsluitend gecodeerd met CMK, nadat ze zijn ingeschakeld. De zeer belangrijke herroeping in uw primaire gegevensopslag kan overal van **een paar notulen aan 24 uren** nemen, en kan langer duren, **tot 7 dagen** voor transient of secundaire gegevensopslag. Voor extra details, verwijs naar de [ implicaties van het intrekken van zeer belangrijke toegangssectie ](#revoke-access).

Dit document biedt een overzicht op hoog niveau van het proces voor het inschakelen van de CMK-functie (Customer-managed keys) in Platform, en de vereiste informatie die nodig is om deze stappen te voltooien.

>[!NOTE]
>
>Voor de klanten van de Customer Journey Analytics, te volgen gelieve de instructies in de [ documentatie van de Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html).

## Vereisten

Als u de sectie [!UICONTROL Encryption] in Adobe Experience Platform wilt weergeven en bezoeken, moet u een rol hebben gemaakt en [!UICONTROL Manage Customer Managed Key] toestemming aan die rol hebben toegewezen. Elke gebruiker met de machtiging [!UICONTROL Manage Customer Managed Key] kan CMK inschakelen voor zijn of haar organisatie.

Voor meer informatie bij het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [ vormen toestemmingendocumentatie ](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Als u CMK wilt inschakelen, moet de [!DNL Azure] Key Vault zijn geconfigureerd met de volgende instellingen:

* [ laat purgebescherming ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection) toe
* [ laat zachte schrapping ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) toe
* [ vorm toegang gebruikend  [!DNL Azure]  op rol-gebaseerde toegangscontrole ](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Lees de gekoppelde documentatie om het proces beter te begrijpen.

## Procesoverzicht {#process-summary}

CMK is opgenomen in het gezondheidsschild en het aanbod van privacy en beveiligingsschild van Adobe. Nadat uw organisatie een licentie voor een van deze aanbiedingen heeft aangeschaft, kunt u een eenmalig proces starten om de functie in te stellen.

>[!WARNING]
>
>Nadat u CMK hebt ingesteld, kunt u niet terugkeren naar de toetsen die door het systeem worden beheerd. U bent verantwoordelijk voor het veilig beheren van uw sleutels en het bieden van toegang tot uw Key Vault-, Key- en CMK-app binnen [!DNL Azure] om te voorkomen dat u toegang tot uw gegevens verliest.

Het proces is als volgt:

1. [ vorm een  [!DNL Azure]  Zeer belangrijke die vault ](./azure-key-vault-config.md) op het beleid van uw organisatie wordt gebaseerd, dan [ produceert een encryptiesleutel ](./azure-key-vault-config.md#generate-a-key) die uiteindelijk met Adobe zal worden gedeeld.
1. Opstelling CMK app met uw [!DNL Azure] huurder door of [ API vraag ](./api-set-up.md#register-app) of [ UI ](./ui-set-up.md#register-app).
1. Verzend uw encryptie zeer belangrijke identiteitskaart aan Adobe en begin het enablement proces voor de eigenschap of [ in UI ](./ui-set-up.md#send-to-adobe) of met een [ API vraag ](./api-set-up.md#send-to-adobe).
1. Controleer de status van de configuratie om te verifiëren of CMK of [ in UI ](./ui-set-up.md#check-status) of met een [ API vraag ](./api-set-up.md#check-status) is toegelaten.

Zodra het installatieproces is voltooid, worden alle gegevens die in het platform worden ingevoerd voor alle sandboxen versleuteld met behulp van de toetsencombinatie [!DNL Azure] . Om CMK te gebruiken, zult u hefboomwerking [!DNL Microsoft Azure] functionaliteit die deel van hun [ openbaar voorproefprogramma ](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/) kan uitmaken.

## Gevolgen van het intrekken van toetstoegang {#revoke-access}

Het intrekken of uitschakelen van de toegang tot de Key Vault-, Key- of CMK-toepassing kan leiden tot aanzienlijke onderbrekingen, zoals het doorbreken van wijzigingen in de activiteiten van uw platform. Zodra deze sleutels worden onbruikbaar gemaakt, kunnen de gegevens in Platform ontoegankelijk worden, en om het even welke stroomafwaartse verrichtingen die op deze gegevens baseren zullen ophouden te functioneren. Het is van cruciaal belang dat u de downstreameffecten volledig begrijpt voordat u wijzigingen aanbrengt in uw sleutelconfiguraties.

Als u besluit om de toegang van het Platform tot uw gegevens in te trekken, kunt u dit doen door de gebruikersrol verbonden aan de toepassing uit de Key Vault binnen [!DNL Azure] te verwijderen.

### Tijdlijnen voor doorgave {#propagation-timelines}

Nadat de toetstoegang is ingetrokken vanuit de [!DNL Azure] Key Vault, worden de wijzigingen als volgt doorgegeven:

| **Type van opslag** | **Beschrijving** | **Tijdlijn** |
|---|---|---|
| Primaire gegevensopslag | Deze winkels zijn onder andere Azure Data Lake en Azure Cosmos DB Profile stores. Zodra toetstoegang wordt ingetrokken, worden de gegevens ontoegankelijk. | A **enkele notulen aan 24 uren**. |
| Gegevensopslag in cache/transient | Omvat gegevensopslag die voor prestaties en kerntoepassingsfunctionaliteit wordt gebruikt. De gevolgen van een belangrijke intrekking worden vertraagd. | **tot 7 dagen**. |

Het dashboard Profiel zal bijvoorbeeld gegevens van zijn geheime voorgeheugen blijven tonen tot zeven dagen alvorens de gegevens verlopen en worden verfrist. Op dezelfde manier duurt het opnieuw inschakelen van toegang tot de toepassing even lang om de beschikbaarheid van gegevens in deze opslagruimten te herstellen.

>[!NOTE]
>
>Er zijn twee gebruik-geval-specifieke uitzonderingen op de zeven dagen datasetvervaldatum op niet primaire (caching/transient) gegevens. Raadpleeg de documentatie bij deze pagina voor meer informatie over deze functies.<ul><li>[ Adobe Journey Optimizer URL Shortener ](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[ de Projecties van Edge ](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Volgende stappen

Om met het proces te beginnen, begin door [ het vormen van een  [!DNL Azure]  Zeer belangrijke Vult ](./azure-key-vault-config.md) en [ produceren een encryptiesleutel ](./azure-key-vault-config.md#generate-a-key) om met Adobe te delen.
