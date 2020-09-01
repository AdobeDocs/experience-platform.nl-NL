---
keywords: Experience Platform;home;popular topics;Audience Manager mapping;audience manager mapping
solution: Experience Platform
title: Veld voor Audience Manager toewijzen
topic: overview
description: De onderstaande tabellen bevatten de toewijzingen tussen de velden in Adobe Audience Manager-gegevens (Realtime, Onboard en Profielgegevens) en de bijbehorende XDM-velden.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Toewijzingsvelden voor Audience Managers

De onderstaande tabellen bevatten de toewijzingen tussen de velden in Adobe Audience Manager-gegevens (Realtime, Onboard en Profielgegevens) en de bijbehorende XDM-velden.

Zie het [XDM-veldwoordenboek](../../../../xdm/schema/field-dictionary.md) voor meer informatie over elk XDM-veld.

## Realtime gegevens

Type: Realtime gegevens

| Realtime-gegevensveld | XDM-veld |
| --- | --- |
| `requestIds[]` | `ExperienceEvent.identityMap["ECID"]` |
| `requestIds[]` | `ExperienceEvent.endUserIds` - *Alleen voor naamruimten in endUserIds en alleen voor de eerste waarde.* |
| `primaryDeviceId` | `ExperienceEvent.identityMap["CORE"]` |
| `primaryDeviceId` | ExperienceEvent.endUserIds - *Alleen voor naamruimten aanwezig in endUserIds en alleen voor de eerste waarde.* |
| `trait[] ` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
| `segments[]` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `mergeRules[]` | `ExperienceEvent.profileStitch[]` |
| `timestamps` | `ExperienceEvent.timeStamp` |
| `deviceMetadata` | `ExperienceEvent.device` <ul><li>primaryHardwareType → type</li><li>fabrikant → fabrikant</li><li>marketingName → model</li><li>modelNumber → model</li></ul> |
| `location` | `ExperienceEvent.placeContext.geo` <ul><li>d_land → landcode</li><li>d_state → stateProvince</li><li>d_city → stad</li><li>d_post → postcode</li><li>d_lat → latitude</li><li>d_longitude → longitude</li></ul> |
| `request_user_agent` | `ExperienceEvent.environment.browserDetails` <ul><li>h_user-agent → userAgent</li><li>h_accept-language → acceptLanguage</li></ul> |
| `client_ip` | `ExperienceEvent.environment` <ul><li>d_os_naam → naam </li><li>d_os_version → os_version</li></ul> |

## Profielgegevens

Type: Profiel XDM

| Profielveld | XDM-veld |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
