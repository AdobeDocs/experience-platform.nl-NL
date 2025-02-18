---
title: Marketo Engage-bestemming
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: c57a519b5a230dc62699808cf5c020d48cc79083
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 1%

---

# Marketo Engage-bestemming {#beta-marketo-engage-destination}

## Doelwijziging {#changelog}

>[!IMPORTANT]
>
>Met de versie van [ verbeterde de bestemmingsschakelaar van Marketo V2 ](/help/release-notes/2022/july-2022.md#destinations), ziet u nu twee kaarten van Marketo in de bestemmingscatalogus.
>* Als u al gegevens activeert naar het **[!UICONTROL Marketo V1]** -doel: maak nieuwe gegevensstromen naar het **[!UICONTROL Marketo V2]** -doel en verwijder bestaande gegevensstromen naar het **[!UICONTROL Marketo V1]** -doel tegen februari 2023. Vanaf die datum wordt de **[!UICONTROL Marketo V1]** doelkaart verwijderd.
>* Als u nog geen gegevensstromen naar de **[!UICONTROL Marketo V1]** bestemming hebt gemaakt, gebruikt u de nieuwe **[!UICONTROL Marketo V2]** -kaart om verbinding te maken met en gegevens te exporteren naar Marketo.

![ Beeld van de twee de bestemmingskaarten van Marketo in een zij-aan-zij mening.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Tot de verbeteringen in de Marketo V2-bestemming behoren:

* In de **[!UICONTROL Schedule segment]** stap van het activeringswerkschema, in Marketo V1, moest u a {**manueel toevoegen 1} Afbeelding identiteitskaart om gegevens naar Marketo met succes uit te voeren.** Deze handmatige stap is niet meer vereist in Marketo V2.
* In de **[!UICONTROL Mapping]** -stap van de activeringsworkflow was het in Marketo V1 mogelijk om XDM-velden toe te wijzen aan slechts drie doelvelden in Marketo: `firstName` , `lastName` en `companyName` . Met de Marketo V2-release kunt u nu XDM-velden toewijzen aan veel meer velden in Marketo. Voor meer informatie, lees de [ gesteunde attributen ](#supported-attributes) sectie verder hieronder.

## Overzicht {#overview}

[!DNL Marketo Engage] is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Hiermee kunt u activiteiten automatiseren en beheren van CRM-beheer en de betrokkenheid van klanten tot marketing en inkomstentoewijzing op basis van account.

De bestemming laat marketers toe om publiek te duwen dat in Adobe Experience Platform wordt gecreeerd aan Marketo waar zij als statische lijsten zullen verschijnen.

## Ondersteunde identiteiten en kenmerken {#supported-identities-attributes}

>[!NOTE]
>
>In de [ toewijzingsstap ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van het activerende bestemmingswerkschema, is het *verplicht* om identiteiten in kaart te brengen en *facultatief* om attributen in kaart te brengen. Het toewijzen van e-mail- en/of ECID via het tabblad Identiteitsnaamruimte is het belangrijkste wat u moet doen om ervoor te zorgen dat de persoon gelijk is aan de persoon in Marketo. Toewijzing via e-mail zorgt voor de hoogste match-rate.

### Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving |
|---|---|
| ECID | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ ECID ](/help/identity-service/features/ecid.md) voor meer informatie. |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |

{style="table-layout:auto"}

### Ondersteunde kenmerken {#supported-attributes}

U kunt kenmerken van Experience Platform toewijzen aan alle kenmerken waartoe uw organisatie in Marketo toegang heeft. In Marketo, kunt u [ gebruiken beschrijf API verzoek ](https://developers.marketo.com/rest-api/lead-database/leads/#describe) om de attributengebieden terug te winnen die uw organisatie toegang heeft tot.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [ ](../../../segmentation/home.md). |
| Aangepaste uploads | ✓ | Het publiek [ ingevoerde ](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers. |

{style="table-layout:auto"}

## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail, ECID) die in de [!DNL Marketo Engage] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [ het stromen bestemmingen ](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Doel instellen en publiek activeren {#set-up}

>[!IMPORTANT]
> 
>* Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig.
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [ toegangsbeheertoestemmingen ](/help/access-control/home.md#permissions) nodig. Lees het [ overzicht van de toegangscontrole ](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Voor gedetailleerde instructies op hoe te opstelling de bestemming en het publiek te activeren, lees [ duw een Push een Publiek van Adobe Experience Platform aan een Statische Lijst van Marketo ](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) in de documentatie van Marketo.

In de onderstaande video ziet u ook de stappen voor het configureren van een Marketo-bestemming en het activeren van het publiek.

>[!IMPORTANT]
>
>De video weerspiegelt niet volledig de huidige mogelijkheden. Voor de meest actuele informatie raadpleegt u de bovenstaande handleiding. De volgende delen van de video zijn verouderd:
> 
>* De doelkaart die u in de gebruikersinterface van Experience Platform moet gebruiken, is **[!UICONTROL Marketo V2]**.
>* De video geeft het nieuwe selectieveld **[!UICONTROL Person creation]** niet weer in de workflow Verbinding maken met doel. Als u dat veld wilt gebruiken, moet u zowel de voornaam als de achternaam toewijzen tijdens de stap voor kenmerktoewijzing.
>* De twee beperkingen die in de video worden aangeroepen, zijn niet meer van toepassing. U kunt nu veel andere profielkenmerkvelden toewijzen naast de lidmaatschapsgegevens voor het publiek die werden ondersteund op het moment dat de video werd opgenomen. U kunt ook publieksleden exporteren naar Marketo die nog niet in uw statische Marketo-lijsten voorkomen. Deze personen worden toegevoegd aan de lijsten.
>* In **[!UICONTROL Schedule audience step]** van de activeringsworkflow moest u in Marketo V1 handmatig een **[!UICONTROL Mapping ID]** toevoegen om gegevens te kunnen exporteren naar Marketo. Deze handmatige stap is niet meer vereist in Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

## Doel van monitor {#monitor-destination}

Na het verbinden met de bestemming en het vestigen van een bestemmingsdataflow, kunt u de [ controlefunctionaliteit ](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP gebruiken om uitgebreide informatie over de profielverslagen te krijgen die aan uw bestemming in elke dataflow in werking worden gesteld.

De monitoringinformatie voor de [!DNL Marketo Engage] -verbinding bevat informatie op publieksniveau over geactiveerde, uitgesloten en mislukte identiteiten in elke dataflow en dataflow die worden uitgevoerd. [Meer informatie](/help/dataflows/ui/monitor-destinations.md#segment-level-view) over de nieuwe functionaliteit.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [ gegeven beheer overzicht ](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

