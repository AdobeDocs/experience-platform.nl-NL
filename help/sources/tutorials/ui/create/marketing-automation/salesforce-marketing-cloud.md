---
title: Verbinding maken met Experience Platform via de gebruikersinterface van uw Salesforce Marketing Cloud-account
description: Leer hoe u uw Salesforce Marketing Cloud-account via de gebruikersinterface met Experience Platform kunt verbinden.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Sluit uw [!DNL Salesforce Marketing Cloud] -account aan op Experience Platform via de gebruikersinterface

>[!WARNING]
>
>De [!DNL Salesforce Marketing Cloud] -bron wordt afgekeurd in januari 2026. Later dit jaar zal een nieuwe bron worden vrijgegeven als alternatief. Zodra de nieuwe bron wordt vrijgegeven, moet u van plan zijn om aan de nieuwe bron te migreren door nieuwe rekeningsverbindingen en dataflows vóór eind Januari 2026 te creëren.

Deze zelfstudie biedt stappen voor het verbinden van uw [!DNL Salesforce Marketing Cloud] -account met Adobe Experience Platform via de gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een [!DNL Salesforce Marketing Cloud] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [ brengend de gegevens van de marketing automatisering aan Experience Platform gebruikend UI ](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Als u toegang wilt krijgen tot uw [!DNL Salesforce Marketing Cloud] -account op Experience Platform, moet u de volgende waarden opgeven:

| Credentials | Beschrijving |
| ---------- | ----------- |
| Host | De hostserver van uw toepassing. Dit is vaak uw subdomein. **Nota:** wanneer het ingaan van uw `host` waarde, moet u `{subdomain}.rest.marketingcloudapis.com` specificeren. Als de host-URL bijvoorbeeld `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/` is, moet u `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` als waarde voor de host invoeren. |
| Client-id | De client-id die aan uw [!DNL Salesforce Marketing Cloud] -toepassing is gekoppeld. |
| Clientgeheim | Het clientgeheim dat aan de toepassing [!DNL Salesforce Marketing Cloud] is gekoppeld. |

Voor meer informatie over authentificatie voor [!DNL Salesforce Marketing Cloud], bezoek de [[!DNL Salesforce]  authentificatiedocumentatie ](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Sluit uw [!DNL Salesforce Marketing Cloud] -account aan

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de bronintegratie van [!DNL Salesforce Marketing Cloud] .

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van [!UICONTROL Sources] . In [!UICONTROL Catalog] worden diverse bronnen weergegeven die door Experience Platform worden ondersteund.

U kunt de juiste categorie selecteren in de lijst met categorieën. U kunt de zoekbalk ook gebruiken om te filteren op een bepaalde bron.

Selecteer onder de categorie [!UICONTROL Marketing automation] de optie **[!UICONTROL Salesforce Marketing Cloud]** en selecteer vervolgens **[!UICONTROL Set up]** .

![ de broncatalogus met de geselecteerde bron van Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

De pagina **[!UICONTROL Connect to Salesforce Marketing Cloud]** wordt weergegeven. Op deze pagina kunt u een nieuw account maken of een bestaand account gebruiken.

### Nieuwe account

Als u een nieuwe account wilt maken, selecteert u **[!UICONTROL New account]** en geeft u een naam voor uw account, een optionele beschrijving en de verificatiereferenties die overeenkomen met uw [!DNL Salesforce Marketing Cloud] -account.

Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat u de nieuwe verbinding enige tijd tot stand brengen.

![ de nieuwe rekeningsinterface waar u een nieuwe rekening voor Salesforce Marketing Cloud kunt voor authentiek verklaren.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Bestaande account

Als u al een bestaande account hebt, selecteert u **[!UICONTROL Existing account]** en selecteert u vervolgens de account die u wilt gebruiken in de lijst die wordt weergegeven.

![ de bestaande rekeningsinterface waar u van een lijst van bestaande rekeningen van Salesforce Marketing Cloud kunt selecteren.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Volgende stappen

Aan de hand van deze zelfstudie hebt u een verbinding tot stand gebracht tussen uw [!DNL Salesforce Marketing Cloud] -account en Experience Platform. U kunt nu aan het volgende leerprogramma verdergaan en [ een dataflow creëren om uw gegevens van de marketing automatisering in Experience Platform ](../../dataflow/marketing-automation.md) te brengen.
