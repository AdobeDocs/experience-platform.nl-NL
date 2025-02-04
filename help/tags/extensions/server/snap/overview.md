---
title: Adobe Snapchat Conversion API-extensie Integratie
description: Met deze Adobe Experience Platform-API voor webgebeurtenissen kunt u interacties van websites rechtstreeks delen met Snapchat.
last-substantial-update: 2025-01-20T00:00:00Z
source-git-commit: 6403c339b2407410e282a25a0382845214bb6a95
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 0%

---

# Overzicht van conversies-API [!DNL Snapchat]

De [!DNL Snap] Uitbreiding van de Omzetting API is een veilige [ API van de Server van de Edge Network ](/help/server-api/overview.md) interface die u toestaat om informatie met [!DNL Snapchat] over gebruikersacties op uw websites direct te delen. U kunt de regels voor het doorsturen van gebeurtenissen gebruiken om gegevens van **[!DNL Adobe Experience Platform Edge Network]** naar **[!DNL Snapchat]** te verzenden met de API-extensie **[!DNL Snap]** Conversion.

## [!DNL Snapchat] voorwaarden {#prerequisites}

Om [!DNL Snapchat] Conversies API te gebruiken, moet u een [ Gebeurtenis hebben die bezit ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started) opstelling in Adobe Experience Platform en [ vereiste toestemmingen ](https://experienceleague.adobe.com/en/docs/experience-platform/collection/permissions) door:sturen om het bezit uit te geven.

Creeer a [ Datastream ](/help/tags/ui/event-forwarding/getting-started.md) en voeg de [ Gebeurtenis toe die dienst ](/help/tags/ui/event-forwarding/getting-started#enable-event-forwarding) door:sturen aan het.

Een **[!DNL Snapchat]** [ BedrijfsManager ](https://business.snapchat.com/) rekening wordt vereist om Conversies API te gebruiken. Met Business Manager kunnen adverteerders de marketinginspanningen van **[!DNL Snapchat]** integreren in hun hele bedrijf en met externe partners. Zie **[!DNL Snapchat]** [ hulp centreert artikel ](https://businesshelp.snapchat.com/s/article/get-started?language=en_US) bij het creëren van een rekening van BedrijfsManager als u geen hebt.

Er moet een **[!DNL Snap Pixel]** (https://businesshelp.snapchat.com/s/article/pixel-website-install?language=en_US) zijn ingesteld in Snapchat Ads Manager en u moet toegang hebben om `Pixel ID` te kunnen bekijken. `Pixel ID` vindt u in de sectie **[!UICONTROL Events Manager]** https://businesshelp.snapchat.com/s/article/events-manager?language=en_US.

U hebt een statisch, langdurig API-token nodig. Zie [[!DNL Snapchat]  Conversies API documentatie ](https://developers.snap.com/api/marketing-api/Conversions-API/GetStarted#access-token) om dit teken te verkrijgen.

## De API-extensie voor [!DNL Snapchat] webgebeurtenissen installeren en configureren {#install}

Om de uitbreiding te installeren, navigeer aan **[!UICONTROL Data Collection]**> **[!UICONTROL Event Forwarding]**. Selecteer de eigenschap waar u de extensie wilt installeren.

Voer de volgende stappen uit als de gewenste eigenschap is geselecteerd:

1. Selecteer **[!UICONTROL Extensions]** in het navigatievenster aan de linkerkant.
2. Zoek naar **[!UICONTROL Snap Conversion API Extension]** en selecteer **[!UICONTROL Install]**.

   ![ Beeld dat installeert knoop ](../../../images/extensions/server/snap/install.png) toont.

3. Voer in het configuratiescherm de volgende waarden in:

* **[!UICONTROL Pixel Id]**
* **[!UICONTROL API Token]**

Selecteer **[!UICONTROL Save]** als u klaar bent.

![ Beeld dat identiteitskaart van het Pixel en API symbolenknoop ](../../../images/extensions/server/snap/configure.png) toont.
<!-- 
![[!DNL Snap] configuration screen for the [!DNL Snap] conversion API extension.](../../../images/extensions/server/snap/configure.png) -->

## Gegevenselementen maken {#create-data-elements}

Om gegevenspunten als parameters tot de [!DNL Snapchat] API uitbreiding van Conversies over te gaan, moet u [ gegevenselementen ](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding#create-an-event-forwarding-data-element) voor elk gegevenspunt tot stand brengen. Voer de volgende stappen uit:

1. Navigeer aan **[!UICONTROL Authoring]**> **[!UICONTROL Data Elements]** in het scherm van uw bezit **[!UICONTROL Property Info]**, en selecteer dan **[!UICONTROL Add Data Element]**.

   ![ Beeld die tonen voegt de knoop van het gegevenselement ](../../../images/extensions/server/snap/add_data_element.png) toe.

2. Voer een naam in voor het gegevenselement.

3. Selecteer **[!UICONTROL Core]** als de extensie en **[!UICONTROL Path]** als het gegevenstype van het gegevenselement.

4. Selecteer in het keuzemenu het juiste item en vul het veld [!UICONTROL Path] in het rechterdeelvenster in om naar de gewenste gegevens in het schema te verwijzen.

   ![ Beeld die tot het scherm van het gegevenselement tonen leidt ](../../../images/extensions/server/snap/create_data_element.png).

Als u bijvoorbeeld een gegevenselement maakt dat verwijst naar `snapClickId` in het hieronder weergegeven schema:

![ Beeld die schema tonen ](../../../images/extensions/server/snap/schema.png).

U moet het gegevenselement configureren, omdat `snapClickId` zich onder `_snap.inc.exchange` in het XDM-schema bevindt.

![ Beeld dat uitgeeft het scherm van het gegevenselement ](../../../images/extensions/server/snap/edit_data_element.png).

Zie de [ Gebeurtenis door:sturen eigenschappen documentatie ](/help/tags/ui/event-forwarding/overview#data-elements.md) voor meer details bij het creëren van gegevenselementen.

## Maak regels om conversiegebeurtenissen naar magnetische uitlijning te verzenden {#create-snap-rules}

[ Regels ](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding#create-an-event-forwarding-rule) worden gebruikt om uitbreidingen in Platform teweeg te brengen. Deze sectie schetst hoe te om regels binnen uw gebeurtenis tot stand te brengen die bezit door:sturen om omzettingsgebeurtenissen naar Breuk te verzenden gebruikend de uitbreiding van Conversies API.

### Een nieuwe regel maken

1. Navigeer naar uw eigenschap voor het doorsturen van gebeurtenissen en selecteer **[!UICONTROL Rules]** in het menu Ontwerpen. Klik vervolgens op **[!UICONTROL Create New Rule]** .

   ![ Beeld dat regels in linkernavigatie ](../../../images/extensions/server/snap/create_new_rule.png) toont.

2. Geef de regel een naam en configureer een voorwaarde voor het activeren van de gebeurtenis Snap. Als u bijvoorbeeld een gebeurtenis `PURCHASE` wilt verzenden wanneer een gebeurtenis een ordernummer bevat, stelt u een voorwaarde in om te controleren of de gebruikersinteractie een geldig inkoopordernummer bevat.

   ![ Beeld dat het scherm van de voorwaardenconfiguratie ](../../../images/extensions/server/snap/action_configuration.png) toont.

3. Nadat u de voorwaarde hebt opgeslagen, voegt u een handeling toe waarmee de magnetische conversie-API wordt geactiveerd. In het linkerpaneel:

   * Stel de vervolgkeuzelijst [!UICONTROL Extension] in op [!UICONTROL Snap Conversions API Extension] .

   * Stel de vervolgkeuzelijst [!UICONTROL Action Type] in op [!UICONTROL Report Web Conversions] .

   * Geef de regel dienovereenkomstig een naam.

   ![ Beeld dat actieconfiguratiescherm ](../../../images/extensions/server/snap/action_configuration.png) toont.

4. Vorm de [ de parameterwaarden van CAPI ](https://developers.snap.com/api/marketing-api/Conversions-API/Parameters) u voor de gebeurtenis in de **[!UICONTROL Data Bindings]** sectie op het rechterpaneel wilt verzenden. De velden in de extensie worden toegewezen aan CAPI-parameters, zoals hieronder wordt weergegeven. Zie de [ documentatie van de Conversies API van de Snapchat ](https://developers.snap.com/api/marketing-api/Conversions-API/Parameters) voor meer informatie over elke parameter.

| Veld voor gegevensbinding | Magnetische CAPI-parameter |
| --- | --- |
| Type gebeurtenis (vereist) | `event_name` |
| Email | `em` |
| Telefoonnummer | `ph` |
| Gebruikersagent | `client_user_agent` |
| IP-adres | `client_ip_address` |
| Klik op ID | `sc_click_id` |
| Cookie1 | `so_cookie1` |
| Voornaam | `fn` |
| Achternaam | `ln` |
| Geslacht | `ge` |
| Plaats | `ph` |
| Staat | `st` |
| Postcode | `zp` |
| Land | `country` |
| Externe id | `external_id` |
| Partner-id | `partner_id` |
| Abonnement-id | `subscription_id` |
| ID lead | `lead_id` |
| Object of rubriek | `content_category` |
| Inhoudsnaam | `content_ids` |
| Inhoudstype | `content_name` |
| Inhoud | `contents` |
| Beschrijving | `description` |
| Gebeurtenistag | `event_tag` |
| Aantal objecten | `num_items` |
| Prijs | `value` |
| Valuta | `currency` |
| Transactie-id | `order_id` (wordt ook verzonden voor `event_id` in plaats van `client dedup idD` ) |
| Voorspelde LTV | `predicted_ltv` |
| Zoektekenreeks | `search_string` |
| Aanmeldingsmethode | `sign_up_method` |
| Id van Client-deduplicatie | `event_id` |
| Beperkt gegevensgebruik | `data_processing_options` |
| URL pagina | `event_source_url` |

### Vereiste en optionele velden

* Vereiste velden:

   * Voor alle gebeurtenissen wordt `event_source` ingesteld op `WEB` .

   * Voor overeenkomsten is ten minste een van de volgende velden of combinaties vereist:

      * E-mail
      * Telefoonnummer
      * IP-adres en gebruikersagent

**Extra nota&#39;s:**

* Voor `Purchase` -gebeurtenissen zijn de velden `Currency` en `Price` vereist.

* Als u het selectievakje **[!UICONTROL Test Mode]** inschakelt, worden gebeurtenissen verzonden als testgebeurtenissen, die in het testgebeurtenisgereedschap worden weergegeven in plaats van als standaardrapportage. Zie dit [ artikel van het bedrijfsHulp centrum ](https://businesshelp.snapchat.com/s/article/capi-event-testing?language=en_US#:~:text=Snap&#39;s%20Conversions%20API%20(CAPI)%20Test,being%20processed%20as%20production%20results.) voor meer details.

* De parameter `contents` moet een JSON-tekenreeks zijn die ten minste een van de volgende velden bevat:

   * `id`
   * `item_category`
   * `brand`
   * `delivery_category`
   * `item_price`
   * `quantity`

Voorbeeld:

```json
{
  "id": "id1",
  "brand": "brand1",
  "delivery_category": "c1",
  "item_price": 2.00,
  "quantity": 2
}
```

Om [ waarde van douaneomzettingen en ROAS te gebruiken die ](https://businesshelp.snapchat.com/s/article/custom-conversions-value-roas?language=en_US) melden, omvat relevante parameters op het `contents` gebied. Bijvoorbeeld `brand` , `item_price` , `id` .

Voorbeeldconfiguratie voor een `Purchase` -gebeurtenis:

[Afbeelding met gegevensbindingen](../../../images/extensions/server/snap/data_bindings.png)

De optionele velden kunnen worden ingesteld als weergegeven:

[Afbeelding met optionele velden](../../../images/extensions/server/snap/optional_fields.png)

Zodra u de naam, de voorwaarde en de actie van de regel zoals hierboven beschreven plaatst, sparen de regel en zorg ervoor het wordt toegelaten.

[Afbeelding met ingeschakelde regel](../../../images/extensions/server/snap/enabled_rule.png)

U kunt deze wijzigingen nu publiceren naar uw eigenschap. Gelieve te zien de documentatie over [ het publiceren stroom ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/publish/overview) voor meer informatie.

## Problemen oplossen {#troubleshoot}

Voor het oplossen van problemen en het optimaliseren van uw opstelling, herzie de [ aanbevelingen van de Score van de Kwaliteit van de Gebeurtenis ](https://businesshelp.snapchat.com/s/article/event-quality-score) om uw gebeurtenissen te verzekeren de hoogst mogelijke gelijke tarieven en prestatiesresultaten bereiken.

Als u kwesties met uw **Score van de Kwaliteit van de Gebeurtenis** ervaart, leer meer over onze aanbevelingen om het [ hier ](https://businesshelp.snapchat.com/s/article/esq-issues-recommendations?language=en_US) te verbeteren.

## Volgende stappen {#next-steps}

In deze handleiding wordt beschreven hoe u gebeurtenisgegevens aan de serverzijde naar **[!DNL Snap]** kunt verzenden met de extensie **[!DNL Snap Conversions API]** . Voor meer informatie over gebeurtenis door:sturen mogelijkheden in Platform, verwijs naar de [ Gebeurtenis door:sturen overzicht ](../../../ui/event-forwarding/overview.md).
