---
title: Door klanten beheerde toetsen in Adobe Experience Platform
description: Leer hoe u uw eigen coderingssleutels instelt voor gegevens die in Adobe Experience Platform zijn opgeslagen.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: c1a28a4b1ce066a87bb7b34b2524800f9d8f1ca0
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# Door klanten beheerde toetsen in Adobe Experience Platform

Gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die bovenop Platform wordt gebouwd, kunt u verkiezen om uw eigen encryptiesleutels in plaats daarvan te gebruiken, die u grotere controle over uw gegevensveiligheid geven.

>[!AVAILABILITY]
>
>Adobe Experience Platform ondersteunt Customer Managed Keys (CMK) voor zowel Microsoft Azure als Amazon Web Services (AWS). Experience Platform dat op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Als uw implementatie op AWS wordt uitgevoerd, kunt u de Key Management Service (KMS) gebruiken voor gegevenscodering van het platform. Voor meer informatie over de gesteunde infrastructuur, zie het [ Experience Platform multi-cloud overzicht ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>Om over encryptie zeer belangrijke verwezenlijking en beheer in AWS KMS te leren, verwijs naar de [ handleiding van de gegevensencryptie van AWS KMS ](./aws/configure-kms.md). Voor Azure implementaties, zie de [ Azure Zeer belangrijke de configuratiegids van de Vault ](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>Voor [!DNL Azure] gehoste platforminstanties worden de gegevens van het klantprofiel die zijn opgeslagen in de platformprofielen [!DNL Azure Data Lake] en [!DNL Azure Cosmos DB] van het profielarchief, uitsluitend gecodeerd met CMK nadat deze zijn ingeschakeld. De zeer belangrijke herroeping in primaire gegevensopslag kan overal van **een paar notulen aan 24 uren** en **tot 7 dagen** voor transient of secundaire gegevensopslag nemen. Voor extra details, verwijs naar de [ implicaties van het intrekken van zeer belangrijke toegangssectie ](#revoke-access).

Dit document biedt een uitgebreid overzicht van het proces voor het inschakelen van de CMK-functie (Customer Managed Keys) in Platform in [!DNL Azure] en AWS, samen met de vereiste informatie die nodig is om deze stappen te voltooien.

>[!NOTE]
>
>Voor de klanten van de Customer Journey Analytics, te volgen gelieve de instructies in de [ documentatie van de Customer Journey Analytics ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html).

## Vereisten

Om CMK in te schakelen, moet de hostingomgeving van uw platform ([!DNL Azure] of AWS) voldoen aan specifieke configuratievereisten:

### Algemene voorwaarden

Als u de sectie [!UICONTROL Encryption] in Adobe Experience Platform wilt weergeven en openen, moet u een rol hebben gemaakt en de machtiging [!UICONTROL Manage Customer Managed Key] aan die rol hebben toegewezen.  Elke gebruiker met de machtiging [!UICONTROL Manage Customer Managed Key] kan CMK inschakelen voor zijn of haar organisatie.

Voor meer informatie bij het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [ vormen toestemmingendocumentatie ](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

### Azure-specifieke voorwaarden

Voor Azure-gehoste implementaties configureert u de [!DNL Azure] Key Vault met de volgende instellingen:

- [ laat purgebescherming ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection) toe
- [ laat zachte schrapping ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) toe
- [ vorm toegang gebruikend  [!DNL Azure]  op rol-gebaseerde toegangscontrole ](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### AWS-specifieke voorwaarden

Voor AWS-gehoste implementaties configureert u de AWS-omgeving als volgt:

- Controleer of u rechten hebt om coderingssleutels te beheren met behulp van AWS Identity and Access Management (IAM). Voor details, zie het [ IAM Beleid voor AWS KMS ](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Stel AWS KMS in met ondersteuning voor CMK. Verwijs naar de [ gids van de de gegevensencryptie van AWS KMS ](./aws/configure-kms.md).

## Procesoverzicht {#process-summary}

CMK (Customer Managed Keys) is beschikbaar via het aanbod van het gezondheidsschild en het privacyschild van Adobe. In Azure wordt CMK ondersteund voor zowel Healthcare Shield als Privacy en Security Shield. In AWS wordt CMK alleen ondersteund voor Privacy en Security Shield en is CMK niet beschikbaar voor Healthcare Shield. Nadat uw organisatie een licentie voor een van deze aanbiedingen heeft aangeschaft, kunt u het eenmalige installatieproces starten om CMK in te schakelen.

>[!WARNING]
>
>Nadat u CMK hebt ingesteld, kunt u niet terugkeren naar de toetsen die door het systeem worden beheerd. U bent verantwoordelijk voor het veilig beheren van uw sleutels om te voorkomen dat de toegang tot uw gegevens verloren gaat.

Het proces is als volgt:

### Voor Azure {#azure-process-summary}

1. [ vorm een  [!DNL Azure]  Zeer belangrijke die vault ](./azure/azure-key-vault-config.md) op het beleid van uw organisatie wordt gebaseerd, dan [ produceert een encryptiesleutel ](./azure/azure-key-vault-config.md#generate-a-key) met Adobe te delen.
1. Opstelling CMK app met uw [!DNL Azure] huurder door of [ API vraag ](./azure/api-set-up.md#register-app) of [ UI ](./azure/ui-set-up.md#register-app).
1. Verzend uw encryptie zeer belangrijke identiteitskaart aan Adobe en begin het enablement proces voor de eigenschap, of [ in UI ](./azure/ui-set-up.md#send-to-adobe) of met een [ API vraag ](./azure/api-set-up.md#send-to-adobe).
1. Controleer de status van de configuratie om te verifiëren of CMK, of [ in UI ](./azure/ui-set-up.md#check-status) of met een [ API vraag ](./azure/api-set-up.md#check-status) is toegelaten.

Zodra het installatieproces is voltooid voor Azure-hosted Platform-instanties, worden alle gegevens die in het platform worden ingevoerd voor alle sandboxen versleuteld met behulp van de [!DNL Azure] -toetsencombinatie. Om CMK te gebruiken, zult u hefboomwerking [!DNL Microsoft Azure] functionaliteit die deel van hun [ openbaar voorproefprogramma ](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/) kan uitmaken.

### Voor AWS {#aws-process-summary}

1. [ Opstelling AWS KMS ](./aws/configure-kms.md) door een encryptiesleutel te vormen die met Adobe moet worden gedeeld.
2. Volg de AWS-specifieke instructies in de [ UI opstellingsgids ](./aws/ui-set-up.md).
3. Valideer de instellingen om te bevestigen dat de gegevens van het platform worden gecodeerd met de op AWS gehoste sleutel.

<!--  Pending: or [API setup guide]() -->

Zodra het installatieproces is voltooid voor door AWS gehoste platforminstanties, worden alle gegevens die in het platform worden ingevoerd voor alle sandboxen gecodeerd met de configuratie van de AWS Key Management Service (KMS). Als u CMK op AWS wilt gebruiken, gebruikt u de AWS Key Management Service om uw coderingssleutels te maken en te beheren in overeenstemming met de beveiligingsvereisten van uw organisatie.

## Gevolgen van het intrekken van toetstoegang {#revoke-access}

Als u de toegang tot de Key Vault-, Key- of CMK-toepassing in Azure of de coderingssleutel in AWS intrekt of uitschakelt, kan dit leiden tot aanzienlijke verstoringen, zoals het doorbreken van wijzigingen in de activiteiten van uw platform. Als toetsen eenmaal zijn uitgeschakeld, kunnen gegevens in Platform niet meer toegankelijk worden en zullen downstreambewerkingen die op deze gegevens vertrouwen, niet meer werken. Het is van cruciaal belang dat u de downstreameffecten volledig begrijpt voordat u wijzigingen aanbrengt in uw sleutelconfiguraties.

Als u de toegang van het platform tot uw gegevens in [!DNL Azure] wilt intrekken, verwijdert u de gebruikersrol die aan de toepassing is gekoppeld uit de Key Vault. Voor AWS kunt u de toets uitschakelen of de beleidsinstructie bijwerken. Voor gedetailleerde instructies op het proces van AWS, verwijs naar de [ zeer belangrijke intrekkingssectie ](./aws/ui-set-up.md#key-revocation).


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
>Er zijn twee gebruik-geval-specifieke uitzonderingen op de zeven dagen datasetvervaldatum op niet primaire (caching/transient) gegevens. Raadpleeg de documentatie bij deze pagina voor meer informatie over deze functies.<ul><li>[ Adobe Journey Optimizer URL Shortener ](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[ de Projecties van Edge ](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Volgende stappen

Het proces starten:

- Voor Azure: Begin door [ vormend een  [!DNL Azure]  Zeer belangrijke Uitvault ](./azure/azure-key-vault-config.md) en [ produceert een encryptiesleutel ](./azure/azure-key-vault-config.md#generate-a-key) om met Adobe te delen.
- Voor AWS: [ opstelling AWS KMS ](./aws/configure-kms.md) en verzekert juiste configuraties IAM en KMS alvorens aan UI of API opstellingshulplijnen te werk te gaan.
