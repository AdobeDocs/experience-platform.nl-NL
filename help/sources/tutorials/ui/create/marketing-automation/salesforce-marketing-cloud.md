---
title: Sluit uw Salesforce-Marketing Cloud-account aan op Experience Platform via de gebruikersinterface
description: Leer hoe u uw Salesforce-account via de gebruikersinterface kunt verbinden met Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# Verbind uw [!DNL Salesforce Marketing Cloud] account aan Experience Platform via de gebruikersinterface

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de [!DNL Salesforce Marketing Cloud] bronintegratie.


Deze zelfstudie bevat stappen voor het tot stand brengen van een verbinding met uw [!DNL Salesforce Marketing Cloud] account aan Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van het Experience Platform:

* [[!DNL Experience Data Model (XDM)] Systeem](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [Zelfstudie Schema Editor](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

Als u al een [!DNL Salesforce Marketing Cloud] account, kunt u de rest van dit document overslaan en doorgaan naar de zelfstudie op [het brengen van de gegevens van de marketing automatisering aan Experience Platform gebruikend UI](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Om toegang te krijgen tot uw [!DNL Salesforce Marketing Cloud] account op Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Host | De hostserver van uw toepassing. Dit is vaak uw subdomein. **Opmerking:** Wanneer u uw `host` waarde, hoeft u alleen het subdomein op te geven en niet de volledige URL. Als de host-URL bijvoorbeeld `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, hoeft u alleen maar in te voeren `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` als uw hostwaarde. |
| Client-id | De client-id die aan uw [!DNL Salesforce Marketing Cloud] toepassing. |
| Clientgeheim | Het clientgeheim dat aan uw [!DNL Salesforce Marketing Cloud] toepassing. |

Voor meer informatie over authenticatie voor [!DNL Salesforce Marketing Cloud], bezoek de [[!DNL Salesforce] verificatiedocumentatie](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Verbind uw [!DNL Salesforce Marketing Cloud] account

Selecteer in de gebruikersinterface van het Platform de optie **[!UICONTROL Sources]** van de linkernavigatie om tot [!UICONTROL Sources] werkruimte. De [!UICONTROL Catalog] Hiermee geeft u diverse bronnen weer die door het Experience Platform worden ondersteund.

U kunt de juiste categorie selecteren in de lijst met categorieën. U kunt de zoekbalk ook gebruiken om te filteren op een bepaalde bron.

Onder de [!UICONTROL Marketing automation] categorie, selecteert u **[!UICONTROL Salesforce Marketing Cloud]** en selecteer vervolgens **[!UICONTROL Set up]**.

![De broncatalogus met de bron van de Marketing Cloud Salesforce geselecteerd.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

De **[!UICONTROL Connect to Salesforce Marketing Cloud]** wordt weergegeven. Op deze pagina kunt u een nieuw account maken of een bestaand account gebruiken.

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geef een naam voor uw account op, een optionele beschrijving en de verificatiegegevens die overeenkomen met uw [!DNL Salesforce Marketing Cloud] account.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat dan wat tijd voor de nieuwe verbinding tot stand brengen.

![De nieuwe accountinterface waar u een nieuw account voor Salesforce-Marketing Cloud kunt verifiëren.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Bestaande account

Als u al een bestaande account hebt, selecteert u **[!UICONTROL Existing account]** en selecteer vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven.

![De bestaande accountinterface waarin u een keuze kunt maken uit een lijst met bestaande Salesforce-Marketing Cloud-accounts.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht tussen uw [!DNL Salesforce Marketing Cloud] account en Experience Platform. U kunt nu verdergaan met de volgende zelfstudie en [een gegevensstroom maken om uw gegevens over marketingautomatisering in Experience Platform te brengen](../../dataflow/marketing-automation.md).
