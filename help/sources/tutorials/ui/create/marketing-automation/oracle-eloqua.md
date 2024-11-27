---
title: Een Eloqua-bronverbinding voor Oracles maken met behulp van Platform UI
description: Leer hoe u Adobe Experience Platform kunt verbinden met Oracle Eloqua via de interface van het platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Een [!DNL Oracle Eloqua] bronverbinding maken met behulp van platforminterface

>[!WARNING]
>
>De bron [!DNL Oracle Eloqua] wordt eind juni 2025 vervangen.

Deze zelfstudie bevat stappen voor het maken van een [!DNL Oracle Eloqua] -bronverbinding met de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Platform:

* [ Bronnen ](../../../../home.md): Het platform staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend de diensten van het Platform.
* [ Sandboxes ](../../../../../sandboxes/home.md): Het platform verstrekt virtuele zandbakken die één enkele instantie van het Platform in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Als u reeds een voor authentiek verklaarde [!DNL Oracle Eloqua] rekening op Platform hebt, dan kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [ creërend een dataflow om de gegevens van de marketing automatisering aan Platform ](../../dataflow/marketing-automation.md) te brengen.

### Vereiste referenties verzamelen

Als u [!DNL Oracle Eloqua] wilt verbinden met Platform, moet u waarden opgeven voor de volgende verificatie-eigenschappen:

| Credentials | Beschrijving |
| --- | --- |
| Endpoint | Het eindpunt van de [!DNL Oracle Eloqua] -server. [!DNL Oracle Eloqua] ondersteunt meerdere datacenters. Om uw eindpunt te vinden, login aan de [[!DNL Oracle Eloqua]  interface ](https://login.eloqua.com) met uw geloofsbrieven en dan het basisURL gedeelte van redirect URL te kopiëren. De notatie voor het URL-patroon is `xxx.xx.eloqua.com` en moet zonder `http` of `https` worden ingevoerd. |
| Gebruikersnaam | De gebruikersnaam van de [!DNL Oracle Eloqua] -server. De gebruikersnaam moet zijn opgemaakt als `siteName + \\ + username` , waarbij `siteName` de bedrijfsnaam is die u hebt gebruikt om u aan te melden bij [!DNL Oracle Eloqua] en `username` de gebruikersnaam is. De gebruikersnaam voor uw aanmelding kan bijvoorbeeld: `Eloqua\Andy` zijn. **Nota**: U moet één enkele backslash (`\`) gebruiken wanneer het gebruiken van UI omdat Experience Platform UI automatisch extra backslash (`\`) toevoegt wanneer het ingaan van een gebruikersbenaming. |
| Wachtwoord | Het wachtwoord voor uw [!DNL Oracle Eloqua] -gebruikersnaam. |

Voor meer informatie over authentificatiegeloofsbrieven voor [!DNL Oracle Eloqua], zie de [[!DNL Oracle Eloqua]  gids over authentificatie ](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Nadat u de vereiste gegevens hebt verzameld, voert u de onderstaande stappen uit om uw [!DNL Oracle Eloqua] -account te koppelen aan Platform.

## Sluit uw [!DNL Oracle Eloqua] -account aan

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In het scherm [!UICONTROL Catalog] worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Selecteer onder de categorie [!UICONTROL Marketing automation] de optie **[!UICONTROL Oracle Eloqua]** en selecteer vervolgens **[!UICONTROL Add data]** .

![ catalogus ](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

De pagina **[!UICONTROL Connect Oracle Eloqua account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de [!DNL Oracle Eloqua] -account waarmee u een nieuwe gegevensstroom wilt maken en selecteert u vervolgens **[!UICONTROL Next]** om door te gaan.

![ bestaand ](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geeft u vervolgens een naam, een optionele beschrijving en de juiste waarden voor uw [!DNL Oracle Eloqua] -referenties op. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ nieuw ](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding tussen uw [!DNL Oracle Eloqua] -account en Platform geverifieerd en gemaakt. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow creëren om de gegevens van de marketing automatisering aan Platform ](../../dataflow/marketing-automation.md) te brengen.
