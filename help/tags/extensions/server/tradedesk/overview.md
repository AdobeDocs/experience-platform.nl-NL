---
title: Het overzicht van de API-extensie voor realtime conversies van het handelsbureau
description: Leer over de Realtime Conversies API uitbreiding van het Handelsbureau voor gebeurtenis door:sturen in Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: 8000bbf36e6763b8fca17c2ae0d5c2fe53bc6964
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# [!DNL The Trade Desk Real-Time Conversions API] extensieoverzicht

[[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) kunt u gebeurtenissen verzenden naar [!DNL The Trade Desk] om heroriëntering en attributie van hefboomfinanciering mogelijk te maken.

U kunt de [!DNL The Trade Desk Real-Time Conversions API] extensie voor het verzenden van gegevens van de Adobe Experience Platform-Edge Network naar [!DNL The Trade Desk] door de mogelijkheden van de API in uw [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) regels.

Gebruiken [!DNL The Trade Desk Real-Time Conversions API] kunt u de API-mogelijkheden in uw [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) regels voor het verzenden van gegevens naar [!DNL The Trade Desk] van de Adobe Experience Platform Edge Network.

Lees dit document om te leren hoe u de extensie installeert en de mogelijkheden van de extensie gebruikt in een gebeurtenis die wordt doorgestuurd [regel](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Deze extensie- en documentatiepagina wordt bijgehouden door [!DNL The Trade Desk] team. Neem voor alle vragen of verzoeken om een update rechtstreeks contact op met hen.

## Vereisten {#prerequisites}

U moet een relevante Advertiser-id, UPixel-id en Beheer-id hebben die vereist zijn vanuit uw [!DNL The Trade Desk] om de [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Als je een handelaar bent, moet je ook je bedrijfs-id opvragen.

## Installeer en configureer de [!DNL The Trade Desk] Real-Time Conversies API {#install}

Als u de extensie wilt installeren, [een eigenschap voor het doorsturen van gebeurtenissen maken](../../../ui/event-forwarding/overview.md#properties) of selecteer een bestaande eigenschap die u wilt bewerken.

Selecteren **[!UICONTROL Extensions]** in de linkernavigatie. In de **[!UICONTROL Catalog]** selecteert u de **[!UICONTROL The Trade Desk]** Real-Time Conversions API-kaart, selecteer vervolgens **[!UICONTROL Install]**.

![De extensiecatalogus die de [!DNL The Trade Desk] installatie van markering voor extensiekaart.](../../../images/extensions/server/tradedesk/install-extension.png)

Voer in het volgende scherm de [!UICONTROL Advertiser ID]en eventueel een [!UICONTROL Merchant ID]. U kunt de id&#39;s rechtstreeks in deze invoer plakken of u kunt een gegevenselement gebruiken. Deze zullen als standaardwaarden dienen die worden gebruikt wanneer het maken van een gebeurtenisvraag aan [!DNL The Trade Desk] Conversies-API voor realtime. Selecteren **[!UICONTROL Save]** wanneer gereed.

Als u wilt leren hoe u gegevenselementen kunt maken en beschikbaar kunt maken voor extensies in de eigenschap Tag, volgt u de opdracht [Gegevenselementen maken](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) zelfstudie.

![De [!DNL The Trade Desk] extensieconfiguratiepagina met de [!UICONTROL Advertiser ID] en [!UICONTROL Merchant ID] gemarkeerde velden.](../../../images/extensions/server/tradedesk/configure-extension.png)

De uitbreiding is geïnstalleerd en u kunt zijn mogelijkheden in uw gebeurtenis nu gebruiken die regels door:sturen.

## Vorm een gebeurtenis door:sturen regel {#rule}

Nadat u de extensie hebt geïnstalleerd en geconfigureerd, kunt u beginnen met het maken van gebeurtenisregels die bepalen hoe en wanneer u gebeurtenissen wilt verzenden naar [!DNL The Trade Desk].

U zou moeten nadenken vormend verscheidene regels om allen te verzenden toegelaten [request-eigenschappen](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] en [!DNL The Trade Desk] Conversies-API voor realtime.

>[!NOTE]
>
>Gebeurtenissen moeten in real-time of zo dicht mogelijk bij real-time worden verzonden.

Een nieuwe gebeurtenis maken door:sturen [regel](../../../ui/managing-resources/rules.md) in uw gebeurtenis die bezit door:sturen. Onder **[!UICONTROL Actions]** voegt u een nieuwe handeling toe en stelt u de extensie in op **[!UICONTROL The Trade Desk]**. Selecteer vervolgens **[!UICONTROL Real Time Conversion]** voor de **[!UICONTROL Action Type]**.

![De gebeurtenis die de mening van de Regels van het Bezit door:sturen, met de gebieden die worden vereist om een gebeurtenis toe te voegen die de benadrukte configuratie van de regelactie door:sturen.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Na selectie, schijnen de extra controles om de gebeurtenisgegevens verder te vormen die zullen worden verzonden naar [!DNL The Trade Desk]. Selecteren **[!UICONTROL Keep Changes]** om de regel op te slaan.

De configuratieopties worden verdeeld in drie hoofdsecties, zoals hieronder beschreven:

**[!UICONTROL Basic Request Properties]**

| Invoer | Beschrijving |
| --- | --- |
| Beheer-id | De platform-id van de gebeurtenissencontrole. |
| UPixel ID | De universele pixel-id voor de gebeurtenis. |
| Referrer-URL | De URL van de website vanaf waar de gebeurtenis heeft plaatsgevonden, indien aanwezig. |
| Gebeurtenisnaam | Het type van gebeurtenis die door het partnerplatform wordt bepaald. |
| Waarde | De waarde voor het bijhouden van de omzet in een decimale tekenreeks (bijvoorbeeld &#39;19.98&#39;). |
| Valuta | Valutacode in ISO-indeling. |
| Client IP | Het client IPv4- of IPv6-adres. |
| ID advertentie | De unieke advertentie-id voor de gebeurtenis. |
| Type advertentie-id | Het type advertentie-id, gespecificeerd in de AD-ID-eigenschap: TDID, IDFA, AID, DAID, NAID, IDL, EUID of UID2. |
| Impressie | Een tekenreeks van 36 tekens (inclusief streepjes) die fungeert als unieke id voor de indruk waaraan de gebeurtenis wordt toegewezen. |
| Order-id | De bijbehorende orde-id van de gebeurtenis. |
| td1-td10 | Tien opeenvolgend genummerde aangepaste dynamische eigenschappen die kunnen worden gebruikt om extra omzettingsmeta-gegevens te verstrekken. |

{style="table-layout:auto"}

![De [!DNL Basic Request Properties] sectie met voorbeeldgegevens die in de velden worden ingevoerd.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Zie de [!DNL The Trade Desk] ontwikkelaarsdocumentatie voor meer informatie over de [request-eigenschappen](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) aanvaard door [!DNL The Trade Desk] Conversies-API voor realtime.

**[!UICONTROL Object Request Parameters]**

Lees de volgende sectie om over de JSON-Geformatteerde verzoekparameters zoals Punten, Privacy, en de Verwerking van Gegevens te leren.

![De [!DNL Object Request Parameters] sectie met beschikbare velden.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Zie de [Real-Time Conversions Event](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) documentatie voor meer informatie over de [!UICONTROL Object Request Parameters] en hun eigenschappen.

**[!UICONTROL Configuration Overrides]**

>OPMERKING
>
>De [!UICONTROL Configuration Overrides] met velden kunt u een andere instelling instellen [!DNL Advertiser ID] en/of [!DNL Merchant ID] op elke regel.

| Invoer | Beschrijving |
| --- | --- |
| Adverteerder-id | De Advertiser-id die u wilt overschrijven met de Advertiser-id die is opgegeven in de extensieconfiguratie. |
| Merchant ID | De Merchant-id die u wilt overschrijven met de Merchant-id die in de extensieconfiguratie is opgegeven. |

![De [!DNL Configuration Overrides] sectie met beschikbare velden.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Als u tevreden bent met de regel, selecteert u **[!UICONTROL Save to Library]**. Ten slotte publiceert u een nieuwe gebeurtenis die wordt doorgestuurd [build](../../../ui/publishing/builds.md) om de wijzigingen in de bibliotheek mogelijk te maken.

## Volgende stappen

In deze handleiding wordt beschreven hoe u gebeurtenisgegevens op de server kunt verzenden naar [!DNL The Trade Desk] met de [!DNL The Trade Desk] Conversies-API-extensie in realtime. Van hier, wordt het geadviseerd om uw integratie uit te breiden door duidelijke regels te creëren die specifieke omzettingsgebeurtenissen verzenden zoals toepasselijk per campagne. Voor meer informatie over gebeurtenis die mogelijkheden door:sturen in [!DNL Adobe Experience Platform], lees de [overzicht van gebeurtenissen doorsturen](../../../ui/event-forwarding/overview.md).

Zie de [!DNL The Trade Desk] documentatie over [beste praktijken voor [!DNL The Trade Desk] Real-Time Conversies API](https://www.facebook.com/business/help/308855623839366?id=818859032317965) voor meer begeleiding over hoe te om uw integratie effectief uit te voeren.

Voor details over hoe te om uw implementatie te zuiveren gebruikend het hulpmiddel van de Controle van Foutopsporing van het Experience Platform en van de Gebeurtenis door:sturen, lees [Overzicht van Adobe Experience Platform Debugger](../../../../debugger/home.md) en [Activiteiten controleren bij het doorsturen van gebeurtenissen](../../../ui/event-forwarding/monitoring.md).
