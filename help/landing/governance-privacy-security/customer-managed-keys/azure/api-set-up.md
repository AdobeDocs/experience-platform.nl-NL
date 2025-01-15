---
title: Door de klant beheerde sleutels voor Azure instellen en configureren met behulp van de API
description: Leer hoe u uw CMK-app instelt met uw Azure-medewerker en uw coderingssleutel-id verzendt naar Adobe Experience Platform.
role: Developer
feature: API, Privacy
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: 53598f86e1876bc6d1807e95a26584da4d7db3f2
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 0%

---

# Door de klant beheerde sleutels voor Azure instellen en configureren met behulp van de API

In dit document worden de Azure-specifieke instructies besproken voor het inschakelen van Customer Managed Keys (CMK) in Adobe Experience Platform met behulp van de API. Voor instructies op hoe te om dit proces te voltooien gebruikend UI voor de instanties van het Azure-ontvangen Platform, verwijs naar het [ interface CMK opstellingsdocument CMK ](./ui-set-up.md).

Voor AWS-specifieke instructies, verwijs naar de [ opstellingsgids van AWS ](../aws/ui-set-up.md).

## Vereisten

Als u de sectie [!UICONTROL Encryption] in Adobe Experience Platform wilt weergeven en bezoeken, moet u een rol hebben gemaakt en [!UICONTROL Manage Customer Managed Key] toestemming aan die rol hebben toegewezen. Elke gebruiker met de machtiging [!UICONTROL Manage Customer Managed Key] kan CMK inschakelen voor zijn of haar organisatie.

Voor meer informatie bij het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [ vormen toestemmingendocumentatie ](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Om CMK voor ver*halen-ontvangen instanties van het Platform toe te laten, moet uw [[!DNL Azure]  Zeer belangrijke vault ](./azure-key-vault-config.md) met de volgende montages worden gevormd:

* [ laat purgebescherming ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection) toe
* [ laat zachte schrapping ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) toe
* [ vorm toegang gebruikend  [!DNL Azure]  op rol-gebaseerde toegangscontrole ](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Vorm een  [!DNL Azure]  Zeer belangrijke vault](./azure-key-vault-config.md)

## De CMK-toepassing instellen {#register-app}

Nadat u uw sleutelkluis hebt gevormd, is de volgende stap voor de toepassing te registreren CMK die aan uw [!DNL Azure] huurder zal verbinden.

### Aan de slag

Voor het registreren van de CMK-toepassing moet u oproepen doen naar platform-API&#39;s. Voor details op hoe te om de vereiste authentificatiekopballen te verzamelen om deze vraag te maken, zie de [ API van het Platform authentificatiegids ](../../../api-authentication.md).

Hoewel de verificatiegids instructies bevat over het genereren van uw eigen unieke waarde voor de vereiste `x-api-key` aanvraagheader, gebruiken alle API-bewerkingen in deze handleiding in plaats daarvan de statische waarde `acp_provisioning` . U moet echter wel uw eigen waarden opgeven voor `{ACCESS_TOKEN}` en `{ORG_ID}` .

In alle API-aanroepen die in deze handleiding worden weergegeven, wordt `platform.adobe.io` gebruikt als het hoofdpad, dat standaard overeenkomt met het VA7-gebied. Als uw organisatie een ander gebied gebruikt, moet `platform` worden gevolgd door een streepje en de regiocode die aan uw organisatie is toegewezen: `nld2` for NLD2 of `aus5` for AUS5 (bijvoorbeeld: `platform-aus5.adobe.io`). Als u het gebied van uw organisatie niet kent, contacteer uw systeembeheerder.

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

**Reactie**

Een geslaagde reactie retourneert een eigenschap `applicationRedirectUrl` die de verificatie-URL bevat.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Kopieer en plak het `applicationRedirectUrl` -adres in een browser om een verificatiedialoogvenster te openen. Selecteer **[!DNL Accept]** om de principal van de CMK-toepassingsservice aan de [!DNL Azure] -gebruiker toe te voegen.

![ de dialoog van het de toestemmingsverzoek van Microsoft met [!UICONTROL Accept] benadrukt.](../../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### De CMK-toepassing toewijzen aan een rol {#assign-to-role}

Navigeer na het voltooien van het verificatieproces terug naar de [!DNL Azure] Key Vault en selecteer **[!DNL Access control]** in de linkernavigatie. Selecteer hier **[!DNL Add]** gevolgd door **[!DNL Add role assignment]** .

![ Microsoft Azure dashboard met [!DNL Add] en [!DNL Add role assignment] benadrukte.](../../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

In het volgende scherm wordt u gevraagd een rol voor deze toewijzing te kiezen. Selecteer **[!DNL Key Vault Crypto Service Encryption User]** voordat u **[!DNL Next]** selecteert om door te gaan.

>[!NOTE]
>
>Als u de laag [!DNL Managed-HSM Key Vault] hebt, moet u de gebruikersrol **[!DNL Managed HSM Crypto Service Encryption User]** selecteren.

![ Microsoft Azure dashboard met [!DNL Key Vault Crypto Service Encryption User] benadrukt.](../../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Kies in het volgende scherm **[!DNL Select members]** om een dialoogvenster te openen in de rechtertrack. Gebruik de zoekbalk om de serviceprincipal voor de CMK-toepassing te zoeken en selecteer deze in de lijst. Selecteer **[!DNL Save]** als u klaar bent.

>[!NOTE]
>
>Als u uw toepassing niet in de lijst kunt vinden, dan is uw de diensthoofd niet in uw huurder goedgekeurd. U kunt controleren of u de juiste rechten hebt door samen te werken met uw [!DNL Azure] -beheerder of -vertegenwoordiger.

## De configuratie van de coderingssleutel op het Experience Platform inschakelen {#send-to-adobe}

Nadat u de CMK-toepassing op [!DNL Azure] hebt geïnstalleerd, kunt u de id van de coderingssleutel naar de Adobe sturen. Selecteer **[!DNL Keys]** in de linkernavigatie, gevolgd door de naam van de sleutel u wilt verzenden.

![ Microsoft Azure dashboard met het [!DNL Keys] voorwerp en de zeer belangrijke benadrukte naam.](../../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecteer de meest recente versie van de sleutel en de detailpagina wordt weergegeven. Van hier, kunt u naar keuze de toegelaten verrichtingen voor de sleutel vormen.

>[!IMPORTANT]
>
>De minimaal vereiste bewerkingen die voor de toets zijn toegestaan, zijn de machtigingen **[!DNL Wrap Key]** en **[!DNL Unwrap Key]** . U kunt [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] en [!DNL Verify] desgewenst opnemen.

In het veld **[!UICONTROL Key Identifier]** wordt de URI-id voor de sleutel weergegeven. Kopieer deze URI-waarde voor gebruik in de volgende stap.

![ Microsoft Azure Belangrijkste details van het dashboard met [!DNL Permitted operations] en de benadrukt secties van de exemplaarsleutel URL.](../../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

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
| `name` | Een naam voor de configuratie. Zorg ervoor dat u deze waarde herinnert aangezien het wordt vereist om de status van de configuratie bij a [ later stap ](#check-status) te controleren. De waarde is hoofdlettergevoelig. |
| `type` | Het configuratietype. Moet worden ingesteld op `BYOK_CONFIG` . |
| `imsOrgId` | Uw organisatie-id. Deze id moet dezelfde waarde hebben als de header `x-gw-ims-org-id` . |
| `configData` | This property contains the following details about the configuration:<ul><li>`providerType` : moet worden ingesteld op `AZURE_KEYVAULT` .</li><li>`keyVaultKeyIdentifier`: De belangrijkste kluis URI die u [ vroeger ](#send-to-adobe) kopieerde.</li></ul> |

+++

**Reactie**

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

U moet `name` van de configuratie toevoegen u aan de weg (`config1` in het voorbeeld hieronder) wilt controleren en een `configType` vraagparameter omvatten die aan `BYOK_CONFIG` wordt geplaatst.

+++ Een steekproefverzoek om de status van het configuratieverzoek te controleren.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Reactie**

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

Het kenmerk `status` kan een van vier waarden hebben met de volgende betekenissen:

1. `RUNNING`: hiermee wordt gevalideerd dat Platform toegang heeft tot de sleutel- en sleutelvault.
1. `UPDATE_EXISTING_RESOURCES`: het systeem voegt de sleutelvault en sleutelnaam aan de datastores over alle zandbakken in uw organisatie toe.
1. `COMPLETED`: De sleutelvault en sleutelnaam zijn toegevoegd aan de datastores.
1. `FAILED`: Er heeft zich een probleem voorgedaan dat voornamelijk te maken heeft met de toepassingsinstellingen voor de toepassing key, key vault of multi-agent.

## Volgende stappen

Door de bovenstaande stappen te voltooien, hebt u CMK voor uw organisatie ingeschakeld. Voor Azure-gehoste platforminstanties worden gegevens die in primaire gegevensopslagruimten worden ingevoerd, nu gecodeerd en gedecodeerd met de sleutel(s) in de [!DNL Azure] Key Vault.

Meer over gegevensencryptie in Adobe Experience Platform leren, zie de [ encryptiedocumentatie ](../../encryption.md).
