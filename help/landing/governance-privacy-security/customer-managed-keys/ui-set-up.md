---
title: Door de klant beheerde toetsen instellen en configureren met behulp van de interface van het platform
description: Leer hoe u uw CMK-app instelt met uw Azure-medewerker en uw coderingssleutel-id verzendt naar Adobe Experience Platform.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# De opstelling en vormt klant-geleide sleutels gebruikend Platform UI

Dit document behandelt het proces voor het toelaten van de klant-geleide sleuteleigenschap (CMK) in Platform gebruikend UI. Raadpleeg voor instructies over het voltooien van dit proces met de API de [API CMK-instellingendocument](./api-set-up.md).

## Vereisten

Ga naar de [!UICONTROL Encryption] in Adobe Experience Platform moet u een rol hebben gemaakt en de [!UICONTROL Manage Customer Managed Key] toestemming voor die rol. Om het even welke gebruiker die heeft [!UICONTROL Manage Customer Managed Key] U kunt CMK inschakelen voor hun organisatie.

Voor meer informatie over het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [machtigingendocumentatie configureren](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Als u CMK wilt inschakelen, moet u [[!DNL Azure] Key Vault moet worden geconfigureerd](./azure-key-vault-config.md) met de volgende instellingen:

* [Reinigingsbeveiliging inschakelen](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [soft-delete inschakelen](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Toegang configureren met [!DNL Azure] rolgebaseerd toegangsbeheer](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Een [!DNL Azure] Key Vault](./azure-key-vault-config.md)

## De CMK-toepassing instellen {#register-app}

Nadat u de sleutelkluis hebt geconfigureerd, bestaat de volgende stap uit het registreren van de CMK-toepassing die een koppeling naar uw [!DNL Azure] huurder.

### Aan de slag

Als u het dialoogvenster [!UICONTROL Encryption configurations] dashboard, selecteren **[!UICONTROL Encryption]** onder de [!UICONTROL Administration] kop van de linkernavigatiebalk.

![Het dashboard Coderingsconfiguratie met codering en de door de klant beheerde toetsenbordkaart gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Selecteren **[!UICONTROL Configure]** om de [!UICONTROL Customer Managed Keys configuration] weergeven. Deze werkruimte bevat alle vereiste waarden om de hieronder beschreven stappen te voltooien en de integratie met uw Azure Key-kluis uit te voeren.

### URL van verificatie kopiëren {#copy-authentication-url}

Als u het registratieproces wilt starten, kopieert u de URL van de toepassingsverificatie voor uw organisatie vanuit de [!UICONTROL Customer Managed Keys configuration] weergeven en plakken in uw [!DNL Azure] milieu **[!DNL Key Vault Crypto Service Encryption User]**. Details over hoe [een rol toewijzen](#assign-to-role) in de volgende sectie.

Selecteer het pictogram Kopiëren (![Het kopieerpictogram.](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png)) door de [!UICONTROL Application authentication url].

![De [!UICONTROL Customer Managed Keys configuration] weergave met de sectie URL voor toepassingsverificatie gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Kopieer en plak de [!UICONTROL Application authentication url] in een browser om een verificatiedialoogvenster te openen. Selecteren **[!DNL Accept]** om de CMK-toepassingsserviceprincipal toe te voegen aan uw [!DNL Azure] huurder. Bevestigend leidt de authentificatie u aan de Experience Cloud het landen pagina opnieuw.

![Een dialoogvenster voor Microsoft-machtigingsaanvragen met [!UICONTROL Accept] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Als u meerdere [!DNL Microsoft Azure] abonnementen, dan kon u uw instantie van het Platform aan de verkeerde zeer belangrijke kluis potentieel verbinden. In deze situatie moet u de `common` van de naam van de URL voor toepassingsverificatie voor de CMK-directory-id.<br>Kopieer de CMK-directory-id van de pagina Portal-instellingen, -directory&#39;s en -abonnementen van het dialoogvenster [!DNL Microsoft Azure] toepassing<br>![De [!DNL Microsoft Azure] de montages, de Folders en de pagina van Abonnementen van het toepassingsportaal met benadrukte identiteitskaart van de Folder.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Vervolgens plakt u deze in de adresbalk van de browser.<br>![Een Google-browserpagina met de sectie &#39;common&#39; van de URL voor toepassingsverificatie gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### De CMK-toepassing toewijzen aan een rol {#assign-to-role}

Navigeer na het voltooien van het verificatieproces terug naar uw [!DNL Azure] Key Vault en selecteer **[!DNL Access control]** in de linkernavigatie. Van hier, selecteer **[!DNL Add]** gevolgd door **[!DNL Add role assignment]**.

![De [!DNL Microsoft Azure] dashboard met [!DNL Add] en [!DNL Add role assignment] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

In het volgende scherm wordt u gevraagd een rol voor deze toewijzing te kiezen. Selecteren **[!DNL Key Vault Crypto Service Encryption User]** voordat u selecteert **[!DNL Next]** om door te gaan.

>[!NOTE]
>
>Als u de [!DNL Managed-HSM Key Vault] laag, dan moet u selecteren **[!DNL Managed HSM Crypto Service Encryption User]** gebruikersrol.

![De [!DNL Microsoft Azure] dashboard met de [!DNL Key Vault Crypto Service Encryption User] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Kies in het volgende scherm **[!DNL Select members]** een dialoog op gang te brengen in het rechterspoor . Gebruik de zoekbalk om de serviceprincipal voor de CMK-toepassing te zoeken en selecteer deze in de lijst. Selecteer **[!DNL Save]**.

>[!NOTE]
>
>Als u uw toepassing niet in de lijst kunt vinden, dan is uw de diensthoofd niet in uw huurder goedgekeurd. Om ervoor te zorgen dat u de juiste rechten hebt, werkt u samen met uw [!DNL Azure] beheerder of vertegenwoordiger.

U kunt de toepassing controleren door de [!UICONTROL Application ID] op de [!UICONTROL Customer Managed Keys configuration] met de [!DNL Application ID] op de [!DNL Microsoft Azure] toepassingsoverzicht.

![De [!UICONTROL Customer Managed Keys configuration] met de [!UICONTROL Application ID] gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Alle details noodzakelijk om Azure hulpmiddelen te verifiëren zijn inbegrepen in de UI van het Platform. Dit niveau van granulariteit wordt verstrekt aangezien vele gebruikers andere Azure hulpmiddelen willen gebruiken om hun capaciteit te verbeteren om deze toepassingen toegang tot hun zeer belangrijke kluis te controleren en te registreren. Kennis van deze id&#39;s is voor dat doel van essentieel belang en om Adobe-services te helpen toegang te krijgen tot de sleutel.

## De configuratie van de coderingssleutel op het Experience Platform inschakelen {#send-to-adobe}

Nadat u de CMK-toepassing hebt geïnstalleerd op [!DNL Azure], kunt u de id van de coderingssleutel naar de Adobe verzenden. Selecteren **[!DNL Keys]** in de linkernavigatie, gevolgd door de naam van de sleutel u wilt verzenden.

![Het Microsoft Azure-dashboard met de [!DNL Keys] en de sleutelnaam gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecteer de meest recente versie van de sleutel en de detailpagina wordt weergegeven. Van hier, kunt u naar keuze de toegelaten verrichtingen voor de sleutel vormen.

>[!IMPORTANT]
>
>De minimaal vereiste bewerkingen voor de toets zijn: **[!DNL Wrap Key]** en **[!DNL Unwrap Key]** machtigingen. U kunt [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], en [!DNL Verify] zou u willen.

De **[!UICONTROL Key Identifier]** wordt de URI-id voor de sleutel weergegeven. Kopieer deze URI-waarde voor gebruik in de volgende stap.

![De Microsoft Azure-dashboard Belangrijke informatie met de [!DNL Permitted operations] en de URL-secties van de kopieersleutel zijn gemarkeerd.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Wanneer u de [!DNL Key vault URI], terug naar de [!UICONTROL Customer Managed Keys configuration] weergeven en een beschrijving invoeren **[!UICONTROL Configuration name]**. Voeg vervolgens de [!DNL Key Identifier] van de detailpagina Azure Key naar de **[!UICONTROL Key vault key identifier]** en selecteert u **[!UICONTROL  Save]**.

![De [!UICONTROL Customer Managed Keys configuration] met de [!UICONTROL Configuration name] en de [!UICONTROL Key vault key identifier] gemarkeerde secties.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

U bent teruggekeerd aan [!UICONTROL Encryption configurations dashboard]. De status van de [!UICONTROL Customer Managed Keys] configuratie wordt weergegeven als [!UICONTROL Processing].

![De [!UICONTROL Encryption configurations] dashboard met [!UICONTROL Processing] op de [!UICONTROL Customer Managed Keys] kaart.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## De status van de configuratie controleren {#check-status}

Zorg voor een aanzienlijke hoeveelheid verwerkingstijd. Ga terug naar de [!UICONTROL Customer Managed Keys configuration] weergeven en omlaag schuiven naar de [!UICONTROL Configuration status]. Op de voortgangsbalk kunt u stap één van de drie gebruiken. Hierin wordt uitgelegd dat het systeem controleert of Platform toegang heeft tot de sleutel- en sleutelvault.

Er zijn vier mogelijke statussen van de CMK-configuratie. Deze zijn als volgt:

* Stap 1: Valideert dat het Platform toegang heeft tot de sleutel- en sleutelvault.
* Stap 2: De belangrijkste vault en belangrijkste naam zijn in proces om aan alle datastores over uw organisatie worden toegevoegd.
* Stap 3: De sleutelvault en sleutelnaam zijn met succes toegevoegd aan de datastores.
* `FAILED`: Er is een probleem opgetreden, dat voornamelijk te maken heeft met de toepassingsinstellingen van de toepassing key, key vault of multi-huurder.

## Volgende stappen

Door de bovenstaande stappen te voltooien, hebt u CMK voor uw organisatie ingeschakeld. Gegevens die in de primaire gegevensopslag worden ingevoerd, worden nu gecodeerd en gedecodeerd met de sleutel(s) in de [!DNL Azure] Key Vault.
