---
title: Verbinding maken met Experience Platform via de gebruikersinterface van uw Salesforce Marketing Cloud-account
description: Leer hoe u uw Salesforce Marketing Cloud-account via de gebruikersinterface met Experience Platform kunt verbinden.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0c6a51d06e57eb6de063a350bd4b17022555a0b4
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# Sluit uw [!DNL Salesforce Marketing Cloud] -account aan op Experience Platform via de gebruikersinterface

>[!WARNING]
>
>De [!DNL Salesforce Marketing Cloud] -bron wordt afgekeurd in januari 2026. Later dit jaar zal een nieuwe bron worden vrijgegeven als alternatief. Zodra de nieuwe bron wordt vrijgegeven, moet u van plan zijn om aan de nieuwe bron te migreren door nieuwe rekeningsverbindingen en dataflows vóór eind Januari 2026 te creëren.

Lees deze handleiding voor informatie over hoe u uw [!DNL Salesforce Marketing Cloud] -account kunt verbinden met Adobe Experience Platform via de werkruimte Bronnen in de Experience Platform-gebruikersinterface.

## Aan de slag

Deze zelfstudie vereist een goed begrip van de volgende onderdelen van Experience Platform:

* [[!DNL Experience Data Model (XDM)]  Systeem ](../../../../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.
   * [ Grondbeginselen van schemacompositie ](../../../../../xdm/schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM, met inbegrip van zeer belangrijke principes en beste praktijken in schemacompositie.
   * [ het leerprogramma van de Redacteur van het Schema ](../../../../../xdm/tutorials/create-schema-ui.md): Leer hoe te om douaneschema&#39;s tot stand te brengen gebruikend de Redacteur UI van het Schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.

Als u reeds een [!DNL Salesforce Marketing Cloud] rekening hebt, kunt u de rest van dit document overslaan en aan het leerprogramma te werk gaan [ brengend de gegevens van de marketing automatisering aan Experience Platform gebruikend UI ](../../dataflow/marketing-automation.md).

### Vereiste referenties verzamelen

Lees het [[!DNL Salesforce Marketing Cloud]  overzicht ](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#prerequisites) voor informatie over authentificatie.

## Navigeren door de catalogus met bronnen

>[!IMPORTANT]
>
>Aangepaste objectinvoer wordt momenteel niet ondersteund door de bronintegratie van [!DNL Salesforce Marketing Cloud] .


Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sources]** in de linkernavigatie voor toegang tot de werkruimte van *[!UICONTROL Sources]* . Kies een categorie of gebruik de zoekbalk om de bron te zoeken.

Als u verbinding wilt maken met [!DNL Salesforce Marketing Cloud] , gaat u naar de categorie *[!UICONTROL Marketing Automation]* , selecteert u de **[!UICONTROL Salesforce Marketing Cloud]** bronkaart en selecteert u vervolgens **[!UICONTROL Set up]** .

>[!TIP]
>
>Bronnen in de catalogus met bronnen geven de optie **[!UICONTROL Set up]** weer wanneer een bepaalde bron nog geen geverifieerde account heeft. Zodra een geverifieerd account is gemaakt, verandert deze optie in **[!UICONTROL Add data]** .

![ de broncatalogus van bronnen met de Salesforce Marketing Cloud geselecteerde bronkaart.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

## Een bestaande account gebruiken {#existing}

Als u een bestaande account wilt gebruiken, selecteert u **[!UICONTROL Existing account]** en vervolgens de [!DNL Salesforce Marketing Cloud] -account die u wilt gebruiken.

![ de bestaande rekeningeninterface in het bronwerkschema met &quot;Bestaande geselecteerde rekening&quot;.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Een nieuwe account maken {#new}

U kunt de [!DNL Salesforce Marketing Cloud] -bron gebruiken om verbinding te maken met Experience Platform op [!DNL Azure] of [!DNL Amazon Web Services] (AWS).

### Verbinding maken met Experience Platform op [!DNL Azure] {#azure}

Om met Experience Platform op [!DNL Azure] te verbinden, verstrek een rekeningsnaam, een facultatieve beschrijving, en uw [ geloofsbrieven van de rekeningsauthentificatie ](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#azure). Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

![ de nieuwe rekeningsinterface in het bronwerkschema voor verbinding aan Experience Platform op Azure.](../../../../images/tutorials/create/salesforce-marketing-cloud/new-azure.png)

### Verbinding maken met Experience Platform op Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform die op Amazon Web Services (AWS) worden uitgevoerd. Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../../../landing/multi-cloud.md).

Om met Experience Platform op [!DNL AWS] te verbinden, zorg ervoor dat u in een zandbak VA6 bent en een rekeningsnaam, een facultatieve beschrijving, en uw [ geloofsbrieven van de rekeningsauthentificatie ](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#aws) verstrekt. Als u klaar bent, selecteert u **[!UICONTROL Connect to source]** en laat de verbinding enkele ogenblikken tot stand komen.

![ de nieuwe rekeningsinterface in het bronwerkschema voor verbinding aan Experience Platform op AWS ](../../../../images/tutorials/create/salesforce-marketing-cloud/new-aws.png)

## Een gegevensstroom maken voor [!DNL Salesforce Marketing Cloud] -gegevens

Nu u met succes uw [!DNL Salesforce Marketing Cloud] hebt verbonden, kunt u [ nu tot een dataflow en gegevens van uw marketing automatiseringsleverancier in Experience Platform ](../../dataflow/marketing-automation.md) leiden.
