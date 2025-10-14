---
title: Een Azure Key Vault configureren voor door de klant beheerde sleutels
description: Leer hoe u een nieuwe bedrijfsaccount maakt met Azure of een bestaande bedrijfsaccount gebruikt en de Key Vault maakt.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c920f78363ee5f040964dbd3a0d0815474094b07
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Een [!DNL Azure] Key Vault configureren voor door de klant beheerde toetsen

CMK (Customer Managed Keys) ondersteunt toetsen van zowel [!DNL Microsoft Azure] Key Vaults als AWS [!DNL Key Management Service (KMS)] . Als uw implementatie wordt gehost op [!DNL Azure] , voert u de onderstaande stappen uit om een Key Vault te maken. Voor AWS-ontvangen implementaties, verwijs naar de [&#x200B; de configuratiegids van AWS KMS &#x200B;](../aws/configure-kms.md).

>[!IMPORTANT]
>
>Alleen de Standard-, Premium- en Managed HSM-lagen voor [!DNL Azure] Key Vault worden ondersteund. [!DNL Azure Dedicated HSM] en [!DNL Azure Payments HSM] worden niet ondersteund. Verwijs naar de [[!DNL Azure]  documentatie &#x200B;](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) voor meer informatie over de aangeboden zeer belangrijke beheersdiensten.

>[!NOTE]
>
>In de onderstaande documentatie worden alleen de basisstappen beschreven voor het maken van de Key Vault. Buiten deze richtlijnen dient u de Key Vault te configureren volgens het beleid van uw organisatie.

Meld u aan bij de portal [!DNL Azure] en zoek **[!DNL Key vaults]** onder de lijst met services op met de zoekbalk.

![&#x200B; de onderzoekseigenschap in [!DNL Microsoft Azure] met [!DNL Key vaults] benadrukt in de onderzoeksresultaten.](../../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

De pagina **[!DNL Key vaults]** wordt weergegeven nadat u de service hebt geselecteerd. Selecteer **[!DNL Create]** van hier.

![&#x200B; het [!DNL Key vaults] dashboard in [!DNL Microsoft Azure] met [!DNL Create] benadrukte.](../../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Vul met het meegeleverde formulier de basisgegevens voor de Key Vault in, inclusief een naam en een toegewezen bronnengroep.

>[!WARNING]
>
>Terwijl de meeste opties als hun standaardwaarden kunnen worden verlaten, **zorg ervoor dat u de zachte schrapping en zuiveringsbeschermingsopties** toelaat. Als u deze functies niet inschakelt, loopt u het risico dat de toegang tot uw gegevens verloren gaat als de Key Vault wordt verwijderd.
>
>![&#x200B; het [!DNL Microsoft Azure] [!DNL Create a Key Vault] werkschema met de zachte benadrukte schrapping en zuiveringsbescherming.](../../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Hierna doorloopt u de workflow voor het maken van de Key Vault en configureert u de verschillende opties volgens het beleid van uw organisatie.

Zodra u de stap **[!DNL Review + create]** hebt ontvangen, kunt u de details van de Key Vault controleren terwijl de validatie wordt doorlopen. Als de validatie eenmaal is voltooid, selecteert u **[!DNL Create]** om het proces te voltooien.

![&#x200B; Microsoft Azure Zeer belangrijke het Overzicht en creeer pagina met Create benadrukt.](../../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Toegang configureren {#configure-access}

Schakel vervolgens Azure op rol gebaseerd toegangsbeheer voor uw sleutelkluis in. Selecteer **[!DNL Access configuration]** in de [!DNL Settings] -sectie van de linkernavigatie en selecteer **[!DNL Azure role-based access control]** om de instelling in te schakelen. Deze stap is van essentieel belang omdat de CMK-app later moet worden gekoppeld aan een Azure-rol. Het toewijzen van een rol wordt gedocumenteerd in zowel [&#x200B; API &#x200B;](./api-set-up.md#assign-to-role) als [&#x200B; UI &#x200B;](./ui-set-up.md#assign-to-role) werkschema&#39;s.

![&#x200B; het [!DNL Microsoft Azure] dashboard met [!DNL Access configuration] en [!DNL Azure role-based access control] benadrukte.](../../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Netwerkopties configureren {#configure-network-options}

Als uw Key Vault is geconfigureerd om de toegang van het publiek tot bepaalde virtuele netwerken te beperken of om de toegang van het publiek volledig uit te schakelen, moet u [!DNL Microsoft] een firewalluitzondering toestaan.

Selecteer **[!DNL Networking]** in de linkernavigatie. Selecteer onder **[!DNL Firewalls and virtual networks]** het selectievakje **[!DNL Allow trusted Microsoft services to bypass this firewall]** en selecteer vervolgens **[!DNL Apply]** .

>[!NOTE]
>
>Als uw sleutelkluis beperkte netwerktoegang gebruikt, adviseert Adobe dat u het volgende statische IP adres toevoegt: `20.88.123.53`. Door dit IP-adres toe te voegen, kunnen Adobe-services de connectiviteit beter controleren en waarschuwingen op het platform geven wanneer toegangsproblemen worden gedetecteerd.
>
>Om meer over te leren wanneer om het IP van Adobe adres te lijsten van gewenste personen, hoe het alarm werkt, en hoe te aan zeer belangrijke berichten van de toegangsmislukking antwoorden, zie [&#x200B; Alarm en IP Toegang voor Azure CMK &#x200B;](./alerts-and-ip-access.md) vormen.
>
>Als uw sleutelkluis reeds wordt gevormd om openbare netwerktoegang toe te staan, wordt geen verdere actie vereist.

![&#x200B; het [!DNL Networking] lusje van [!DNL Microsoft Azure] met [!DNL Networking] en [!DNL Allow trusted Microsoft surfaces to bypass this firewall] benadrukte uitzondering.](../../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Een sleutel genereren {#generate-a-key}

Nadat u een Key Vault hebt gemaakt, kunt u een nieuwe sleutel genereren. Navigeer naar de tab **[!DNL Keys]** en selecteer **[!DNL Generate/Import]** .

![&#x200B; het [!DNL Keys] lusje van [!DNL Azure] met [!DNL Generate import] benadrukt.](../../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Gebruik de verstrekte vorm om een naam voor de sleutel te verstrekken, en of **RSA** of **RSA-HSM** voor het zeer belangrijke type te selecteren. Voor [!DNL Azure] - ontvangen implementaties, moet **[!DNL RSA key size]** minstens **3072** beetjes zijn zoals vereist voor [!DNL Azure Cosmos DB]. [!DNL Azure Data Lake Storage] is ook compatibel met RSA 3027.

>[!NOTE]
>
>Onthoud de naam die u voor de sleutel opgeeft, omdat deze nodig is om de sleutel naar Adobe te verzenden.

Gebruik de resterende besturingselementen om de sleutel te configureren die u naar wens wilt genereren of importeren. Selecteer **[!DNL Create]** als u klaar bent.

![&#x200B; het [!DNL Create a key] dashboard met [!DNL 3072] benadrukte beetjes.](../../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

De geconfigureerde sleutel wordt weergegeven in de lijst met toetsen voor de vault.

![&#x200B; de [!DNL Keys] werkruimte met de zeer belangrijke benadrukte naam.](../../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Volgende stappen

Volg de installatiehandleidingen voor de hostingomgeving van uw platform om het eenmalige proces voor het instellen van de door de klant beheerde sleutels voort te zetten:

- Voor [!DNL Azure], gebruik [&#x200B; API &#x200B;](./api-set-up.md) of [&#x200B; UI &#x200B;](./ui-set-up.md) opstellingsgidsen.
- Voor AWS, verwijs naar [&#x200B; AWS vormt KMS gids &#x200B;](../aws/configure-kms.md) en de [&#x200B; UI opstellingsgids &#x200B;](../aws/ui-set-up.md).
