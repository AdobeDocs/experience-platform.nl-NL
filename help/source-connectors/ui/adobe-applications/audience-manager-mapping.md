---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Toewijzingsveld voor Audiontanager
topic: overview
translation-type: tm+mt
source-git-commit: 985c450a174712fa4b4185d5a6527962e697b5ba

---


# Toewijzingsveld voor Audiontanager

De onderstaande tabellen bevatten de toewijzingen tussen de velden in Adobe Audience Manager-gegevens (Realtime, Onboded en Profielgegevens) en de bijbehorende XDM-velden.

Zie het [XDM-veldwoordenboek](../../../xdm/schema/field-dictionary.md) voor meer informatie over elk XDM-veld.

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
| `Signals` | ExperienceEvent.signes |

## Binnenkomende gegevens **(afgekeurd)**

Type: ExperienceEvent

| Binnenkomend veld | XDM-veld |
| --- | --- |
| `uuid` | `ExperienceEvent.identityMap[<ID Type>]` |
| `deviceIds` | `ExperienceEvent.identityMap["CORE"] And calculated ECIDs  ExperienceEvent.identityMap["ECID"]` |
| `signals` | `ExperienceEvent.signals` |
| `b_time` | `ExperienceEvent.timeStamp` |
| `overwrite` | `overwriteTraits` |

>[!NOTE] Binnenkomende velden worden in een toekomstige versie afgekeurd.

## Profielgegevens

Type: Profiel XDM

| Profielveld | XDM-veld |
| --- | --- |
| `ids` | `identityMap` |
| `smem` | `ExperienceEvent.segmentMemberships["AAMSegments"]` |
| `tmem` | `ExperienceEvent.segmentMemberships["AAMTraits"]` |
