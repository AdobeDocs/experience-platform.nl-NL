---
title: Samenvatting Gecodeerde Gegevens in Brongebruikersinterface Workspace
description: Leer hoe u gecodeerde gegevens kunt invoeren in de UI-werkruimte voor bronnen.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Voeg gecodeerde gegevens in de interface van bronnen in

>[!AVAILABILITY]
>
>Ondersteuning voor gecodeerde gegevensinvoer in de interface van bronnen vindt u in bèta en is mogelijk niet beschikbaar voor uw organisatie. De functie en documentatie kunnen worden gewijzigd.

U kunt gecodeerde gegevensbestanden en -mappen via batchbronnen voor cloudopslag opnemen in Adobe Experience Platform. Met gecodeerde gegevensinvoer kunt u gebruikmaken van asymmetrische coderingsmechanismen om batchgegevens veilig naar het Experience Platform over te brengen. Momenteel, zijn de gesteunde asymmetrische encryptiemechanismen PGP en GPG.

Deze functie is beschikbaar voor de volgende bronnen:

* [Amazon S3]
* [ Azure Blob ]
* [ Azure Data Lake Storage Gen2 ]
* [ Azure de Opslag van het Dossier ]
* [ Gegevens die Zone ] aanvoeren
* [ FTP ]
* [ Google Cloud Storage ]
* [ HDFS ]
* {de Opslag van de Objecten van 0} Oracle ][
* [SFTP]

Lees deze handleiding om te leren hoe u gecodeerde gegevens met bronnen voor opslagbatch voor de cloud kunt invoeren met behulp van de gebruikersinterface.

## Aan de slag

Het is nuttig om inzicht in de volgende eigenschappen en de concepten van het Experience Platform te hebben alvorens met gecodeerde gegevensopname in UI te werken:

* [ Bronnen ](../../home.md): De bronnen van het gebruik in Experience Platform om gegevens van een Toepassing van de Adobe of een derdegegevensbron in te voeren.
* [ Dataflows ](../../../dataflows/home.md): Dataflows zijn vertegenwoordiging van gegevensbanen die gegevens over Experience Platform bewegen. U kunt de werkruimte van bronnen gebruiken om gegevensstromen tot stand te brengen die gegevens van een bepaalde bron aan Experience Platform opnemen.
* [ Sandboxes ](../../../sandboxes/home.md): De zandbakken van het gebruik in Experience Platform om virtuele verdelingen tussen uw instanties van het Experience Platform tot stand te brengen en milieu&#39;s te creëren gewijd aan ontwikkeling of productie.

### Overzicht op hoog niveau

1. Creeer een encryptiesleutel gebruikend de bronwerkruimte in Experience Platform UI. Desgewenst kunt u ook sleutelpaar voor gebarentverificatie maken om een extra beveiligingslaag voor de gecodeerde gegevens te bieden.
2. Gebruik de openbare sleutel om uw gegevens te coderen.
3. Plaats uw gecodeerde gegevens in uw provider voor cloudopslag. Tijdens deze stap, moet u ook ervoor zorgen dat u een steekproefdossier hebt dat als verwijzing kan worden gebruikt om uw brongegevens aan een Model van de Gegevens van de Ervaring in kaart te brengen (XDM) schema.
4. Verzamel gecodeerde gegevens naar het Experience Platform door een bronverbinding te maken.
5. Geef tijdens het maken van de bronverbinding de sleutel-id op die overeenkomt met de openbare sleutel waarmee u uw gegevens hebt versleuteld. Als u ook het sleutelpaar voor handtekeningverificatie hebt gebruikt, moet u ook de sleutel-id voor tekenverificatie opgeven die overeenkomt met uw gecodeerde gegevens.
6. Ga door met de stappen voor het maken van de gegevensstroom.

## Een sleutelpaar voor versleuteling maken {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="Versleutelingssleutel-id"
>abstract="Geef de coderingssleutel-id op die overeenkomt met de coderingssleutel die is gebruikt om de brongegevens te coderen."

* Navigeer in de interface Platform naar de werkruimte Bronnen en selecteer vervolgens [!UICONTROL Key Pairs] in de bovenste koptekst.
* U wordt genomen aan een pagina die een lijst van bestaande encryptie zeer belangrijke paren in uw organisatie toont. Deze pagina bevat informatie over de titel, de id, het type, het versleutelingsalgoritme, de vervaldatum en de status van een bepaalde sleutel. Selecteer **[!UICONTROL Create Key]** als u een nieuw sleutelpaar wilt maken.
* Kies vervolgens het toetstype dat u wilt maken. Als u een coderingssleutel wilt maken, selecteert u **[!UICONTROL Encryption Key]** en geeft u een titel en een wachtwoordzin voor de coderingssleutel op. Passphrase is een extra laag van bescherming voor uw encryptiesleutels. Op verwezenlijking, slaat het Experience Platform passphrase in een verschillend veilige kluis van de openbare sleutel op. U moet een niet-lege tekenreeks opgeven als een wachtwoordzin.

### Een verificatietoets voor handtekeningen maken {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Verificatiesleutel-id ondertekenen"
>abstract="Geef de sleutel-id voor ondertekeningsverificatie op die overeenkomt met uw ondertekende, gecodeerde brongegevens."

## Gecodeerde gegevens verzamelen {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Is het bestand versleuteld?"
>abstract="Selecteer deze schakeloptie als u een reeds gecodeerd bestand wilt invoeren."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Voorbeeldbestand selecteren"
>abstract="Als u een toewijzing wilt maken, moet u een voorbeeldbestand invoeren bij het invoeren van gecodeerde gegevens."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
