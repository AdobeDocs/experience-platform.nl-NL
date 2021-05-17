---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: XDM ExperienceEvent-klasse
topic-legacy: overview
description: Dit document biedt een overzicht van de klasse XDM ExperienceEvent.
exl-id: a8e59413-b52f-4ea5-867b-8d81088a3321
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '1458'
ht-degree: 0%

---

# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] is een standaardklasse van het Gegevensmodel van de Ervaring (XDM) die u toestaat om een timestamped momentopname van het systeem tot stand te brengen wanneer een specifieke gebeurtenis voorkomt of een bepaalde reeks voorwaarden zijn bereikt.

Een ervaringsgebeurtenis is een feitenverslag van wat voorkwam, met inbegrip van het tijdstip en de identiteit van de betrokken persoon. Gebeurtenissen kunnen expliciet (direct waarneembare menselijke acties) of impliciet (zonder directe menselijke actie) zijn en worden geregistreerd zonder aggregatie of interpretatie. Voor meer informatie op hoog niveau over het gebruik van deze klasse in het Platform ecosysteem, verwijs naar [XDM overzicht](../home.md#data-behaviors).

De klasse [!DNL XDM ExperienceEvent] zelf verstrekt verscheidene op tijd-reeksen betrekking hebbende gebieden aan een schema. De waarden van sommige van deze velden worden automatisch ingevuld wanneer gegevens worden ingevoerd:

![](../images/classes/experienceevent/structure.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_id` | Een unieke tekenreeks-id voor de gebeurtenis. Dit veld wordt gebruikt om de unieke aard van een individuele gebeurtenis te volgen, om te voorkomen dat gegevens worden herhaald en om die gebeurtenis in downstreamdiensten op te zoeken.<br><br>In sommige gevallen,  `_id` kan een  [universeel Unieke Herkenningsteken (UUID)](https://tools.ietf.org/html/rfc4122) of  [Globally Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) zijn. In Adobe Experience Platform Data Prep kan deze waarde worden gegenereerd met de toewijzingsfuncties [`uuid` of `guid`](../../data-prep/functions.md#special-operations).<br><br>Als u gegevens streamt vanuit een bronverbinding of rechtstreeks vanuit een Parquet-bestand opgeeft, moet u deze waarde genereren door een aantal combinatievelden samen te voegen die de even unieke velden maken, zoals een primaire id, tijdstempel, gebeurtenistype, enzovoort.<br><br>Het is belangrijk om te onderscheiden dat  **dit veld geen identiteit vertegenwoordigt die verband houdt met een individuele persoon**, maar eerder de registratie van gegevens zelf. Identiteitsgegevens met betrekking tot een persoon moeten worden beperkt tot [identiteitsvelden](../schema/composition.md#identity) die in plaats daarvan door compatibele mixen worden verstrekt. |
| `eventMergeId` | Als u de [Adobe Experience Platform Web SDK](../../edge/home.md) gebruikt om gegevens in te voeren, vertegenwoordigt dit de id van de ingesloten batch die ervoor zorgde dat de record werd gemaakt. Dit veld wordt automatisch ingevuld door het systeem bij het invoeren van gegevens. Het gebruik van dit gebied buiten de context van een implementatie van SDK van het Web wordt niet gesteund. |
| `eventType` | Een tekenreeks die het type of de categorie voor de gebeurtenis aangeeft. Dit gebied kan worden gebruikt als u verschillende gebeurtenistypen binnen het zelfde schema en de dataset wilt onderscheiden, zoals het onderscheiden van een gebeurtenis van de productmening van toe:voegen-aan-winkelwagentje voor een detailhandelsbedrijf.<br><br>Standaardwaarden voor deze eigenschap worden gegeven in de  [ ](#eventType)bijlage, met inbegrip van beschrijvingen van het beoogde gebruik ervan. Dit veld is een uitbreidbare opsomming. Dit houdt in dat u ook uw eigen tekenreeksen voor gebeurtenistypen kunt gebruiken om de gebeurtenissen die u bijhoudt, te categoriseren. |
| `producedBy` | Een tekenreekswaarde die de producent of oorsprong van de gebeurtenis beschrijft. Dit veld kan worden gebruikt om bepaalde gebeurtenisproducenten uit te filteren als dat voor segmentatiedoeleinden nodig is.<br><br>Sommige voorgestelde waarden voor deze eigenschap zijn opgenomen in de  [appendix sectie](#producedBy). Dit veld is een uitbreidbare opsomming. Dit houdt in dat u ook uw eigen tekenreeksen kunt gebruiken om verschillende gebeurtenisproducenten te vertegenwoordigen. |
| `identityMap` | Een toewijzingsveld dat een set naamloze identiteiten bevat voor de persoon op wie de gebeurtenis van toepassing is. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. Als u dit veld correct wilt gebruiken voor [Real-time klantprofiel](../../profile/home.md), moet u niet handmatig de inhoud van het veld bijwerken in uw gegevensbewerkingen.<br /><br />Zie de sectie over identiteitskaarten in de  [grondbeginselen van schemacompositie voor meer informatie ](../schema/composition.md#identityMap) over hun gebruiksgeval. |
| `timestamp` | Een tijdstempel volgens ISO 8601 van het tijdstip van de gebeurtenis, opgemaakt volgens [RFC 339 Section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). Deze tijdstempel moet in het verleden voorkomen. Zie de sectie hieronder op [timestamps](#timestamps) voor beste praktijken op het gebruik van dit gebied. |

## Aanbevolen procedures voor het modelleren van gebeurtenissen

De volgende secties behandelen beste praktijken voor het ontwerpen van uw op gebeurtenis-gebaseerde schema&#39;s van de Gegevens van de Ervaring (XDM) in Adobe Experience Platform.

### Tijdstempels {#timestamps}

Het hoofdveld `timestamp` van een gebeurtenisschema kan **only** de waarneming van de gebeurtenis zelf vertegenwoordigen, en moet in het verleden voorkomen. Als voor uw segmentatiegebruik tijdstempels moeten worden gebruikt die in de toekomst kunnen voorkomen, moeten deze waarden elders in het schema van de Experience-gebeurtenis worden beperkt.

Als een bedrijf in de reis- en gastsector bijvoorbeeld een gebeurtenis voor reservering van vluchten modelleert, geeft het veld op klasseniveau `timestamp` het tijdstip weer waarop de reserveringsgebeurtenis werd waargenomen. Andere tijdstempels die verband houden met de gebeurtenis, zoals de begindatum van de reisreservering, moeten worden vastgelegd in afzonderlijke velden die worden verschaft door standaardmixen of aangepaste mixen.

![](../images/classes/experienceevent/timestamps.png)

Door de klasse-vlakke timestamp gescheiden van andere verwante datetime waarden in uw gebeurtenisschema&#39;s te houden, kunt u de flexibele gevallen van het segmentatiegebruik uitvoeren terwijl het bewaren van een timestamped rekening van klantenreizen in uw ervaringstoepassing.

### Berekende velden gebruiken

Bepaalde interacties in uw ervaringstoepassingen kunnen resulteren in meerdere gerelateerde gebeurtenissen die technisch dezelfde tijdstempel voor de gebeurtenis hebben en daarom kunnen worden weergegeven als één gebeurtenisrecord. Als een klant bijvoorbeeld een product op uw website weergeeft, kan dit resulteren in een gebeurtenisrecord die zowel kenmerken van de &quot;productweergave&quot; als enkele overlappende algemene kenmerken van de &quot;paginaweergave&quot; bevat. In deze gevallen kunt u berekende velden gebruiken om de belangrijkste kenmerken vast te leggen wanneer meerdere gebeurtenissen in een record worden vastgelegd.

[Met Adobe Experience Platform Data ](../../data-prep/home.md) kunt u gegevens toewijzen, transformeren en valideren naar en van XDM. Met behulp van de beschikbare [toewijzingsfuncties](../../data-prep/functions.md) die door de service worden geboden, kunt u logische operatoren aanroepen om gegevens uit records met meerdere gebeurtenissen te prioriteren, te transformeren en/of te consolideren wanneer deze in Experience Platform worden opgenomen.

Als u gegevens handmatig via de gebruikersinterface in het Platform invoert, raadpleegt u de handleiding bij [het toewijzen van een CSV-bestand aan XDM](../../ingestion/tutorials/map-a-csv-file.md) voor specifieke stappen voor het maken van berekende velden.

Als u gegevens aan Platform stroomt gebruikend een bronverbinding, kunt u de bron vormen om berekende gebieden in plaats daarvan te gebruiken. Raadpleeg de [documentatie voor uw specifieke bron](../../sources/home.md) voor instructies over hoe te om berekende gebieden uit te voeren wanneer het vormen van de verbinding.

## Compatibele schemagebiedgroepen {#field-groups}

>[!NOTE]
>
>De namen van verschillende veldgroepen zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../field-groups/name-updates.md) voor meer informatie.

Adobe biedt verschillende standaardveldgroepen voor gebruik met de klasse [!DNL XDM ExperienceEvent]. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

* [[!UICONTROL End User ID Details]](../field-groups/event/enduserids.md)
* [[!UICONTROL Environment Details]](../field-groups/event/environment-details.md)

## Aanhangsel

De volgende sectie bevat aanvullende informatie over de klasse [!UICONTROL XDM ExperienceEvent].

### Geaccepteerde waarden voor `eventType` {#eventType}

In de volgende tabel worden de geaccepteerde waarden voor `eventType` beschreven, samen met de bijbehorende definities:

| Value | Definitie |
| --- | --- |
| `advertising.completes` | Een getimede media-element is gecontroleerd op voltooiing. Dit betekent niet noodzakelijkerwijs dat de viewer de hele video heeft bekeken, aangezien de viewer vooruit had kunnen overgeslagen. |
| `advertising.timePlayed` | Beschrijft de hoeveelheid tijd die door een gebruiker aan een specifiek getimed media activa wordt doorgebracht. |
| `advertising.federated` | Geeft aan of een Experience Event is gemaakt via gegevensfederatie (gegevens delen tussen klanten). |
| `advertising.clicks` | Klik op een handeling(en) op een advertentie. |
| `advertising.conversions` | Vooraf gedefinieerde actie(s) uitgevoerd door een klant die een gebeurtenis voor prestatiebeoordeling start. |
| `advertising.firstQuartiles` | Een digitale video heeft 25% van de duur bij normale snelheid afgespeeld. |
| `advertising.impressions` | Indrukking(en) van een advertentie voor een klant die mogelijk wordt bekeken. |
| `advertising.midpoints` | Een digitale video heeft 50% van zijn duur bij normale snelheid afgespeeld. |
| `advertising.starts` | Er is een digitale video afgespeeld. |
| `advertising.thirdQuartiles` | Een digitale video heeft 75% van zijn duur bij normale snelheid afgespeeld. |
| `web.webpagedetails.pageViews` | Een webpagina heeft een of meer weergaven ontvangen. |
| `web.webinteraction.linkClicks` | Een koppeling is een of meer keer geselecteerd. |
| `commerce.checkouts` | Er is een uitcheckgebeurtenis opgetreden voor een productlijst. Er kunnen meerdere uitcheckgebeurtenissen zijn als er meerdere stappen in een uitcheckproces zijn. Als er meerdere stappen zijn, worden de tijdstempel en de pagina/ervaring waarnaar wordt verwezen voor elke gebeurtenis gebruikt om elke afzonderlijke gebeurtenis (stap) in volgorde weer te geven. |
| `commerce.productListAdds` | Er is een product toegevoegd aan de productlijst of winkelwagentje. |
| `commerce.productListOpens` | Er is een nieuwe productlijst (winkelwagentje) geïnitialiseerd of gemaakt. |
| `commerce.productListRemovals` | Een of meer productvermeldingen zijn uit een productlijst of winkelwagentje verwijderd. |
| `commerce.productListReopens` | Een productlijst (winkelwagentje) die niet meer toegankelijk (verlaten) was, is door een klant opnieuw geactiveerd, bijvoorbeeld via een hermarketingactiviteit. |
| `commerce.productListViews` | Een productlijst of winkelwagentje heeft een of meer weergaven ontvangen. |
| `commerce.productViews` | Een product heeft een of meer weergaven ontvangen. |
| `commerce.purchases` | Er is een bestelling geaccepteerd. Dit is de enige vereiste actie in een commerciële omschakeling. Een aankoopgebeurtenis moet een productlijst hebben waarnaar wordt verwezen. |
| `commerce.saveForLaters` | Er is een productlijst opgeslagen voor toekomstig gebruik, zoals een wenslijst voor een product. |
| `delivery.feedback` | Feedbackgebeurtenissen voor een levering, zoals een e-maillevering. |
| `message.feedback` | Feedbackgebeurtenissen zoals verzonden/stuit/fout voor berichten die naar een klant worden verzonden. |
| `message.tracking` | Gebeurtenissen bijhouden zoals open/klikken/aangepaste handelingen voor berichten die naar een klant worden verzonden. |

### Voorgestelde waarden voor `producedBy` {#producedBy}

In de volgende tabel worden enkele toegestane waarden voor `producedBy` weergegeven:

| Waarde | Definitie |
| --- | --- |
| `self` | Zelf |
| `system` | Systeem |
| `salesRef` | Verkoopvertegenwoordiger |
| `customerRep` | Vertegenwoordiger van klant |
