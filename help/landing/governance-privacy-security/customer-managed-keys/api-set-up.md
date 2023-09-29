---
title: Door de klant beheerde toetsen instellen en configureren met behulp van de API
description: Leer hoe u uw CMK-app instelt met uw Azure-medewerker en uw coderingssleutel-id verzendt naar Adobe Experience Platform.
source-git-commit: a0df05cde19e97d4abdad7abd19eafea8efe1096
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Door de klant beheerde sleutels instellen en configureren met behulp van de API

In dit document wordt beschreven hoe de CMK-functie (door de klant beheerde sleutels) in Adobe Experience Platform met de API kan worden ingeschakeld. Voor instructies over hoe te om dit proces te voltooien gebruikend UI, verwijs naar [UI CMK-instellingsdocument](./ui-set-up.md).

## Vereisten

Ga naar de [!UICONTROL Encryption] in Adobe Experience Platform moet u een rol hebben gemaakt en de [!UICONTROL Manage Customer Managed Key] toestemming voor die rol. Om het even welke gebruiker die heeft [!UICONTROL Manage Customer Managed Key] U kunt CMK inschakelen voor hun organisatie.

Voor meer informatie over het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [machtigingendocumentatie configureren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Als u CMK wilt inschakelen, moet u [[!DNL Azure] Key Vault moet worden geconfigureerd](./azure-key-vault-config.md) met de volgende instellingen:

* [Reinigingsbeveiliging inschakelen](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [soft-delete inschakelen](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Toegang configureren met [!DNL Azure] rolgebaseerd toegangsbeheer](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Een [!DNL Azure] Key Vault](./azure-key-vault-config.md)

## De CMK-toepassing instellen {#register-app}

Nadat u de sleutelkluis hebt geconfigureerd, moet u zich registreren voor de CMK-toepassing die een koppeling naar uw [!DNL Azure] huurder.

### Aan de slag

Voor het registreren van de CMK-toepassing moet u oproepen doen naar platform-API&#39;s. Voor details op hoe te om de vereiste authentificatiekopballen te verzamelen om deze vraag te maken, zie [Platform API-verificatiehandleiding](../../api-authentication.md).

Terwijl de authentificatiegids instructies op hoe te om uw eigen unieke waarde voor vereiste te produceren verstrekt `x-api-key` request header, alle API bewerkingen in deze handleiding gebruiken de statische waarde `acp_provisioning` in plaats daarvan. U moet nog steeds uw eigen waarden opgeven voor `{ACCESS_TOKEN}` en `{ORG_ID}`, echter.

In alle API-aanroepen in deze handleiding `platform.adobe.io` wordt gebruikt als wortelweg, die aan het gebied VA7 in gebreke blijft. Als uw organisatie een ander gebied gebruikt, `platform` moet worden gevolgd door een streepje en de regiocode die aan uw organisatie is toegewezen: `nld2` voor NLD2 of `aus5` voor AUS5 (bijvoorbeeld: `platform-aus5.adobe.io`). Als u het gebied van uw organisatie niet kent, contacteer uw systeembeheerder.

### URL voor verificatie ophalen {#fetch-authentication-url}

Als u het registratieproces wilt starten, vraagt u een GET aan bij het eindpunt van de toepassingsregistratie om de vereiste verificatie-URL voor uw organisatie op te halen.

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Antwoord**

Een geslaagde reactie retourneert een `applicationRedirectUrl` eigenschap, die de verificatie-URL bevat.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Kopieer en plak de `applicationRedirectUrl` adres in browser om een authentificatiedialoog te openen. Selecteren **[!DNL Accept]** om de CMK-toepassingsserviceprincipal toe te voegen aan uw [!DNL Azure] huurder.

![Een dialoogvenster voor Microsoft-machtigingsaanvragen met [!UICONTROL Accept] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### De CMK-toepassing toewijzen aan een rol {#assign-to-role}

Navigeer na het voltooien van het verificatieproces terug naar uw [!DNL Azure] Key Vault en selecteer **[!DNL Access control]** in de linkernavigatie. Van hier, selecteer **[!DNL Add]** gevolgd door **[!DNL Add role assignment]**.

![Het Microsoft Azure-dashboard met [!DNL Add] en [!DNL Add role assignment] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

In het volgende scherm wordt u gevraagd een rol voor deze toewijzing te kiezen. Selecteren **[!DNL Key Vault Crypto Service Encryption User]** voordat u selecteert **[!DNL Next]** om door te gaan.

![Het Microsoft Azure-dashboard met de [!DNL Key Vault Crypto Service Encryption User] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Kies in het volgende scherm **[!DNL Select members]** een dialoog op gang te brengen in het rechterspoor . Gebruik de zoekbalk om de serviceprincipal voor de CMK-toepassing te zoeken en selecteer deze in de lijst. Selecteer **[!DNL Save]**.

>[!NOTE]
>
>Als u uw toepassing niet in de lijst kunt vinden, dan is uw de diensthoofd niet in uw huurder goedgekeurd. Om ervoor te zorgen dat u de juiste rechten hebt, werkt u samen met uw [!DNL Azure] beheerder of vertegenwoordiger.

## De configuratie van de coderingssleutel op het Experience Platform inschakelen {#send-to-adobe}

Nadat u de CMK-toepassing hebt geïnstalleerd op [!DNL Azure], kunt u de id van de coderingssleutel naar de Adobe verzenden. Selecteren **[!DNL Keys]** in de linkernavigatie, gevolgd door de naam van de sleutel u wilt verzenden.

![Het Microsoft Azure-dashboard met de [!DNL Keys] en de sleutelnaam gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecteer de meest recente versie van de sleutel en de detailpagina wordt weergegeven. Van hier, kunt u naar keuze de toegelaten verrichtingen voor de sleutel vormen.

>[!IMPORTANT]
>
>De minimaal vereiste bewerkingen voor de toets zijn: **[!DNL Wrap Key]** en **[!DNL Unwrap Key]** machtigingen. U kunt [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], en [!DNL Verify] zou u willen.

De **[!UICONTROL Key Identifier]** wordt de URI-id voor de sleutel weergegeven. Kopieer deze URI-waarde voor gebruik in de volgende stap.

![De Microsoft Azure-dashboard Belangrijke informatie met de [!DNL Permitted operations] en de URL-secties van de kopieersleutel zijn gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Nadat u de sleutelvault-URI hebt verkregen, kunt u deze met een verzoek van de POST naar het CMK-configuratiepunt verzenden.

>[!NOTE]
>
>Alleen de sleutelvault en sleutelnaam worden met Adobe opgeslagen, niet de belangrijkste versie.

**Verzoek**

+++ Een voorbeeldverzoek om sleutel-URI naar het CMK-configuratiepunt te verzenden.

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | Een naam voor de configuratie. Zorg ervoor dat u deze waarde onthoudt omdat deze nodig is om de status van de configuratie bij een [latere stap](#check-status). De waarde is hoofdlettergevoelig. |
| `type` | Het configuratietype. Moet worden ingesteld op `BYOK_CONFIG`. |
| `imsOrgId` | Uw organisatie-id. Deze id moet dezelfde waarde hebben als in het dialoogvenster `x-gw-ims-org-id` header. |
| `configData` | This property contains the following details about the configuration:<ul><li>`providerType`: Moet worden ingesteld op `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: De sleutelkluis-URI die u hebt gekopieerd [eerder](#send-to-adobe).</li></ul> |

+++

**Antwoord**

+++ De succesvolle reactie keert de details van de configuratietaak terug.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

De taak moet de verwerking binnen een paar minuten voltooien.

## De status van de configuratie controleren {#check-status}

Om de status van het configuratieverzoek te controleren, kunt u een verzoek van de GET indienen.

**Verzoek**

U moet de opdracht `name` van de configuratie die u wilt controleren op het pad (`config1` in het onderstaande voorbeeld) en een `configType` queryparameter ingesteld op `BYOK_CONFIG`.

+++ Een steekproefverzoek om de status van het configuratieverzoek te controleren.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Antwoord**

+++ De geslaagde reactie retourneert de status van de taak.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

De `status` attribuut kan één van vier waarden met de volgende betekenis hebben:

1. `RUNNING`: Valideert of Platform toegang heeft tot de sleutel- en toetsvault.
1. `UPDATE_EXISTING_RESOURCES`: Het systeem voegt de sleutelvault en sleutelnaam aan de datastores over alle zandbakken in uw organisatie toe.
1. `COMPLETED`: De sleutelvault en sleutelnaam zijn aan de datastores toegevoegd.
1. `FAILED`: Er is een probleem opgetreden, dat voornamelijk te maken heeft met de toepassingsinstellingen van de toepassing key, key vault of multi-huurder.

## Volgende stappen

Door de bovenstaande stappen te voltooien, hebt u CMK voor uw organisatie ingeschakeld. Gegevens die in de primaire gegevensopslag worden ingevoerd, worden nu gecodeerd en gedecodeerd met de sleutel(s) in de [!DNL Azure] Key Vault. Ga voor meer informatie over gegevenscodering in Adobe Experience Platform naar de [versleutelingsdocumentatie](../encryption.md).
