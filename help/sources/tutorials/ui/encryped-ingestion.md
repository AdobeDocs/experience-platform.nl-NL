---
title: Samenvatting Gecodeerde Gegevens in Brongebruikersinterface Workspace
description: Leer hoe u gecodeerde gegevens kunt invoeren in de UI-werkruimte voor bronnen.
badge: Beta
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 70bfebc747c7e6267939eb313048cb2d0e132202
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Voeg gecodeerde gegevens in de interface van bronnen in

>[!AVAILABILITY]
>
>De ondersteuning voor gecodeerde gegevensinvoer in de interface voor bronnen is in bèta. De functie en documentatie kunnen worden gewijzigd.

U kunt gecodeerde gegevensbestanden en -mappen via batchbronnen voor cloudopslag opnemen in Adobe Experience Platform. Met gecodeerde gegevensinvoer kunt u gebruikmaken van asymmetrische coderingsmechanismen om batchgegevens veilig naar het Experience Platform over te brengen. De ondersteunde asymmetrische versleutelingsmechanismen zijn PGP en GPG.

Lees deze handleiding om te leren hoe u gecodeerde gegevens met bronnen voor opslagbatch voor de cloud kunt invoeren met behulp van de gebruikersinterface.

## Aan de slag

Lees voordat u verdergaat met deze zelfstudie de volgende documenten om de volgende Experience Platforms en concepten beter te begrijpen.

* [ Bronnen ](../../home.md): De bronnen van het gebruik in Experience Platform om gegevens van een Toepassing van de Adobe of een derdegegevensbron in te voeren.
* [ Dataflows ](../../../dataflows/home.md): Dataflows zijn vertegenwoordiging van gegevensbanen die gegevens over Experience Platform bewegen. U kunt de werkruimte van bronnen gebruiken om gegevensstromen tot stand te brengen die gegevens van een bepaalde bron aan Experience Platform opnemen.
* [ Sandboxes ](../../../sandboxes/home.md): De zandbakken van het gebruik in Experience Platform om virtuele verdelingen tussen uw instanties van het Experience Platform tot stand te brengen en milieu&#39;s te creëren gewijd aan ontwikkeling of productie.

### Overzicht op hoog niveau

* Creeer een encryptiesleutel gebruikend de bronwerkruimte in Experience Platform UI.
   * Desgewenst kunt u ook uw eigen sleutelpaar voor tekenverificatie maken om een extra beveiligingslaag voor de gecodeerde gegevens te bieden.
* Gebruik de openbare sleutel van uw encryptiesleutel om uw gegevens te coderen.
* Plaats de gecodeerde gegevens in de cloudopslag. Tijdens deze stap moet u er ook voor zorgen dat u een voorbeeldbestand van uw gegevens in uw cloudopslag hebt dat als referentie kan worden gebruikt om uw brongegevens toe te wijzen aan een XDM-schema (Experience Data Model).
* Gebruik uw bron van de de opslagpartij van de wolk en begin het proces van de gegevensopname in de bronwerkruimte in de UI van het Experience Platform.
* Geef tijdens het maken van de bronverbinding de sleutel-id op die overeenkomt met de openbare sleutel waarmee u uw gegevens hebt versleuteld.
   * Als u ook het sleutelpaar voor handtekeningverificatie hebt gebruikt, moet u ook de sleutel-id voor tekenverificatie opgeven die overeenkomt met uw gecodeerde gegevens.
* Ga door met de stappen voor het maken van de gegevensstroom.

## Een sleutelpaar voor versleuteling maken {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="Versleutelingssleutel-id"
>abstract="Geef de coderingssleutel-id op die overeenkomt met de coderingssleutel die is gebruikt om de brongegevens te coderen."

>[!BEGINSHADEBOX]

**wat is een encryptie zeer belangrijk paar?**

Een sleutelpaar van de encryptie is een asymmetrisch cryptografiemechanisme dat uit een openbare sleutel en een privé sleutel bestaat. De openbare sleutel wordt gebruikt om gegevens te coderen en de privé sleutel wordt dan gebruikt om genoemde gegevens te decrypteren.

U kunt uw encryptiesleutel tot stand brengen door het Experience Platform UI. Wanneer gegenereerd, ontvangt u een openbare sleutel en een bijbehorende sleutel-id. Gebruik de openbare sleutel om uw gegevens te coderen en gebruik vervolgens de sleutel-id om uw identiteit te bevestigen wanneer u bezig bent met het invoeren van uw gecodeerde gegevens. De persoonlijke sleutel gaat automatisch naar het Experience Platform, waar het in een veilige kluis wordt opgeslagen, en zal slechts worden gebruikt zodra uw gegevens klaar voor decryptie zijn.

>[!ENDSHADEBOX]

Navigeer in de interface Platform naar de werkruimte Bronnen en selecteer vervolgens [!UICONTROL Key Pairs] in de bovenste koptekst.

![ de broncatalogus met de &quot;Belangrijkste Geselecteerde kopbal van Paren&quot;.](../../images/tutorials/edi/catalog.png)

U wordt genomen aan een pagina die een lijst van bestaande encryptie zeer belangrijke paren in uw organisatie toont. Deze pagina bevat informatie over de titel, de id, het type, het versleutelingsalgoritme, de vervaldatum en de status van een bepaalde sleutel. Selecteer **[!UICONTROL Create Key]** als u een nieuw sleutelpaar wilt maken.

![ de Zeer belangrijke pagina van Paren, met &quot;encryptiesleutel&quot;geselecteerd als zeer belangrijk type en &quot;creeer sleutel&quot;knoop.](../../images/tutorials/edi/encryption_key_page.png)

Kies vervolgens het toetstype dat u wilt maken. Als u een coderingssleutel wilt maken, selecteert u **[!UICONTROL Encryption Key]** en vervolgens **[!UICONTROL Continue]** .

![ het zeer belangrijke creatievenster, met geselecteerde encryptiesleutel.](../../images/tutorials/edi/choose_encryption_key_type.png)

Geef een titel en een wachtwoordzin op voor de coderingssleutel. Passphrase is een extra laag van bescherming voor uw encryptiesleutels. Op verwezenlijking, slaat het Experience Platform passphrase in een verschillend veilige kluis van de openbare sleutel op. U moet een niet-lege tekenreeks opgeven als een wachtwoordzin. Selecteer **[!UICONTROL Create]** als u klaar bent.

![ het venster van de encryptiesleutel verwezenlijking, waar een titel en een passphrase wordt verstrekt.](../../images/tutorials/edi/create_encryption_key.png)

Als dit gelukt is, wordt een nieuw venster weergegeven met de nieuwe coderingssleutel, inclusief de titel, openbare sleutel en sleutel-id. Gebruik de waarde van de openbare sleutel om uw gegevens te coderen. U gebruikt de sleutel-id later om uw identiteit te bewijzen wanneer u uw gecodeerde gegevens opgeeft tijdens het maken van de gegevensstroom.

![ het venster dat informatie over uw onlangs gecreeerd encryptie zeer belangrijk paar toont.](../../images/tutorials/edi/encryption_key_details.png)

Om informatie over een bestaande encryptiesleutel te bekijken, selecteer de ellipsen (`...`) naast de belangrijkste titel. Selecteer **[!UICONTROL Key details]** om de openbare sleutel en belangrijkste identiteitskaart te bekijken Of selecteer **[!UICONTROL Delete]** als u de coderingssleutel wilt verwijderen.

![ de belangrijkste paren pagina, waar een lijst van encryptiesleutels wordt getoond. De ellipsen naast &quot;acme-encryptie-sleutel&quot;wordt geselecteerd en dropdown vertoningenopties om zeer belangrijke details te bekijken of de sleutels te schrappen.](../../images/tutorials/edi/configuration_options.png)

### Een verificatietoets voor handtekeningen maken {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Verificatiesleutel-id ondertekenen"
>abstract="Geef de sleutel-id voor ondertekeningsverificatie op die overeenkomt met uw ondertekende, gecodeerde brongegevens."

>[!BEGINSHADEBOX]

**wat is een sleutel van de signaalcontrole?**

Een verificatiesleutel is een ander versleutelingsmechanisme dat een persoonlijke sleutel en een openbare sleutel omvat. In dit geval kunt u een sleutelpaar voor de verificatie van uw handtekening maken en de persoonlijke sleutel gebruiken om uw gegevens te ondertekenen en een extra coderingslaag toe te voegen. U zult dan de overeenkomstige openbare sleutel aan Experience Platform delen. Tijdens opname gebruikt Experience Platform de openbare sleutel om de handtekening te verifiëren die aan uw persoonlijke sleutel is gekoppeld.

>[!ENDSHADEBOX]

Als u een verificatietoets voor handtekeningen wilt maken, selecteert u **[!UICONTROL Sign Verification Key]** in het selectievenster voor het type sleutel en selecteert u vervolgens **[!UICONTROL Continue]** .

![ het zeer belangrijke venster van de typeselectie waar de sleutel van de handtekeningscontrole wordt geselecteerd.](../../images/tutorials/edi/choose_sign_verification_key_type.png)

Geef vervolgens een titel en een [!DNL Base64] -gecodeerde PGP-sleutel op als openbare sleutel en selecteer **[!UICONTROL Create]** .

![ creeer de sleutel van de sign controle venster.](../../images/tutorials/edi/create_sign_verification_key.png)

Als dit gelukt is, wordt een nieuw venster weergegeven met daarin de nieuwe verificatietoets voor handtekeningen, inclusief de titel en sleutel-id.

![ de details van de pas gecreëerde sleutel van de gebarentverificatie.](../../images/tutorials/edi/sign_verification_key_details.png)

## Gecodeerde gegevens verzamelen {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Is het bestand versleuteld?"
>abstract="Selecteer deze schakeloptie als u een reeds gecodeerd bestand wilt invoeren."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Voorbeeldbestand selecteren"
>abstract="Als u een toewijzing wilt maken, moet u een voorbeeldbestand invoeren bij het invoeren van gecodeerde gegevens."

U kunt gecodeerde gegevens invoeren met de volgende batchbronnen voor cloudopslag:

* [[!DNL Amazon S3]](../ui/create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../ui/create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../ui/create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../ui/create/cloud-storage/azure-file-storage.md)
* [[!DNL Data Landing Zone]](../ui/create/cloud-storage/data-landing-zone.md)
* [[!DNL FTP]](../ui/create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../ui/create/cloud-storage/google-cloud-storage.md)
* [[!DNL HDFS]](../ui/create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../ui/create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../ui/create/cloud-storage/sftp.md)

Verifieer met de bron van de wolkenopslag van uw keus. Selecteer tijdens de stap voor gegevensselectie van de workflow het gecodeerde bestand of de gecodeerde map die u wilt invoegen en schakel vervolgens de **[!UICONTROL Is the file encrypted]** -schakeloptie in.

![ de &quot;uitgezochte gegevens&quot;stap van het bronwerkschema, waar een gecodeerd gegevensdossier voor ingebed wordt geselecteerd.](../../images/tutorials/edi/select_data.png)

Selecteer vervolgens een voorbeeldbestand uit de brongegevens. Aangezien uw gegevens gecodeerd zijn, vereist Experience Platform een voorbeeldbestand om een XDM-schema te maken dat aan uw brongegevens kan worden toegewezen.

![ &quot;Is dit dossier gecodeerd?&quot; Schakel deze optie in en selecteer de knop Voorbeeldbestand selecteren. ](../../images/tutorials/edi/select_sample_file.png)

Nadat u het voorbeeldbestand hebt geselecteerd, configureert u instellingen voor uw gegevens, zoals de bijbehorende gegevensindeling, het scheidingsteken en het compressietype. Zorg ervoor dat de voorvertoningsinterface enige tijd heeft om volledig te renderen en selecteer vervolgens **[!UICONTROL Save]** .

![ een steekproef van A wordt geselecteerd voor opname en de dossiervoorproef wordt volledig geladen.](../../images/tutorials/edi/file_preview.png)

Van hier, gebruik dropdown menu om de openbare zeer belangrijke titel van openbare zeer belangrijke identiteitskaart te selecteren die met de openbare sleutel beantwoordt die u gebruikte om uw gegevens te coderen.

![ de openbare zeer belangrijke titel van openbare zeer belangrijke identiteitskaart die met de openbare sleutel beantwoordt die wordt gebruikt om uw gegevens te coderen.](../../images/tutorials/edi/public_key_id.png)

Als u ook het sleutelpaar voor handtekeningverificatie hebt gebruikt om een extra coderingslaag op te geven, schakelt u het selectievakje voor handtekeningverificatie in en selecteert u op dezelfde manier de sleutel-id voor tekenverificatie die overeenkomt met de sleutel waarmee u uw gegevens hebt versleuteld.

![ De sleuteltitel van de ondertekeningscontrole van zeer belangrijke identiteitskaart die met uw encryptie van de gebarentverificatie beantwoordt.](../../images/tutorials/edi/custom_key_id.png)

Selecteer **[!UICONTROL Next]** wanneer u klaar bent.

Voltooi de overige stappen in de workflow voor bronnen om het maken van de gegevensstroom te voltooien.

* [Gegevens over gegevensstroom en gegevenssets opgeven](../ui/dataflow/batch/cloud-storage.md#provide-dataflow-details)
* [Wijs uw brongegevens toe aan een XDM-schema](../ui/dataflow/batch/cloud-storage.md#map-data-fields-to-an-xdm-schema)
* [Vorm een innameschema voor uw gegevensstroom](../ui/dataflow/batch/cloud-storage.md#schedule-ingestion-runs)
* [Controleer uw gegevensstroom](../ui/dataflow/batch/cloud-storage.md#review-your-dataflow)

U kunt blijven [ updates aan uw dataflow ](../ui/update-dataflows.md) maken zodra het met succes is gecreeerd.

## Volgende stappen

Door dit document te lezen, kunt u nu gecodeerde gegevens van uw blokbron voor cloudopslag opnemen in het Experience Platform. Voor informatie over hoe te om gecodeerde gegevens in te voeren gebruikend APIs, lees de gids over [ het opnemen van gecodeerde gegevens gebruikend  [!DNL Flow Service]  API ](../api/encrypt-data.md). Voor algemene informatie over bronnen op Experience Platform, lees het [ overzicht van bronnen ](../../home.md).
