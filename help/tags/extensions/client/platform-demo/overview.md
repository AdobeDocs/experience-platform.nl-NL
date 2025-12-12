---
title: Overzicht van Adobe Experience Platform Demo-extensie
description: Meer informatie over de Adobe Experience Platform Demo-extensie in Adobe Experience Platform.
exl-id: 4bafa132-0d21-4140-ab46-f09cc20bce6f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# Adobe Experience Platform Demo-extensie

>[!NOTE]
>
>Deze uitbreiding is afgekeurd ten gunste van [ Adobe Experience Platform Web SDK ](../web-sdk/overview.md).

De functies van deze extensie worden overgebracht naar een nieuwe extensie. Hier volgt een snelle vergelijking van de huidige functies.

| Experience Platform Demo-extensie | Experience Platform Web SDK |
| ------------------ | ----------- |
| Ondersteuning voor aangepaste klant-id&#39;s | Ondersteuning voor aangepaste gebruikers-id&#39;s |
| Interface voor clienttoewijzing voor XDM | Ingebouwde ECID (geen bezoeker.js nodig) |
| Mogelijkheid om een streamingverbinding te maken | Ondersteuning voor aanmelding |
| | XDM-ondersteuning als gegevenselement |
| | Domeinondersteuning van eerste partij |
| | Ingebouwde foutopsporingsgereedschappen |
| | Automatisch verzamelt browsercontext |
| | Volledige open bron |


## De Adobe Experience Platform-extensie configureren

Deze sectie bevat een verwijzing naar de opties die beschikbaar zijn bij het configureren van de Adobe Experience Platform-extensie.

Als de Adobe Experience Platform-extensie nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]** , plaatst u de aanwijzer op de Adobe Experience Platform-extensie en selecteert u **[!UICONTROL Install]** .

Als u de extensie wilt configureren, opent u het tabblad [!UICONTROL Extensions] , plaatst u de muisaanwijzer op de extensie en selecteert u **[!UICONTROL Configure]** .

![](../../../images/adobe-experience-platform-extension-configuration.png)

### Streaming verbinding

Als u een streamingverbinding kiest, begint u met het streamen van gegevens naar Adobe Experience Platform. U kunt er een selecteren in de keuzelijst met streamingverbindingen. Streaming verbinding is een verplicht veld. Als er geen streamingverbinding wordt gemaakt, kunt u er een maken door op de knop **[!UICONTROL Create a streaming connection]** te klikken.

Als u **[!UICONTROL Create a streaming connection]** selecteert, wordt een modaal venster weergegeven.

![](../../../images/adobe-experienc-platform-create-streaming-connection.png)

Het modaal bevat velden met vooraf ingevulde waarden die naar wens kunnen worden gewijzigd. Als u meerdere streamingverbindingen wilt maken, moet u er rekening mee houden dat het veld **[!UICONTROL Data Source]** uniek moet zijn. Het maken van een andere streamingverbinding met een **[!UICONTROL Data Source]** -verbinding die al voor een andere verbinding wordt gebruikt, mislukt.

Nadat u een streamingeindpunt hebt geselecteerd, kiest u het streamingeindpunt URL en de bron.

![](../../../images/adobe-experience-platform-streaming-endpoint-selected.png)

## Handelingstypen voor Adobe Experience Platform-extensies

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de Adobe Experience Platform-extensie.

### Bandbaken verzenden {#send-beacon}

Dit is het handelingstype dat u gebruikt om gegevens naar de Adobe Experience Platform te verzenden.

![](../../../images/adobe-experience-platform-send-beacon-dataset.png)

U moet eerst de dataset selecteren waar de gegevens zullen worden opgeslagen. Over het algemeen, vertegenwoordigen de datasets een lijst die de gegevens zal opslaan die via de het stromen verbinding worden verzonden. U moet de datasets binnen Adobe Experience Platform creëren alvorens dit actietype te gebruiken.

![](../../../images/adobe-experience-platform-send-beacon-dataset-selected1.png)

Nadat u de dataset selecteert waar de gegevens zullen worden opgeslagen, zult u details over het schema zien dat met de geselecteerde dataset verbonden is.

### Schema toewijzen

Na het selecteren van de dataset kunt u uw schemaafbeelding bepalen.

![](../../../images/adobe-experience-platform-send-beacon-schema-mapping.png)

Het veld Bronwaarde accepteert een waarde of een gegevenselement. U kunt een gegevenselement toevoegen door de knoop van het gegevenselement te selecteren die naast het gebied van de bronwaarde wordt gevestigd.

Het veld Doelschema bevat het pad van een XDM-veld dat in het schema van de gegevensset is gedefinieerd. Voor velden die dieper in de schemahiërarchie zijn gedefinieerd, kunt u de punt gebruiken als scheidingsteken tussen de padonderdelen (bijvoorbeeld timeSeriesEvents.eventType).

### Selector schemaveld

De uitbreiding biedt ook de mogelijkheid om een gebied van het doelschema te selecteren gebruikend een visuele selecteur. Als u de doelknoop selecteert die naast de het gebiedsinput van het doelschema zit, zal een modaal worden getoond waar u de het schemaboom van de dataset zult zien. U kunt een gebied kiezen, dan de **Uitgezochte** knoop selecteren en de input van het doelschemagebied zal worden bijgewerkt bevat de correcte weg XDM.

![](../../../images/adobe-experience-platform-send-beacon-schema-field-selector.png)

### Identiteitsvelden in de Adobe Experience Platform

De schema&#39;s van de gegevens van het verslag en de reeksen gegevensschema&#39;s kunnen één of meerdere identiteitsgebieden bevatten. Identiteitsvelden worden aan elkaar gekoppeld om één identiteitsrepresentatie van een onderwerp te vormen en bevatten informatie zoals een CRM-id, Experience Cloud-id (ECID), browsercookie, advertentie-id of andere id&#39;s in verschillende domeinen.

Identiteitsvelden kunnen op twee manieren binnen het schema worden gedefinieerd:

1. De schema&#39;s van het verslag en van de Reeks van de Tijd allebei bevatten een speciaal gebied genoemd `xdm:identityMap` dat een kaart van identiteiten kan bevatten.
1. De zeer belangrijke gebieden kunnen als gebieden van de Identiteit binnen het schema worden gemerkt.

### Identiteitsvelden in de Adobe Experience Platform-extensie

Voor elk schemagebied dat als identiteitsgebied wordt bepaald, zal een rij aan de sectie van de schemaafbeelding worden toegevoegd. Elke toegevoegde rij bevat het doelschemaveld dat al is ingevuld met het bijbehorende XDM-schemapad. U kunt zien of een schemaveld ook een identiteitsveld is als u een profielpictogram bij het veld ziet.

![](../../../images/adobe-experience-platform-send-beacon-identity-field.png)

De primaire identiteitsgebieden worden altijd vereist, zodat kunt u niet de rijen schrappen die hen uit de sectie van de schemaafbeelding bevatten.

Een schemagebied dat als niet-primair identiteitsgebied wordt bepaald, zal automatisch aan de sectie van de schemaafbeelding worden toegevoegd, maar de bronwaardeinput kan leeg blijven. Dat veld kan worden verwijderd. Het veld wordt verwijderd als de bijbehorende bronwaarde leeg is.

![](../../../images/adobe-experience-platform-send-beacon-identity-field-warning.png)

Er wordt een waarschuwingspictogram weergegeven bij elk niet-primair identiteitsveld dat geen waarde bevat.

Een identiteitssectie zal zichtbaar zijn als uw schema een `xdm:identityMap` gebied bevat. U kunt deze sectie gebruiken als u liever gegevens met betrekking tot identiteiten verzendt met de `xdm:identityMap` .

![](../../../images/adobe-experience-platform-send-beacon-identity-section.png)

De sectie voor identiteitstoewijzing kan meerdere rijen bevatten. Elke rij kan een bepaald identiteitstype bepalen. U kunt de volgende kenmerken definiëren voor een identiteit: type, geverifieerde status, primair en waarde.

Als u meerdere identiteiten hebt binnen de sectie voor identiteitstoewijzing, kan slechts één identiteit als primair worden gemarkeerd.

Als u een schema hebt dat een `xdm:identityMap` gebied heeft en tezelfdertijd een ander gebied duidelijk als primair identiteitsgebied is, zal de primaire kolom van binnen de sectie van de identiteitstoewijzing niet zichtbaar zijn.

![](../../../images/adobe-experience-platform-send-beacon-identity-section-not-primary.png)

### Vereiste velden

Sommige schema&#39;s hebben verplichte velden op hoofdniveau. De meest voorkomende zijn `timestamp` en `_id` . Zonder deze gebieden te bepalen, zal het baken ontbreken. U kunt ze definiëren in de sectie voor schematoewijzing.

Als uw sectie van de schemaafbeelding niet `timestamp` of `_id` zal bevatten, maar het datasetschema vereist hen, zal de uitbreiding van Adobe Experience Platform een baken verzenden die automatisch geproduceerde waarden bevat zodat het baken niet zal ontbreken. De automatisch geproduceerde waarden zullen aan de bakengegevens slechts worden toegevoegd als u die gebieden binnen de sectie van de schemaafbeelding niet hebt bepaald.
