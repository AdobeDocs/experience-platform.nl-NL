---
keywords: Experience Platform;home;populaire onderwerpen;identiteit;Identiteit;XDM grafieken;Identiteitsservice;Identiteitsservice
solution: Experience Platform
title: Overzicht van identiteitsservice
description: Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 0%

---

# Adobe Experience Platform Identity Service

Om relevante digitale ervaringen te kunnen bieden, hebt u een uitgebreide en nauwkeurige weergave nodig van de echte entiteiten waaruit uw klantenbestand bestaat.

Organisaties en bedrijven hebben tegenwoordig te maken met een groot aantal verschillende datasets: uw individuele klanten worden vertegenwoordigd door een verscheidenheid aan verschillende id&#39;s. Uw klant kan worden gekoppeld aan verschillende webbrowsers (Safari, Google Chrome), hardwareapparaten (telefoons, laptops) en andere personen-id&#39;s (CRM-id&#39;s, e-mailaccounts). Zo ontstaat een onsamenhangende weergave van uw klant.

U kunt deze uitdagingen met de Dienst van de Identiteit van Adobe Experience Platform en zijn mogelijkheden oplossen:

* Een **identiteitsgrafiek** die verschillende identiteiten met elkaar verbindt, zodat u een visuele vertegenwoordiging van krijgt hoe een klant met uw merk over verschillende kanalen interactie aangaat.
* Maak een grafiek voor Real-Time Klantprofiel, die vervolgens wordt gebruikt om een uitgebreide weergave van de klant te maken door kenmerken en gedragingen samen te voegen.
* Voer validatie en foutopsporing uit met de verschillende gereedschappen.

Dit document biedt een overzicht van Identiteitsservice en hoe u de functionaliteit ervan kunt gebruiken binnen de context van het Experience Platform.

## Terminologie {#terminology}

Lees, voordat u op de details van Identity Service gaat duiken, de volgende tabel voor een overzicht van de belangrijkste termen:

| Term | Definitie |
| --- | --- |
| Identiteit | Een identiteit is gegevens die uniek zijn voor een entiteit. Dit is doorgaans een echt object, zoals een individuele persoon, een hardwareapparaat of een webbrowser (vertegenwoordigd door een cookie). Een volledig gekwalificeerde identiteit bestaat uit twee elementen: een **naamruimte identity** en **identiteitswaarde**. |
| Naamruimte identiteit | Een naamruimte voor identiteiten is de context van een bepaalde identiteit. Bijvoorbeeld een naamruimte van `Email` kan overeenkomen met de identiteitswaarde: **julien<span>@acme.com**. Een naamruimte van `Phone` kan overeenkomen met de identiteitswaarde: `555-555-1234`. Lees voor meer informatie de [Overzicht van naamruimte in identiteit](./features/namespaces.md). |
| Identiteitswaarde | Een identiteitswaarde is een koord dat een real-world entiteit vertegenwoordigt en binnen de Dienst van de Identiteit door namespace gecategoriseerd is. De identiteitswaarde (tekenreeks) **julien<span>@acme.com** kan worden gecategoriseerd als `Email` naamruimte. |
| Identiteitstype | Een identiteitstype is een component van een naamruimte voor identiteiten. Het identiteitstype geeft aan of identiteitsgegevens al dan niet zijn gekoppeld in een identiteitsgrafiek. |
| Koppeling | Een koppeling of een koppeling is een methode om vast te stellen dat twee verschillende identiteiten dezelfde entiteit vertegenwoordigen. Bijvoorbeeld een koppeling tussen &quot;`Email` = julien<span>@acme.com&quot; en &quot;`Phone` = 555-555-1234&quot; betekent dat beide identiteiten dezelfde entiteit vertegenwoordigen. Dit suggereert dat de klant die met uw merk met zowel het e-mailadres van julien als interactie heeft gehad<span>@acme.com en het telefoonnummer 555-555-1234 is hetzelfde. |
| Identiteitsservice | De Dienst van de identiteit is de dienst binnen Experience Platform die (of unlinks) identiteiten verbindt om identiteitsgrafieken te handhaven. |
| Identiteitsgrafiek | De identiteitsgrafiek is een inzameling van identiteiten die één enkele klant vertegenwoordigen. Lees voor meer informatie de handleiding op [de viewer voor identiteitsgrafieken gebruiken](./features/identity-graph-viewer.md). |
| Klantprofiel in realtime | Real-Time klantprofiel is een service in Adobe Experience Platform die: <ul><li>Hiermee voegt u profielfragmenten samen om een profiel te maken op basis van een identiteitsgrafiek.</li><li>Segmenteert profielen zodat deze vervolgens naar de bestemming kunnen worden verzonden voor activering.</li></ul> |
| Profiel | Een profiel is een weergave van een onderwerp, een organisatie of een individu. Een profiel bestaat uit vier elementen: <ul><li>Attributen: kenmerken geven informatie zoals naam, leeftijd of geslacht.</li><li>Gedrag: gedrag geeft informatie over de activiteiten van een bepaald profiel. Een profielgedrag kan bijvoorbeeld zien of een bepaald profiel &quot;naar sandalen zoeken&quot; of &quot;naar t-shirts opdracht geven&quot; was.</li><li>Identiteiten: voor een samengevoegd profiel wordt hier informatie gegeven over alle identiteiten die aan de persoon zijn gekoppeld. Identiteiten kunnen in drie categorieën worden ingedeeld: Persoon (CRMID, e-mail, telefoon), apparaat (IDFA, GAID) en cookie (ECID, STEUN).</li><li>Lidmaatschap van het publiek: De groepen waarin het profiel tot (loyale gebruikers, gebruikers die in Californië wonen, enz.) behoort</li></ul> |

{style="table-layout:auto"}

## Wat is identiteitsdienst?

![Identiteitskoppelen op platform](./images/identity-service-stitching.png)

In een B2C-context (Business-To-Customer) communiceren klanten met uw bedrijf en maken ze een relatie met uw merk. Een typische klant kan actief zijn in om het even welk aantal systemen binnen de gegevensinfrastructuur van uw organisatie. Om het even welke bepaalde klant kan binnen uw e-handel, loyaliteit, en helpdesksystemen actief zijn. Die zelfde klant kan ook anoniem of door voor authentiek verklaarde middelen op om het even welk aantal verschillende apparaten aanspreken.

Overweeg de volgende klantenreis:

* Julien heeft een account op uw e-commercewebsite gemaakt en in het verleden een aantal items besteld. Julien gebruikt doorgaans haar persoonlijke laptop om te winkelen en zich bij elke gebruikstijd aan te melden bij haar account.
* Tijdens een van haar bezoeken aan uw site gebruikt ze echter een tablet om naar sandalen te zoeken. Tijdens deze sessie, omdat ze een ander apparaat gebruikte, meldt ze zich niet aan en plaatst ze geen bestelling.
* Op dit moment worden de activiteiten van Julien in twee afzonderlijke profielen weergegeven:
   * Haar eerste profiel is haar aanmeldings-id voor e-commerce. Dit profiel wordt gebruikt wanneer zij een gebruikersbenaming en een wachtwoordcombinatie gebruikt om haar zitting op uw e-commercesplaats voor authentiek te verklaren. Dit profiel wordt geïdentificeerd door een apparaat-id.
   * Haar tweede profiel is haar tabletapparaat. Dit profiel is gemaakt nadat ze anoniem door uw e-commercesite heeft gebladerd met een tablet zonder u aan te melden bij haar account. Dit profiel wordt geïdentificeerd door een cookie-id.
* Later hervat Julien haar tabletsessie. Deze keer meldt ze zich echter aan bij haar account. Dientengevolge, relateert de Dienst van de Identiteit nu dat de activiteit van het het tabletapparaat van Julien met haar e-commercelogine identiteitskaart
* Als u vooruit gaat, kan uw doelinhoud het volledige profiel, de aankoopgeschiedenis en anonieme browseractiviteiten van Julien weerspiegelen.

>[!IMPORTANT]
>
>U kunt de Dienst van de Identiteit gebruiken om identiteiten te verbinden en een volledig beeld van uw klant samen te brengen die anders over verschillende systemen zou kunnen worden verspreid.

## Wat doet de Identiteitsdienst?

Identiteitsdienst verricht de volgende activiteiten om zijn opdracht te verwezenlijken:

* Aangepaste naamruimten maken die aan de behoeften van uw organisatie voldoen.
* Identiteitsgrafieken maken, bijwerken en weergeven.
* Identiteiten verwijderen op basis van gegevenssets.
* Schrap identiteiten om regelgevende naleving te verzekeren.

## Identiteitsservice koppelt identiteiten

Er wordt een koppeling tussen twee identiteiten tot stand gebracht wanneer de naamruimte van de identiteit en de identiteitswaarden overeenkomen.

Een typische aanmeldingsgebeurtenis **verzendt twee identiteiten** in Experience Platform:

* De persoonsidentificatie (zoals een CRM-id) die een geverifieerde gebruiker vertegenwoordigt.
* De browser-id (bijvoorbeeld een ECID) die de webbrowser vertegenwoordigt.

Bekijk het volgende voorbeeld:

* U kunt zich met uw laptop aanmelden met uw gebruikersnaam en wachtwoord voor een e-commercewebsite. Deze gebeurtenis kwalificeert u als voor authentiek verklaarde gebruiker, zodat erkent de Dienst van de Identiteit uw identiteitskaart van CRM
* Uw gebruik van een browser om tot de e-commercewebsite toegang te hebben wordt ook erkend door de Dienst van de Identiteit als gebeurtenis. Deze gebeurtenis wordt via een ECID vertegenwoordigd in Identity Service.
* Achter de scènes verwerkt de Dienst van de Identiteit de twee gebeurtenissen als: `CRM_ID:ABC, ECID:123`.
   * CRM-id: ABC is de naamruimte en waarde die u als geverifieerde gebruiker vertegenwoordigt.
   * ECID: 123 is de naamruimte en waarde die het webbrowsergebruik op uw laptop vertegenwoordigt.
* Als u zich vervolgens met dezelfde gegevens aanmeldt bij dezelfde e-commercewebsite, maar de webbrowser op uw telefoon gebruikt in plaats van de webbrowser op uw laptop, wordt een nieuwe ECID geregistreerd in Identity Service.
* De identiteitsservice verwerkt deze nieuwe gebeurtenis achter de schermen als `{CRM_ID:ABC, ECID:456}`, waarbij CRM_ID: ABC staat voor uw geverifieerde klant-id en ECID:456 staat voor de webbrowser op uw mobiele apparaat.

Gezien de bovenstaande scenario&#39;s legt de Identiteitsdienst een verband tussen `{CRM_ID:ABC, ECID:123}`, alsmede `{CRM_ID:ABC, ECID:456}`. Dit resulteert in een identiteitsgrafiek waarbij u drie identiteiten &quot;bezit&quot;: één voor persoon-id (CRM-id) en twee voor cookie-id&#39;s (ECID&#39;s).

Lees voor meer informatie de handleiding op [Hoe de Dienst van de Identiteit identiteiten verbindt](./features/identity-linking-logic.md).

## Identiteitsgrafieken

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteitsnamespaces, toestaand u om te visualiseren en beter te begrijpen welke klantenidentiteiten samen, en hoe worden vastgemaakt. Lees de zelfstudie aan [de viewer voor identiteitsgrafieken gebruiken](./features/identity-graph-viewer.md) voor meer informatie .

De volgende video is bedoeld als ondersteuning voor uw begrip van identiteiten en identiteitsgrafieken.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Inzicht in de rol van de identiteitsdienst binnen de Experience Platform-infrastructuur

Identiteitsdienst speelt een cruciale rol in Experience Platform. Enkele van deze belangrijke integraties zijn:

* [Schemas](../xdm/home.md): Binnen een bepaald schema, staan de schemagebieden die als identiteit duidelijk zijn voor identiteitsgrafieken toe om worden gebouwd.
* [Gegevenssets](../catalog/datasets/overview.md): Wanneer een dataset voor opname in het Profiel van de Klant in real time wordt toegelaten, worden de identiteitsgrafieken geproduceerd van de dataset, gegeven dat de dataset als minstens twee gebieden duidelijk als identiteit is.
* [Web SDK](../web-sdk/home.md): Web SDK verzendt ervaringsgebeurtenissen naar Adobe Experience Platform en Identity Service genereert een grafiek wanneer twee of meer identiteiten in de gebeurtenis bestaan.
* [Klantprofiel in realtime](../profile/home.md): Voordat kenmerken en gebeurtenissen voor een bepaald profiel worden samengevoegd, kan het Real-Time klantprofiel verwijzen naar de identiteitsgrafiek. Lees voor meer informatie de handleiding op [inzicht krijgen in de relatie tussen Identiteitsservice en Real-Time Klantprofiel](./identity-and-profile.md).
* [Doelen](../destinations/home.md): Doelen kunnen profielgegevens naar andere systemen verzenden op basis van een naamruimte van een identiteit, zoals gehashte e-mail.
* [Segmentovereenkomst](../segmentation/ui/segment-match/overview.md): Segmentovereenkomst komt overeen met twee profielen in twee verschillende sandboxen met dezelfde naamruimte en identiteitswaarde.
* [Privacy Service](../privacy-service/home.md): Indien het verzoek tot verwijdering het volgende bevat `identity`, dan kan de gespecificeerde namespace en de combinatie van de identiteitswaarde van de Dienst van de Identiteit worden geschrapt gebruikend de eigenschap van de privacyverzoekverwerking in Privacy Service.

