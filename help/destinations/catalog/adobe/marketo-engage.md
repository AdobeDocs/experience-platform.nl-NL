---
title: Bestemming Marketo Engage
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Marketo Engage bestemming {#beta-marketo-engage-destination}

## Doelwijziging {#changelog}

>[!IMPORTANT]
>
>Met de release van de [Uitgebreide Marketo V2-doelconnector](/help/release-notes/2022/july-2022.md#destinations)En nu ziet u twee Marketo-kaarten in de lijst met doelen.
>* Als u gegevens al activeert voor de **[!UICONTROL Marketo V1]** doel: Maak nieuwe gegevensstromen naar de **[!UICONTROL Marketo V2]** doel en verwijder bestaande gegevensstromen naar de **[!UICONTROL Marketo V1]** uiterlijk in februari 2023. Met ingang van die datum **[!UICONTROL Marketo V1]** de doelkaart wordt verwijderd.
>* Als u nog geen gegevens hebt gemaakt voor de **[!UICONTROL Marketo V1]** bestemming, gelieve te gebruiken nieuwe **[!UICONTROL Marketo V2]** om verbinding te maken met en gegevens te exporteren naar Marketo.

![Afbeelding van de twee Marketo-doelkaarten in een weergave Naast elkaar.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Tot de verbeteringen in de Marketo V2-bestemming behoren:

* In de **[!UICONTROL Schedule segment]** in Marketo V1 moet u handmatig een **Toewijzing-id** om gegevens naar Marketo te exporteren. Deze handmatige stap is niet meer vereist in Marketo V2.
* In de **[!UICONTROL Mapping]** In Marketo V1 kon u in stap van de activeringsworkflow XDM-velden toewijzen aan slechts drie doelvelden in Marketo: `firstName`, `lastName`, en `companyName`. Met de Marketo V2-release kunt u nu XDM-velden toewijzen aan veel meer velden in Marketo. Lees voor meer informatie de [ondersteunde kenmerken](#supported-attributes) hieronder.

## Overzicht {#overview}

[!DNL Marketo Engage] is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.

De bestemming laat marketers toe om publiek te duwen dat in Adobe Experience Platform wordt gecreeerd aan Marketo waar zij als statische lijsten zullen verschijnen.

## Ondersteunde identiteiten en kenmerken {#supported-identities-attributes}

>[!NOTE]
>
>In de [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de workflow voor het activeren van het doel is *verplicht* om identiteiten toe te wijzen en *optioneel* aan kaartkenmerken. Het toewijzen van e-mail- en/of ECID via het tabblad Identiteitsnaamruimte is het belangrijkste wat u moet doen om ervoor te zorgen dat de persoon gelijk is aan de persoon in Marketo. Toewijzing via e-mail zorgt voor de hoogste match-rate.

### Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving |
|---|---|
| ECID | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie . |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |

{style="table-layout:auto"}

### Ondersteunde kenmerken {#supported-attributes}

U kunt kenmerken van het Experience Platform toewijzen aan alle kenmerken waartoe uw organisatie toegang heeft in Marketo. In Marketo kunt u de opdracht [Beschrijf API-aanvraag](https://developers.marketo.com/rest-api/lead-database/leads/#describe) om de kenmerkvelden op te halen waartoe uw organisatie toegang heeft.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Door het Experience Platform gegenereerde soorten publiek [Segmenteringsservice](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Soorten publiek [geïmporteerd](../../../segmentation/ui/overview.md#import-audience) in Experience Platform van CSV-bestanden. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail, ECID) die worden gebruikt in het dialoogvenster [!DNL Marketo Engage] bestemming. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Doel instellen en publiek activeren {#set-up}

>[!IMPORTANT]
> 
>* Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions).
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.

Voor gedetailleerde instructies over hoe te opstelling de bestemming en activeert publiek [Een Adobe Experience Platform-publiek naar een statische Marketo-lijst duwen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) in de documentatie van Marketo.

In de onderstaande video ziet u ook de stappen voor het configureren van een Marketo-bestemming en het activeren van het publiek.

>[!IMPORTANT]
>
>De video weerspiegelt niet volledig de huidige mogelijkheden. Voor de meest actuele informatie raadpleegt u de bovenstaande handleiding. De volgende delen van de video zijn verouderd:
> 
>* De doelkaart die u in UI van het Experience Platform zou moeten gebruiken is **[!UICONTROL Marketo V2]**.
>* De nieuwe video wordt niet weergegeven **[!UICONTROL Person creation]** in het veld Verbinding maken met doel.
>* De twee beperkingen die in de video worden aangeroepen, zijn niet meer van toepassing. U kunt nu veel andere profielkenmerkvelden toewijzen naast de lidmaatschapsgegevens voor het publiek die werden ondersteund op het moment dat de video werd opgenomen. U kunt ook publieksleden exporteren naar Marketo die nog niet in uw statische Marketo-lijsten voorkomen. Deze personen worden toegevoegd aan de lijsten.
>* In de **[!UICONTROL Schedule audience step]** In Marketo V1 moest u handmatig een **[!UICONTROL Mapping ID]** om gegevens naar Marketo te exporteren. Deze handmatige stap is niet meer vereist in Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [gegevensbeheer - overzicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
