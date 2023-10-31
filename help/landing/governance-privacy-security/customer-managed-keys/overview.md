---
title: Door de klant beheerde toetsen in Adobe Experience Platform
description: Leer hoe u uw eigen coderingssleutels instelt voor gegevens die in Adobe Experience Platform zijn opgeslagen.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 930c786db51063c55f731dc90f2ee66e98624555
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# Door de klant beheerde sleutels in Adobe Experience Platform

Gegevens die op Adobe Experience Platform zijn opgeslagen, worden in rust gecodeerd met systeemtoetsen. Als u een toepassing gebruikt die bovenop Platform wordt gebouwd, kunt u verkiezen om uw eigen encryptiesleutels in plaats daarvan te gebruiken, die u grotere controle over uw gegevensveiligheid geven.

>[!NOTE]
>
>Gegevens in het Adobe Experience Platform-gegevenspeer en -profielarchief worden gecodeerd met CMK. Deze worden beschouwd als uw primaire gegevensopslag.

Dit document biedt een overzicht op hoog niveau van het proces voor het inschakelen van de CMK-functie (Customer-managed keys) in Platform, en de vereiste informatie die nodig is om deze stappen te voltooien.

>[!NOTE]
>
>Voor klanten van de Customer Journey Analytics gelieve de instructies in te volgen [Documentatie Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=en).

## Vereisten

Ga naar de [!UICONTROL Encryption] in Adobe Experience Platform moet u een rol hebben gemaakt en de [!UICONTROL Manage Customer Managed Key] toestemming voor die rol. Om het even welke gebruiker die heeft [!UICONTROL Manage Customer Managed Key] U kunt CMK inschakelen voor hun organisatie.

Voor meer informatie over het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [machtigingendocumentatie configureren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Als u CMK wilt inschakelen, moet u [!DNL Azure] Key Vault moet worden geconfigureerd met de volgende instellingen:

* [Reinigingsbeveiliging inschakelen](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [soft-delete inschakelen](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Toegang configureren met [!DNL Azure] rolgebaseerd toegangsbeheer](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Lees de gekoppelde documentatie om het proces beter te begrijpen.

## Procesoverzicht {#process-summary}

CMK is opgenomen in het gezondheidsschild en het aanbod van privacy en beveiligingsschild van Adobe. Nadat uw organisatie een licentie voor een van deze aanbiedingen heeft aangeschaft, kunt u een eenmalig proces starten om de functie in te stellen.

>[!WARNING]
>
>Nadat u CMK hebt ingesteld, kunt u niet terugkeren naar de toetsen die door het systeem worden beheerd. U bent verantwoordelijk voor het veilig beheren van uw sleutels en het bieden van toegang tot uw Key Vault-, Key- en CMK-app binnen [!DNL Azure] om te voorkomen dat toegang tot uw gegevens verloren gaat.

Het proces is als volgt:

1. [Een [!DNL Azure] Key Vault](./azure-key-vault-config.md) op basis van het beleid van uw organisatie [een coderingssleutel genereren](./azure-key-vault-config.md#generate-a-key) dat zal uiteindelijk met Adobe worden gedeeld .
1. Stel de CMK-toepassing in met uw [!DNL Azure] pachter door [API-aanroepen](./api-set-up.md#register-app) of de [UI](./ui-set-up.md#register-app).
1. Verstuur uw encryptie zeer belangrijke identiteitskaart naar Adobe en begin het enablement proces voor de eigenschap of [in de gebruikersinterface](./ui-set-up.md#send-to-adobe) of met een [API-aanroep](./api-set-up.md#send-to-adobe).
1. Controleer de status van de configuratie om te controleren of CMK is ingeschakeld of [in de gebruikersinterface](./ui-set-up.md#check-status) of met een [API-aanroep](./api-set-up.md#check-status).

Zodra het installatieproces is voltooid, worden alle gegevens die in het platform worden ingevoerd in alle sandboxen gecodeerd met uw [!DNL Azure] toetsinstelling. Als u CMK wilt gebruiken, gebruikt u [!DNL Microsoft Azure] functionaliteit die deel kan uitmaken van hun [openbaar voorvertoningsprogramma](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Toegang intrekken {#revoke-access}

Als u de toegang van het Platform tot uw gegevens wilt intrekken, kunt u de gebruikersrol verbonden aan de toepassing uit de sleutelkluis binnen verwijderen [!DNL Azure].

>[!WARNING]
>
>Als u de sleutelvault-, toets- of CMK-toepassing uitschakelt, kan dit resulteren in een regeleindewijziging. Wanneer de sleutelvault-, sleutel- of CMK-toepassing is uitgeschakeld en de gegevens niet meer toegankelijk zijn in Platform, zijn downstreambewerkingen met betrekking tot die gegevens niet meer mogelijk. Zorg ervoor dat u de downstreameffecten begrijpt van het intrekken van de toegang van het Platform tot uw sleutel voordat u wijzigingen aanbrengt in uw configuratie.

Nadat u de toegang tot de sleutel hebt verwijderd of de sleutel uit uw [!DNL Azure] zeer belangrijke vault, kan het van een paar minuten, tot 24 uren voor deze configuratie overal vergen om aan primaire gegevensopslag te verspreiden. De werkstromen van het platform omvatten ook caching en transient gegevensopslag die voor prestaties en kerntoepassingsfunctionaliteit wordt vereist. Het doorgeven van CMK-intrekking via dergelijke opgeslagen en tijdelijke opslagplaatsen kan maximaal zeven dagen in beslag nemen, zoals wordt bepaald door de gegevensverwerkingsworkflows. Dit betekent bijvoorbeeld dat het dashboard Profiel gegevens uit de opslag van cachegegevens bewaart en weergeeft en dat het zeven dagen duurt voordat de gegevens in de opslagruimten voor cachegegevens verlopen als onderdeel van de vernieuwingscyclus. Dezelfde tijdvertraging geldt voor gegevens die weer beschikbaar komen wanneer de toegang tot de toepassing opnieuw wordt ingeschakeld.

>[!NOTE]
>
>Er zijn twee gebruik-geval-specifieke uitzonderingen op de zeven dagen datasetvervaldatum op niet primaire (caching/transient) gegevens. Raadpleeg de documentatie bij deze pagina voor meer informatie over deze functies.<ul><li>[Adobe Journey Optimizer URL Shortener](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[Edge-projecties](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Volgende stappen

Als u het proces wilt starten, begint u met [configureren en [!DNL Azure] Key Vault](./azure-key-vault-config.md) en [een coderingssleutel genereren](./azure-key-vault-config.md#generate-a-key) delen met Adobe.
