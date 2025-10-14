---
keywords: Experience Platform;home;populaire onderwerpen;Audience Manager-aansluiting;Auditiebeheer;publieksmanager
solution: Experience Platform
title: Audience Manager Source - Overzicht
description: De Adobe Audience Manager-bronstroom streamt gegevens van de eerste partij die in Audience Manager naar Adobe Experience Platform zijn verzameld.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---

# Audience Manager-bron

>[!IMPORTANT]
>
>Bij de eerste configuratie retourneert de Adobe Audience Manager-bron een foutbericht waarin wordt uitgelegd dat er geen naamruimte met een bepaalde naam `namespaceCode={VALUE}` bestaat. **Nota**: In het achterste eind, `namespaceCode` wordt gebruikt om naar identiteitssymbool te verwijzen. Om uw integratie te voltooien, moet u:
>
>- [&#x200B; creeer een douane namespace in de Dienst van de Identiteit &#x200B;](../../../identity-service/features/namespaces.md#create-custom-namespaces) met het gespecificeerde identiteitssymbool (`VALUE`).
>- Voer uw gegevens opnieuw in.

De Adobe Audience Manager-bronstroom streamt gegevens van de eerste partij die in Adobe Audience Manager zijn verzameld voor activering in Adobe Experience Platform. De Audience Manager-bron voert twee typen gegevens in op Experience Platform:

- **gegevens in real time:** Gegevens die in echt - tijd op de server van de de gegevensinzameling van Audience Manager worden gevangen. Deze gegevens worden gebruikt in Audience Manager om op regels gebaseerde kenmerken te vullen en zullen in Experience Platform in de kortste latentietijd verschijnen.
- **gegevens van het Profiel:** Audience Manager gebruikt real time en ongebogen gegevens om klantenprofielen af te leiden. Deze profielen worden gebruikt om identiteitsgrafieken en eigenschappen op segmentrealisaties te bevolken.

De Audience Manager-bron wijst deze gegevenstypen toe aan een XDM-schema (Experience Data Model) en verzendt deze vervolgens naar Experience Platform. In real time gegevens worden verzonden als gegevens XDM ExperienceEvent, terwijl de gegevens van het Profiel als gegevens van het Individuele Profiel XDM worden verzonden.

Voor meer informatie, lees de gids bij [&#x200B; het creëren van een Audience Manager bronverbinding in UI &#x200B;](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Wat is het Model van de Gegevens van de Ervaring (XDM)?

XDM is een openbaar gedocumenteerde specificatie die een gestandaardiseerd kader verstrekt waardoor Experience Platform gegevens van de klantenervaring organiseert.

Door zich aan XDM-standaarden te houden, kunnen gegevens voor klantervaring op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over hoe XDM in Experience Platform wordt gebruikt, lees het [&#x200B; overzicht van het Systeem XDM &#x200B;](../../../xdm/home.md). Meer over leren hoe de schema&#39;s XDM tussen profielen en gebeurtenissen gestructureerd zijn, lees de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../../../xdm/schema/composition.md).

## Voorbeelden van XDM-schema&#39;s

Hieronder volgen voorbeelden van de Audience Manager-structuur die is toegewezen aan XDM ExperienceEvent en XDM Individual Profile in Experience Platform.

### ExperienceEvent - voor realtime gegevens en onbeheerde gegevens

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Afzonderlijk XDM-profiel - voor profielgegevens

![](images/aam-profile-xdm-for-profile-data.png)

Voor informatie over hoe de gebieden van Audience Manager aan XDM in kaart worden gebracht, lees de documentatie over [&#x200B; de kaartgebieden van Audience Manager &#x200B;](./mapping/audience-manager.md).

## Gegevensbeheer op Experience Platform

### Gegevenssets

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat en door een gegevensverbinding ter beschikking wordt gesteld. Audience Manager-gegevens bestaan uit realtime gegevens, binnenkomende gegevens en profielgegevens. Om van uw datasets van Audience Manager de plaats te bepalen, gebruik de onderzoeksfunctie in UI met de verstrekte noemende overeenkomsten voor elk type van gegevens.

De datasets van Audience Manager worden onbruikbaar gemaakt voor Profiel door gebrek en de gebruikers hebben de capaciteit om datasets toe te laten of onbruikbaar te maken die op hun gebruiksgevallen worden gebaseerd. Het wordt niet geadviseerd om datasets onbruikbaar te maken die voor segmentlidmaatschap in Profiel zullen worden gebruikt.

>[!NOTE]
>
>AAM Real-time is de enige dataset die naar het data Lake gaat. Alle andere Audience Manager-gegevenssets gaan naar [!DNL Profile] als deze zijn ingeschakeld voor [!DNL Profile] . Als ze niet zijn ingeschakeld voor [!DNL Profile] , ontvangen ze geen gegevens en worden ze als leeg weergegeven.

| Naam gegevensset | Beschrijving | Klasse |
| --- | --- | --- |
| AAM Real-time | Deze dataset bevat gegevens die zijn verzameld door directe hits op Audience Manager DCS-eindpunten en identiteitskaarten voor Audience Manager-profielen. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. | Gebeurtenis Experience |
| AAM Updates voor realtime profiel | Deze dataset laat in real time het richten van de eigenschappen en de segmenten van Audience Manager toe. Het omvat informatie voor het regionale verpletteren van Edge, eigenschap, en segmentlidmaatschap. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de schakeloptie **[!UICONTROL Profile]** inschakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| AAM-apparaatgegevens | Apparaatgegevens met ECID&#39;s en bijbehorende segmentrealisaties geaggregeerd in Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de schakeloptie **[!UICONTROL Profile]** inschakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| AAM-apparaatprofielgegevens | Wordt gebruikt voor Audience Manager-connector diagnostiek. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de schakeloptie **[!UICONTROL Profile]** inschakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| AAM-geverifieerde profielen | Deze dataset bevat voor Audience Manager geauthenticeerde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de schakeloptie **[!UICONTROL Profile]** inschakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Metagegevens voor geverifieerde AAM-profielen | Wordt gebruikt voor diagnostiek van Audience Manager Connector. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de schakeloptie **[!UICONTROL Profile]** inschakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| AAM-apparaten - Gegevensback-up | Dataset van het brengen in vroegere apparatengegevens. Deze bevat ECID&#39;s en de bijbehorende segmentrealisaties die in Audience Manager zijn geaggregeerd. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de schakeloptie **[!UICONTROL Profile]** inschakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Backfill voor AAM-geverifieerde profielen | Dataset van het brengen in verleden voor authentiek verklaarde gegevens. Dit bevat Audience Manager-geverifieerde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de schakeloptie **[!UICONTROL Profile]** inschakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |

### Verbindingen

Adobe Audience Manager maakt één verbinding in Catalog: Audience Manager Connection. Catalog is het systeem van de verslagen voor gegevensplaats en lijn binnen Adobe Experience Platform. Een verbinding is een voorwerp van de Catalogus dat een klant-specifiek geval van schakelaars is. Gelieve te lezen het [&#x200B; overzicht van de Dienst van de Catalogus &#x200B;](../../../catalog/home.md) voor meer informatie over Catalogus, verbindingen, en schakelaars.

### Segmentpopulatie voor profieleffect

Grootte van segmentpopulatie heeft een directe invloed op profielnummers wanneer u voor het eerst een Audience Manager-segment naar Experience Platform verzendt. Dit betekent dat het selecteren van alle segmenten mogelijk Profieloverschrijdingen kan veroorzaken die uw gebruiksrechten voor licenties overschrijden. Experience Platform maakt ook onderscheid tussen nieuwe gegevens en historische gegevens voor het opnemen van profielen. Een segment met 100 op de eerste plaats gebaseerde identiteiten zal tot 100 profielen leiden. Als de populatie van hetzelfde segment echter tot 150 werd verhoogd en aan Experience Platform werd geconsumeerd, zal het aantal profielen slechts met 50 stijgen, aangezien er slechts 50 nieuwe profielen zijn.

U kunt het profielgebruik ook controleren uw rekening beschikbaar door het [&#x200B; dashboard van het Gebruik van de Vergunning &#x200B;](../../../dashboards/guides/license-usage.md) heeft.

## Wat is de verwachte vertraging voor Audience Manager Data op Experience Platform?

| Audience Manager-gegevens | Type | Latentie | Notities |
| --- | --- | --- | --- |
| Gegevens in realtime | Gebeurtenissen | &lt;25 minuten | Tijd van vastleggen op Audience Manager Edge-knooppunt tot verschijnen in data Lake. |
| Gegevens in realtime | Profielupdates | &lt;10 minuten | Tijd om in het Profiel van de Klant in real time te landen. |
| Gegevens in realtime en ongeboekt | Profielupdates | 24 tot 36 uur | Tijd vanaf het vastleggen via DCS/PCS Edge-gegevens en opgenomen gegevens, het verwerken naar een gebruikersprofiel en het vervolgens weergeven in Real-Time klantprofiel. Momenteel landen deze gegevens niet rechtstreeks in het datumpeer. De knevel van het profiel kan voor de datasets van het Profiel van Audience Manager worden toegelaten om deze gegevens direct in het Profiel van de Klant in real time in te voeren. |
