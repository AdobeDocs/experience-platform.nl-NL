---
title: Marketo Engage-bestemming
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: e68bbc07f7d2e4e05b725cbef37a1810a5825742
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# Marketo Engage-bestemming {#beta-marketo-engage-destination}

## Doelwijziging {#changelog}

>[!IMPORTANT]
>
>Met de release van de [Uitgebreide Marketo V2-doelconnector](/help/release-notes/2022/july-2022.md#destinations)En nu ziet u twee Marketo-kaarten in de lijst met doelen.
>* Als u gegevens al activeert voor de **[!UICONTROL Marketo V1]** bestemming: Maak nieuwe gegevensstromen naar de **[!UICONTROL Marketo V2]** doel en verwijder bestaande gegevensstromen naar **[!UICONTROL Marketo V1]** uiterlijk in februari 2023. Met ingang van die datum **[!UICONTROL Marketo V1]** de doelkaart wordt verwijderd.
>* Als u nog geen gegevens hebt gemaakt voor de **[!UICONTROL Marketo V1]** bestemming, gelieve te gebruiken nieuwe **[!UICONTROL Marketo V2]** om verbinding te maken met en gegevens te exporteren naar Marketo.


![Afbeelding van de twee Marketo-doelkaarten in een weergave Naast elkaar.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Tot de verbeteringen in de Marketo V2-bestemming behoren:

* In de **[!UICONTROL Schedule segment]** in Marketo V1 moet u handmatig een **Toewijzing-id** om gegevens naar Marketo te exporteren. Deze handmatige stap is niet meer vereist in Marketo V2.
* In de **[!UICONTROL Mapping]** In Marketo V1 kon u in stap van de activeringsworkflow XDM-velden toewijzen aan slechts drie doelvelden in Marketo: `firstName`, `lastName`, en `companyName`. Met de Marketo V2-release kunt u nu XDM-velden toewijzen aan veel meer velden in Marketo. Lees voor meer informatie de [ondersteunde kenmerken](#supported-attributes) hieronder.

## Overzicht {#overview}

[!DNL Marketo Engage] is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.

De bestemming laat marketers toe om segmenten te duwen die in Adobe Experience Platform aan Marketo worden gecreeerd waar zij als statische lijsten zullen verschijnen.

## Ondersteunde identiteiten en kenmerken {#supported-identities-attributes}

>[!NOTE]
>
>In de [toewijzingsstap](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van de doelworkflow activeren: *verplicht* om identiteiten toe te wijzen en *optioneel* om kenmerken toe te wijzen. Het toewijzen van e-mail- en/of ECID via het tabblad Identiteitsnaamruimte is het belangrijkste wat u moet doen om ervoor te zorgen dat de persoon gelijk is aan de persoon in Marketo. Toewijzing via e-mail zorgt voor de hoogste match-rate.

### Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving |
|---|---|
| ECID | Een naamruimte die ECID vertegenwoordigt. Naar deze naamruimte kan ook worden verwezen door de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ECID](/help/identity-service/ecid.md) voor meer informatie . |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |

{style=&quot;table-layout:auto&quot;}

### Ondersteunde kenmerken {#supported-attributes}

U kunt kenmerken van het Experience Platform toewijzen aan alle kenmerken waartoe uw organisatie toegang heeft in Marketo. In Marketo kunt u de opdracht [Beschrijf API-aanvraag](https://developers.marketo.com/rest-api/lead-database/leads/#describe) om de kenmerkvelden op te halen waartoe uw organisatie toegang heeft.

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Segment export]** | U exporteert alle leden van een segment (publiek) met de id&#39;s (e-mail, ECID) die worden gebruikt in het dialoogvenster [!DNL Marketo Engage] bestemming. |
| Uitvoerfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op segmentevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Meer informatie over [streaming doelen](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Doel instellen en segmenten activeren {#set-up}

>[!IMPORTANT]
> 
>* Om met de bestemming te verbinden, hebt u nodig **[!UICONTROL Manage Destinations]** [toegangsbeheermachtiging](/help/access-control/home.md#permissions).
>* Als u gegevens wilt activeren, hebt u de opdracht **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [toegangsbeheermachtigingen](/help/access-control/home.md#permissions). Lees de [toegangsbeheeroverzicht](/help/access-control/ui/overview.md) of neem contact op met de productbeheerder om de vereiste machtigingen te verkrijgen.


Voor gedetailleerde instructies over hoe te opstelling de bestemming en activeert segmenten, lees [Een Adobe Experience Platform-segment naar een statische Marketo-lijst verplaatsen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) in de documentatie van Marketo.

In de onderstaande video ziet u ook de stappen voor het configureren van een Marketo-bestemming en het activeren van segmenten.

>[!IMPORTANT]
>
>De video weerspiegelt niet volledig de huidige mogelijkheden. Voor de meest actuele informatie raadpleegt u de bovenstaande handleiding. De volgende delen van de video zijn verouderd:
> 
>* De doelkaart die u in UI van het Experience Platform zou moeten gebruiken is **[!UICONTROL Marketo V2]**.
>* De nieuwe video wordt niet weergegeven **[!UICONTROL Person creation]** in het veld Verbinding maken met doel.
>* De twee beperkingen die in de video worden aangeroepen, zijn niet meer van toepassing. U kunt nu vele andere gebieden van profielattributen naast de informatie van het segmentlidmaatschap in kaart brengen die op het ogenblik werd gesteund de video werd geregistreerd. U kunt ook segmentleden exporteren naar Marketo die nog niet voorkomen in uw statische Marketo-lijsten. Deze leden worden toegevoegd aan de lijsten.
>* In de **[!UICONTROL Schedule segment step]** van de activeringsworkflow moest u in Marketo V1 handmatig een **[!UICONTROL Mapping ID]** om gegevens naar Marketo te exporteren. Deze handmatige stap is niet meer vereist in Marketo V2.


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] handhaaft gegevensbeheer, zie [gegevensbeheer - overzicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
