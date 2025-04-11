---
title: Verbinding maken tussen MariaDB en Experience Platform via de gebruikersinterface
description: Leer hoe u uw MariaDB-account met Experience Platform kunt verbinden aan de hand van de werkruimte Bronnen in de Experience Platform-gebruikersinterface.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: 0bf31c76f86b4515688d3aa60deb8744e38b4cd5
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# Verbinding maken [!DNL MariaDB] met Experience Platform via de gebruikersinterface

Lees deze handleiding voor informatie over hoe u uw [!DNL MariaDB] -account kunt verbinden met Adobe Experience Platform via de werkruimte Bronnen in de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [ Real-Time Profiel van de Klant ](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u reeds een [!DNL MariaDB] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [ vormend een dataflow ](../../dataflow/databases.md).

### Vereiste referenties verzamelen

Lees het [[!DNL MariaDB]  overzicht ](../../../../connectors/databases/mariadb.md#prerequisites) voor informatie over authentificatie.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Selecteer de juiste categorie in het deelvenster *[!UICONTROL Categories]*. U kunt ook op de zoekbalk navigeren naar de specifieke bron die u wilt gebruiken.

Als u [!DNL MariaDB] wilt gebruiken, selecteert u de **[!UICONTROL MariaDB]** bronkaart onder *[!UICONTROL Databases]* en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus in UI met geselecteerde kaart MariaDB.](../../../../images/tutorials/create/maria-db/catalog.png)

## Een bestaande account gebruiken {#existing}

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL MariaDB] -account die u wilt gebruiken.

![ de bestaande rekeningeninterface in het bronwerkschema met &quot;Bestaande geselecteerde rekening&quot;.](../../../../images/tutorials/create/maria-db/existing.png)

## Een nieuwe account maken {#create}

Als u geen bestaand account hebt, moet u een nieuw account maken door de vereiste verificatiereferenties op te geven die overeenkomen met uw bron.

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam op en voegt u desgewenst een beschrijving voor uw account toe.

![ de nieuwe rekeningsinterface in het bronwerkschema met een rekeningsnaam en facultatieve verstrekte beschrijving.](../../../../images/tutorials/create/maria-db/new.png)

### Verbinding maken met Experience Platform on Azure {#azure}

U kunt uw [!DNL MariaDB] -account op Azure verbinden met Experience Platform met behulp van een accountsleutel of een basisverificatie.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Om rekeningszeer belangrijke authentificatie te gebruiken, selecteer **[!UICONTROL Account key authentication]**, verstrek uw [ verbindingskoord ](../../../../connectors/databases/mariadb.md#azure), en selecteer dan **[!UICONTROL Connect to source]**.

![ de nieuwe rekeningsinterface in het bronwerkschema met &quot;de belangrijkste geselecteerde authentificatie van de Rekening&quot;.](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB  Basisauthentificatie ]

Om basisauthentificatie te gebruiken, selecteer **[!UICONTROL Basic authentication]**, verstrek waarden voor uw [ authentificatiegeloofsbrieven ](../../../../connectors/databases/mariadb.md#azure), en selecteer dan **[!UICONTROL Connect to source]**.

![ de nieuwe rekeningsinterface in het bronwerkschema met &quot;Basisauthentificatie&quot;geselecteerd.](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

### Verbinding maken met Experience Platform op Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../../landing/multi-cloud.md).

Om een nieuwe [!DNL MariaDB] rekening tot stand te brengen en met Experience Platform op AWS te verbinden, zorg ervoor dat u in een zandbak VA6 bent en dan de noodzakelijke [ geloofsbrieven voor authentificatie ](../../../../connectors/databases/mariadb.md#aws) verstrekt.

![ de nieuwe rekeningsinterface in het bronwerkschema om met AWS te verbinden.](../../../../images/tutorials/create/maria-db/basic-auth.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL MariaDB] -account. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow vormen om gegevens in Experience Platform ](../../dataflow/databases.md) te brengen.
