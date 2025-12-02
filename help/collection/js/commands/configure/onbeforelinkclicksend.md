---
title: onBeforeLinkClickSend
description: Callback die net alvorens verbinding het volgen gegevens wordt verzonden.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Deze callback is vervangen. Gebruik in plaats hiervan [`clickCollection.filterClickDetails`](clickcollection.md) .

Met de callback van `onBeforeLinkClickSend` kunt u een JavaScript-functie registreren die de gegevens voor het bijhouden van koppelingen die u verzendt, kan wijzigen voordat die gegevens naar Adobe worden verzonden. Hiermee kunt u het object `xdm` of `data` bewerken, inclusief de mogelijkheid om elementen toe te voegen, te bewerken of te verwijderen. U kunt het verzenden van gegevens ook voorwaardelijk annuleren, zoals met ontdekt cliënt-zijbot verkeer.

Deze callback wordt alleen uitgevoerd als [`clickCollectionEnabled`](clickcollectionenabled.md) is ingeschakeld en `filterClickDetails` geen geregistreerde functie bevat.

Als [`onBeforeEventSend`](onbeforeeventsend.md) en `onBeforeLinkClickSend` allebei geregistreerde functies bevatten, wordt `onBeforeLinkClickSend` eerst uitgevoerd.

>[!WARNING]
>
>Deze callback staat het gebruik van douanecode toe. Als een code die u in de callback opneemt, een niet-afgevangen uitzondering genereert, wordt de verwerking voor de gebeurtenis gestopt. Gegevens worden niet naar Adobe verzonden.

## `onBeforeLinkClickSend` en `filterClickDetails`

De callback van [`clickCollection.filterClickDetails`](clickcollection.md) is ontworpen om `onBeforeLinkClickSend` te vervangen. Adobe raadt beide callback-functies niet tegelijkertijd aan. Wanneer u een callback-functie toewijst aan zowel `filterClickDetails` als `onBeforeLinkClickSend` , gebruikt de bibliotheek de volgende logica:

* Alleen `filterClickDetails` wordt uitgevoerd; `onBeforeLinkClickSend` niet.
* Gebeurtenisgroepering `clickCollection.eventGroupingEnabled` werkt niet.
