---
title: Connect Azure Blob Storage naar Experience Platform in de gebruikersinterface
description: Leer hoe u uw Azure Blob Storage-account koppelt aan Experience Platform met behulp van de bronwerkruimte in de gebruikersinterface.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Verbinding maken [!DNL Azure Blob Storage] met Experience Platform via de gebruikersinterface

Lees deze gids om te leren hoe te om uw [!DNL Azure Blob Storage] instantie met Adobe Experience Platform te verbinden gebruikend de bronwerkruimte in het gebruikersinterface van Experience Platform.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem &#x200B;](../../../../../xdm/home.md): Het gestandaardiseerde kader voor het organiseren van de gegevens van de klantenervaring in Experience Platform.
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [&#x200B; het leerprogramma van de Redacteur van het Schema &#x200B;](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een geldige [!DNL Azure Blob Storage] verbinding hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan op [&#x200B; vormend een dataflow &#x200B;](../../dataflow/batch/cloud-storage.md).

### Ondersteunde bestandsindelingen

Experience Platform ondersteunt de volgende bestandsindelingen die door externe opslagmedia moeten worden ingevoerd:

* DSV (Delimiter-separated values, door scheidingstekens gescheiden waarden): u kunt elke scheidingsteken voor één kolom gebruiken, zoals een tab, komma, pipe, puntkomma of hash, om platte bestanden in elke gewenste indeling te verzamelen.
* JavaScript Object Notation (JSON): gegevensbestanden met JSON-indeling moeten XDM-compatibel zijn.
* Apache Parquet: gegevensbestanden met Parketindeling moeten XDM-compatibel zijn.

### Vereiste referenties verzamelen

Lees het [[!DNL Azure Blob Storage]  overzicht &#x200B;](../../../../connectors/cloud-storage/blob.md#authentication) voor informatie over authentificatie.

## Navigeren door de catalogus met bronnen

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Azure Blob Storage] , gaat u naar de categorie *[!UICONTROL Cloud storage]* , selecteert u de **[!UICONTROL Azure Blob Storage]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen tonen **[!UICONTROL Set up]** voor nieuwe verbindingen en **[!UICONTROL Add data]** als er al een account bestaat.

![&#x200B; de broncatalogus met de Azure Blob Geselecteerde bron van de Opslag.](../../../../images/tutorials/create/blob/catalog.png)

## Een bestaande account gebruiken

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL Azure Blob Storage] -account die u wilt gebruiken.

![&#x200B; de bestaande broninterface voor de opslag van Azure Blob.](../../../../images/tutorials/create/blob/existing.png)

## Een nieuwe account maken

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam op en voegt u desgewenst een beschrijving voor uw account toe. U kunt uw [!DNL Azure Blob Storage] -account verbinden met Experience Platform door de volgende verificatietypen te gebruiken:

* **de belangrijkste authentificatie van de Rekening**: Gebruikt de toegangssleutel van de opslagrekening om met uw [!DNL Azure Blob Storage] rekening voor authentiek te verklaren en te verbinden.
* **Gedeelde toegangshandtekening (SAS)**: Gebruikt een SAS URI om gedelegeerde, tijd-beperkte toegang tot middelen in uw [!DNL Azure Blob Storage] rekening te verlenen.
* **de hoofd gebaseerde authentificatie van de Dienst**: Gebruikt een Azure Actieve de dienstprincipal van de Folder (AAD) (cliënt identiteitskaart en geheim) om aan uw rekening van de Opslag van Azure Blob veilig voor authentiek te verklaren.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Selecteer **[!UICONTROL Account key authentication]** en voer de opties `connectionString` , `container` en `folderPath` in. Selecteer vervolgens **[!UICONTROL Connect to source]** en wacht even tot de verbinding tot stand is gebracht.

![&#x200B; de optie van de rekeningszeer belangrijke authentificatie in de nieuwe stap van de rekeningsverwezenlijking.](../../../../images/tutorials/create/blob/account-key.png)

>[!TAB  Gedeelde toegangshandtekening ]

Selecteer **[!UICONTROL Shared access signature]** en voer de opties `sasUri` , `container` en `folderPath` in. Selecteer vervolgens **[!UICONTROL Connect to source]** en wacht even tot de verbinding tot stand is gebracht.

![&#x200B; de gedeelde optie van de de authentificatieauthentificatie van de toegangshandtekening in de nieuwe stap van de rekeningsverwezenlijking.](../../../../images/tutorials/create/blob/sas.png)

>[!TAB  de dienst belangrijkste gebaseerde authentificatie ]

Selecteer **[!UICONTROL Service principal based authentication]** en geef de opties `serviceEndpoint` , `servicePrincipalId` , `servicePrincipalKey` , `accountKind` , `tenant` , `container` en `folderPath` op. Selecteer vervolgens **[!UICONTROL Connect to source]** en wacht even tot de verbinding tot stand is gebracht.

![&#x200B; de dienst belangrijkste gebaseerde authentificatieoptie in de nieuwe stap van de rekeningsverwezenlijking.](../../../../images/tutorials/create/blob/service-principal.png)

>[!ENDTABS]

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht met uw [!DNL Azure Blob Storage] -account. U kunt nu aan het volgende leerprogramma verdergaan en [&#x200B; een dataflow vormen om gegevens van uw wolkenopslag in Experience Platform &#x200B;](../../dataflow/batch/cloud-storage.md) te brengen.
