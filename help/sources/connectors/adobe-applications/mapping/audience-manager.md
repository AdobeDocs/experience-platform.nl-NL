---
keywords: Experience Platform;thuis;populaire onderwerpen;Audience Manager toewijzen;publieksbeheertoewijzing
solution: Experience Platform
title: Toewijzingsvelden voor de Adobe Audience Manager Source Connector
topic-legacy: overview
description: Leer hoe u Adobe Audience Manager-gegevens (Realtime, Onboard en Profielgegevens) toewijst aan corresponderende XDM-velden (Experience Data Model) voor de Audience Manager-bronaansluiting.
exl-id: b800ba43-c308-4334-adce-3d554d50cefb
translation-type: tm+mt
source-git-commit: af5564a07577a0123e1a45043d5479f6ad45d73e
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Veldtoewijzingen Audience Manager

De onderstaande tabellen bevatten de toewijzingen tussen de velden in Adobe Audience Manager-gegevens (Realtime, Onboard en Profielgegevens) en de bijbehorende XDM-velden.

Zie [XDM-veldwoordenboek](../../../../xdm/schema/field-dictionary.md) voor meer informatie over elk XDM-veld.

## Realtime gegevens

Type: Realtime gegevens

| Realtime-gegevensveld | XDM-veld |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` -  *Alleen voor naamruimten in endUserIds en alleen voor de eerste waarde.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Alleen voor naamruimten aanwezig in endUserIds en alleen de eerste waarde.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → type</li><li>fabrikant → fabrikant</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_land → landcode</li><li>d_state → stateProvince</li><li>d_city → stad</li><li>d_post → postcode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_naam → naam </li><li>d_os_version → os_version</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Profielgegevens

Type: Profiel XDM

| Profielveld | XDM-veld |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |

{style=&quot;table-layout:auto&quot;}
