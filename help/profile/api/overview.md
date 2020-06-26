---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: fd6516d1c1d3792b41de65d0f44d78af1124ccc7
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime

In real time het Profiel van de Klant laat u toe om een holistische mening van elk van uw individuele klanten binnen Adobe Experience Platform te zien. Het profiel staat u toe om verschillende klantengegevens van veelvoudige kanalen, zoals online, off-line, CRM, en derdegegevens, in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

De realtime-API voor klantprofielen bevat meerdere eindpunten, die hieronder worden beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar de [begonnen gids](getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt bekijken, raadpleegt u de API-naslagwerker voor [realtime-klantprofiel](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (Alpha) Berekende kenmerken

>[!IMPORTANT]
>De functie voor berekende kenmerken staat in alfa en is niet beschikbaar voor alle gebruikers. Documentatie en functionaliteit kunnen worden gewijzigd.

Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op het profielniveau, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen. Elk berekend kenmerk bevat een expressie, ofwel &quot;rule&quot;, die binnenkomende gegevens evalueert en de resulterende waarde opslaat in een profielkenmerk of in een gebeurtenis. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. U kunt gegevens verwerkte attributen tot stand brengen, bekijken, uitgeven en schrappen gebruikend het `config/computedAttributes` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, bezoek de [gegevens verwerkte gids](computed-attributes.md)van het attributeneindpunt.

## Edge-prognoses

Adobe Experience Platform maakt het mogelijk om in real time de ervaringen van klanten te personaliseren door gegevens gemakkelijk toegankelijk te maken op strategisch gelegen servers die &quot;randen&quot; worden genoemd. De Real-time API van het Profiel van de Klant verstrekt eindpunten voor het werken met randen door componenten genoemd &quot;projecties.&quot; Dit omvat projectieconfiguraties om te bepalen welke gegevens aan elke rand moeten worden geprojecteerd, evenals projectiebestemmingen om te bepalen waar te om een projectie te leiden. Voor gedetailleerde informatie over het werken met randprojecties, gelieve de [projectieconfiguraties en bestemmingseindpuntgids](edge-projections.md)te bezoeken.

## Entiteiten

Via het Adobe Experience Platform hebt u toegang tot realtime gegevens van het klantprofiel met RESTful-API&#39;s of de gebruikersinterface. Als u wilt leren hoe u toegang krijgt tot entiteiten, beter bekend als &quot;profielen&quot;, gebruikt u de API, volgt u de stappen die worden beschreven in de handleiding voor het eindpunt van [entiteiten](entities.md). Raadpleeg de gebruikershandleiding bij [Profiel voor toegang tot profielen met de gebruikersinterface van het Platform](../ui/user-guide.md).

## Beleid samenvoegen

Wanneer het brengen van gegevens uit veelvoudige bronnen samen in Experience Platform, is het samenvoegbeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om individuele klantenprofielen tot stand te brengen. Met behulp van de Real-Time Customer Profile API kunt u een nieuw samenvoegbeleid maken, bestaand beleid beheren en een standaardsamenvoegbeleid voor uw organisatie instellen. Meer over het werken met fusiebeleid gebruikend API, gelieve te bezoeken de gids [van het eindpunt van het](merge-policies.md)fusiebeleid.

Voor een gids aan het werken met samenvoegbeleid gebruikend de UI van het Platform, gelieve te zien de de gebruikersgids [van het Beleid van de](../ui/merge-policies.md)Samenvoegen.

## Systeemtaken profiel

Gegevens die in Platform worden opgenomen, worden opgeslagen in het Data Lake en in de gegevensopslag van het Profiel van de Klant in real time. Soms kan het nodig zijn om een gegevensset of batch uit de profielopslag te verwijderen om gegevens te verwijderen die u niet meer nodig hebt of die in een fout zijn toegevoegd. Dit vereist het gebruiken van API om een Baan van het Systeem van het Profiel tot stand te brengen, die als &quot;schrappingsverzoek&quot;wordt bekend, die ook kan worden gewijzigd, worden gecontroleerd, of indien nodig worden geschrapt. Leer hoe te met schrappingsverzoeken te werken gebruikend het `/system/jobs` eindpunt in het Echte-tijdProfiel van de Klant API, de stappen volgen die in de [gids](profile-system-jobs.md)van het de baaneindpunt van het profielsysteem worden geschetst.

## Volgende stappen

Beginnen het maken van vraag gebruikend Real-time het Profiel van de Klant API, lees de [begonnen gids](getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke op profiel betrekking hebbende eindpunten te gebruiken. Raadpleeg voor meer informatie over het werken met profielgegevens via de gebruikersinterface van het Platform de gebruikershandleiding voor het [realtime gebruikersprofiel](../ui/user-guide.md).