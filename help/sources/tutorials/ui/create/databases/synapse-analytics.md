---
title: Een Azure Synapse Analytics Source Connection maken in de gebruikersinterface
description: Leer hoe u een Azure Synapse Analytics-bronverbinding (hierna "Synapse" genoemd) maakt met behulp van de Adobe Experience Platform-gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 1f1ce317-eaaf-4ad2-a5fb-236983220bd7
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Een [!DNL Azure Synapse Analytics] bronverbinding maken in de gebruikersinterface

>[!IMPORTANT]
>
>De [!DNL Azure Synapse Analytics] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time Customer Data Platform Ultimate hebben aangeschaft.

Lees deze handleiding voor informatie over hoe u uw [!DNL Azure Synapse Analytics] -account kunt verbinden met Adobe Experience Platform via de werkruimte voor bronnen in de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Azure Synapse Analytics] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Lees het [[!DNL Azure Synapse Analytics]  overzicht &#x200B;](../../../../connectors/databases/synapse-analytics.md#prerequisites) voor informatie over authentificatie.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Azure Synapse Analytics] , gaat u naar de categorie *[!UICONTROL Databases]* , selecteert u de **[!UICONTROL Azure Synapse analytics]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![&#x200B; de broncatalogus met &quot;Analytics van Azure Synapse&quot;geselecteerd.](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

## Een bestaande account gebruiken {#existing}

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL Azure Synapse Analytics] -account die u wilt gebruiken.

![&#x200B; de bestaande rekeningsinterface van het bronwerkschema.](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Een nieuwe account maken {#new}

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam op en voegt u desgewenst een beschrijving voor uw account toe.

![&#x200B; de nieuwe rekeningsinterface van het bronwerkschema.](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Verbinding maken met Experience Platform

U kunt uw [!DNL Azure Synapse Analytics] -account verbinden met Experience Platform met behulp van accountsleutelverificatie of service principal en sleutelverificatie.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Om rekeningszeer belangrijke authentificatie te gebruiken, selecteer **[!UICONTROL Account key authentication]**, verstrek uw [&#x200B; verbindingskoord &#x200B;](../../../../connectors/databases/synapse-analytics.md#prerequisites), en selecteer dan **[!UICONTROL Connect to source]**.

![&#x200B; &quot;creeer nieuwe rekening&quot;stap in het bronwerkschema met &quot;geselecteerde de authentificatie van de rekeningssleutel.](../../../../images/tutorials/create/azure-synapse-analytics/account-key-auth.png)

>[!TAB  het hoofd van de dienst en zeer belangrijke authentificatie ]

Alternatief, selecteer **[!UICONTROL Service principal and key authentication]**, verstrek waarden voor uw [&#x200B; authentificatiegeloofsbrieven &#x200B;](../../../../connectors/databases/synapse-analytics.md#prerequisites), en selecteer dan **[!UICONTROL Connect to source]**.

![&#x200B; &quot;creeer nieuwe rekening&quot;stap in het bronwerkschema met de &quot;dienst belangrijkste en zeer belangrijke geselecteerde authentificatie&quot;.](../../../../images/tutorials/create/azure-synapse-analytics/service-principal.png)

>[!ENDTABS]

## Een gegevensstroom maken voor [!DNL Azure Synapse Analytics] -gegevens

Nu u met succes uw [!DNL Azure Synapse Analytics] gegevensbestand hebt verbonden, kunt u [&#x200B; nu tot een dataflow leiden en gegevens van uw gegevensbestand in Experience Platform &#x200B;](../../dataflow/databases.md) opnemen.
