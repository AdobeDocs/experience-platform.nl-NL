---
title: Door klanten beheerde toetsen in Adobe Experience Platform
description: Leer hoe u uw eigen coderingssleutels instelt voor gegevens die in Adobe Experience Platform zijn opgeslagen.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---

# Door klanten beheerde toetsen in Adobe Experience Platform

Gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die op Experience Platform is gebouwd, kunt u ervoor kiezen om uw eigen coderingssleutels te gebruiken, zodat u meer controle hebt over de gegevensbeveiliging.

>[!AVAILABILITY]
>
>Adobe Experience Platform ondersteunt Customer Managed Keys (CMK) voor zowel Microsoft Azure als Amazon Web Services (AWS). Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Als uw implementatie op AWS wordt uitgevoerd, kunt u de Key Management Service (KMS) voor Experience Platform-gegevenscodering gebruiken. Voor meer informatie over de gesteunde infrastructuur, zie het [&#x200B; multi-wolkenoverzicht van Experience Platform &#x200B;](https://experienceleague.adobe.com/nl/docs/experience-platform/landing/multi-cloud).
>
>Om over encryptie zeer belangrijke verwezenlijking en beheer in AWS KMS te leren, verwijs naar de [&#x200B; handleiding van de gegevensencryptie van AWS KMS &#x200B;](./aws/configure-kms.md). Voor Azure implementaties, zie de [&#x200B; Azure Zeer belangrijke de configuratiegids van de Vault &#x200B;](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>Voor [!DNL Azure] gehoste Experience Platform-instanties worden de gegevens van het klantprofiel die zijn opgeslagen in Experience Platform [!DNL Azure Data Lake] en het [!DNL Azure Cosmos DB] Profile store, uitsluitend gecodeerd met CMK als deze eenmaal is ingeschakeld. De zeer belangrijke herroeping in primaire gegevensopslag kan overal van **een paar notulen aan 24 uren** en **tot 7 dagen** voor transient of secundaire gegevensopslag nemen. Voor extra details, verwijs naar de [&#x200B; implicaties van het intrekken van zeer belangrijke toegangssectie &#x200B;](#revoke-access).

Dit document biedt een uitgebreid overzicht van het proces voor het inschakelen van de CMK-functie (Customer Managed Keys) in Experience Platform in [!DNL Azure] en AWS, samen met de vereiste informatie die vereist is om deze stappen te voltooien.

>[!NOTE]
>
>Voor klanten van Customer Journey Analytics, te volgen gelieve de instructies in de [&#x200B; documentatie van Customer Journey Analytics &#x200B;](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=nl-NL).

## Vereisten

Om CMK in te schakelen, moet de hostingomgeving van uw platform ([!DNL Azure] of AWS) voldoen aan specifieke configuratievereisten:

### Algemene voorwaarden

Als u de sectie [!UICONTROL Encryption] in Adobe Experience Platform wilt weergeven en openen, moet u een rol hebben gemaakt en de machtiging [!UICONTROL Manage Customer Managed Key] aan die rol hebben toegewezen.  Elke gebruiker met de machtiging [!UICONTROL Manage Customer Managed Key] kan CMK inschakelen voor zijn of haar organisatie.

Voor meer informatie bij het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [&#x200B; vormen toestemmingendocumentatie &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=nl-NL).

### Azure-specifieke voorwaarden

Voor Azure-gehoste implementaties configureert u de [!DNL Azure] Key Vault met de volgende instellingen:

- [&#x200B; laat purgebescherming &#x200B;](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection) toe
- [&#x200B; laat zachte schrapping &#x200B;](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) toe
- [&#x200B; vorm toegang gebruikend  [!DNL Azure]  op rol-gebaseerde toegangscontrole &#x200B;](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### AWS-specifieke voorwaarden

Voor AWS-gehoste implementaties configureert u de AWS-omgeving als volgt:

- Controleer of u rechten hebt om coderingssleutels te beheren met behulp van AWS Identity and Access Management (IAM). Voor details, zie het [&#x200B; IAM Beleid voor AWS KMS &#x200B;](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Stel AWS KMS in met ondersteuning voor CMK. Verwijs naar de [&#x200B; gids van de de gegevensencryptie van AWS KMS &#x200B;](./aws/configure-kms.md).

## Procesoverzicht {#process-summary}

CMK (Customer Managed Keys) is beschikbaar via het aanbod van het Adobe Healthcare Shield and Privacy and Security Shield. In Azure wordt CMK ondersteund voor zowel Healthcare Shield als Privacy en Security Shield. In AWS wordt CMK alleen ondersteund voor Privacy en Security Shield en is CMK niet beschikbaar voor Healthcare Shield. Nadat uw organisatie een licentie voor een van deze aanbiedingen heeft aangeschaft, kunt u het eenmalige installatieproces starten om CMK in te schakelen.

>[!WARNING]
>
>Nadat u CMK hebt ingesteld, kunt u niet terugkeren naar de toetsen die door het systeem worden beheerd. U bent verantwoordelijk voor het veilig beheren van uw sleutels om te voorkomen dat de toegang tot uw gegevens verloren gaat.

Het proces is als volgt:

### Voor Azure {#azure-process-summary}

1. [&#x200B; vorm een  [!DNL Azure]  Zeer belangrijke die vault &#x200B;](./azure/azure-key-vault-config.md) op het beleid van uw organisatie wordt gebaseerd, dan [&#x200B; produceert een encryptiesleutel &#x200B;](./azure/azure-key-vault-config.md#generate-a-key) met Adobe te delen.
1. Opstelling CMK app met uw [!DNL Azure] huurder door of [&#x200B; API vraag &#x200B;](./azure/api-set-up.md#register-app) of [&#x200B; UI &#x200B;](./azure/ui-set-up.md#register-app).
1. Verzend uw encryptie zeer belangrijke identiteitskaart naar Adobe en begin het enablement proces voor de eigenschap, of [&#x200B; in UI &#x200B;](./azure/ui-set-up.md#send-to-adobe) of met een [&#x200B; API vraag &#x200B;](./azure/api-set-up.md#send-to-adobe).
1. Controleer de status van de configuratie om te verifiëren of CMK, of [&#x200B; in UI &#x200B;](./azure/ui-set-up.md#check-status) of met een [&#x200B; API vraag &#x200B;](./azure/api-set-up.md#check-status) is toegelaten.

Zodra het installatieproces is voltooid voor Experience Platform-instanties die in Azure worden gehost, worden alle gegevens die in Experience Platform in alle sandboxen worden ingevoerd, gecodeerd met de toetsencombinatie [!DNL Azure] . Om CMK te gebruiken, zult u hefboomwerking [!DNL Microsoft Azure] functionaliteit die deel van hun [&#x200B; openbaar voorproefprogramma &#x200B;](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/) kan uitmaken.

### Voor AWS {#aws-process-summary}

1. [&#x200B; Opstelling AWS KMS &#x200B;](./aws/configure-kms.md) door een encryptiesleutel te vormen die met Adobe moet worden gedeeld.
2. Volg de AWS-specifieke instructies in de [&#x200B; UI opstellingsgids &#x200B;](./aws/ui-set-up.md).
3. Valideer de instelling om te bevestigen dat Experience Platform-gegevens zijn versleuteld met de door AWS gehoste sleutel.

<!--  Pending: or [API setup guide]() -->

Zodra het installatieproces is voltooid voor Experience Platform-instanties die door AWS worden gehost, worden alle gegevens die in Experience Platform in alle sandboxen zijn opgeslagen, gecodeerd met de configuratie van uw AWS Key Management Service (KMS). Als u CMK op AWS wilt gebruiken, gebruikt u de AWS Key Management Service om uw coderingssleutels te maken en te beheren in overeenstemming met de beveiligingsvereisten van uw organisatie.

## Gevolgen van het intrekken van toetstoegang {#revoke-access}

Als u de toegang tot de Key Vault-, Key- of CMK-toepassing in Azure of de coderingssleutel in AWS intrekt of uitschakelt, kan dit leiden tot aanzienlijke verstoringen, zoals het doorbreken van wijzigingen in uw Experience Platform-bewerkingen. Als toetsen eenmaal zijn uitgeschakeld, kunnen gegevens in Experience Platform ontoegankelijk worden en zullen downstreambewerkingen die op deze gegevens vertrouwen, niet meer werken. Het is van cruciaal belang dat u de downstreameffecten volledig begrijpt voordat u wijzigingen aanbrengt in uw sleutelconfiguraties.

Als u de toegang van Experience Platform tot uw gegevens in [!DNL Azure] wilt intrekken, verwijdert u de gebruikersrol die aan de toepassing is gekoppeld uit de Key Vault. Voor AWS kunt u de toets uitschakelen of de beleidsinstructie bijwerken. Voor gedetailleerde instructies op het proces van AWS, verwijs naar de [&#x200B; zeer belangrijke intrekkingssectie &#x200B;](./aws/ui-set-up.md#key-revocation).


### Tijdlijnen voor doorgave {#propagation-timelines}

Nadat de toetstoegang is ingetrokken vanuit de [!DNL Azure] Key Vault, worden de wijzigingen als volgt doorgegeven:

| **Type van opslag** | **Beschrijving** | **Tijdlijn** |
|---|---|---|
| Primaire gegevensopslag | Omvat gegevensmeren (Azure Data Lake, AWS S3) en Azure Cosmos DB Profile stores. Zodra toetstoegang wordt ingetrokken, worden de gegevens ontoegankelijk. | A **enkele notulen aan 24 uren**. |
| Gegevensopslag in cache/transient | Omvat secundaire gegevensopslag die voor prestaties en kerntoepassingsfunctionaliteit wordt gebruikt. De gevolgen van een belangrijke intrekking worden vertraagd. | **tot 7 dagen**. |

Het dashboard Profiel zal bijvoorbeeld gegevens van zijn geheime voorgeheugen blijven tonen tot zeven dagen alvorens de gegevens verlopen en worden verfrist. Op dezelfde manier duurt het opnieuw inschakelen van toegang tot de toepassing even lang om de beschikbaarheid van gegevens in deze opslagruimten te herstellen.

>[!NOTE]
>
>Het opnieuw inschakelen van toegang tot de toepassing kan even veel tijd in beslag nemen als het intrekken van het verzoek om de beschikbaarheid van gegevens in deze opslagruimten te herstellen.

>[!TIP]
>
>Er zijn twee gebruik-geval-specifieke uitzonderingen op de zeven dagen datasetvervaldatum op niet primaire (caching/transient) gegevens. Raadpleeg de documentatie bij deze pagina voor meer informatie over deze functies.<ul><li>[&#x200B; Adobe Journey Optimizer URL Shortener &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=nl-NL#message-preset-sms)</li><li>[&#x200B; de Projecties van Edge &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=nl-NL#edge-projections)</li></ul>

## Volgende stappen

Het proces starten:

- Voor Azure: Begin door [&#x200B; vormend een  [!DNL Azure]  Zeer belangrijke Uitvault &#x200B;](./azure/azure-key-vault-config.md) en [&#x200B; produceert een encryptiesleutel &#x200B;](./azure/azure-key-vault-config.md#generate-a-key) om met Adobe te delen.
- Voor AWS: [&#x200B; opstelling AWS KMS &#x200B;](./aws/configure-kms.md) en verzekert juiste configuraties IAM en KMS alvorens aan UI of API opstellingshulplijnen te werk te gaan.
