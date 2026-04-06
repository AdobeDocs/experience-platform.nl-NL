---
title: Marketo Engage-bestemming
description: Marketo Engage is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Gebruik dit programma om activiteiten te automatiseren en te beheren van CRM-beheer en de betrokkenheid van klanten tot marketing op basis van account en inkomstentoewijzing.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# (Verouderd) (V2) Marketo Engage-bestemming {#beta-marketo-engage-destination}

## Doelwijziging {#changelog}

<!--
>[!IMPORTANT]
>
>The **[!UICONTROL (Legacy) (V2) Marketo Engage]** will be deprecated in **March 2026**.
>
>To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** destination, review the following key points and required actions:
>
>* All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.
>* **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.

-->

![&#x200B; Beeld van de twee de bestemmingskaarten van Marketo in een zij-aan-zij mening.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Tot de verbeteringen in de Marketo V2-bestemming behoren:

* In de **[!UICONTROL Schedule segment]** stap van het activeringswerkschema, in Marketo V1, moest u a {**manueel toevoegen 1} Afbeelding identiteitskaart om gegevens naar Marketo met succes uit te voeren.** Deze handmatige stap is niet meer vereist in Marketo V2.
* In de **[!UICONTROL Mapping]** -stap van de activeringsworkflow was het in Marketo V1 mogelijk om XDM-velden toe te wijzen aan slechts drie doelvelden in Marketo: `firstName` , `lastName` en `companyName` . Met de Marketo V2-release kunt u nu XDM-velden toewijzen aan veel meer velden in Marketo. Voor meer informatie, lees de [&#x200B; gesteunde attributen &#x200B;](#supported-attributes) sectie verder hieronder.

## Overzicht {#overview}

[!DNL Marketo Engage] is de enige CXM-oplossing (end-to-end Customer Experience Management) voor marketing, reclame, analyse en handel. Gebruik dit programma om activiteiten te automatiseren en te beheren van CRM-beheer en de betrokkenheid van klanten tot marketing op basis van account en inkomstentoewijzing.

Met het doel kunnen marketers een publiek dat in [!DNL Adobe Experience Platform] is gemaakt, naar Marketo duwen waar het wordt weergegeven als statische lijsten.

## Ondersteunde identiteiten en kenmerken {#supported-identities-attributes}

>[!NOTE]
>
>In de [&#x200B; toewijzingsstap &#x200B;](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) van het activerende bestemmingswerkschema, is het *verplicht* om identiteiten in kaart te brengen en *facultatief* om attributen in kaart te brengen. Het toewijzen van e-mail- en/of ECID via het tabblad Identiteitsnaamruimte is het belangrijkste wat u moet doen om ervoor te zorgen dat de persoon gelijk is aan de persoon in Marketo. Toewijzing via e-mail zorgt voor de hoogste match-rate.

### Ondersteunde identiteiten {#supported-identities}

| Doelidentiteit | Beschrijving |
|---|---|
| ECID | Een naamruimte die ECID vertegenwoordigt. Deze namespace kan ook door de volgende aliassen worden bedoeld: &quot;identiteitskaart van Adobe Marketing Cloud&quot;, &quot;[!DNL Adobe Experience Cloud] identiteitskaart&quot;, &quot;[!DNL Adobe Experience Platform] identiteitskaart&quot;. Zie het volgende document op [&#x200B; ECID &#x200B;](/help/identity-service/features/ecid.md) voor meer informatie. |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte wordt vaak gekoppeld aan één persoon en identificeert daarom die persoon op verschillende kanalen. |

{style="table-layout:auto"}

### Ondersteunde kenmerken {#supported-attributes}

U kunt kenmerken van Experience Platform toewijzen aan alle kenmerken waartoe uw organisatie in Marketo toegang heeft. In Marketo, kunt u [&#x200B; gebruiken beschrijf API verzoek &#x200B;](https://developers.marketo.com/rest-api/lead-database/leads/#describe) om de attributengebieden terug te winnen die uw organisatie toegang heeft tot.

## Ondersteunde doelgroepen {#supported-audiences}

In deze sectie wordt beschreven welke soorten publiek u naar dit doel kunt exporteren.

| Oorsprong publiek | Ondersteund | Beschrijving |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Het publiek produceerde door de Dienst van de Segmentatie van Experience Platform [&#x200B; &#x200B;](../../../segmentation/home.md). |
| Alle andere doelgroepen | Nee | Deze categorie omvat alle oorsprong van het publiek buiten het publiek dat via [!DNL Segmentation Service] wordt gegenereerd. Lees over de [&#x200B; diverse publieksoorsprong &#x200B;](/help/segmentation/ui/audience-portal.md#customize). Voorbeelden zijn: <ul><li> de douane uploadt publiek [&#x200B; ingevoerde &#x200B;](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform van Csv- dossiers,</li><li> gelijksoortige doelgroepen, </li><li> federaal publiek, </li><li> publiek dat wordt gegenereerd in andere Experience Platform-toepassingen, zoals [!DNL Adobe Journey Optimizer] , </li><li> en meer. </li></ul> |

{style="table-layout:auto"}



Ondersteund publiek per type publieksgegevens:

| Gegevenstype Publiek | Ondersteund | Beschrijving | Gebruiksscenario&#39;s |
|--------------------|-----------|-------------|-----------|
| [&#x200B; het publiek van Mensen &#x200B;](/help/segmentation/types/people-audiences.md) | Ja | Gebaseerd op klantenprofielen, die u toestaan om specifieke groepen mensen voor marketing campagnes te richten. | Frequente kopers, winkeliers |
| [&#x200B; publiek van de Rekening &#x200B;](/help/segmentation/types/account-audiences.md) | Nee | Doelpersonen binnen specifieke organisaties voor marketingstrategieën op basis van account. | B2B-marketing |
| [&#x200B; Het publiek van het Vooruitzicht &#x200B;](/help/segmentation/types/prospect-audiences.md) | Nee | De individuen van het doel die nog geen klanten zijn maar eigenschappen met uw doelpubliek delen. | Waarschuwing met gegevens van derden |
| [&#x200B; de uitvoer van de Dataset &#x200B;](/help/catalog/datasets/overview.md) | Nee | Verzamelingen gestructureerde gegevens die zijn opgeslagen in het [!DNL Adobe Experience Platform] Data Lake. | Rapportage, workflows voor gegevenswetenschap |

{style="table-layout:auto"}


## Type en frequentie exporteren {#export-type-frequency}

Raadpleeg de onderstaande tabel voor informatie over het exporttype en de exportfrequentie van de bestemming.

| Item | Type | Notities |
|---------|----------|---------|
| Exporttype | **[!UICONTROL Audience export]** | U exporteert alle leden van een publiek met de id&#39;s (e-mail, ECID) die in de [!DNL Marketo Engage] -bestemming worden gebruikt. |
| Exportfrequentie | **[!UICONTROL Streaming]** | Streaming doelen zijn &quot;altijd aan&quot; API-verbindingen. Zodra een profiel in Experience Platform wordt bijgewerkt dat op publieksevaluatie wordt gebaseerd, verzendt de schakelaar de update stroomafwaarts naar het bestemmingsplatform. Lees meer over [&#x200B; het stromen bestemmingen &#x200B;](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Doel instellen en publiek activeren {#set-up}

>[!IMPORTANT]
>
>* Om met de bestemming te verbinden, hebt u **[!UICONTROL View Destinations]** en **[!UICONTROL Manage Destinations]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig.
>* Om gegevens te activeren, hebt u **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, en **[!UICONTROL View Segments]** [&#x200B; toegangsbeheertoestemmingen &#x200B;](/help/access-control/home.md#permissions) nodig. Lees het [&#x200B; overzicht van de toegangscontrole &#x200B;](/help/access-control/ui/overview.md) of contacteer uw productbeheerder om de vereiste toestemmingen te verkrijgen.

Voor gedetailleerde instructies op hoe te opstelling de bestemming en het publiek te activeren, lees [&#x200B; duw een Push een Publiek van Adobe Experience Platform aan een Statische Lijst van Marketo &#x200B;](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) in de documentatie van Marketo.

In de onderstaande video ziet u ook de stappen voor het configureren van een Marketo-bestemming en het activeren van het publiek.

>[!IMPORTANT]
>
>De video weerspiegelt niet volledig de huidige mogelijkheden. Raadpleeg de bovenstaande handleiding voor de meest actuele informatie. De volgende delen van de video zijn verouderd:
> 
>* De doelkaart die u in de gebruikersinterface van Experience Platform moet gebruiken, is **[!UICONTROL Marketo V2]**.
>* De video geeft het nieuwe selectieveld **[!UICONTROL Person creation]** niet weer in de workflow Verbinding maken met doel. Als u dat veld wilt gebruiken, moet u zowel de voornaam als de achternaam toewijzen tijdens de stap voor kenmerktoewijzing.
>* De twee beperkingen die in de video worden aangeroepen, zijn niet meer van toepassing. U kunt nu veel andere profielkenmerkvelden toewijzen naast de lidmaatschapsgegevens voor het publiek die werden ondersteund op het moment dat de video werd opgenomen. U kunt ook publieksleden exporteren naar Marketo die nog niet in uw statische Marketo-lijsten voorkomen. Deze personen worden toegevoegd aan de lijsten.
>* In **[!UICONTROL Schedule audience step]** van de activeringsworkflow moest u in Marketo V1 handmatig een **[!UICONTROL Mapping ID]** toevoegen om gegevens te kunnen exporteren naar Marketo. Deze handmatige stap is niet meer vereist in Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

## Doel van monitor {#monitor-destination}

Na het verbinden met de bestemming en het vestigen van een bestemmingsdataflow, kunt u [&#x200B; controlefunctionaliteit &#x200B;](/help/dataflows/ui/monitor-destinations.md) in [!DNL Real-Time CDP] gebruiken om uitgebreide informatie over de profielverslagen te krijgen die aan uw bestemming in elke dataflow in werking worden gesteld.

De monitoringinformatie voor de [!DNL Marketo Engage] -verbinding bevat informatie op publieksniveau over geactiveerde, uitgesloten en mislukte identiteiten in elke dataflow en dataflow die worden uitgevoerd. [Lees meer](/help/dataflows/ui/monitor-destinations.md#segment-level-view) over de nieuwe functionaliteit.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] -doelen zijn compatibel met het beleid voor gegevensgebruik bij het verwerken van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] gegevensbeheer afdwingt, zie het [&#x200B; gegeven beheer overzicht &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
