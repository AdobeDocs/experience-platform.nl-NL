---
title: Een Eloqua-bronverbinding met een Oracle maken met de gebruikersinterface van het Platform
description: Leer hoe u Adobe Experience Platform kunt verbinden met Oracle Eloqua via de gebruikersinterface van het Platform.
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: e8f54f06ad3431227e140219a9960e8e04f83ccc
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 1%

---

# Een [!DNL Oracle Eloqua] bronverbinding met gebruikersinterface van Platform

Deze zelfstudie bevat stappen voor het maken van een [!DNL Oracle Eloqua] bronverbinding via de Adobe Experience Platform-gebruikersinterface.

## Aan de slag

Deze gids vereist een werkend inzicht in de volgende componenten van Platform:

* [Bronnen](../../../../home.md): Met Platform kunnen gegevens uit verschillende bronnen worden ingepakt en kunt u inkomende gegevens structureren, labelen en verbeteren met behulp van de services van Platforms.
* [Sandboxen](../../../../../sandboxes/home.md): Platform biedt virtuele sandboxen die één Platform-instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Als u al een geverifieerde [!DNL Oracle Eloqua] account op Platform, dan kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het creëren van een gegevensstroom om de gegevens van de marketing automatisering aan Platform te brengen](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Om verbinding te maken [!DNL Oracle Eloqua] aan Platform, moet u waarden voor de volgende authentificatieeigenschappen verstrekken:

| Credentials | Beschrijving |
| --- | --- |
| Endpoint | Het eindpunt van uw [!DNL Oracle Eloqua] server. [!DNL Oracle Eloqua] ondersteunt meerdere datacenters. Om uw eindpunt te vinden, login aan [[!DNL Oracle Eloqua] interface](https://login.eloqua.com) met uw referenties en kopieer vervolgens het basis-URL-gedeelte van de omleidings-URL. De notatie voor uw URL-patroon is `xxx.xx.eloqua.com` en moet zonder `http` of `https`. |
| Gebruikersnaam | De gebruikersnaam van uw [!DNL Oracle Eloqua] server. De gebruikersnaam moet zijn opgemaakt als `siteName + \\ + username`, waarbij `siteName` is de bedrijfsnaam waarmee u zich hebt aangemeld [!DNL Oracle Eloqua] en `username` is uw gebruikersnaam. Uw gebruikersnaam voor aanmelding kan bijvoorbeeld: `Eloqua\Andy`. **Opmerking**: U moet één backslash gebruiken (`\`) bij het gebruik van de gebruikersinterface omdat de gebruikersinterface van het Experience Platform automatisch een extra backslash toevoegt (`\`) bij het invoeren van een gebruikersnaam. |
| Wachtwoord | Het wachtwoord dat overeenkomt met uw [!DNL Oracle Eloqua] gebruikersnaam. |

Voor meer informatie over verificatiereferenties voor [!DNL Oracle Eloqua], zie de [[!DNL Oracle Eloqua] handleiding voor verificatie](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

Nadat u de vereiste gegevens hebt verzameld, kunt u de onderstaande stappen volgen om uw [!DNL Oracle Eloqua] aan Platform.

## Verbind uw [!DNL Oracle Eloqua] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] in het scherm worden diverse bronnen weergegeven waarmee u een account kunt maken.

U kunt de juiste categorie selecteren in de catalogus aan de linkerkant van het scherm. U kunt ook de specifieke bron vinden waarmee u wilt werken met de zoekoptie.

Onder de [!UICONTROL Marketing automation] categorie, selecteert u **[!UICONTROL Oracle Eloqua]** en selecteer vervolgens **[!UICONTROL Add data]**.

![catalogus](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

De **[!UICONTROL Connect Oracle Eloqua account]** wordt weergegeven. Op deze pagina kunt u nieuwe of bestaande referenties gebruiken.

### Bestaande account

Als u een bestaande account wilt gebruiken, selecteert u de optie [!DNL Oracle Eloqua] account waarmee u een nieuwe gegevensstroom wilt maken, selecteert u **[!UICONTROL Next]** om verder te gaan.

![bestaand](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### Nieuwe account

Als u een nieuwe account maakt, selecteert u **[!UICONTROL New account]** en geef vervolgens een naam, een optionele beschrijving en de juiste waarden voor uw [!DNL Oracle Eloqua] referenties. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![new](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een bronverbinding tussen uw [!DNL Oracle Eloqua] account en Platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom maken om gegevens over marketingautomatisering naar het Platform te brengen](../../dataflow/marketing-automation.md).
