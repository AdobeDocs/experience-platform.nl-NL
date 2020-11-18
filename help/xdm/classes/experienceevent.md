---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM ExperienceEvent, klasse
topic: overview
description: Dit document biedt een overzicht van de klasse XDM ExperienceEvent.
translation-type: tm+mt
source-git-commit: 4d109244e57799c7e3837ceee3e2f5d17fbf0a18
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---


# [!DNL XDM ExperienceEvent] class

[!DNL XDM ExperienceEvent] is een standaard XDM-klasse waarmee u een momentopname met tijdstempel van het systeem kunt maken wanneer een specifieke gebeurtenis plaatsvindt of een bepaalde set voorwaarden is bereikt.

Een ervaringsgebeurtenis is een feitenverslag van wat voorkwam, met inbegrip van het tijdstip en de identiteit van de betrokken persoon. Gebeurtenissen kunnen expliciet (direct waarneembare menselijke acties) of impliciet (zonder directe menselijke actie) zijn en worden geregistreerd zonder aggregatie of interpretatie. Raadpleeg het [XDM-overzicht](../home.md#data-behaviors)voor informatie op hoog niveau over het gebruik van deze klasse in het ecosysteem van het Platform.

De [!DNL XDM ExperienceEvent] klasse zelf verstrekt verscheidene op tijd-reeksen betrekking hebbende gebieden aan een schema. De waarden van sommige van deze velden worden automatisch ingevuld wanneer gegevens worden ingevoerd:

<img src="../images/classes/experienceevent.png" width="650" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `_id` | Een unieke, door het systeem gegenereerde tekenreeks-id voor de gebeurtenis. Dit veld wordt gebruikt om het unieke karakter van een individuele gebeurtenis te volgen, om dubbel werk van gegevens te voorkomen en om die gebeurtenis in downstreamdiensten op te zoeken. Aangezien dit veld door het systeem wordt gegenereerd, mag er tijdens het invoeren van gegevens geen expliciete waarde worden opgegeven.<br><br>Het is van belang te onderscheiden dat dit veld **geen** identiteit vertegenwoordigt die verband houdt met een individuele persoon, maar eerder de registratie van gegevens zelf. Identiteitsgegevens betreffende een persoon moeten in plaats daarvan worden beperkt tot [identiteitsvelden](../schema/composition.md#identity) . |
| `eventMergeId` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. Dit veld wordt automatisch ingevuld door het systeem bij het invoeren van gegevens. |
| `eventType` | Een tekenreeks die het primaire gebeurtenistype voor de record aangeeft. De aanvaarde waarden en de definities daarvan zijn opgenomen in de [bijlage](#eventType). |
| `identityMap` | Een toewijzingsveld dat een set naamloze identiteiten bevat voor de persoon op wie de gebeurtenis van toepassing is. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. Probeer niet handmatig de inhoud van het veld bij te werken in uw gegevensbewerkingen om dit veld correct te kunnen gebruiken voor [realtime klantprofiel](../../profile/home.md).<br /><br />Zie de sectie over identiteitskaarten in de [grondbeginselen van schemacompositie](../schema/composition.md#identityMap) voor meer informatie over hun gebruiksgeval. |
| `timestamp` | Het tijdstip waarop de gebeurtenis of waarneming heeft plaatsgevonden. Alle datetime waarden moeten in [formaat RFC 3339](https://tools.ietf.org/html/rfc3339) worden verstrekt. |

## Compatibele combinaties {#mixins}

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document over de updates [van de](../mixins/name-updates.md) mixnaam voor meer informatie.

Adobe biedt verschillende standaardmixen voor gebruik met de [!DNL XDM ExperienceEvent] klasse. Hieronder volgt een lijst met enkele veelgebruikte combinaties voor de klasse:

* [[!UICONTROL Gegevens van eindgebruiker]](../mixins/event/enduserids.md)
* [[!UICONTROL Omgevingsdetails]](../mixins/event/environment-details.md)

## Aanhangsel

De volgende sectie bevat aanvullende informatie over de [!UICONTROL klasse XDM ExperienceEvent] .

### Geaccepteerde waarden voor xdm:eventType {#eventType}

In de volgende tabel worden de geaccepteerde waarden voor `xdm:eventType`en de bijbehorende definities weergegeven:

| Waarde | Definitie |
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
| `web.webinteraction.linkClicks` | Een koppeling heeft een of meer klikken ontvangen. |
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