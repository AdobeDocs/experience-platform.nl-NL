---
title: Verbinding maken tussen MariaDB en Experience Platform via de gebruikersinterface
description: Leer hoe u uw MariaDB-account met Experience Platform kunt verbinden aan de hand van de werkruimte Bronnen in de Experience Platform-gebruikersinterface.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# Verbinding maken [!DNL MariaDB] met Experience Platform via de gebruikersinterface

Lees deze handleiding voor informatie over hoe u uw [!DNL MariaDB] -account kunt verbinden met Adobe Experience Platform via de werkruimte Bronnen in de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [&#x200B; Real-Time Profiel van de Klant &#x200B;](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een [!DNL MariaDB] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Lees het [[!DNL MariaDB]  overzicht &#x200B;](../../../../connectors/databases/mariadb.md#prerequisites) voor informatie over authentificatie.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Selecteer de juiste categorie in het deelvenster *[!UICONTROL Categories]*. U kunt ook op de zoekbalk navigeren naar de specifieke bron die u wilt gebruiken.

Als u [!DNL MariaDB] wilt gebruiken, selecteert u de **[!UICONTROL MariaDB]** bronkaart onder *[!UICONTROL Databases]* en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![&#x200B; de broncatalogus in UI met geselecteerde kaart MariaDB.](../../../../images/tutorials/create/maria-db/catalog.png)

## Een bestaande account gebruiken {#existing}

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL MariaDB] -account die u wilt gebruiken.

![&#x200B; de bestaande rekeningeninterface in het bronwerkschema met &quot;Bestaande geselecteerde rekening&quot;.](../../../../images/tutorials/create/maria-db/existing.png)

## Een nieuwe account maken {#create}

Als u geen bestaand account hebt, moet u een nieuw account maken door de vereiste verificatiereferenties op te geven die overeenkomen met uw bron.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam op en voegt u desgewenst een beschrijving voor uw account toe.

![&#x200B; de nieuwe rekeningsinterface in het bronwerkschema met een rekeningsnaam en facultatieve verstrekte beschrijving.](../../../../images/tutorials/create/maria-db/new.png)

### Verbinding maken met Experience Platform

U kunt uw [!DNL MariaDB] -account verbinden met Experience Platform met behulp van een accountsleutel of basisverificatie.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Om rekeningszeer belangrijke authentificatie te gebruiken, selecteer **[!UICONTROL Account key authentication]**, verstrek uw [&#x200B; verbindingskoord &#x200B;](../../../../connectors/databases/mariadb.md#azure), en selecteer dan **[!UICONTROL Connect to source]**.

![&#x200B; de nieuwe rekeningsinterface in het bronwerkschema met &quot;de belangrijkste geselecteerde authentificatie van de Rekening&quot;.](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB  Basisauthentificatie ]

Om basisauthentificatie te gebruiken, selecteer **[!UICONTROL Basic authentication]**, verstrek waarden voor uw [&#x200B; authentificatiegeloofsbrieven &#x200B;](../../../../connectors/databases/mariadb.md#azure), en selecteer dan **[!UICONTROL Connect to source]**.

![&#x200B; de nieuwe rekeningsinterface in het bronwerkschema met &quot;Basisauthentificatie&quot;geselecteerd.](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL MariaDB] -account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens in Experience Platform &#x200B;](../../dataflow/databases.md) te brengen.
