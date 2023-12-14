---
title: MediaAnalytics Interaction Details Schema Field Group
description: Leer over de MediaAnalytics het schemagroep van Details van de Interactie.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# [!UICONTROL MediaAnalytics Interaction Details] schemaveldgroep

[!UICONTROL MediaAnalytics Interaction Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Gebruik deze veldgroep om verrijkte gegevensvelden vast te leggen die de interactie met media-inhoud op verschillende platforms of kanalen volledig controleren en analyseren.

![Een schema van het schema [!UICONTROL MediaAnalytics Interaction Details] schemaveldgroep.](../../images/field-groups/mediaanalytics-interaction.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|---| --- | --- | --- |
| [!UICONTROL Media Collection Details] | `mediaCollection` | [[!UICONTROL Media details information]](../../data-types/media-details-information.md) | Attributen die betrekking hebben op een verzameling media-items. |
| [!UICONTROL Media Reporting Details] | `mediaReporting` | [[!UICONTROL Media details information]](../../data-types/media-details-information.md) | Gegevens en metriek rapporteren die aan de media-inhoud zijn gekoppeld. |
| [!UICONTROL List Of Media Collection Downloaded Content Events] | `mediaDownloadedEvents` | [!UICONTROL Array] van [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Gebeurtenissen die het downloaden van inhoud in de media-verzameling bijhouden. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json)
