---
title: MediaAnalytics Interaction Details Schema Field Group
description: Leer over de MediaAnalytics het schemagroep van Details van de Interactie.
exl-id: 1096d28a-5796-49cc-bd45-b3f5188f699e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# [!UICONTROL MediaAnalytics Interaction Details] schemaveldgroep

[!UICONTROL MediaAnalytics Interaction Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md). Gebruik deze veldgroep om verrijkte gegevensvelden vast te leggen die de interactie met media-inhoud op verschillende platforms of kanalen volledig controleren en analyseren.

![ het schemadiagram van A van de [!UICONTROL MediaAnalytics Interaction Details] groep van het schemagebied.](../../images/field-groups/mediaanalytics-interaction.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|---| --- | --- | --- |
| [!UICONTROL Media Collection Details] | `mediaCollection` | [[!UICONTROL Media Collection details]](../../data-types/media-collection-details.md) | Attributen die betrekking hebben op een verzameling media-items. Met de velden Media Collection kunt u gegevens vastleggen en naar andere Adobe-services verzenden voor verdere verwerking. |
| [!UICONTROL Media Reporting Details] | `mediaReporting` | [[!UICONTROL Media Reporting details]](../../data-types/media-reporting-details.md) | Gegevens en metriek rapporteren die aan de media-inhoud zijn gekoppeld. * Media Reporting-velden worden door Adobe-services gebruikt voor het analyseren van de velden Media Collection die door gebruikers worden verzonden. Deze gegevens worden, samen met andere specifieke maatstaven voor gebruikers, berekend en gerapporteerd. |
| [!UICONTROL List Of Media Collection Downloaded Content Events] | `mediaDownloadedEvents` | [!UICONTROL Array] van [[!UICONTROL mediaEvent]](../../data-types/media-event-information.md) | Gebeurtenissen die het downloaden van inhoud in de media-verzameling bijhouden. |

{style="table-layout:auto"}

>[!TIP]
>
>U kunt velden verbergen die niet worden gebruikt door de Media Edge API. Het verbergen van deze gebieden maakt het schema gemakkelijker te lezen en te begrijpen, maar het wordt niet vereist. Deze velden verwijzen alleen naar de velden in de veldgroep [!UICONTROL MediaAnalytics Interaction Details] . Om leesbaarheid in Experience Platform UI te verbeteren, volg de instructies in de [ documentatie van de Analytics van Media op hoe te om ongebruikte gebieden ](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) te verbergen.

<!-- 
>[!NOTE]
>
>Schemas contain fields that are not used in every context or situation. They provide a potential blueprint to map an object. Schemas displayed for the Media Edge API Collection or Reporting data types only portray the relevant fields. You can manually select and deselect the fields that you want to use if you intend to use a schema for the Media Edge API interaction. You can find instructions on [hiding unnecessary fields](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/implementation-edge.html#set-up-the-schema-in-adobe-experience-platform) in the guide to install Media Analytics with Experience Platform Edge.
 -->
