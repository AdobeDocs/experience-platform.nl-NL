---
title: Samenvatting Gecodeerde Gegevens in Brongebruikersinterface Workspace
description: Leer hoe u gecodeerde gegevens kunt invoeren in de UI-werkruimte voor bronnen.
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Voeg gecodeerde gegevens in de interface van bronnen in

Lees deze handleiding om te leren hoe u gecodeerde gegevens aan Adobe Experience Platform kunt toevoegen met behulp van bronnen voor cloudopslag voor batchgegevens.

## Vereisten

* Gegevens versleutelen

## Gecodeerde gegevens verzamelen {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Is het bestand versleuteld?"
>abstract="Selecteer deze schakeloptie als u een reeds gecodeerd bestand wilt invoeren."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Voorbeeldbestand selecteren"
>abstract="Als u een toewijzing wilt maken, moet u een voorbeeldbestand invoeren bij het invoeren van gecodeerde gegevens."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="Versleutelingssleutel-id"
>abstract="Geef de coderingssleutel-id op die overeenkomt met de coderingssleutel die is gebruikt om de brongegevens te coderen."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Verificatiesleutel-id ondertekenen"
>abstract="Geef de sleutel-id voor ondertekeningsverificatie op die overeenkomt met uw ondertekende, gecodeerde brongegevens."

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
