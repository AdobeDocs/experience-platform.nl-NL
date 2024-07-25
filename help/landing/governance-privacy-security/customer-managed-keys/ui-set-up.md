---
title: Door de klant beheerde toetsen instellen en configureren met behulp van de interface van het platform
description: Leer hoe u uw CMK-app instelt met uw Azure-medewerker en uw coderingssleutel-id verzendt naar Adobe Experience Platform.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# De opstelling en vormt klant-geleide sleutels gebruikend Platform UI

Dit document behandelt het proces voor het toelaten van de klant-geleide sleuteleigenschap (CMK) in Platform gebruikend UI. Voor instructies op hoe te om dit proces te voltooien gebruikend API, verwijs naar het [ API CMK opstellingsdocument ](./api-set-up.md).

## Vereisten

Als u de sectie [!UICONTROL Encryption] in Adobe Experience Platform wilt weergeven en bezoeken, moet u een rol hebben gemaakt en [!UICONTROL Manage Customer Managed Key] toestemming aan die rol hebben toegewezen. Elke gebruiker met de machtiging [!UICONTROL Manage Customer Managed Key] kan CMK inschakelen voor zijn of haar organisatie.

Voor meer informatie bij het toewijzen van rollen en toestemmingen in Experience Platform, verwijs naar [ vormen toestemmingendocumentatie ](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Om CMK toe te laten, moet uw [[!DNL Azure]  Zeer belangrijke vault ](./azure-key-vault-config.md) met de volgende montages worden gevormd:

* [ laat purgebescherming ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection) toe
* [ laat zachte schrapping ](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview) toe
* [ vorm toegang gebruikend  [!DNL Azure]  op rol-gebaseerde toegangscontrole ](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Vorm een  [!DNL Azure]  Zeer belangrijke vault](./azure-key-vault-config.md)

## De CMK-toepassing instellen {#register-app}

Nadat u uw sleutelkluis hebt gevormd, is de volgende stap de toepassing te registreren CMK die aan uw [!DNL Azure] huurder zal verbinden.

### Aan de slag

Als u het dashboard van [!UICONTROL Encryption configurations] wilt weergeven, selecteert u **[!UICONTROL Encryption]** onder de kop [!UICONTROL Administration] van het linkernavigatiezijpaneel.

![ het dashboard van de Configuratie van de Encryptie met Versleuteling en de Klant Beheerde Sleutelkaart benadrukte.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Selecteer **[!UICONTROL Configure]** om de weergave [!UICONTROL Customer Managed Keys configuration] te openen. Deze werkruimte bevat alle vereiste waarden om de hieronder beschreven stappen te voltooien en de integratie met uw Azure Key-kluis uit te voeren.

### URL van verificatie kopiëren {#copy-authentication-url}

Als u het registratieproces wilt starten, kopieert u de URL van de toepassingsverificatie voor uw organisatie vanuit de [!UICONTROL Customer Managed Keys configuration] -weergave en plakt u deze in uw [!DNL Azure] -omgeving **[!DNL Key Vault Crypto Service Encryption User]** . De details op hoe te om [ een rol ](#assign-to-role) toe te wijzen worden verstrekt in de volgende sectie.

Selecteer het exemplaarpictogram (![ het exemplaarpictogram.](/help/images/icons/copy.png) ) door de [!UICONTROL Application authentication url] .

![ de [!UICONTROL Customer Managed Keys configuration] mening met de benadrukte sectie van de de authentificatieurl van de Toepassing.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Kopieer en plak de [!UICONTROL Application authentication url] in een browser om een verificatiedialoogvenster te openen. Selecteer **[!DNL Accept]** om de principal van de CMK-toepassingsservice aan de [!DNL Azure] -gebruiker toe te voegen. Bevestigend leidt de authentificatie u aan de Experience Cloud het landen pagina opnieuw.

![ de dialoog van het de toestemmingsverzoek van Microsoft met [!UICONTROL Accept] benadrukt.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Als u meerdere [!DNL Microsoft Azure] -abonnementen hebt, kunt u mogelijk een verbinding maken tussen de instantie Platform en de verkeerde sleutelkluis. In dit geval moet u het gedeelte `common` van de URL-naam voor toepassingsverificatie vervangen door de CMK-directory-id.<br> Kopieer CMK folderidentiteitskaart van de Poortmontages, de Folders, en de pagina van Abonnementen van de [!DNL Microsoft Azure] toepassing <br>![ de [!DNL Microsoft Azure] montages van het toepassingsPortaal, de Folders en de pagina van Abonnementen met benadrukte identiteitskaart van de Folder.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br> daarna, kleef het in uw browser adresbar.<br>![ browser van Google browser van met de &quot;gemeenschappelijke&quot;sectie van de benadrukte de authentificatieurl van de Toepassing.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### De CMK-toepassing toewijzen aan een rol {#assign-to-role}

Navigeer na het voltooien van het verificatieproces terug naar de [!DNL Azure] Key Vault en selecteer **[!DNL Access control]** in de linkernavigatie. Selecteer hier **[!DNL Add]** gevolgd door **[!DNL Add role assignment]** .

![ het [!DNL Microsoft Azure] dashboard met [!DNL Add] en [!DNL Add role assignment] benadrukte.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

In het volgende scherm wordt u gevraagd een rol voor deze toewijzing te kiezen. Selecteer **[!DNL Key Vault Crypto Service Encryption User]** voordat u **[!DNL Next]** selecteert om door te gaan.

>[!NOTE]
>
>Als u de laag [!DNL Managed-HSM Key Vault] hebt, moet u de gebruikersrol **[!DNL Managed HSM Crypto Service Encryption User]** selecteren.

![ het [!DNL Microsoft Azure] dashboard met [!DNL Key Vault Crypto Service Encryption User] benadrukte.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Kies in het volgende scherm **[!DNL Select members]** om een dialoogvenster te openen in de rechtertrack. Gebruik de zoekbalk om de serviceprincipal voor de CMK-toepassing te zoeken en selecteer deze in de lijst. Selecteer **[!DNL Save]** als u klaar bent.

>[!NOTE]
>
>Als u uw toepassing niet in de lijst kunt vinden, dan is uw de diensthoofd niet in uw huurder goedgekeurd. U kunt controleren of u de juiste rechten hebt door samen te werken met uw [!DNL Azure] -beheerder of -vertegenwoordiger.

U kunt de toepassing verifiëren door de [!UICONTROL Application ID] in de [!UICONTROL Customer Managed Keys configuration] weergave te vergelijken met de [!DNL Application ID] in het [!DNL Microsoft Azure] -toepassingsoverzicht.

![ de [!UICONTROL Customer Managed Keys configuration] mening met [!UICONTROL Application ID] benadrukte.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Alle details noodzakelijk om Azure hulpmiddelen te verifiëren zijn inbegrepen in de UI van het Platform. Dit niveau van granulariteit wordt verstrekt aangezien vele gebruikers andere Azure hulpmiddelen willen gebruiken om hun capaciteit te verbeteren om deze toepassingen toegang tot hun zeer belangrijke kluis te controleren en te registreren. Kennis van deze id&#39;s is voor dat doel van essentieel belang en om Adobe-services te helpen toegang te krijgen tot de sleutel.

## De configuratie van de coderingssleutel op het Experience Platform inschakelen {#send-to-adobe}

Nadat u de CMK-toepassing op [!DNL Azure] hebt geïnstalleerd, kunt u de id van de coderingssleutel naar de Adobe sturen. Selecteer **[!DNL Keys]** in de linkernavigatie, gevolgd door de naam van de sleutel u wilt verzenden.

![ Microsoft Azure dashboard met het [!DNL Keys] voorwerp en de zeer belangrijke benadrukte naam.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Selecteer de meest recente versie van de sleutel en de detailpagina wordt weergegeven. Van hier, kunt u naar keuze de toegelaten verrichtingen voor de sleutel vormen.

>[!IMPORTANT]
>
>De minimaal vereiste bewerkingen die voor de toets zijn toegestaan, zijn de machtigingen **[!DNL Wrap Key]** en **[!DNL Unwrap Key]** . U kunt [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] en [!DNL Verify] desgewenst opnemen.

In het veld **[!UICONTROL Key Identifier]** wordt de URI-id voor de sleutel weergegeven. Kopieer deze URI-waarde voor gebruik in de volgende stap.

![ Microsoft Azure Belangrijkste details van het dashboard met [!DNL Permitted operations] en de benadrukt secties van de exemplaarsleutel URL.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Wanneer u de instructie [!DNL Key vault URI] hebt gekregen, gaat u terug naar de [!UICONTROL Customer Managed Keys configuration] -weergave en voert u een beschrijving in **[!UICONTROL Configuration name]** . Voeg vervolgens de [!DNL Key Identifier] toe die u van de detailpagina Azure Key hebt genomen in de **[!UICONTROL Key vault key identifier]** en selecteer **[!UICONTROL  Save]** .

![ de [!UICONTROL Customer Managed Keys configuration] mening met [!UICONTROL Configuration name] en [!UICONTROL Key vault key identifier] benadrukte secties.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

U wordt teruggestuurd naar de map [!UICONTROL Encryption configurations dashboard] . De status van de [!UICONTROL Customer Managed Keys] -configuratie wordt weergegeven als [!UICONTROL Processing] .

![ het [!UICONTROL Encryption configurations] dashboard met [!UICONTROL Processing] op de [!UICONTROL Customer Managed Keys] kaart wordt benadrukt.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## De status van de configuratie controleren {#check-status}

Zorg voor een aanzienlijke hoeveelheid verwerkingstijd. Als u de status van de configuratie wilt controleren, gaat u terug naar de [!UICONTROL Customer Managed Keys configuration] -weergave en schuift u omlaag naar de [!UICONTROL Configuration status] -weergave. Op de voortgangsbalk kunt u stap één van de drie gebruiken. Hierin wordt uitgelegd dat het systeem controleert of Platform toegang heeft tot de sleutel- en sleutelvault.

Er zijn vier mogelijke statussen van de CMK-configuratie. Deze zijn als volgt:

* Stap 1: Valideert dat het Platform toegang heeft tot de sleutel- en sleutelvault.
* Stap 2: De belangrijkste vault en belangrijkste naam zijn in proces om aan alle datastores over uw organisatie worden toegevoegd.
* Stap 3: De sleutelvault en sleutelnaam zijn met succes toegevoegd aan de datastores.
* `FAILED`: Er heeft zich een probleem voorgedaan dat voornamelijk te maken heeft met de toepassingsinstellingen voor de toepassing key, key vault of multi-agent.

## Volgende stappen

Door de bovenstaande stappen te voltooien, hebt u CMK voor uw organisatie ingeschakeld. Gegevens die in de primaire gegevensopslagruimten worden ingevoerd, worden nu gecodeerd en ontsleuteld met de sleutel(s) in de [!DNL Azure] Key Vault.
