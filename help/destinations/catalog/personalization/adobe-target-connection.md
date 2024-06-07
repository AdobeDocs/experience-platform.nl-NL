---
keywords: doelpersonalisatie; bestemming; ervaring doelbestemming platform;doelbestemming adobe;
title: Adobe Target-verbinding
description: Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie- en experimentatiemogelijkheden biedt voor alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: e5c34ffb9b27ddad0c6523a7279fdf712c84f3ff
workflow-type: tm+mt
source-wordcount: '1526'
ht-degree: 0%

---

# Adobe Target-verbinding {#adobe-target-connection}

## Doelwijziging {#changelog}

| Releasedatum | Type bijwerken | Beschrijving |
|---|---|---|
| April 2024 | Bijwerken van functionaliteit en documentatie | Wanneer u verbinding maakt met het doel Doel en een gegevensstroom-id gebruikt, kunt u nu *niet nodig* om noodzakelijk de gegevensstroom voor randsegmentatie toe te laten. Dit betekent dat de bestemming van het Doel met partij en het stromen publiek zal werken, hoewel de gebruiksgevallen die u kunt verwezenlijken verschillen. De tabel weergeven in het dialoogvenster [verbindingsparameters](#parameters) voor meer informatie. |
| Januari 2024 | Bijwerken van functionaliteit en documentatie | U kunt nu soorten publiek- en profielkenmerken delen met de Adobe Target-verbinding voor de standaardproductiesandbox en andere niet-standaardsandboxen. |
| Juni 2023 | Bijwerken van functionaliteit en documentatie | Vanaf juni 2023 kunt u bij het configureren van een nieuwe Adobe Target-doelverbinding de Adobe Target-werkruimte selecteren waarnaar u het publiek wilt delen. Zie de [verbindingsparameters](#parameters) voor meer informatie. Raadpleeg de zelfstudie over [werkruimten configureren](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) in Adobe Target voor meer informatie over werkruimten. |
| Mei 2023 | Bijwerken van functionaliteit en documentatie | Vanaf mei 2023 **[!UICONTROL Adobe Target]** verbinding wordt ondersteund [kenmerkgebaseerde personalisatie](../../ui/activate-edge-personalization-destinations.md#map-attributes) en is algemeen beschikbaar voor alle klanten. |

{style="table-layout:auto"}

## Overzicht {#overview}

Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie- en experimentatiemogelijkheden biedt voor alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.

Adobe Target is een personalisatieverbinding in de Adobe Experience Platform-bestemmingscatalogus.

## Video-overzicht {#video-overview}

Bekijk de onderstaande video voor een kort overzicht van het configureren van de Adobe Target-verbinding in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Vereisten {#prerequisites}

### DataStream-id {#datastream-id}

Bij het configureren van de Adobe Target-verbinding naar [een gegevensstroom-id gebruiken](#parameters), moet u beschikken over de [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) geïmplementeerd.

Als u de Adobe Target-verbinding configureert zonder een gegevensstroom-id te gebruiken, hoeft u de Web SDK niet te implementeren.

>[!IMPORTANT]
>
>Voordat u een [!DNL Adobe Target] verbinding, lees de gids over hoe te [vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking](../../ui/activate-edge-personalization-destinations.md). Deze gids neemt u door de vereiste configuratiestappen voor zelfde-pagina en volgende-paginagrootte het gebruiksgevallen van het verpersoonlijkingsgebruik, over veelvoudige Experience Platform componenten. Als u gebruikstoepassingen van dezelfde pagina en volgende pagina wilt maken, moet u een gegevensstroom-id gebruiken wanneer u de Adobe Target-verbinding configureert.

### Vereisten in Adobe Target {#prerequisites-in-adobe-target}

In Adobe Target moet je ervoor zorgen dat de gebruiker:

* Toegang tot de [standaardwerkruimte](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* De **Fiatteur** [rol](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

Meer informatie over het verlenen van machtigingen voor [Doelpremie](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) en voor [Doelstandaard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

>[!IMPORTANT]
>
>Bij activering *randpubliek voor gebruiksgevallen voor personalisatie op dezelfde pagina en op de volgende pagina*, het publiek *moet* een [actief-op-rand samenvoegbeleid](../../../segmentation/ui/segment-builder.md#merge-policies). De [!DNL active-on-edge] samenvoegingsbeleid zorgt ervoor dat het publiek constant wordt geëvalueerd [op de rand](../../../segmentation/ui/edge-segmentation.md) en zijn beschikbaar voor gebruiksgevallen voor realtime en paginagrootte personalisatie.  Meer informatie [alle beschikbare gebruiksgevallen](#parameter), op basis van het implementatietype.
>Als u randpubliek toewijst dat een verschillend fusiebeleid aan de bestemmingen van Adobe Target gebruikt, zullen die publiek niet voor real time en volgende-paginagebeurtenissen worden geëvalueerd.
>Volg de instructies op [samenvoegingsbeleid maken](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy)en zorgt ervoor dat de **[!UICONTROL Active-On-Edge Merge Policy]** schakelen.


| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | X | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!DNL Profile request]** | U vraagt om alle soorten publiek die in de Adobe Target-bestemming zijn toegewezen voor één profiel. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informatie over gegevensstroom-id&#39;s"
>abstract="Met deze optie bepaalt u in welke gegevensstroom de doelgroep wordt opgenomen. Het drop-down menu toont slechts gegevensstromen die de toegelaten configuratie van het Doel hebben. Als u randsegmentatie wilt gebruiken, moet u een gegevensstroom-id selecteren. Als u Geen selecteert, worden alle gevallen uitgeschakeld waarin randsegmentatie wordt gebruikt."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Meer informatie over het selecteren van gegevensstromen"

>[!IMPORTANT]
> 
>Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

Adobe Experience Platform maakt automatisch verbinding met het Adobe Target-exemplaar van uw bedrijf. Er is geen verificatie vereist.

### Verbindingsparameters {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Informatie over Adobe Target Workspaces"
>abstract="Selecteer de Adobe Target-werkruimte waarin het publiek wordt gedeeld. U kunt één werkruimte selecteren voor elke Adobe Target-verbinding. Bij activering worden doelgroepen naar de geselecteerde werkruimte gerouteerd terwijl ze de toepasselijke labels voor gegevensgebruik in het Experience Platform volgen."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html" text="Meer informatie over Adobe Target-werkruimten"

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Beschrijving**: Voer een beschrijving in voor uw doel. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **DataStream-id**: Dit bepaalt in welke gegevensstroom gegevensverzameling het publiek wordt opgenomen. In het keuzemenu worden alleen gegevensstromen weergegeven waarvoor de services Doel en Adobe Experience Platform zijn ingeschakeld. Zie [configureren van een gegevensstroom](../../../datastreams/configure.md#aep) voor meer informatie over het configureren van een gegevensstroom voor Adobe Experience Platform en Adobe Target.

  >[!IMPORTANT]
  >
  >De gegevensstroom-id is uniek voor elke Adobe Target-doelverbinding. Als u hetzelfde publiek aan meerdere gegevensstromen moet toewijzen, moet u [een nieuwe doelverbinding maken](../../ui/connect-destination.md) voor elke gegevensstroom-id en doorloopt de [activeringsstroom voor publiek](#activate).

   * **[!UICONTROL None]**: Selecteer deze optie als u de personalisatie van Adobe Target moet configureren, maar u kunt het dialoogvenster [Experience Platform Web SDK](/help/web-sdk/home.md). Wanneer u deze optie gebruikt, worden soorten publiek die van Experience Platform naar Doel zijn geëxporteerd, alleen ondersteuning voor verpersoonlijking in de volgende sessie en wordt randsegmentatie uitgeschakeld. Verwijs de lijst hieronder voor een vergelijking van beschikbare gebruiksgevallen per implementatietype.

  | Adobe Target-implementatie *zonder* Web SDK | Adobe Target-implementatie *with* Web SDK | Adobe Target-implementatie *with* Web SDK *en* randsegmentatie uitgeschakeld |
  |---|---|---|
  | <ul><li>Een gegevensstroom is niet vereist. Adobe Target kan worden geïmplementeerd via [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [server-kant](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation), of [hybride](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) uitvoeringsmethoden.</li><li>[Randsegmentatie](../../../segmentation/ui/edge-segmentation.md) wordt niet ondersteund.</li><li>[Zelfde pagina en volgende pagina personalisatie](../../ui/activate-edge-personalization-destinations.md) worden niet ondersteund.</li><li>U kunt publiek- en profielkenmerken delen met de Adobe Target-verbinding voor de *standaardproductiesandbox* en niet-standaardsandboxen.</li><li>Om volgende-zittingsverpersoonlijking te vormen zonder een gegevensstroomidentiteitskaart te gebruiken, gebruik [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>Een gegevensstroom met Adobe Target en Experience Platform die als diensten wordt gevormd wordt vereist.</li><li>De segmentatie van de rand werkt zoals verwacht.</li><li>[Zelfde pagina en volgende pagina personalisatie](../../ui/activate-edge-personalization-destinations.md#use-cases) worden ondersteund.</li><li>Het delen van publiek- en profielkenmerken van andere sandboxen wordt ondersteund.</li></ul> | <ul><li>Een gegevensstroom met Adobe Target en Experience Platform die als diensten wordt gevormd wordt vereist.</li><li>Wanneer [configureren van de gegevensstroom](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), selecteer de **Randsegmentatie** selectievakje.</li><li>[Aanpassing van volgende sessie](../../ui/activate-edge-personalization-destinations.md#next-session) wordt ondersteund.</li><li>Het delen van publiek- en profielkenmerken van andere sandboxen wordt ondersteund.</li></ul> |

* **Werkruimte**: Selecteer de Adobe Target [werkruimte](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) waaraan het publiek deelneemt. U kunt één werkruimte selecteren voor elke Adobe Target-verbinding. Bij activering worden de doelgroepen naar de geselecteerde werkruimte geleid terwijl ze de toepasselijke [Labels voor gegevensgebruik van Experience Platforms](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>Als u een aangepaste doelwerkruimte gebruikt voor [personalisatie van dezelfde pagina en van volgende pagina met kenmerken](../../ui/activate-edge-personalization-destinations.md), alleen de [geselecteerd publiek](../../ui/activate-edge-personalization-destinations.md#select-audiences) worden verzonden naar de geselecteerde doelwerkruimte. De [toegewezen kenmerken](../../ui/activate-edge-personalization-destinations.md#mapping) worden verzonden naar de standaardwerkruimte Doel.
><br>
>Dit gedrag verandert in een toekomstige update.

### Waarschuwingen inschakelen {#enable-alerts}

U kunt alarm toelaten om berichten over de status van dataflow aan uw bestemming te ontvangen. Selecteer een waarschuwing in de lijst om u te abonneren op meldingen over de status van uw gegevensstroom. Zie de handleiding voor meer informatie over waarschuwingen [abonneren op bestemmingen die het alarm gebruiken UI](../../ui/alerts.md).

Wanneer u klaar bent met het opgeven van details voor uw doelverbinding, selecteert u **[!UICONTROL Next]**.

## Soorten publiek naar dit doel activeren {#activate}

>[!IMPORTANT]
> 
>Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Lezen [Het publiek activeren voor verpersoonlijkingsdoelen van randen](../../ui/activate-edge-personalization-destinations.md) voor instructies voor het activeren van het publiek naar deze bestemming.

## Soorten publiek verwijderen uit een doeldoel {#remove}

Er zijn extra stappen vereist om een publiek te verwijderen uit een bestaande Adobe Target-verbinding wanneer dat publiek al in een Adobe Target wordt gebruikt [activiteit](https://experienceleague.adobe.com/en/docs/target/using/activities/activities). Wanneer u een publiek probeert te verwijderen uit een Adobe Target-verbinding, treedt een fout op als het publiek wordt gebruikt door een Adobe Target-activiteit.

![De beeld van UI van het platform die een fout toont die door het proberen wordt veroorzaakt om een publiek te verwijderen dat door een activiteit van het Doel wordt gebruikt.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Om een publiek uit een bestemming van het Doel te verwijderen wanneer het publiek in een activiteit wordt gebruikt, moet u of het publiek uit de activiteit van het Doel eerst verwijderen die het gebruikt, of de activiteit volledig schrappen. Vervolgens kunt u het publiek verwijderen uit de doelverbinding.

Als het publiek niet in een activiteit wordt gebruikt, ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** > **[!UICONTROL Select destination dataflow]** > **[!UICONTROL Activation data]** selecteert u het publiek dat u wilt verwijderen en selecteert u vervolgens **[!UICONTROL Remove audiences]**.

## Geëxporteerde gegevens {#exported-data}

Adobe Target *leest* profielgegevens uit de Adobe Experience Platform-Edge Network, zodat er geen gegevens worden geëxporteerd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
