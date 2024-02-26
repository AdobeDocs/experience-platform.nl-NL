---
title: Een Azure Key Vault configureren
description: Leer hoe u een nieuwe bedrijfsaccount maakt met Azure of een bestaande bedrijfsaccount gebruikt en de Key Vault maakt.
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Een [!DNL Azure] Key Vault

Door de klant beheerde toetsen (CMK) ondersteunen alleen toetsen van een [!DNL Microsoft Azure] Key Vault. Om aan de slag te gaan, moet u werken met [!DNL Azure] om een nieuwe bedrijfsaccount te maken, of gebruik een bestaande bedrijfsaccount en volg de onderstaande stappen om de Key Vault te maken.

>[!IMPORTANT]
>
>Alleen de Standard-, Premium- en Managed HSM-lagen voor [!DNL Azure] Key Vault wordt ondersteund. [!DNL Azure Dedicated HSM] en [!DNL Azure Payments HSM] worden niet ondersteund. Zie de [[!DNL Azure] documentatie](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) voor meer informatie over de aangeboden services voor sleutelbeheer.

>[!NOTE]
>
>In de onderstaande documentatie worden alleen de basisstappen beschreven voor het maken van de Key Vault. Buiten deze richtlijnen dient u de Key Vault te configureren volgens het beleid van uw organisatie.

Aanmelden bij de [!DNL Azure] openen en de zoekbalk gebruiken om te zoeken naar **[!DNL Key vaults]** onder de lijst van diensten.

![De zoekfunctie in [!DNL Microsoft Azure] with [!DNL Key vaults] gemarkeerd in de zoekresultaten.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

De **[!DNL Key vaults]** wordt weergegeven nadat u de service hebt geselecteerd. Van hier, selecteer **[!DNL Create]**.

![De [!DNL Key vaults] dashboard in [!DNL Microsoft Azure] with [!DNL Create] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Vul met het meegeleverde formulier de basisgegevens voor de Key Vault in, inclusief een naam en een toegewezen bronnengroep.

>[!WARNING]
>
>Hoewel de meeste opties als standaardwaarden kunnen worden gelaten, **zorg ervoor dat u de opties voor het verwijderen en wissen van de software inschakelt**. Als u deze functies niet inschakelt, loopt u het risico dat de toegang tot uw gegevens verloren gaat als de Key Vault wordt verwijderd.
>
>![De [!DNL Microsoft Azure] [!DNL Create a Key Vault] workflow met soft delete en purge protection gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

Hierna doorloopt u de workflow voor het maken van de Key Vault en configureert u de verschillende opties volgens het beleid van uw organisatie.

Zodra u bij **[!DNL Review + create]** U kunt de details van de Key Vault controleren tijdens de validatie. Selecteer **[!DNL Create]** om het proces te voltooien.

![Microsoft Azure Key vaults Review en creeer pagina met Create gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Toegang configureren {#configure-access}

Schakel vervolgens Azure op rol gebaseerd toegangsbeheer voor uw sleutelkluis in. Selecteren **[!DNL Access configuration]** in de [!DNL Settings] van de linkernavigatie en selecteer vervolgens **[!DNL Azure role-based access control]** om de instelling in te schakelen. Deze stap is van essentieel belang omdat de CMK-app later moet worden gekoppeld aan een Azure-rol. Het toewijzen van een rol wordt gedocumenteerd in zowel de [API](./api-set-up.md#assign-to-role) en [UI](./ui-set-up.md#assign-to-role) workflows.

![De [!DNL Microsoft Azure] dashboard met [!DNL Access configuration] en [!DNL Azure role-based access control] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Netwerkopties configureren {#configure-network-options}

Als uw Key Vault is geconfigureerd om de toegang van het publiek tot bepaalde virtuele netwerken te beperken of om de toegang van het publiek volledig uit te schakelen, moet u [!DNL Microsoft] een firewalluitzondering.

Selecteren **[!DNL Networking]** in de linkernavigatie. Onder **[!DNL Firewalls and virtual networks]**, selecteert u het selectievakje **[!DNL Allow trusted Microsoft services to bypass this firewall]** selecteert u vervolgens **[!DNL Apply]**.

![De [!DNL Networking] tabblad van [!DNL Microsoft Azure] with [!DNL Networking] en [!DNL Allow trusted Microsoft surfaces to bypass this firewall] gemarkeerde uitzondering.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Een sleutel genereren {#generate-a-key}

Nadat u een Key Vault hebt gemaakt, kunt u een nieuwe sleutel genereren. Ga naar de **[!DNL Keys]** en selecteert u **[!DNL Generate/Import]**.

![De [!DNL Keys] tabblad van [!DNL Azure] with [!DNL Generate import] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Gebruik het opgegeven formulier om een naam voor de sleutel op te geven en selecteer een van de volgende **RSA** of **RSA-HSM** voor het toetstype. De **[!DNL RSA key size]** moet ten minste **3072** bits zoals vereist door [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] is ook compatibel met RSA 3027.

>[!NOTE]
>
>Onthoud de naam die u voor de sleutel opgeeft, omdat deze nodig is om de sleutel naar de Adobe te verzenden.

Gebruik de resterende besturingselementen om de sleutel te configureren die u naar wens wilt genereren of importeren. Selecteer **[!DNL Create]**.

![De [!DNL Create a key] dashboard met [!DNL 3072] bits gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

De geconfigureerde sleutel wordt weergegeven in de lijst met toetsen voor de vault.

![De [!DNL Keys] werkruimte met de sleutelnaam gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Volgende stappen

Om het eenmalig proces voor vestiging de klant-geleide sleuteleigenschap voort te zetten, ga met of verder [API](./api-set-up.md) of [UI](./ui-set-up.md) door de klant beheerde handleidingen voor het instellen van sleutels.
